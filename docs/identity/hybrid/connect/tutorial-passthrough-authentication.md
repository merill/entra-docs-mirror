---
layout: Conceptual
title: 'Tutorial: Use pass-through authentication for hybrid identity in a single Active Directory forest - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/tutorial-passthrough-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to set up a hybrid identity environment by using pass-through authentication to integrate a Windows Server Active Directory forest with Microsoft Entra ID.
ms.topic: tutorial
ms.date: 2025-09-29T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4390fa0d-72c0-e0ec-97f6-68bcc25b169d
document_version_independent_id: 886fbc24-4d8d-e891-9e4e-4fbb4679cd1a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/tutorial-passthrough-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/tutorial-passthrough-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/tutorial-passthrough-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a6c76016-1651-6c24-dbcf-1d650a0ed859
---

# Tutorial: Use pass-through authentication for hybrid identity in a single Active Directory forest - Microsoft Entra ID | Microsoft Learn

This tutorial shows you how to create a hybrid identity environment in Azure by using pass-through authentication and Windows Server Active Directory (Windows Server AD). You can use the hybrid identity environment you create for testing or to get more familiar with how hybrid identity works.

![Diagram that shows how to create a hybrid identity environment in Azure by using pass-through authentication.](media/tutorial-passthrough-authentication/diagram.png)

In this tutorial, you learn how to:

- Create a virtual machine.
- Create a Windows Server Active Directory environment.
- Create a Windows Server Active Directory user.
- Create a Microsoft Entra tenant.
- Create a Hybrid Identity Administrator account in Azure.
- Add a custom domain to your directory.
- Set up Microsoft Entra Connect.
- Test and verify that users are synced.

## Prerequisites

- A computer with [Hyper-V](/en-us/windows-server/virtualization/hyper-v/hyper-v-technology-overview) installed. We suggest that you install Hyper-V on a [Windows 10](/en-us/virtualization/hyper-v-on-windows/about/supported-guest-os) or [Windows Server 2025](/en-us/windows-server/virtualization/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) computer.
- An Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.
- An [external network adapter](/en-us/virtualization/hyper-v-on-windows/quick-start/connect-to-network), so the virtual machine can connect to the internet.
- A copy of Windows Server 2025 or Windows Server 2022.
- A [custom domain](../../../fundamentals/add-custom-domain) that can be verified.

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
    $ipdns2 = "8.8.8.8" 
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
    $Password = ConvertTo-SecureString "Passw0rd" -AsPlainText -Force
    
    #Install Active Directory Domain Services, DNS, and Group Policy Management Console 
    start-job -Name addFeature -ScriptBlock { 
    Add-WindowsFeature -Name "ad-domain-services" -IncludeAllSubFeature -IncludeManagementTools 
    Add-WindowsFeature -Name "dns" -IncludeAllSubFeature -IncludeManagementTools 
    Add-WindowsFeature -Name "gpmc" -IncludeAllSubFeature -IncludeManagementTools } 
    Wait-Job -Name addFeature 
    Get-WindowsFeature | Where installed >>$featureLogPath
    
    #Create a new Windows Server AD forest
    Install-ADDSForest -CreateDnsDelegation:$false -DatabasePath $DatabasePath -DomainMode $DomainMode -DomainName $DomainName -SafeModeAdministratorPassword $Password -DomainNetbiosName $DomainNetBIOSName -ForestMode $ForestMode -InstallDns:$true -LogPath $LogPath -NoRebootOnCompletion:$false -SysvolPath $SysVolPath -Force:$true
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

If you don't have one, follow the steps in the article [Create a new tenant in Microsoft Entra ID](../../../fundamentals/create-new-tenant) to create a new tenant.

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

## Add a custom domain name to your directory

Now that you have a tenant and a Hybrid Identity Administrator account, add your custom domain so that Azure can verify it.

To add a custom domain name to a directory:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Domain names**.
3. Select **Add custom domain**.

    ![Screenshot that shows the Add custom domain button highlighted.](media/tutorial-passthrough-authentication/custom1.png)
4. In **Custom domain names**, enter the name of your custom domain, and then select **Add domain**.
5. In **Custom domain name**, either TXT or MX information is shown. You must add this information to the DNS information of the domain registrar under your domain. Go to your domain registrar and enter either the TXT or the MX information in the DNS settings for your domain.

    ![Screenshot that shows where you get TXT or MX information.](media/tutorial-passthrough-authentication/custom2.png) Adding this information to your domain registrar allows Azure to verify your domain. Domain verification might take up to 24 hours.

    For more information, see the [add a custom domain](../../../fundamentals/add-custom-domain) documentation.
6. To ensure that the domain is verified, select **Verify**.

    ![Screenshot that shows a success message after you select Verify.](media/tutorial-passthrough-authentication/custom3.png)

### Download and install Microsoft Entra Connect

Now it's time to download and install Microsoft Entra Connect. After it's installed, you'll use the express installation.

1. Download [Microsoft Entra Connect](https://www.microsoft.com/download/details.aspx?id=47594).
2. Go to *AzureADConnect.msi* and double-click to open the installation file.
3. In **Welcome**, select the checkbox to agree to the licensing terms, and then select **Continue**.
4. In **Express settings**, select **Customize**.
5. In **Install required components**, select **Install**.
6. In **User sign-in**, select **Pass-through authentication** and **Enable single sign-on**, and then select **Next**.
7. In **Connect to Microsoft Entra ID**, enter the username and password of the Hybrid Identity Administrator account you created earlier, and then select **Next**.
8. In **Connect your directories**, select **Add directory**. Then select **Create new AD account** and enter the contoso\Administrator username and password. Select **OK**.
9. Select **Next**.
10. In **Microsoft Entra sign-in configuration**, select **Continue without matching all UPN suffixes to verified domains**. Select **Next.**
11. In **Domain and OU filtering**, select **Next**.
12. In **Uniquely identifying your users**, select **Next**.
13. In **Filter users and devices**, select **Next**.
14. In **Optional features**, select **Next**.
15. In **Enable single sign-in credentials**, enter the contoso\Administrator username and password, and then select **Next.**
16. In **Ready to configure**, select **Install**.
17. When the installation is finished, select **Exit**.
18. Before you use Synchronization Service Manager or Synchronization Rule Editor, sign out, and then sign in again.

## Check for users in the portal

Now you'll verify that the users in your on-premises Active Directory tenant have synced and are now in your Microsoft Entra tenant. This section might take a few hours to complete.

To verify that the users are synced:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Users**
3. Verify that the new users appear in your tenant.

    ![Screenshot that shows verifying that users were synced in Microsoft Entra ID.](media/tutorial-passthrough-authentication/sync1.png)

## Sign in with a user account to test sync

To test that users from your Windows Server AD tenant are synced with your Microsoft Entra tenant, sign in as one of the users:

1. Go to https://myapps.microsoft.com.
2. Sign in with a user account that was created in your new tenant.

    For the username, use the format `user@domain.onmicrosoft.com`. Use the same password the user uses to sign in to on-premises Active Directory.

You've successfully set up a hybrid identity environment that you can use to test and to get familiar with what Azure has to offer.