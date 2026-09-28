---
layout: Conceptual
title: Govern cloud users and groups with provisioning from on-premises and Entra Connect Sync | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/scenarios/provision-active-directory-to-entra-connect-sync
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: femila
description: This article a tutorial on how to provision users and groups using connect sync.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: 
locale: en-us
document_id: 56fe738a-cef0-1b30-91b4-e007d7689174
document_version_independent_id: 56fe738a-cef0-1b30-91b4-e007d7689174
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/scenarios/provision-active-directory-to-entra-connect-sync.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/scenarios/provision-active-directory-to-entra-connect-sync
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/scenarios/provision-active-directory-to-entra-connect-sync.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a81d7d31-9928-6860-5989-65a845741a05
---

# Govern cloud users and groups with provisioning from on-premises and Entra Connect Sync | Microsoft Learn

**Scenario:** Manage cloud users and groups that are provisioned from Active Directory using Microsoft Entra connect sync.

## Prerequisites

- A computer with [Hyper-V](/en-us/windows-server/virtualization/hyper-v/hyper-v-technology-overview) installed. We suggest that you install Hyper-V on a [Windows 10](/en-us/virtualization/hyper-v-on-windows/about/supported-guest-os) or [Windows Server 2016](/en-us/windows-server/virtualization/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) computer.
- An Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.
- An [external network adapter](/en-us/virtualization/hyper-v-on-windows/quick-start/connect-to-network), so the virtual machine can connect to the internet.
- A copy of Windows Server 2016.

Note

This tutorial uses PowerShell scripts to quickly create the tutorial environment. Each script uses variables that are declared at the beginning of the script. Be sure to change the variables to reflect your environment.

The scripts in the tutorial create a general Windows Server Active Directory (Windows Server AD) environment before they install Microsoft Entra Connect. The scripts are also used in related tutorials.

The PowerShell scripts that are used in this tutorial are available on [GitHub](https://github.com/billmath/tutorial-phs).

## Create a virtual machine

To create a hybrid identity environment, the first task is to create a virtual machine to use as an on-premises Windows Server AD server.

Note

If you've never run a script in PowerShell on your host machine, before you run any scripts, open Windows PowerShell ISE as administrator and run `Set-ExecutionPolicy remotesigned`. In the **Execution Policy Change** dialog, select **Yes**.

To create the virtual machine:

1. Open Windows PowerShell ISE as administrator.
2. Run the following script:

    ```powershell
    #Declare variables
    $VMName = 'DC1'
    $Switch = 'External'
    $InstallMedia = 'D:\ISO\en_windows_server_2016_updated_feb_2018_x64_dvd_11636692.iso'
    $Path = 'D:\VM'
    $VHDPath = 'D:\VM\DC1\DC1.vhdx'
    $VHDSize = '64424509440'
    
    #Create a new virtual machine
    New-VM -Name $VMName -MemoryStartupBytes 16GB -BootDevice VHD -Path $Path -NewVHDPath $VHDPath -NewVHDSizeBytes $VHDSize  -Generation 2 -Switch $Switch  
    
    #Set the memory to be non-dynamic
    Set-VMMemory $VMName -DynamicMemoryEnabled $false
    
    #Add a DVD drive to the virtual machine
    Add-VMDvdDrive -VMName $VMName -ControllerNumber 0 -ControllerLocation 1 -Path $InstallMedia
    
    #Mount installation media
    $DVDDrive = Get-VMDvdDrive -VMName $VMName
    
    #Configure the virtual machine to boot from the DVD
    Set-VMFirmware -VMName $VMName -FirstBootDevice $DVDDrive 
    ```

## Install the operating system

To finish creating the virtual machine, install the operating system:

1. In Hyper-V Manager, double-click the virtual machine.
2. Select **Start**.
3. At the prompt, press any key to boot from CD or DVD.
4. In the Windows Server start window, select your language, and then select **Next**.
5. Select **Install Now**.
6. Enter your license key and select **Next**.
7. Select the **I accept the license terms** checkbox and select **Next**.
8. Select **Custom: Install Windows Only (Advanced)**.
9. Select **Next**.
10. When the installation is finished, restart the virtual machine. Sign in, and then check Windows Update. Install any updates to ensure that the VM is fully up-to-date.

## Install Windows Server AD prerequisites

Before you install Windows Server AD, run a script that installs prerequisites:

1. Open Windows PowerShell ISE as administrator.
2. Run `Set-ExecutionPolicy remotesigned`. In the **Execution Policy Change** dialog, select **Yes to All**.
3. Run the following script:

    ```powershell
    #Declare variables
    $ipaddress = "10.0.1.117" 
    $ipprefix = "24" 
    $ipgw = "10.0.1.1" 
    $ipdns = "10.0.1.117"
    $ipdns2 = "4.2.2.2" 
    $ipif = (Get-NetAdapter).ifIndex 
    $featureLogPath = "c:\poshlog\featurelog.txt" 
    $newname = "DC1"
    $addsTools = "RSAT-AD-Tools" 
    
    #Set a static IP address
    New-NetIPAddress -IPAddress $ipaddress -PrefixLength $ipprefix -InterfaceIndex $ipif -DefaultGateway $ipgw 
    
    # Set the DNS servers
    Set-DnsClientServerAddress -InterfaceIndex $ipif -ServerAddresses ($ipdns, $ipdns2)
    
    #Rename the computer 
    Rename-Computer -NewName $newname -force 
    
    #Install features 
    New-Item $featureLogPath -ItemType file -Force 
    Add-WindowsFeature $addsTools 
    Get-WindowsFeature | Where installed >>$featureLogPath 
    
    #Restart the computer 
    Restart-Computer
    ```

## Create a Windows Server AD environment

Now, install and configure Active Directory Domain Services to create the environment:

1. Open Windows PowerShell ISE as administrator.
2. Run the following script:

    ```powershell
    #Declare variables
    $DatabasePath = "c:\windows\NTDS"
    $DomainMode = "WinThreshold"
    $DomainName = "contoso.com"
    $DomainNetBIOSName = "CONTOSO"
    $ForestMode = "WinThreshold"
    $LogPath = "c:\windows\NTDS"
    $SysVolPath = "c:\windows\SYSVOL"
    $featureLogPath = "c:\poshlog\featurelog.txt" 
    $Password = "Pass1w0rd"
    $SecureString = ConvertTo-SecureString $Password -AsPlainText -Force
    
    #Install Active Directory Domain Services, DNS, and Group Policy Management Console 
    start-job -Name addFeature -ScriptBlock { 
    Add-WindowsFeature -Name "ad-domain-services" -IncludeAllSubFeature -IncludeManagementTools 
    Add-WindowsFeature -Name "dns" -IncludeAllSubFeature -IncludeManagementTools 
    Add-WindowsFeature -Name "gpmc" -IncludeAllSubFeature -IncludeManagementTools } 
    Wait-Job -Name addFeature 
    Get-WindowsFeature | Where installed >>$featureLogPath
    
    #Create a new Windows Server AD forest
    Install-ADDSForest -CreateDnsDelegation:$false -DatabasePath $DatabasePath -DomainMode $DomainMode -DomainName $DomainName -SafeModeAdministratorPassword $SecureString -DomainNetbiosName $DomainNetBIOSName -ForestMode $ForestMode -InstallDns:$true -LogPath $LogPath -NoRebootOnCompletion:$false -SysvolPath $SysVolPath -Force:$true
    ```

## Create a Windows Server AD user

Next, create a test user account. Create this account in your on-premises Active Directory environment. The account is then synced to Microsoft Entra ID.

1. Open Windows PowerShell ISE as administrator.
2. Run the following script:

    ```powershell
    #Declare variables
    $Givenname = "Allie"
    $Surname = "McCray"
    $Displayname = "Allie McCray"
    $Name = "amccray"
    $Password = "Pass1w0rd"
    $Identity = "CN=ammccray,CN=Users,DC=contoso,DC=com"
    $SecureString = ConvertTo-SecureString $Password -AsPlainText -Force
    
    #Create the user
    New-ADUser -Name $Name -GivenName $Givenname -Surname $Surname -DisplayName $Displayname -AccountPassword $SecureString
    
    #Set the password to never expire
    Set-ADUser -Identity $Identity -PasswordNeverExpires $true -ChangePasswordAtLogon $false -Enabled $true
    ```

## Create a Microsoft Entra tenant

If you don't have one, follow the steps in the article [Create a new tenant in Microsoft Entra ID](../../fundamentals/create-new-tenant) to create a new tenant.

## Create a Hybrid Identity Administrator in Microsoft Entra ID

The next task is to create a Hybrid Identity Administrator account. This account is used to create the Microsoft Entra Connector account during Microsoft Entra Connect installation. The Microsoft Entra Connector account is used to write information to Microsoft Entra ID.

To create the Hybrid Identity Administrator account:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Users**
3. Select **New user** &gt; **Create new user**.
4. In the **Create new user** pane, enter a **Display name** and a **User principal name**for the new user. You're creating your Hybrid Identity Administrator account for the tenant. You can show and copy the temporary password.
    1. Under **Assignments**, select **Add role**, and select **Hybrid Identity Administrator**.
5. Then select **Review + create** &gt; **Create**.
6. In a new web browser window, sign in to `myapps.microsoft.com` by using the new Hybrid Identity Administrator account and the temporary password.

## Download and install Microsoft Entra Connect

Now it's time to download and install Microsoft Entra Connect. After it's installed, you'll use the express installation.

1. Download [Microsoft Entra Connect](https://www.microsoft.com/download/details.aspx?id=47594).
2. Go to *AzureADConnect.msi* and double-click to open the installation file.
3. In **Welcome**, select the checkbox to agree to the licensing terms and select **Continue**.
4. In **Express settings**, select **Use express settings**.
5. In **Connect to Microsoft Entra ID**, enter the username and password for the Hybrid Identity Administrator account for Microsoft Entra ID. Select **Next**.
6. In **Connect to AD DS**, enter the username and password for an enterprise admin account. Select **Next**.
7. In **Ready to configure**, select **Install**.
8. When the installation is finished, select **Exit**.
9. Before you use Synchronization Service Manager or Synchronization Rule Editor, sign out, and then sign in again.

## Check for users in the portal

Now you'll verify that the users in your on-premises Active Directory tenant have synced and are now in your Microsoft Entra tenant. This section might take a few hours to complete.

To verify that the users are synced:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../identity/role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Users**
3. Verify that the new users appear in your tenant.

    ![Screenshot that shows verifying that users were synced in Microsoft Entra ID.](../../includes/governance/media/tutorial-password-hash-sync/sync1.png)

## Sign in with a user account to test sync

To test that users from your Windows Server AD tenant are synced with your Microsoft Entra tenant, sign in as one of the users:

1. Go to https://myapps.microsoft.com.
2. Sign in with a user account that was created in your new tenant.

    For the username, use the format `user@domain.onmicrosoft.com`. Use the same password the user uses to sign in to on-premises Active Directory.

You've successfully set up a hybrid identity environment that you can use to test and to get familiar with what Azure has to offer.