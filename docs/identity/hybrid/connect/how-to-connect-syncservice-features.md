---
layout: Conceptual
title: Microsoft Entra Connect Sync service features and configuration - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-syncservice-features
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Describes service side features for Microsoft Entra Connect Sync service.
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.tgt_pltfrm: na
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.subservice: hybrid-connect
ai-usage: ai-assisted
locale: en-us
document_id: 927c291d-30dd-7d84-8fe3-3b50f30c5f52
document_version_independent_id: 3477adb1-4a2e-2ad0-5cf6-402269e3d1dd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-syncservice-features.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-syncservice-features
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-syncservice-features.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 93940460-32b3-8677-7ccc-7a60bd392b98
---

# Microsoft Entra Connect Sync service features and configuration - Microsoft Entra ID | Microsoft Learn

The synchronization feature of Microsoft Entra Connect has two components:

- The on-premises component named **Microsoft Entra Connect Sync**, also called **sync engine**.
- The service residing in Microsoft Entra ID also known as **Microsoft Entra Connect Sync service**

This topic explains how the following features of the **Microsoft Entra Connect Sync service** work and how you can configure them using PowerShell.

To see the configuration in your Microsoft Entra directory using the Graph PowerShell, use the following commands:

```powershell
Connect-MgGraph -Scopes "OnPremDirectorySynchronization.Read.All"

Get-MgDirectoryOnPremiseSynchronization | Select-Object -ExpandProperty Features | Format-List
```

The result looks like this output:

```powershell
BlockCloudObjectTakeoverThroughHardMatchEnabled  : False
BlockSoftMatchEnabled                            : False
BypassDirSyncOverridesEnabled                    : False
CloudPasswordPolicyForPasswordSyncedUsersEnabled : False
ConcurrentCredentialUpdateEnabled                : False
ConcurrentOrgIdProvisioningEnabled               : False
DeviceWritebackEnabled                           : False
DirectoryExtensionsEnabled                       : True
FopeConflictResolutionEnabled                    : False
GroupWriteBackEnabled                            : False
PasswordSyncEnabled                              : True
PasswordWritebackEnabled                         : False
QuarantineUponProxyAddressesConflictEnabled      : False
QuarantineUponUpnConflictEnabled                 : False
SoftMatchOnUpnEnabled                            : True
SynchronizeUpnForManagedUsersEnabled             : False
UnifiedGroupWritebackEnabled                     : True
UserForcePasswordChangeOnLogonEnabled            : False
UserWritebackEnabled                             : True
AdditionalProperties                             : {
       allowOnPremUpdateOfOnPremisesObjectIdentifierEnabled : False
}
```

Note

From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Microsoft Entra directories. This feature was rolled out and enabled on directories created before this date. You'll receive an email notification when your directory is about to get this feature enabled.

The following settings are configured in Microsoft Entra Connect:

| DirSyncFeature | Comment |
| --- | --- |
| SoftMatchOnUpn | Allows objects to join on userPrincipalName in addition to primary SMTP address. |
| SynchronizeUpnForManagedUsers | Allows the sync engine to update the userPrincipalName attribute for managed/licensed (nonfederated) users. |
| DeviceWriteback | [Microsoft Entra Connect: Enabling device writeback](how-to-connect-device-writeback) |
| DirectoryExtensions | [Microsoft Entra Connect Sync: Directory extensions](how-to-connect-sync-feature-directory-extensions) |
| DuplicateProxyAddressResiliencyDuplicateUPNResiliency | Allows an attribute to be quarantined when it's a duplicate of another object rather than failing the entire object during export. |
| Password Hash Sync | [Implementing password hash synchronization with Microsoft Entra Connect Sync](how-to-connect-password-hash-synchronization) |
| Password Writeback | Not supported. This service feature is discontinued. To configure Password Writeback see [Enable password writeback in Microsoft Entra Connect](../../authentication/tutorial-enable-sspr-writeback#enable-password-writeback-in-microsoft-entra-connect) |
| Pass-through Authentication | [User sign-in with Microsoft Entra pass-through authentication](how-to-connect-pta) |
| UnifiedGroupWriteback | Group writeback |
| UserWriteback | Not currently supported. |

## Duplicate attribute resiliency

Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is "quarantined" and a temporary value is assigned. When the conflict is resolved, the temporary UPN is changed to the proper value automatically. For more information, see [Identity synchronization and duplicate attribute resiliency](how-to-connect-syncservice-duplicate-attribute-resiliency).

## UserPrincipalName soft match

When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled. Soft-match is used to match existing cloud users in Microsoft Entra ID with on-premises users.

If you need to match on-premises AD accounts with existing accounts created in the cloud and you aren't using Exchange Online, then this feature is useful. In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.

This feature is on by default for newly created Microsoft Entra directories. You can see if this feature is enabled for you by running:

```powershell
Connect-MgGraph -Scopes "OnPremDirectorySynchronization.Read.All"

$DirectorySync = Get-MgDirectoryOnPremiseSynchronization
$DirectorySync.Features.SoftMatchOnUpnEnabled
```

If this feature isn't enabled for your Microsoft Entra directory, then you can enable it by running:

```powershell
Connect-MgGraph -Scopes "OnPremDirectorySynchronization.ReadWrite.All"

$SoftMatchOnUpn = @{ SoftMatchOnUpnEnabled = "true" }
Update-MgDirectoryOnPremiseSynchronization -Features $SoftMatchOnUpn `
   -OnPremisesDirectorySynchronizationId $DirectorySync.Id
```

## BlockSoftMatch

When this feature is enabled, it blocks the Soft Match feature. Customers are encouraged to enable this feature and keep it at enabled until Soft Matching is required again for their tenancy. This flag should be enabled again after any soft matching has completed and is no longer needed.

Example - Blocking soft matching in your tenant:

```powershell
Connect-MgGraph -Scopes "OnPremDirectorySynchronization.ReadWrite.All"

$SoftBlock = @{ BlockSoftMatchEnabled = "true" }
Update-MgDirectoryOnPremiseSynchronization -Features $SoftBlock `
   -OnPremisesDirectorySynchronizationId $DirectorySync.Id
```

Note

When BlockSoftMatch is enabled, new hybrid-joined devices will encounter an InvalidSoftMatch error during a Soft Match attempt. This occurs when the computer object synchronized from on-premises Active Directory (AD) to Entra is merged with the new device registered in the cloud. To resolve this issue, administrators should temporarily disable BlockSoftMatch to allow the hybrid join to proceed.

## Allow onPremisesObjectIdentifier updates during hard match enforcement

Due to hard-match security enforcement, Microsoft Entra ID blocks a hard match when the target cloud user's `onPremisesObjectIdentifier` value differs from the incoming value from the on-premises object. To remediate the issue, clear the existing cloud user's `onPremisesObjectIdentifier` value and retry the hard match.

If remediation isn't possible, temporarily enable the tenant-level feature flag `allowOnPremUpdateOfOnPremisesObjectIdentifierEnabled` to allow the update. The flag is disabled by default and should be used only as a temporary bypass during migration, recovery, or consolidation scenarios. Disable the flag after remediation is complete.

For the enablement steps and guidance on when to use this bypass, see [Temporarily allow onPremisesObjectIdentifier updates](how-to-connect-install-existing-tenant#temporarily-allow-onpremisesobjectidentifier-updates).

## Synchronize userPrincipalName updates

Historically, updates to the UserPrincipalName attribute using the sync service from on-premises was blocked, unless both of these conditions were true:

- The user managed (nonfederated).
- The user doesn't have a license assigned.

Note

From March 2019, synchronizing UPN changes for federated user accounts is allowed.

Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password hash sync or pass-through authentication.

This feature is on by default for newly created Microsoft Entra directories. You can see if this feature is enabled for you by running:

```powershell
Connect-MgGraph -Scopes "OnPremDirectorySynchronization.Read.All"

$DirectorySync = Get-MgDirectoryOnPremiseSynchronization
$DirectorySync.Features.SynchronizeUpnForManagedUsersEnabled
```

If this feature isn't enabled for your Microsoft Entra directory, then you can enable it by running:

```powershell
Connect-MgGraph -Scopes "OnPremDirectorySynchronization.ReadWrite.All"

$SyncUpnManagedUsers = @{ SynchronizeUpnForManagedUsersEnabled = "true" }
Update-MgDirectoryOnPremiseSynchronization -Features $SyncUpnManagedUsers `
   -OnPremisesDirectorySynchronizationId $DirectorySync.Id
```

After enabling this feature, existing userPrincipalName values remain as-is. On next change of the userPrincipalName attribute on-premises, the normal delta sync on users updates the UPN. Once this feature is enabled, it's not possible to disable it.

## Password Hash Sync

This feature allows the sync engine to use password hash synchronization and is automatically enabled by the sync client.

You can see if this feature is enabled for you by running:

```powershell
# Connect to Microsoft Graph
Connect-MgGraph -Scopes "OnPremDirectorySynchronization.Read.All"

# Retrieve DirSync service features
$DirectorySync = Get-MgDirectoryOnPremiseSynchronization
$DirectorySync.Features.PasswordSyncEnabled
```

If password hash sync is no longer needed, for example, after decommissioning synchronization from on-premises Active Directory, you can disable it using:

```powershell
# Connect to Microsoft Graph
Connect-MgGraph -Scopes "OnPremDirectorySynchronization.ReadWrite.All"

# Disable Password Hash Sync
$DirectorySync = Get-MgDirectoryOnPremiseSynchronization
$DirectorySync.Features.PasswordSyncEnabled = $false
Update-MgDirectoryOnPremiseSynchronization -Features $DirectorySync.Features -OnPremisesDirectorySynchronizationId $DirectorySync.Id

```

## Password Writeback

This property indicates whether password writeback from Microsoft Entra ID to on-premises Active Directory is enabled.

Important

This property is no longer in use, and updating it is not supported.