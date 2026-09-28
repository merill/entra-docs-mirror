---
layout: Conceptual
title: Enable password hash sync for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/tutorial-configure-password-hash-sync
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: In this tutorial, learn how to enable password hash synchronization using Microsoft Entra Connect to a Microsoft Entra Domain Services managed domain.
ms.topic: tutorial
ms.date: 2025-02-19T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: dedc709c-19ce-e83b-dae8-7cc18793632e
document_version_independent_id: 1f14d8cc-761d-1cf3-e40a-6a8774b7e812
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/tutorial-configure-password-hash-sync.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/tutorial-configure-password-hash-sync
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/tutorial-configure-password-hash-sync.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 80445d33-8e16-d1bb-166b-b08b12891882
---

# Enable password hash sync for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

For hybrid environments, a Microsoft Entra tenant can be configured to synchronize with an on-premises Active Directory Domain Services (AD DS) environment using Microsoft Entra Connect. By default, Microsoft Entra Connect doesn't synchronize legacy NT LAN Manager (NTLM) and Kerberos password hashes that are needed for Microsoft Entra Domain Services.

To use Domain Services with accounts synchronized from an on-premises AD DS environment, you need to configure Microsoft Entra Connect to synchronize those password hashes required for NTLM and Kerberos authentication. After Microsoft Entra Connect is configured, an on-premises account creation or password change event also then synchronizes the legacy password hashes to Microsoft Entra ID.

You don't need to perform these steps if you use cloud-only accounts with no on-premises AD DS environment.

In this tutorial, you learn:

- Why legacy NTLM and Kerberos password hashes are needed
- How to configure legacy password hash synchronization for Microsoft Entra Connect

If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

To complete this tutorial, you need the following resources:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription that's synchronized with an on-premises directory using Microsoft Entra Connect.
    - If needed, [create a Microsoft Entra tenant](/en-us/azure/active-directory/fundamentals/sign-up-organization) or [associate an Azure subscription with your account](/en-us/azure/active-directory/fundamentals/how-subscriptions-associated-directory).
    - If needed, [enable Microsoft Entra Connect for password hash synchronization](/en-us/azure/active-directory/hybrid/connect/how-to-connect-install-express).
- A Microsoft Entra Domain Services managed domain enabled and configured in your Microsoft Entra tenant.
    - If needed, [create and configure a Microsoft Entra Domain Services managed domain](tutorial-create-instance).

## Password hash synchronization using Microsoft Entra Connect

Microsoft Entra Connect is used to synchronize objects like user accounts and groups from an on-premises AD DS environment into a Microsoft Entra tenant. As part of the process, password hash synchronization enables accounts to use the same password in the on-premises AD DS environment and Microsoft Entra ID.

To authenticate users on the managed domain, Domain Services needs password hashes in a format that's suitable for NTLM and Kerberos authentication. Microsoft Entra ID doesn't store password hashes in the format that's required for NTLM or Kerberos authentication until you enable Domain Services for your tenant. For security reasons, Microsoft Entra ID also doesn't store any password credentials in clear-text form. Therefore, Microsoft Entra ID can't automatically generate these NTLM or Kerberos password hashes based on users' existing credentials.

Microsoft Entra Connect can be configured to synchronize the required NTLM or Kerberos password hashes for Domain Services. Make sure that you have completed the steps to [enable Microsoft Entra Connect for password hash synchronization](/en-us/azure/active-directory/hybrid/connect/how-to-connect-install-express). If you had an existing instance of Microsoft Entra Connect, [download and update to the latest version](https://www.microsoft.com/download/details.aspx?id=47594) to make sure you can synchronize the legacy password hashes for NTLM and Kerberos. This functionality isn't available in early releases of Microsoft Entra Connect or with the legacy DirSync tool. Microsoft Entra Connect version *1.1.614.0* or later is required.

Important

Microsoft Entra Connect should only be installed and configured for synchronization with on-premises AD DS environments. It's not supported to install Microsoft Entra Connect in a Domain Services managed domain to synchronize objects back to Microsoft Entra ID.

## Enable synchronization of password hashes

With Microsoft Entra Connect installed and configured to synchronize with Microsoft Entra ID, now configure the legacy password hash sync for NTLM and Kerberos. A PowerShell script is used to configure the required settings and then start a full password synchronization to Microsoft Entra ID. When that Microsoft Entra Connect password hash synchronization process is complete, users can sign in to applications through Domain Services that use legacy NTLM or Kerberos password hashes.

1. On the computer with Microsoft Entra Connect installed, from the Start menu, open the **Microsoft Entra Connect &gt; Synchronization Service**.
2. Select the **Connectors** tab. The connection information used to establish the synchronization between the on-premises AD DS environment and Microsoft Entra ID are listed.

    The **Type** indicates either *Windows Microsoft Entra ID (Microsoft)* for the Microsoft Entra connector or *Active Directory Domain Services* for the on-premises AD DS connector. Make a note of the connector names to use in the PowerShell script in the next step.

    ![List the connector names in Sync Service Manager](media/tutorial-configure-password-hash-sync/service-sync-manager.png)

    In this example screenshot, the following connectors are used:

    - The Microsoft Entra connector is named *contoso.onmicrosoft.com - Microsoft Entra ID*
    - The on-premises AD DS connector is named *onprem.contoso.com*
3. Copy and paste the following PowerShell script to the computer with Microsoft Entra Connect installed. The script triggers a full password sync that includes legacy password hashes. Update the `$azureadConnector` and `$adConnector` variables with the connector names from the previous step.

    Run this script on each AD forest to synchronize on-premises account NTLM and Kerberos password hashes to Microsoft Entra ID.

    ```powershell
    # Define the Azure AD Connect connector names and import the required PowerShell module
    $azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"
    $adConnector = "<CASE SENSITIVE AD DS CONNECTOR NAME>"
    
    Import-Module "C:\Program Files\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1"
    Import-Module "C:\Program Files\Microsoft Azure Active Directory Connect\AdSyncConfig\AdSyncConfig.psm1"
    
    # Create a new ForceFullPasswordSync configuration parameter object then
    # update the existing connector with this new configuration
    $c = Get-ADSyncConnector -Name $adConnector
    $p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
    $p.Value = 1
    $c.GlobalParameters.Remove($p.Name)
    $c.GlobalParameters.Add($p)
    $c = Add-ADSyncConnector -Connector $c
    
    # Disable and re-enable Azure AD Connect to force a full password synchronization
    Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false
    Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true
    ```

    Depending on the size of your directory in terms of number of accounts and groups, synchronization of the legacy password hashes to Microsoft Entra ID may take some time. The passwords are then synchronized to the managed domain after they've synchronized to Microsoft Entra ID.