---
layout: Conceptual
title: Deployment considerations for Microsoft Entra multifactor authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-mfa-getstarted
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about deployment considerations and strategy for successful implementation of Microsoft Entra multifactor authentication
ms.custom: no-azure-ad-ps-ref
ms.topic: how-to
ms.date: 2025-11-02T00:00:00.0000000Z
ms.reviewer: jpettere
locale: en-us
document_id: 329ec11e-2b1a-c837-14fa-ce37843cc0af
document_version_independent_id: f3502c0a-f6fe-b004-39fe-c82c5a85f3b3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-mfa-getstarted.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-mfa-getstarted
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-mfa-getstarted.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
2PlusCloud:
- Azure
- M365
- Power
__autotagging_hash:
- 0C87747657918E322CC7C54D1064F65E658A9A4647BF45025E2B7D4F85EAB0CE
platformId: 6491a4e7-9bd6-8d4e-f0d4-e32a6346f665
---

# Deployment considerations for Microsoft Entra multifactor authentication - Microsoft Entra ID | Microsoft Learn

Microsoft Entra multifactor authentication helps safeguard access to data and applications, providing another layer of security by using a second form of authentication. Organizations can enable multifactor authentication with [Conditional Access](../conditional-access/overview) to make the solution fit their specific needs.

This deployment guide shows you how to plan and implement a [Microsoft Entra multifactor authentication](concept-mfa-howitworks) roll-out.

## Prerequisites for deploying Microsoft Entra multifactor authentication

Before you begin your deployment, ensure you meet the following prerequisites for your relevant scenarios.

| Scenario | Prerequisite |
| --- | --- |
| **Cloud-only** identity environment with modern authentication | **No prerequisite tasks** |
| **Hybrid identity** scenarios | Deploy [Microsoft Entra Connect](../hybrid/whatis-hybrid-identity) and synchronize user identities between the on-premises Active Directory Domain Services (AD DS) and Microsoft Entra ID. |
| **On-premises legacy applications** published for cloud access | Deploy [Microsoft Entra application proxy](../app-proxy/conceptual-deployment-plan) |

## Choose authentication methods for MFA

There are many methods that can be used for a second-factor authentication. You can choose from the list of available authentication methods, evaluating each in terms of security, usability, and availability.

Important

Enable more than one MFA method so that users have a backup method available in case their primary method is unavailable. Methods include:

- [Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/hello-overview)
- [Microsoft Authenticator app](concept-authentication-authenticator-app)
- [FIDO2 security key](concept-authentication-passkeys-fido2)
- [Microsoft Authenticator passkey](concept-authentication-authenticator-app)
- Synced passkey (preview)
- [Hardware OATH tokens (preview)](concept-authentication-oath-tokens#hardware-oath-tokens-preview)
- [Software OATH tokens](concept-authentication-oath-tokens#software-oath-tokens)
- [SMS verification](concept-authentication-phone-options#mobile-phone-verification)
- [Voice call verification](concept-authentication-phone-options)

To learn more about the strength and security of these methods and how they work, see the following resources:

- [What authentication and verification methods are available in Microsoft Entra ID?](overview-authentication)
- [Video: Choose the right authentication methods to keep your organization safe](https://youtu.be/LB2yj4HSptc)

For the best flexibility and usability, use the Microsoft Authenticator app. This authentication method provides the best user experience and multiple modes, such as passwordless, MFA push notifications, and OATH codes. The Microsoft Authenticator app also meets the National Institute of Standards and Technology (NIST) [Authenticator Assurance Level 2 requirements](../../standards/nist-authenticator-assurance-level-2).

You can control the authentication methods available in your tenant. For example, you may want to block some of the least secure methods, such as SMS.

| Authentication method | Manage from | Scoping |
| --- | --- | --- |
| Microsoft Authenticator (Push notification and passwordless phone sign-in) | MFA settings or Authentication methods policy | Authenticator passwordless phone sign-in can be scoped to users and groups |
| FIDO2 security key | Authentication methods policy | Can be scoped to users and groups |
| Software or Hardware OATH tokens | MFA settings |  |
| SMS verification | MFA settings Manage SMS sign-in for primary authentication in authentication policy | SMS sign-in can be scoped to users and groups. |
| Voice calls | Authentication methods policy |  |

## Plan Conditional Access policies

Microsoft Entra multifactor authentication is enforced with Conditional Access policies. These policies allow you to prompt users for MFA when needed for security and stay out of users' way when not needed.

![Conceptual Conditional Access process flow](media/howto-mfa-getstarted/conditional-access-overview-how-it-works.png)

In the Microsoft Entra admin center, you configure Conditional Access policies under **Entra ID** &gt; **Conditional Access**.

To learn more about creating Conditional Access policies, see [Conditional Access policy to prompt for Microsoft Entra multifactor authentication when a user signs in](tutorial-enable-azure-mfa). This helps you to:

- Become familiar with the user interface
- Get a first impression of how Conditional Access works

For end-to-end guidance on Microsoft Entra Conditional Access deployment, see the [Conditional Access deployment plan](../conditional-access/plan-conditional-access).

### Common policies for Microsoft Entra multifactor authentication

Common use cases to require Microsoft Entra multifactor authentication include:

- For [administrators](../conditional-access/policy-old-require-mfa-admin)
- To [specific applications](tutorial-enable-azure-mfa)
- For [all users](../conditional-access/policy-all-users-mfa-strength)
- For [Azure management](../conditional-access/policy-old-require-mfa-azure-mgmt)
- From [network locations you don't trust](../conditional-access/policy-all-users-mfa-strength)

### Named locations

To manage your Conditional Access policies, the location condition of a Conditional Access policy enables you to tie access controls settings to the network locations of your users. We recommend using [Named Locations](../conditional-access/concept-assignment-network) so that you can create logical groupings of IP address ranges or countries and regions. This creates a policy for all apps that blocks sign-in from that named location. Be sure to exempt your administrators from this policy.

### Risk-based policies

If your organization uses [Microsoft Entra ID Protection](../../id-protection/overview-identity-protection) to detect risk signals, consider using [risk-based policies](../../id-protection/howto-identity-protection-configure-risk-policies) instead of named locations. Policies can be created to force password changes when there's a threat of compromised identity or require MFA when a sign-in is deemed [at risk](../../id-protection/howto-identity-protection-configure-risk-policies) such as leaked credentials, sign-ins from anonymous IP addresses, and more.

Risk policies include:

- [Require all users to register for Microsoft Entra multifactor authentication](../../id-protection/howto-identity-protection-configure-mfa-policy)
- [Require a password change for users that are high-risk](../../id-protection/howto-identity-protection-configure-risk-policies#user-risk-policy-in-conditional-access)
- [Require MFA for users with medium or high sign in risk](../../id-protection/howto-identity-protection-configure-risk-policies#sign-in-risk-policy-in-conditional-access)

### Convert users from per-user MFA to Conditional Access based MFA

If your users were enabled using per-user MFA enabled and enforced Microsoft Entra multifactor authentication, we recommend that you enable Conditional Access for all users and then manually disable per-user multifactor authentication. For more information, see [Create a Conditional Access policy](../conditional-access/policy-all-users-mfa-strength#create-a-conditional-access-policy).

## Plan user session lifetime

When planning your multifactor authentication deployment, it's important to think about how frequently you would like to prompt your users. Asking users for credentials often seems like a sensible thing to do, but it can backfire. If users are trained to enter their credentials without thinking, they can unintentionally supply them to a malicious credential prompt. Microsoft Entra ID has multiple settings that determine how often you need to reauthenticate. Understand the needs of your business and users and configure settings that provide the best balance for your environment.

We recommend using devices with Primary Refresh Tokens (PRT) for improved end user experience and reduce the session lifetime with sign-in frequency policy only on specific business use cases.

For more information, see [Optimize reauthentication prompts and understand session lifetime for Microsoft Entra multifactor authentication](concepts-azure-multi-factor-authentication-prompts-session-lifetime).

## Plan user registration

A major step in every multifactor authentication deployment is getting users registered to use Microsoft Entra multifactor authentication. Authentication methods such as Voice and SMS allow preregistration, while others like the Authenticator App require user interaction. Administrators must determine how users will register their methods.

### Combined registration for SSPR and Microsoft Entra multifactor authentication

[The combined registration experience for Microsoft Entra multifactor authentication and self-service password reset (SSPR)](howto-registration-mfa-sspr-combined) enables users to register for both MFA and SSPR in a unified experience. SSPR allows users to reset their password in a secure way using the same methods they use for Microsoft Entra multifactor authentication. To make sure you understand the functionality and end-user experience, see the [Combined security information registration concepts](concept-registration-mfa-sspr-combined).

It's critical to inform users about upcoming changes, registration requirements, and any necessary user actions. We provide [communication templates](https://aka.ms/mfatemplates) and [user documentation](https://support.microsoft.com/account-billing/set-up-security-info-from-a-sign-in-page-28180870-c256-4ebf-8bd7-5335571bf9a8) to prepare your users for the new experience and help to ensure a successful rollout. Send users to https://myprofile.microsoft.com to register by selecting the **Security Info** link on that page.

### Registration with Microsoft Entra ID Protection

Microsoft Entra ID Protection contributes both a registration policy for and automated risk detection and remediation policies to the Microsoft Entra multifactor authentication story. Policies can be created to force password changes when there's a threat of compromised identity or require MFA when a sign-in is deemed risky. If you use Microsoft Entra ID Protection, [configure the Microsoft Entra multifactor authentication registration policy](../../id-protection/howto-identity-protection-configure-mfa-policy) to prompt your users to register the next time they sign in interactively.

### Registration without Microsoft Entra ID Protection

If you don't have licenses that enable Microsoft Entra ID Protection, users are prompted to register the next time that MFA is required at sign-in. To require users to use MFA, you can use Conditional Access policies and target frequently used applications like HR systems. If a user's password is compromised, it could be used to register for MFA, taking control of their account. We therefore recommend [securing the security registration process with Conditional Access policies](../conditional-access/policy-all-users-security-info-registration) requiring trusted devices and locations. You can further secure the process by also requiring a [Temporary Access Pass](howto-authentication-temporary-access-pass). A time-limited passcode issued by an admin that satisfies strong authentication requirements and can be used to onboard other authentication methods, including Passwordless ones.

### Increase the security of registered users

If you have users registered for MFA using SMS or voice calls, you may want to move them to more secure methods such as the Microsoft Authenticator app. Microsoft now offers a public preview of functionality that allows you to prompt users to set up the Microsoft Authenticator app during sign-in. You can set these prompts by group, controlling who is prompted, enabling targeted campaigns to move users to the more secure method.

### Plan recovery scenarios

As mentioned before, ensure users are registered for more than one MFA method, so that if one is unavailable, they have a backup. If the user doesn't have a backup method available, you can:

- Provide them with a Temporary Access Pass so that they can manage their own authentication methods. You can also provide a Temporary Access Pass to enable temporary access to resources.
- Update their methods as an administrator. To do so, select the user in the Microsoft Entra admin center, then select **Entra ID** &gt; **Authentication methods** and update their methods.

## Plan integration with on-premises systems

Applications that authenticate directly with Microsoft Entra ID and have modern authentication (WS-Fed, SAML, OAuth, OpenID Connect) can make use of Conditional Access policies. Some legacy and on-premises applications don't authenticate directly against Microsoft Entra ID and require additional steps to use Microsoft Entra multifactor authentication. You can integrate them by using Microsoft Entra application proxy or [Network policy services](/en-us/windows-server/networking/core-network-guide/core-network-guide#BKMK_optionalfeatures).

### Integrate with AD FS resources

We recommend migrating applications secured with Active Directory Federation Services (AD FS) to Microsoft Entra ID. However, if you aren't ready to migrate these to Microsoft Entra ID, you can use the Azure multifactor authentication adapter with AD FS 2016 or newer.

If your organization is federated with Microsoft Entra ID, you can [configure Microsoft Entra multifactor authentication as an authentication provider with AD FS resources](/en-us/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa) both on-premises and in the cloud.

### RADIUS clients and Microsoft Entra multifactor authentication

For applications that are using RADIUS authentication, we recommend moving client applications to modern protocols such as SAML, OpenID Connect, or OAuth on Microsoft Entra ID. If the application can't be updated, then you can deploy [Network Policy Server (NPS) extension](howto-mfa-nps-extension). The network policy server (NPS) extension acts as an adapter between RADIUS-based applications and Microsoft Entra multifactor authentication to provide a second factor of authentication.

#### Common integrations

Many vendors now support SAML authentication for their applications. When possible, we recommend federating these applications with Microsoft Entra ID and enforcing MFA through Conditional Access. If your vendor doesn't support modern authentication – you can use the NPS extension. Common RADIUS client integrations include applications such as [Remote Desktop Gateways](howto-mfa-nps-extension-rdg) and [VPN servers](howto-mfa-nps-extension-vpn).

Others might include:

- Citrix Gateway

    [Citrix Gateway](https://docs.citrix.com/en-us/advanced-concepts/implementation-guides/citrix-gateway-microsoft-azure.html#microsoft-azure-mfa-deployment-methods) supports both RADIUS and NPS extension integration, and a SAML integration.
- Cisco VPN

    - The Cisco VPN supports both RADIUS and [SAML authentication for SSO](../saas-apps/cisco-secure-firewall-secure-client).
    - By moving from RADIUS authentication to SAML, you can integrate the Cisco VPN without deploying the NPS extension.
- All VPNs

## Deploy Microsoft Entra multifactor authentication

Your Microsoft Entra multifactor authentication rollout plan should include a pilot deployment followed by deployment waves that are within your support capacity. Begin your rollout by applying your Conditional Access policies to a small group of pilot users. After evaluating the effect on the pilot users, process used, and registration behaviors, you can either add more groups to the policy or add more users to the existing groups.

Follow these steps:

1. Meet the necessary prerequisites
2. Configure chosen authentication methods
3. Configure your Conditional Access policies
4. Configure session lifetime settings
5. Configure Microsoft Entra multifactor authentication registration policies

## Manage Microsoft Entra multifactor authentication

This section provides reporting and troubleshooting information for Microsoft Entra multifactor authentication.

### Reporting and Monitoring

Microsoft Entra ID has reports that provide technical and business insights, follow the progress of your deployment and check if your users are successful at sign-in with MFA. Have your business and technical application owners assume ownership of and consume these reports based on your organization's requirements.

You can monitor authentication method registration and usage across your organization using the [Authentication Methods Activity dashboard](howto-authentication-methods-activity). This helps you understand what methods are being registered and how they're being used.

#### Use sign-in logs to review MFA events

The Microsoft Entra sign-in logs include authentication details for events when a user is prompted for MFA, and if any Conditional Access policies were in use.

NPS extension and AD FS logs for cloud MFA activity are now included in the [sign-in logs](../monitoring-health/concept-sign-ins), and no longer published to the **Activity report**.

For more information, and additional Microsoft Entra multifactor authentication reports, see [Review Microsoft Entra multifactor authentication events](howto-mfa-reporting#view-the-azure-ad-sign-ins-report).

### Troubleshoot Microsoft Entra multifactor authentication

See [Troubleshooting Microsoft Entra multifactor authentication](https://support.microsoft.com/help/2937344/troubleshooting-azure-multi-factor-authentication-issues) for common issues.

## Guided walkthrough

For a guided walkthrough of many of the recommendations in this article, see the [Microsoft 365 Configure multifactor authentication guided walkthrough](https://go.microsoft.com/fwlink/?linkid=2221401).