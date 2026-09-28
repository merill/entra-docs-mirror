---
layout: Conceptual
title: Configure Security Defaults for Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/security-defaults
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Enable Microsoft Entra ID security defaults to strengthen your organization's security posture with preconfigured MFA requirements and legacy authentication protection.
ms.topic: how-to
ms.date: 2025-07-21T00:00:00.0000000Z
ms.reviewer: sama
ms.custom:
- sfi-ga-nochange, sfi-image-nochange
- ai-gen-docs-bap
- ai-gen-title
- ai-seo-date:07/21/2025
- ai-gen-description
locale: en-us
document_id: cfac0ecf-e5a9-c5ff-f8c2-ce27789708f5
document_version_independent_id: 0f5e0cc9-a54f-a5c8-192d-d60a6a4db3ff
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/security-defaults.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/security-defaults
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/security-defaults.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: fa3ceeb3-bbaf-ab83-23bb-167c081d0d54
---

# Configure Security Defaults for Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Security defaults make it easier to help protect your organization from identity-related attacks like password spray, replay, and phishing common in today's environments.

Microsoft is making these preconfigured security settings available to everyone, because we know managing security can be difficult. Based on our learnings more than 99.9% of those common identity-related attacks are stopped by using multifactor authentication and blocking legacy authentication. Our goal is to ensure that all organizations have at least a basic level of security enabled at no extra cost.

These basic controls include:

- Requiring all users to register for multifactor authentication
- Requiring administrators to do multifactor authentication
- Requiring users to do multifactor authentication when necessary
- Blocking legacy authentication protocols
- Blocking device code flow
- Protecting privileged activities like access to the Azure portal

## Who's it for?

- Organizations who want to increase their security posture, but don't know how or where to start.
- Organizations using the free tier of Microsoft Entra ID licensing.

### Who should use Conditional Access?

- If you're an organization with Microsoft Entra ID P1 or P2 licenses, security defaults are probably not right for you.
- If your organization has complex security requirements, you should consider [Conditional Access](/en-us/entra/identity/conditional-access/concept-conditional-access-policy-common).

## Enabling security defaults

If your tenant was created on or after October 22, 2019, security defaults might be enabled in your tenant. To protect all of our users, security defaults are being rolled out to all new tenants at creation.

While security defaults is enabled on all new tenants by default, there is a 24‑hour grace period before protections are enforced. This allows customers to access and provision their tenant before MFA is required.

To help protect organizations, we're always working to improve the security of Microsoft account services. As part of this protection, customers are periodically notified for the automatic enablement of the security defaults if they:

- Don't have any Conditional Access policies
- Don't have premium licenses
- Aren’t actively using legacy authentication clients

After this setting is enabled, all users in the organization will need to register for multifactor authentication. To avoid confusion, refer to the email you received and alternatively you can disable security defaults after it's enabled.

To configure security defaults in your directory, you must be assigned at least the [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) role.

By default, the user who creates a Microsoft Entra tenant is automatically assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role.

To enable security defaults:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Overview** &gt; **Properties**.
3. Select **Manage security defaults**.
4. Set **Security defaults** to **Enabled**.
5. Select **Save**.

[![Screenshot of the Microsoft Entra admin center with the toggle to enable security defaults](media/security-defaults/security-defaults-entra-admin-center.png)](media/security-defaults/security-defaults-entra-admin-center.png#lightbox)

### Revoking active tokens

As part of enabling security defaults, administrators should revoke all existing tokens to require all users to register for multifactor authentication. This revocation event forces previously authenticated users to authenticate and register for multifactor authentication. This task can be accomplished using the [Revoke-MgUserSignInSession](/en-us/powershell/module/microsoft.graph.users.actions/revoke-mgusersigninsession) cmdlet in the Microsoft Graph PowerShell SDK.

## Enforced security policies

### Require all users to register for Microsoft Entra multifactor authentication

Note

Starting July 29, 2024, new tenants and existing tenants have the 14-day grace period for users to register for MFA removed. We made this change to help reduce the risk of account compromise during the 14-day window, as MFA can block over 99.2% of identity-based attacks.

When users sign in and are prompted to perform multifactor authentication, they see a screen providing them with a number to enter in the Microsoft Authenticator app. This measure helps prevent users from falling for MFA fatigue attacks.

![Screenshot showing an example of the Approve sign in request window with a number to enter.](media/security-defaults/approve-sign-in-request.png)

### Require administrators to do multifactor authentication

Administrators have more access to your environment. Because of the power these highly privileged accounts have, treat them with special care. One common method to improve the protection of privileged accounts is to require a stronger form of account verification for sign-in, like requiring multifactor authentication.

Tip

Recommendations for your admins:

- Ensure all your admins sign in after enabling security defaults so that they can register for authentication methods.
- Have separate accounts for administration and standard productivity tasks to significantly reduce the number of times your admins are prompted for MFA.

After registration is finished, the following administrator roles will be required to do multifactor authentication every time they sign in:

- Global Administrator
- Application Administrator
- Authentication Administrator
- Billing Administrator
- Cloud Application Administrator
- Conditional Access Administrator
- Exchange Administrator
- Helpdesk Administrator
- Password Administrator
- Privileged Authentication Administrator
- Privileged Role Administrator
- Security Administrator
- SharePoint Administrator
- User Administrator

- Authentication Policy Administrator
- Identity Governance Administrator

*Also available as a [Microsoft-managed Conditional Access policy](../identity/conditional-access/managed-policies#upgrade-from-security-defaults) if you disable security defaults.*

### Require users to do multifactor authentication when necessary

We tend to think that administrator accounts are the only accounts that need extra layers of authentication. Administrators have broad access to sensitive information and can make changes to subscription-wide settings. But attackers frequently target end users.

After these attackers gain access, they can request access to privileged information for the original account holder. They can even download the entire directory to do a phishing attack on your whole organization.

One common method to improve protection for all users is to require a stronger form of account verification, such as multifactor authentication, for everyone. After users complete registration, they'll be prompted for another authentication whenever necessary. Microsoft decides when a user is prompted for multifactor authentication, based on factors such as location, device, role, and task. This functionality protects all registered applications, including SaaS applications.

Note

In case of [B2B direct connect](../external-id/b2b-direct-connect-overview) users, any multifactor authentication requirement from security defaults enabled in resource tenant needs to be satisfied, including multifactor authentication registration by the direct connect user in their home tenant.

*Also available as a [Microsoft-managed Conditional Access policy](../identity/conditional-access/managed-policies#upgrade-from-security-defaults) if you disable security defaults.*

### Block legacy authentication protocols

To give your users easy access to your cloud apps, we support various authentication protocols, including legacy authentication. *Legacy authentication* is a term that refers to an authentication request made by:

- Clients that don't use modern authentication (for example, an Office 2010 client)
- Any client that uses older mail protocols such as IMAP, SMTP, or POP3

Today, most compromising sign-in attempts come from legacy authentication. Legacy authentication doesn't support multifactor authentication. Even if you have a multifactor authentication policy enabled on your directory, an attacker can authenticate by using an older protocol and bypass multifactor authentication.

After security defaults are enabled in your tenant, all authentication requests made by an older protocol will be blocked. Security defaults blocks Exchange Active Sync basic authentication.

Warning

Before you enable security defaults, make sure your administrators aren't using older authentication protocols. For more information, see [How to move away from legacy authentication](../identity/conditional-access/policy-block-legacy-authentication).

- [How to set up a multifunction device or application to send email using Microsoft 365](/en-us/exchange/mail-flow-best-practices/how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365)

*Also available as a [Microsoft-managed Conditional Access policy](../identity/conditional-access/managed-policies#upgrade-from-security-defaults) if you disable security defaults.*

### Block device code flow

Device code flow is an authentication flow that lets users sign in to devices or applications that have limited input capabilities, such as devices without a browser or keyboard. Attackers can abuse device code flow in phishing attacks by tricking users into entering a code on another device.

After security defaults are enabled in your tenant, authentication requests that use device code flow are blocked. Applications or devices that depend on device code flow won't be able to complete sign-in while security defaults are enabled. If your organization needs granular control and exceptions, you should consider [Conditional Access](/en-us/entra/identity/conditional-access/concept-conditional-access-policy-common).

Note

Starting July 1, 2026, all new Microsoft Entra tenants block device code flow as part of security defaults. Applications or devices that depend on device code flow won't be able to complete sign-in while security defaults are enabled.

### Protect privileged activities like access to the Azure portal

Organizations use various Azure services managed through the Azure Resource Manager API, including:

- Azure portal
- Microsoft Entra admin center
- Azure PowerShell
- Azure CLI

Using Azure Resource Manager to manage your services is a highly privileged action. Azure Resource Manager can alter tenant-wide configurations, such as service settings and subscription billing. Single-factor authentication is vulnerable to various attacks like phishing and password spray.

It's important to verify the identity of users who want to access Azure Resource Manager and update configurations. You verify their identity by requiring more authentication before you allow access.

After you enable security defaults in your tenant, any user accessing the following services must complete multifactor authentication:

- Azure portal
- Microsoft Entra admin center
- Azure PowerShell
- Azure CLI

This policy applies to all users who are accessing Azure Resource Manager services, whether they're an administrator or a user. This policy applies to Azure Resource Manager APIs such as accessing your subscription, VMs, storage accounts, and so on. This policy doesn't include Microsoft Entra ID or Microsoft Graph.

Note

Exchange Online tenants created before 2017 have modern authentication disabled by default. In order to avoid the possibility of a login loop while authenticating through these tenants, you must [enable modern authentication](/en-us/exchange/clients-and-mobile-in-exchange-online/enable-or-disable-modern-authentication-in-exchange-online).

Note

The Microsoft Entra Connect / Microsoft Entra Cloud Sync synchronization accounts (or any security principal assigned to the "Directory Synchronization Accounts" role) are excluded from security defaults and aren't prompted to register for or perform multifactor authentication. Organizations shouldn't be using this account for other purposes.

*Also available as a [Microsoft-managed Conditional Access policy](../identity/conditional-access/managed-policies#upgrade-from-security-defaults) if you disable security defaults.*

## Deployment considerations

### Preparing your users

It's critical to inform users about upcoming changes, registration requirements, and any necessary user actions. We provide [communication templates](https://aka.ms/mfatemplates) and [user documentation](https://support.microsoft.com/account-billing/set-up-security-info-from-a-sign-in-page-28180870-c256-4ebf-8bd7-5335571bf9a8) to prepare your users for the new experience and help to ensure a successful rollout. Send users to https://myprofile.microsoft.com to register by selecting the **Security Info** link on that page.

### Authentication methods

Security defaults users are required to register for and use multifactor authentication using the [Microsoft Authenticator app using notifications](../identity/authentication/concept-authentication-authenticator-app). Users might use verification codes from the Microsoft Authenticator app but can only register using the notification option. Users can also use any non-Microsoft application using [OATH TOTP](../identity/authentication/concept-authentication-oath-tokens) to generate codes.

Warning

Don't disable methods for your organization if you're using security defaults. Disabling methods might lead to locking yourself out of your tenant. Leave all **Methods available to users** enabled in the [MFA service settings portal](../identity/authentication/howto-mfa-getstarted#choose-authentication-methods-for-mfa).

### B2B users

Any [B2B guest](../external-id/what-is-b2b) users or [B2B direct connect](../external-id/b2b-direct-connect-overview) users that access your directory are treated the same as your organization's users.

### Disabled MFA status

If your organization is a previous user of per-user based multifactor authentication, don't be alarmed to not see users in an **Enabled** or **Enforced** status if you look at the multifactor authentication status page. **Disabled** is the appropriate status for users who are using security defaults or Conditional Access based multifactor authentication.

## Disabling security defaults

Organizations that choose to implement Conditional Access policies that replace security defaults must disable security defaults.

Disable security defaults in your directory:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Overview** &gt; **Properties**.
3. Select **Manage security defaults**.
4. Set **Security defaults** to **Disabled (not recommended)**.
5. Select **Save**.

### Move from security defaults to Conditional Access

While security defaults are a good baseline to start your security posture from, they don't allow for the customization that many organizations require. Conditional Access policies provide a full range of customization that more complex organizations require.

| - | Security defaults | Conditional Access |
| --- | --- | --- |
| **Required licenses** | None | At least Microsoft Entra ID P1 |
| **Customization** | No customization (on or off) | Fully customizable |
| **Enabled by** | Microsoft or administrator | Microsoft or administrator |
| **Complexity** | Simple to use | Fully customizable based on your requirements |

Organizations who would like to test out the features of Conditional Access can [sign up for a free trial](get-started-premium) to get started.

After administrators disable security defaults, organizations should immediately enable Conditional Access policies to protect their organization. [Microsoft-managed Conditional Access policies](../identity/conditional-access/managed-policies#upgrade-from-security-defaults) are available to maintain the same protections, covering blocking legacy authentication, requiring MFA for Azure management, requiring MFA for admins, and requiring MFA for all users. Organizations should review these policies and consider enabling more policies from the [secure foundations category of Conditional Access templates](../identity/conditional-access/concept-conditional-access-policy-common?tabs=secure-foundation#template-categories). Organizations with Microsoft Entra ID P2 licenses that include Microsoft Entra ID Protection can expand on this list to include [user and sign in risk-based policies](../id-protection/howto-identity-protection-configure-risk-policies) to further strengthen their posture.

Microsoft recommends that organizations have two cloud-only emergency access accounts permanently assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role. These accounts are highly privileged and aren't assigned to specific individuals. The accounts are limited to emergency or "break glass" scenarios where normal accounts can't be used or all other administrators are accidentally locked out. These accounts should be created following the [emergency access account recommendations](/en-us/entra/identity/role-based-access-control/security-emergency-access).