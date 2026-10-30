---
layout: Conceptual
title: On-premises password writeback with self-service password reset - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-sspr-writeback
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how password change or reset events in Microsoft Entra ID can be written back to an on-premises directory environment
ms.topic: concept-article
ms.date: 2025-10-25T00:00:00.0000000Z
ms.reviewer: tilarso
locale: en-us
document_id: ebc51bb0-dd9d-cb3f-3e3f-b9765b48f21d
document_version_independent_id: d597a70e-8fb1-0e4e-8ae0-e3cd87de1118
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-sspr-writeback.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-sspr-writeback
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-sspr-writeback.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e6566d12-f1c0-1d55-5b2a-8f5e4cedd5b8
---

# On-premises password writeback with self-service password reset - Microsoft Entra ID | Microsoft Learn

Microsoft Entra self-service password reset (SSPR) lets users reset their passwords in the cloud, but most companies also have an on-premises Active Directory Domain Services (AD DS) environment for users. Password writeback allows password changes in the cloud to be written back to an on-premises directory in real time by using either [Microsoft Entra Connect](../hybrid/whatis-hybrid-identity) or [Microsoft Entra Connect cloud sync](tutorial-enable-cloud-sync-sspr-writeback). When users change or reset their passwords using SSPR in the cloud, the updated passwords also written back to the on-premises AD DS environment.

Important

This conceptual article explains to an administrator how self-service password reset writeback works. If you're an end user already registered for self-service password reset and need to get back into your account, go to https://aka.ms/sspr.

If your IT team hasn't enabled the ability to reset your own password, reach out to your helpdesk for additional assistance.

Password writeback is supported in environments that use the following hybrid identity models:

- [Password hash synchronization](../hybrid/connect/how-to-connect-password-hash-synchronization)
- [Pass-through authentication](../hybrid/connect/how-to-connect-pta)
- [Active Directory Federation Services](../hybrid/connect/how-to-connect-fed-management)

Note

SSPR with writeback to an on-premises domain isn't supported when staged rollout is enabled for a security group. Although it works in some cases, SSPR can't be guaranteed to work consistently when staged rollout is enabled.

Password writeback provides the following features:

- **Enforcement of on-premises Active Directory Domain Services (AD DS) password policies**: When a user resets their password, it's checked to ensure it meets your on-premises AD DS policy before committing it to that directory. This review includes checking the history, complexity, age, password filters, and any other password restrictions that you define in AD DS.
- **Zero-delay feedback**: Password writeback is a synchronous operation. Users are notified immediately if their password doesn't meet the policy or can't be reset or changed for any reason.
- **Supports password changes from the access panel and Microsoft 365**: When federated or password hash synchronized users come to change their expired or non-expired passwords, those passwords are written back to AD DS.
- **Supports password writeback when an admin resets them from the Microsoft Entra admin center**: When an admin resets a user's password in the [Microsoft Entra admin center](https://entra.microsoft.com), if that user is federated or password hash synchronized, the password is written back to on-premises. This functionality is currently not supported in the Office admin portal.
- **Doesn't require any inbound firewall rules**: Password writeback uses an Azure Service Bus relay as an underlying communication channel. All communication is outbound over port 443.
- **Supports side-by-side domain-level deployment** using [Microsoft Entra Connect](tutorial-enable-sspr-writeback) or [cloud sync](tutorial-enable-cloud-sync-sspr-writeback) to target different sets of users depending on their needs, including users who are in disconnected domains.

Note

The on-premises service account that handles password write-back requests cannot change the passwords for users that belong to protected groups. Administrators can change their password in the cloud but they cannot use password write-back to reset a forgotten password for their on-premises user. For more information about protected groups, see [Protected accounts and groups in AD DS](/en-us/windows-server/identity/ad-ds/plan/security-best-practices/appendix-c--protected-accounts-and-groups-in-active-directory).

To get started with SSPR writeback, complete either one or both of the following tutorials:

- [Tutorial: Enable self-service password reset (SSPR) writeback](tutorial-enable-sspr-writeback)
- [Tutorial: Enable Microsoft Entra Connect cloud sync self-service password reset writeback to an on-premises environment](tutorial-enable-cloud-sync-sspr-writeback)

## Microsoft Entra Connect and cloud sync side-by-side deployment

You can deploy Microsoft Entra Connect and cloud sync side-by-side in different domains to target different sets of users. This helps existing users continue to writeback password changes while adding the option in cases where users are in disconnected domains because of a company merger or split. Microsoft Entra Connect and cloud sync can be configured in different domains so users from one domain can use Microsoft Entra Connect while users in another domain use cloud sync. Cloud sync can also provide higher availability because it doesn't rely on a single instance of Microsoft Entra Connect. For a feature comparison between the two deployment options, see [Comparison between Microsoft Entra Connect and cloud sync](../hybrid/cloud-sync/connect-to-cloud-sync-decision-guide#comparison-between-microsoft-entra-connect-and-cloud-sync).

Note

When Microsoft Entra Connect Cloud Sync and Microsoft Entra Connect Sync coexist and are configured for the same domain, all password writeback operations for users synchronized from that domain are processed by the Cloud Sync agent.

## How password writeback works

When a user account configured for federation, password hash synchronization (or, in the case of a Microsoft Entra Connect deployment, pass-through authentication) attempts to reset or change a password in the cloud, the following actions occur:

1. A check is performed to see what type of password the user has. If the password is managed on-premises:

    - A check is performed to see if the writeback service is up and running. If it is, the user can proceed.
    - If the writeback service is down, the user is informed that their password can't be reset right now.
2. Next, the user passes the appropriate authentication gates and reaches the **Reset password** page.
3. The user selects a new password and confirms it.
4. When the user selects **Submit**, the plaintext password is encrypted with a public key created during the writeback setup process.
5. The encrypted password is included in a payload that gets sent over an HTTPS channel to your tenant-specific service bus relay (that is set up for you during the writeback setup process). This relay is protected by a randomly generated password that only your on-premises installation knows.
6. After the message reaches the service bus, the password-reset endpoint automatically wakes up and sees that it has a reset request pending.
7. The service then looks for the user by using the cloud anchor attribute. For this lookup to succeed, the following conditions must be met:

    - The user object must exist in the AD DS connector space.
    - The user object must be linked to the corresponding metaverse (MV) object.
    - The user object must be linked to the corresponding Microsoft Entra connector object.
    - The link from the AD DS connector object to the MV must have the synchronization rule `Microsoft.InformADUserAccountEnabled.xxx` on the link.

    When the call comes in from the cloud, the synchronization engine uses the **cloudAnchor** attribute to look up the Microsoft Entra connector space object. It then follows the link back to the MV object, and then follows the link back to the AD DS object. Because there can be multiple AD DS objects (multi-forest) for the same user, the sync engine relies on the `Microsoft.InformADUserAccountEnabled.xxx` link to pick the correct one.
8. After the user account is found, an attempt to reset the password directly in the appropriate AD DS forest is made.
9. If the password set operation is successful, the user is told their password has been changed.

    Note

    If the user's password hash is synchronized to Microsoft Entra ID by using password hash synchronization, there's a chance that the on-premises password policy is weaker than the cloud password policy. In this case, the on-premises policy is enforced. This policy ensures that your on-premises policy is enforced in the cloud, no matter if you use password hash synchronization or federation to provide single sign-on.
10. If the password set operation fails, an error prompts the user to try again. The operation might fail because of the following reasons:

    - The service was down.
    - The password they selected doesn't meet the organization's policies.
    - Unable to find the user in local AD DS environment.

    The error messages provide guidance to users so they can attempt to resolve without administrator intervention.

## Password writeback security

Password writeback is a highly secure service. To ensure your information is protected, a four-tiered security model is enabled as follows:

- **Tenant-specific service-bus relay**
    - When you set up the service, a tenant-specific service bus relay is set up that's protected by a randomly generated strong password that Microsoft never has access to.
- **Locked down, cryptographically strong, password encryption key**
    - After the service bus relay is created, a strong symmetric key is created that is used to encrypt the password as it comes over the wire. This key only lives in your company's secret store in the cloud, which is heavily locked down and audited, just like any other password in the directory.
- **Industry standard Transport Layer Security (TLS)**
    1. When a password reset or change operation occurs in the cloud, the plaintext password is encrypted with your public key.
    2. The encrypted password is placed into an HTTPS message that's sent over an encrypted channel by using Microsoft TLS/SSL certs to your service bus relay.
    3. After the message arrives in the service bus, your on-premises agent wakes up and authenticates to the service bus by using the strong password that was previously generated.
    4. The on-premises agent picks up the encrypted message and decrypts it by using the private key.
    5. The on-premises agent attempts to set the password through the AD DS SetPassword API. This step is what allows enforcement of your AD DS on-premises password policy (such as the complexity, age, history, and filters) in the cloud.
- **Message expiration policies**
    - If the message sits in service bus because your on-premises service is down, it times out and is removed after several minutes. The time-out and removal of the message increases security even further.

### Password writeback encryption details

After a user submits a password reset, the reset request goes through several encryption steps before it arrives in your on-premises environment. These encryption steps ensure maximum service reliability and security. They are described as follows:

1. **Password encryption with 2048-bit RSA Key**: After a user submits a password to be written back to on-premises, the submitted password itself is encrypted with a 2048-bit RSA key.
2. **Package-level encryption with 256-bit AES-GCM**: The entire package, the password plus the required metadata, is encrypted by using AES-GCM (with a key size of 256 bits). This encryption prevents anyone with direct access to the underlying Service Bus channel from viewing or tampering with the contents.
3. **All communication occurs over TLS/SSL**: All the communication with Service Bus happens in an SSL/TLS channel. This encryption secures the contents from unauthorized third parties.
4. **Automatic key rollover every six months**: All keys roll over every six months, or every time password writeback is disabled and then re-enabled on Microsoft Entra Connect, to ensure maximum service security and safety.

### Password writeback bandwidth usage

Password writeback is a low-bandwidth service that only sends requests back to the on-premises agent under the following circumstances:

- Two messages are sent when the feature is enabled or disabled through Microsoft Entra Connect.
- One message is sent once every five minutes as a service heartbeat for as long as the service is running.
- Two messages are sent each time a new password is submitted:
    - The first message is a request to perform the operation.
    - The second message contains the result of the operation, and is sent in the following circumstances:
        - Each time a new password is submitted during a user self-service password reset.
        - Each time a new password is submitted during a user password change operation.
        - Each time a new password is submitted during an admin-initiated user password reset (only from Entra admin portals).

#### Message size and bandwidth considerations

The size of each of the message described previously is typically under 1 KB. Even under extreme loads, the password writeback service itself is consuming a few kilobits per second of bandwidth. Because each message is sent in real time, only when required by a password update operation, and because the message size is so small, the bandwidth usage of the writeback capability is too small to have a measurable impact.

## Supported writeback operations

Passwords are written back in all the following situations:

- **Supported end-user operations**

    - Any end-user self-service voluntary change password operation.
    - Any end-user self-service force change password operation, for example, password expiration.
    - Any end-user self-service password reset that originates from the [password reset portal](https://passwordreset.microsoftonline.com).
- **Supported administrator operations**

    - Any administrator self-service voluntary change password operation.
    - Any administrator self-service force change password operation, for example, password expiration.
    - Any administrator self-service password reset that originates from the [password reset portal](https://passwordreset.microsoftonline.com).
    - Any administrator-initiated end-user password reset from the Microsoft Entra admin center.
    - Any administrator-initiated end-user password reset from the [Microsoft Graph API](/en-us/graph/api/authenticationmethod-resetpassword).

## Unsupported writeback operations

Passwords aren't written back in any of the following situations:

- **Unsupported end-user operations**

    - Any end user resetting their own password by using PowerShell version 1, version 2, or the Microsoft Graph API.
- **Unsupported administrator operations**

    - Any administrator-initiated end-user password reset from PowerShell version 1, or version 2.
    - Any administrator-initiated end-user password reset from the [Microsoft 365 admin center](https://admin.microsoft.com).
    - Any administrator cannot use password reset tool to reset their own password for password writeback.

Note

If a user has the option "Password never expires" set in Active Directory (AD), the force password change flag will not be set in Active Directory (AD), so the user will not be prompted to change the password during the next sign-in even if the option to force the user to change their password on next logon option is selected during an administrator-initiated end-user password reset.