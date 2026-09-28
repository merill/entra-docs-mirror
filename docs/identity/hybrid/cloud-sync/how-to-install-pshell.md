---
layout: Conceptual
title: Install the Microsoft Entra Connect cloud provisioning agent using a command-line interface (CLI) and PowerShell - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-install-pshell
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Learn how to install the Microsoft Entra Connect cloud provisioning agent by using PowerShell cmdlets.
ms.topic: how-to
ms.date: 2025-09-18T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: 7348ef24-c335-95dd-d5fe-873be14c75d6
document_version_independent_id: 286d1c21-590e-1ee1-f6cc-5d4986712819
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-install-pshell.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-install-pshell
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-install-pshell.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 41307367-289a-21cf-2df6-4c131478324d
---

# Install the Microsoft Entra Connect cloud provisioning agent using a command-line interface (CLI) and PowerShell - Microsoft Entra ID | Microsoft Learn

This article shows you how to install the Microsoft Entra provisioning agent by using PowerShell cmdlets.

Note

This article deals with installing the provisioning agent by using the command-line interface (CLI). For information on how to install the Microsoft Entra provisioning agent by using the wizard, see [Install the Microsoft Entra provisioning agent](how-to-install).

## Prerequisite

The Windows server must have TLS 1.2 enabled before you install the Microsoft Entra provisioning agent by using PowerShell cmdlets. To enable TLS 1.2, follow the steps in [Prerequisites for Microsoft Entra Cloud Sync](how-to-prerequisites#tls-requirements).

Important

The following installation instructions assume that all the [prerequisites](how-to-prerequisites) were met.

## Install the Microsoft Entra provisioning agent by using PowerShell cmdlets

Note

By default, the Microsoft Entra provisioning agent is installed in the default Azure environment.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Select **Manage**.
2. Select **Download provisioning agent**
3. On the right, select **Accept terms and download**.
4. For the purposes of these instructions, the agent was downloaded to the C:\temp folder.
5. Install ProvisioningAgent in quiet mode. 

    ```
    $installerProcess = Start-Process 'c:\temp\ProvisioningAgentSetup.exe' /quiet -NoNewWindow -PassThru 
    $installerProcess.WaitForExit()
    
    ```
6. Import the Provisioning Agent PS module. 

    ```
    Import-Module "C:\Program Files\Microsoft Azure AD Connect Provisioning Agent\Microsoft.CloudSync.PowerShell.dll" 
    ```
7. Connect to Microsoft Entra ID by using an account with the hybrid identity role. You can customize this section to fetch a password from a secure store. 

    ```
    $hybridAdminPassword = ConvertTo-SecureString -String "Hybrid Identity Administrator password" -AsPlainText -Force 
    
    $hybridAdminCreds = New-Object System.Management.Automation.PSCredential -ArgumentList ("HybridIDAdmin@contoso.onmicrosoft.com", $hybridAdminPassword) 
    
    Connect-AADCloudSyncAzureAD -Credential $hybridAdminCreds 
    ```
8. Add the gMSA account, and provide credentials of the domain admin to create the default gMSA account. 

    ```
    $domainAdminPassword = ConvertTo-SecureString -String "Domain admin password" -AsPlainText -Force 
    
    $domainAdminCreds = New-Object System.Management.Automation.PSCredential -ArgumentList ("DomainName\DomainAdminAccountName", $domainAdminPassword) 
    
    Add-AADCloudSyncGMSA -Credential $domainAdminCreds 
    ```
9. Or use the preceding cmdlet to provide a precreated gMSA account. 

    ```
    Add-AADCloudSyncGMSA -CustomGMSAName preCreatedGMSAName$ 
    ```
10. Add the domain. 

    ```
    $contosoDomainAdminPassword = ConvertTo-SecureString -String "Domain admin password" -AsPlainText -Force 
    
    $contosoDomainAdminCreds = New-Object System.Management.Automation.PSCredential -ArgumentList ("DomainName\DomainAdminAccountName", $contosoDomainAdminPassword) 
    
    Add-AADCloudSyncADDomain -DomainName contoso.com -Credential $contosoDomainAdminCreds 
    ```
11. Or use the preceding cmdlet to configure preferred domain controllers. 

    ```
    $preferredDCs = @("PreferredDC1", "PreferredDC2", "PreferredDC3") 
    
    Add-AADCloudSyncADDomain -DomainName contoso.com -Credential $contosoDomainAdminCreds -PreferredDomainControllers $preferredDCs 
    ```
12. To add more domains, repeat the previous step. Provide the account names and domain names of the respective domains.
13. Restart the service. 

    ```
    Restart-Service -Name AADConnectProvisioningAgent  
    ```
14. To create the cloud sync configuration, go to the Microsoft Entra admin center.

## Provisioning agent gMSA PowerShell cmdlets

After you install the agent, you can apply more granular permissions to the gMSA. For information and step-by-step instructions on how to configure the permissions, see [Microsoft Entra Connect cloud provisioning agent gMSA PowerShell cmdlets](how-to-gmsa-cmdlets).