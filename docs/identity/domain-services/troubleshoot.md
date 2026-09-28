---
layout: Conceptual
title: Microsoft Entra Domain Services troubleshooting - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/troubleshoot
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to troubleshoot common errors when you create or manage Microsoft Entra Domain Services
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done
ms.topic: troubleshooting
ms.date: 2025-02-19T00:00:00.0000000Z
locale: en-us
document_id: 7236bae9-3382-65d8-221e-581be68fb0ba
document_version_independent_id: 65bcb458-1a82-9a5a-e2f3-a6d0a633316d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/troubleshoot.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/troubleshoot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 78267700-4ddc-f7f5-16fe-f87a94a91804
---

# Microsoft Entra Domain Services troubleshooting - Microsoft Entra ID | Microsoft Learn

As a central part of identity and authentication for applications, Microsoft Entra Domain Services sometimes has problems. If you run into issues, there are some common error messages and associated troubleshooting steps to help you get things running again. At any time, you can also [open an Azure support request](/en-us/azure/active-directory/fundamentals/how-to-get-support) for more troubleshooting help.

This article provides troubleshooting steps for common issues in Domain Services.

## You cannot enable Microsoft Entra Domain Services for your Microsoft Entra directory

If you have problems enabling Domain Services, review the following common errors and steps to resolve them:

| **Sample error Message** | **Resolution** |
| --- | --- |
| *The name aaddscontoso.com is already in use on this network. Specify a name that is not in use.* | [Domain name conflict in the virtual network](troubleshoot#domain-name-conflict) |
| *Domain Services could not be enabled in this Microsoft Entra tenant. The service does not have adequate permissions to the application called Microsoft Entra Domain Services Sync. Delete the application called 'Microsoft Entra Domain Services Sync' and then try to enable Domain Services for your Microsoft Entra tenant.* | [Domain Services doesn't have adequate permissions to the Microsoft Entra Domain Services Sync application](troubleshoot#inadequate-permissions) |
| *Domain Services could not be enabled in this Microsoft Entra tenant. The Domain Services application in your Microsoft Entra tenant does not have the required permissions to enable Domain Services. Delete the application with the application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try to enable Domain Services for your Microsoft Entra tenant.* | [The Domain Services application isn't configured properly in your Microsoft Entra tenant](troubleshoot#invalid-configuration) |
| *Domain Services could not be enabled in this Microsoft Entra tenant. The Microsoft Entra application is disabled in your Microsoft Entra tenant. Enable the application with the application identifier 00000002-0000-0000-c000-000000000000 and then try to enable Domain Services for your Microsoft Entra tenant.* | [The Microsoft Graph application is disabled in your Microsoft Entra tenant](troubleshoot#microsoft-graph-disabled) |

### Domain name conflict

**Error message**

*The name aaddscontoso.com is already in use on this network. Specify a name that is not in use.*

**Resolution**

Check that you don't have an existing AD DS environment with the same domain name on the same, or a peered, virtual network. For example, you may have an AD DS domain named *aaddscontoso.com* that runs on Azure VMs. When you try to enable a Domain Services managed domain with the same domain name of *aaddscontoso.com* on the virtual network, the requested operation fails.

This failure is due to name conflicts for the domain name on the virtual network. A DNS lookup checks if an existing AD DS environment responds on the requested domain name. To resolve this failure, use a different name to set up your managed domain, or deprovision the existing AD DS domain and then try again to enable Domain Services.

### Inadequate permissions

**Error message**

*Domain Services could not be enabled in this Microsoft Entra tenant. The service does not have adequate permissions to the application called Microsoft Entra Domain Services Sync. Delete the application called 'Microsoft Entra Domain Services Sync' and then try to enable Domain Services for your Microsoft Entra tenant.*

**Resolution**

Check if there's an application named *Microsoft Entra Domain Services Sync* in your Microsoft Entra directory. If this application exists, delete it, then try again to enable Domain Services. To check for an existing application and delete it if needed, complete the following steps:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), select **Microsoft Entra ID** from the left-hand navigation menu.
2. Select **Enterprise applications**. Choose *All applications* from the **Application Type** drop-down menu, then select **Apply**.
3. In the search box, enter *Microsoft Entra Domain Services Sync*. If the application exists, select it and choose **Delete**.
4. Once you've deleted the application, try to enable Domain Services again.

### Invalid configuration

**Error message**

*Domain Services could not be enabled in this Microsoft Entra tenant. The Domain Services application in your Microsoft Entra tenant does not have the required permissions to enable Domain Services. Delete the application with the application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try to enable Domain Services for your Microsoft Entra tenant.*

**Resolution**

Check if you have an existing application named *AzureActiveDirectoryDomainControllerServices* with an application identifier of *d87dcbc6-a371-462e-88e3-28ad15ec4e64* in your Microsoft Entra directory. If this application exists, delete it and then try again to enable Domain Services.

Use the following PowerShell script to search for an existing application instance and delete it if needed:

```powershell
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-MgServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-MgServicePrincipal -ServicePrincipalId $aadDsSp.Id
    Write-Information "Deleted the Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-MgApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-MgApplication -ApplicationId  $app.Id
    Write-Information "Deleted the Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-MgServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-MgServicePrincipal -ObjectId $sp.Id
    Write-Information "Deleted the Azure AD Domain Services Sync service principal."
}
```

### Microsoft Graph disabled

**Error message**

*Domain Services could not be enabled in this Microsoft Entra tenant. The Microsoft Entra application is disabled in your Microsoft Entra tenant. Enable the application with the application identifier 00000002-0000-0000-c000-000000000000 and then try to enable Domain Services for your Microsoft Entra tenant.*

**Resolution**

Check if you've disabled an application with the identifier *00000002-0000-0000-c000-000000000000*. This application is the Microsoft Entra application and provides Graph API access to your Microsoft Entra tenant. To synchronize your Microsoft Entra tenant, this application must be enabled.

To check the status of this application and enable it if needed, complete the following steps:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), search for and select **Enterprise applications**.
2. Choose *All applications* from the **Application Type** drop-down menu, then select **Apply**.
3. In the search box, enter *00000002-0000-0000-c000-00000000000*. Select the application, then choose **Properties**.
4. If **Enabled for users to sign-in** is set to *No*, set the value to *Yes*, then select **Save**.
5. Once you've enabled the application, try to enable Domain Services again.

## Users are unable to sign in to the Microsoft Entra Domain Services managed domain

If one or more users in your Microsoft Entra tenant can't sign in to the managed domain, complete the following troubleshooting steps:

- **Credentials format** - Try using the UPN format to specify credentials, such as `dee@aaddscontoso.onmicrosoft.com`. The UPN format is the recommended way to specify credentials in Domain Services. Make sure this UPN is configured correctly in Microsoft Entra ID.

    The *SAMAccountName* for your account, such as *AADDSCONTOSO\driley* may be autogenerated if there are multiple users with the same UPN prefix in your tenant or if your UPN prefix is overly long. Therefore, the *SAMAccountName* format for your account may be different from what you expect or use in your on-premises domain.
- **Password synchronization** - Make sure that you've enabled password synchronization for [cloud-only users](tutorial-create-instance#enable-user-accounts-for-azure-ad-ds) or for [hybrid environments using Microsoft Entra Connect](tutorial-configure-password-hash-sync).

    - **Hybrid synchronized accounts:** If the affected user accounts are synchronized from an on-premises directory, verify the following areas:

        - You've deployed, or updated to, the [latest recommended release of Microsoft Entra Connect](https://www.microsoft.com/download/details.aspx?id=47594).
        - You've configured Microsoft Entra Connect to [perform a full synchronization](tutorial-configure-password-hash-sync).
        - Depending on the size of your directory, it may take a while for user accounts and credential hashes to be available in the managed domain. Make sure you wait long enough before trying to authenticate against the managed domain.
        - If the issue persists after verifying the previous steps, try restarting the *Azure AD Sync Service*. From your Microsoft Entra Connect server, open a command prompt, then run the following commands:

            ```console
            net stop 'Microsoft Azure AD Sync'
            net start 'Microsoft Azure AD Sync'
            ```
    - **Cloud-only accounts**: If the affected user account is a cloud-only user account, make sure that the [user has changed their password after you enabled Domain Services](tutorial-create-instance#enable-user-accounts-for-azure-ad-ds). This password reset causes the required credential hashes for the managed domain to be generated.
- **Verify the user account is active**: By default, five invalid password attempts within 2 minutes on the managed domain cause a user account to be locked out for 30 minutes. The user can't sign in while the account is locked out. After 30 minutes, the user account is automatically unlocked.

    - Invalid password attempts on the managed domain don't lock out the user account in Microsoft Entra ID. The user account is locked out only within the managed domain. Check the user account status in the *Active Directory Administrative Console (ADAC)* using the [management VM](tutorial-create-management-vm), not in Microsoft Entra ID.
    - You can also [configure fine grained password policies](password-policy) to change the default lockout threshold and duration.
- **External accounts** - Check that the affected user account isn't an external account in the Microsoft Entra tenant. Examples of external accounts include Microsoft accounts like `dee@live.com` or user accounts from an external Microsoft Entra directory. Domain Services doesn't store credentials for external user accounts so they can't sign in to the managed domain.

## There are one or more alerts on your managed domain

If there are active alerts on the managed domain, it may prevent the authentication process from working correctly.

To see if there are any active alerts, [check the health status of a managed domain](check-health). If any alerts are shown, [troubleshoot and resolve them](troubleshoot-alerts).

## Users removed from your Microsoft Entra tenant are not removed from your managed domain

Microsoft Entra ID protects against accidental deletion of user objects. When you delete a user account from a Microsoft Entra tenant, the corresponding user object is moved to the recycle bin. When this delete operation is synchronized to your managed domain, the corresponding user account is deleted because Domain Services doesn't have a recycle bin.

If the user account is restored in the tenant, Domain Services fetches all links for the account when it synchronizes the change to the managed domain. The user account in the managed domain gets a new globally unique identifier (GUID) and security ID (SID).