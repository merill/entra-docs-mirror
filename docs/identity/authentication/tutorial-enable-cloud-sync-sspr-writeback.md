---
layout: Conceptual
title: Enable Microsoft Entra Connect cloud sync password writeback - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/tutorial-enable-cloud-sync-sspr-writeback
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: In this tutorial, you learn how to enable Microsoft Entra self-service password reset writeback using Microsoft Entra Connect cloud sync to synchronize changes back to an on-premises Active Directory Domain Services environment.
ms.topic: tutorial
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: tilarso
locale: en-us
document_id: 2ca26ebb-5558-75b9-7394-862bbd22b120
document_version_independent_id: e84b2a95-67ad-7e54-d4c7-977e01a0d3ea
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/tutorial-enable-cloud-sync-sspr-writeback.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/tutorial-enable-cloud-sync-sspr-writeback
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/tutorial-enable-cloud-sync-sspr-writeback.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9a4e85a5-5f68-5a9e-2f0f-ca3e0ff5b042
---

# Enable Microsoft Entra Connect cloud sync password writeback - Microsoft Entra ID | Microsoft Learn

Note

Self-service password reset writeback with Cloud sync isn't supported in Microsoft Azure operated by 21Vianet. Instead, admins can deploy SSPR writeback with [Microsoft Entra Connect sync](tutorial-enable-sspr-writeback).

Microsoft Entra Cloud sync can synchronize Microsoft Entra password changes in real time between users in disconnected on-premises Active Directory Domain Services (AD DS) domains. Microsoft Entra Cloud sync can run side-by-side with [Microsoft Entra Connect](tutorial-enable-sspr-writeback) at the domain level to simplify password writeback for additional scenarios, such as users who are in disconnected domains because of a company split or merge. You can configure each service in different domains to target different sets of users depending on their needs. Microsoft Entra Cloud sync uses the lightweight Microsoft Entra cloud provisioning agent to simplify the setup for self-service password reset (SSPR) writeback and provide a secure way to send password changes in the cloud back to an on-premises directory.

## Prerequisites

- A Microsoft Entra tenant with at least a Microsoft Entra ID P1 or trial license enabled. If needed, [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator) account
- Microsoft Entra ID configured for self-service password reset. If needed, complete this tutorial to enable Microsoft Entra SSPR.
- An on-premises AD DS environment configured with [Microsoft Entra Cloud sync version 1.1.977.0 or later](../app-provisioning/provisioning-agent-release-version-history). Learn how to [identify the agent's current version](../hybrid/cloud-sync/how-to-automatic-upgrade).

## Deployment steps

1. Configure Microsoft Entra Cloud sync service account permissions
2. Enable password writeback in Microsoft Entra Connect cloud sync
3. Enable password writeback for SSPR

### Configure Microsoft Entra Cloud sync service account permissions

Permissions for cloud sync are configured by default. If permissions need to be reset, see Troubleshooting for more details about the specific permissions required for password writeback and how to set them by using PowerShell.

### Enable password writeback in SSPR

You can enable Microsoft Entra Connect cloud sync provisioning directly in the Microsoft Entra admin center or through PowerShell.

#### Enable password writeback in the Microsoft Entra admin center

With password writeback enabled in Microsoft Entra Connect cloud sync, now verify, and configure Microsoft Entra self-service password reset (SSPR) for password writeback. When you enable SSPR to use password writeback, users who change or reset their password have that updated password synchronized back to the on-premises AD DS environment as well.

To verify and enable password writeback in SSPR, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Password reset**, then choose **On-premises integration**.
3. Check the option for **Enable password write back for synced users**.
4. (optional) If Microsoft Entra Connect provisioning agents are detected, you can additionally check the option for **Write back passwords with Microsoft Entra Connect cloud sync**.
5. Check the option for **Allow users to unlock accounts without resetting their password** to *Yes*.

    ![Enable Microsoft Entra self-service password reset for password writeback](media/tutorial-enable-sspr-writeback/enable-sspr-writeback-cloudsync.png)
6. When ready, select **Save**.

#### PowerShell

With PowerShell you can enable Microsoft Entra Connect cloud sync by using the Set-AADCloudSyncPasswordWritebackConfiguration cmdlet on the servers with the provisioning agents.

```powershell
Import-Module 'C:\\Program Files\\Microsoft Azure AD Connect Provisioning Agent\\Microsoft.CloudSync.Powershell.dll' 
Set-AADCloudSyncPasswordWritebackConfiguration -Enable $true -Credential $(Get-Credential)
```

## Clean up resources

If you no longer want to use the SSPR writeback functionality you configured as part of this tutorial, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Password reset**, then choose **On-premises integration**.
3. Uncheck the option for **Enable password write back for synced users**.
4. Uncheck the option for **Write back passwords with Microsoft Entra Connect cloud sync**.
5. Uncheck the option for **Allow users to unlock accounts without resetting their password**.
6. When ready, select **Save**.

If you no longer want to use the Microsoft Entra Connect cloud sync for SSPR writeback functionality but want to continue using Microsoft Entra Connect Sync agent for writebacks complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Password reset**, then choose **On-premises integration**.
3. Uncheck the option for **Write back passwords with Microsoft Entra Connect cloud sync**.
4. When ready, select **Save**.

You can also use PowerShell to disable Microsoft Entra Connect cloud sync for SSPR writeback functionality, from your Microsoft Entra Connect cloud sync server, run `Set-AADCloudSyncPasswordWritebackConfiguration` using Hybrid Identity Administrator credentials to disable password writeback with Microsoft Entra Connect cloud sync.

```powershell
Import-Module ‘C:\\Program Files\\Microsoft Azure AD Connect Provisioning Agent\\Microsoft.CloudSync.Powershell.dll’ 
Set-AADCloudSyncPasswordWritebackConfiguration -Enable $false -Credential $(Get-Credential)
```

## Supported operations

Passwords are written back in the following situations for end-users and administrators.

| Account | Supported operations |
| --- | --- |
| End users | Any end-user self-service voluntary change password operation.Any end-user self-service force change password operation, for example, password expiration.Any end-user self-service password reset that originates from password reset. |
| Administrators | Any administrator self-service voluntary change password operation.Any administrator self-service force change password operation, for example, password expiration.Any administrator self-service password reset that originates from password reset. Any administrator-initiated end-user password reset from the Microsoft Entra admin center.Any administrator-initiated end-user password reset from the Microsoft Graph API. |

## Unsupported operations

Passwords aren't written back in the following situations.

| Account | Unsupported operations |
| --- | --- |
| End users | Any end user resetting their own password by using PowerShell cmdlets or the Microsoft Graph API. |
| Administrators | Any administrator-initiated end-user password reset by using PowerShell cmdlets.Any administrator-initiated end-user password reset from the Microsoft 365 admin center.Any administrator can't use password reset tool to reset their own password, or any other Administrator in Microsoft Entra ID for password writeback. |

## Validation scenarios

Try the following operations to validate scenarios using password writeback. All validation scenarios require cloud sync is installed and the user is in scope for password writeback.

| Scenario | Details |
| --- | --- |
| Reset password from the sign-in page | Have two users from disconnected domains and forests perform SSPR. You could also have Microsoft Entra Connect and cloud sync deployed side-by-side and have one user in the scope of cloud sync configuration and another in scope of Microsoft Entra Connect and have those users reset their password. |
| Force expired password change | Have two users from disconnected domains and forests change expired passwords. You could also have Microsoft Entra Connect and cloud sync deployed side-by-side and have one user in the scope of cloud sync configuration and another in scope of Microsoft Entra Connect. |
| Regular password change | Have two users from disconnected domains and forests perform routine password change. You could also have Microsoft Entra Connect and cloud sync side by side and have one user in the scope of cloud sync config and another in scope of Microsoft Entra Connect. |
| Admin reset user password | Have two users disconnected domains and forests reset their password from the Microsoft Entra admin center or Frontline worker portal. You could also have Microsoft Entra Connect and cloud sync side by side and have one user in the scope of cloud sync config and another in scope of Microsoft Entra Connect |
| Self-service account unlock | Have two users from disconnected domains and forests unlock accounts in the SSPR portal resetting the password. You could also have Microsoft Entra Connect and cloud sync side by side and have one user in the scope of cloud sync config and another in scope of Microsoft Entra Connect. |

## Troubleshooting

- The Microsoft Entra Connect cloud sync group Managed Service Account should have the following permissions set to writeback the passwords by default:

    - Reset password
    - Write permissions on lockoutTime
    - Write permissions on pwdLastSet
    - Extended rights for "Unexpire Password" on the root object of each domain in that forest, if not already set.

    If these permissions aren't set, you can set the PasswordWriteBack permission on the service account by using the Set-AADCloudSyncPermissions cmdlet and on-premises enterprise administrator credentials:

    ```powershell
    Import-Module ‘C:\\Program Files\\Microsoft Azure AD Connect Provisioning Agent\\Microsoft.CloudSync.Powershell.dll’ 
    Set-AADCloudSyncPermissions -PermissionType PasswordWriteBack -EACredential $(Get-Credential)
    ```

    After you updated the permissions, it can take up to an hour or more for these permissions to replicate to all the objects in your directory.
- If passwords for some user accounts aren't written back to the on-premises directory, make sure that inheritance isn't disabled for the account in the on-premises AD DS environment. Write permissions for passwords must be applied to descendant objects for the feature to work correctly.
- Password policies in the on-premises AD DS environment can prevent password resets from being correctly processed. If you're testing this feature and want to reset password for users more than once per day, the group policy for Minimum password age must be set to 0. This setting can be found under Computer Configuration &gt; Policies &gt; Windows Settings &gt; Security Settings &gt; Account Policies &gt; Password Policy within gpmc.msc.
- If you update the group policy, wait for the updated policy to replicate, or use the gpupdate /force command.
- For passwords to be changed immediately, Minimum password age must be set to 0. However, if users adhere to the on-premises policies, and the Minimum password age is set to a value greater than zero, password writeback won't work after the on-premises policies are evaluated.

For more information about how to validate or set up the appropriate permissions, see [Configure account permissions for Microsoft Entra Connect](tutorial-enable-sspr-writeback#configure-account-permissions-for-azure-ad-connect).