---
layout: Conceptual
title: Microsoft Entra provisioning Agent gMSA PowerShell cmdlets - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-gmsa-cmdlets
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Learn how to use the Microsoft Entra provisioning agent gMSA PowerShell cmdlets.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: 506de53d-f0c0-585e-7009-1ea579db907e
document_version_independent_id: fa4a19c4-2db7-93bd-6d56-3c65aea9bd39
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-gmsa-cmdlets.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-gmsa-cmdlets
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-gmsa-cmdlets.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 44eb8e65-81af-d23d-48b8-01cddfc13541
---

# Microsoft Entra provisioning Agent gMSA PowerShell cmdlets - Microsoft Entra ID | Microsoft Learn

The purpose of this document is to describe the Microsoft Entra Connect cloud provisioning agent gMSA PowerShell cmdlets. These cmdlets allow you to have more granularity on the permissions that are applied on the service account (gMSA). By default, Microsoft Entra Cloud Sync applies all permissions similar to Microsoft Entra Connect on the default gMSA or a custom gMSA, during cloud provisioning agent install.

This document covers the following cmdlets:

`Set-AADCloudSyncPermissions`

`Set-AADCloudSyncRestrictedPermissions`

## How to use the cmdlets:

The following prerequisites are required to use these cmdlets.

1. Install provisioning agent.
2. Import Provisioning Agent PowerShell module into a PowerShell session.

    ```powershell
    Import-Module "C:\Program Files\Microsoft Azure AD Connect Provisioning Agent\Microsoft.CloudSync.Powershell.dll"
    ```
3. These cmdlets require a parameter called `Credential` which can be passed, or prompts the user if not provided in the command line. Depending on the cmdlet syntax used, these credentials must be an enterprise admin account or, at a minimum, a domain administrator of the target domain where you're setting the permissions.
4. To create a variable for credentials, use:

    `$credential = Get-Credential`
5. To set Active Directory permissions for cloud provisioning agent, you can use the following cmdlet. This grants permissions in the root of the domain allowing the service account to manage on-premises Active Directory objects. See Using Set-AADCloudSyncPermissions below for examples on setting the permissions.

    `Set-AADCloudSyncPermissions -EACredential $credential`
6. To restrict Active Directory permissions set by default on the cloud provisioning agent account, you can use the following cmdlet. This increases service account security by disabling permission inheritance and removing all existing permissions, except SELF and Full Control for administrators. See Using Set-AADCloudSyncRestrictedPermission below for examples on restricting the permissions.

    `Set-AADCloudSyncRestrictedPermission -Credential $credential`

## Using Set-AADCloudSyncPermissions

`Set-AADCloudSyncPermissions` supports the following permission types which are identical to the permissions used by Azure AD Connect Classic Sync (ADSync). The following permission types are supported:

| Permission type | Description |
| --- | --- |
| BasicRead | See [BasicRead](../connect/how-to-connect-configure-ad-ds-connector-account#configure-basic-read-only-permissions) permissions for Microsoft Entra Connect |
| PasswordHashSync | See [PasswordHashSync](../connect/how-to-connect-configure-ad-ds-connector-account#permissions-for-password-hash-synchronization) permissions for Microsoft Entra Connect |
| PasswordWriteBack | See [PasswordWriteBack](../connect/how-to-connect-configure-ad-ds-connector-account#permissions-for-password-writeback) permissions for Microsoft Entra Connect |
| HybridExchangePermissions | See [HybridExchangePermissions](../connect/how-to-connect-configure-ad-ds-connector-account#permissions-for-exchange-hybrid-deployment) permissions for Microsoft Entra Connect |
| ExchangeMailPublicFolderPermissions | See [ExchangeMailPublicFolderPermissions](../connect/how-to-connect-configure-ad-ds-connector-account#permissions-for-exchange-mail-public-folders) permissions for Microsoft Entra Connect |
| UserGroupCreateDelete | Permissions for Microsoft Entra Cloud Sync's Group Provision to AD. Applies 'Create/delete User objects' on 'This object and all descendant objects' and Applies 'Create/delete group objects' on 'This object and all descendant objects' |
| All | Applies all the above permissions |

You can use AADCloudSyncPermissions in one of two ways:

- Grant permissions to all configured domains
- Grant permissions to a specific domain

## Grant permissions to all configured domains

Granting certain permissions to all configured domains requires the use of an enterprise admin account.

```powershell
$credential = Get-Credential
Set-AADCloudSyncPermissions -PermissionType "Any mentioned above" -EACredential $credential 
```

## Grant permissions to a specific domain

Granting certain permissions to a specific domain requires the use of a TargetDomainCredential that is enterprise admin or, domain admin of the target domain. The TargetDomain has to be already configured through wizard.

```powershell
$credential = Get-Credential
Set-AADCloudSyncPermissions -PermissionType "Any mentioned above" -TargetDomain "FQDN of domain" -TargetDomainCredential $credential
```

## Using Set-AADCloudSyncRestrictedPermissions

For increased security, `Set-AADCloudSyncRestrictedPermissions` refines the permissions set on the cloud provisioning agent account itself. Hardening permissions on the cloud provisioning agent account involves the following changes:

- Disable inheritance
- Remove all default permissions, except ACEs specific to SELF.
- Set Full Control permissions for SYSTEM, Administrators, Domain Admins, and Enterprise Admins.
- Set Read permissions for Authenticated Users and Enterprise Domain Controllers.

    The -Credential parameter is necessary to specify the Administrator account that has the necessary privileges to restrict Active Directory permissions on the cloud provisioning agent account. This is typically the domain or enterprise administrator.

For Example:

```powershell
$credential = Get-Credential 
Set-AADCloudSyncRestrictedPermissions -Credential $credential  
```