---
layout: Conceptual
title: Prevent Attacks Using Smart Lockout - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-password-smart-lockout
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how Microsoft Entra smart lockout helps protect your organization from brute-force attacks that try to guess user passwords.
ms.topic: how-to
ms.date: 2026-06-03T00:00:00.0000000Z
ms.reviewer: rogoya
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 9c7b90ca-a2b1-9cd8-9769-cd48c27f10ea
document_version_independent_id: b8c29389-c435-b2f0-4186-1e9c47ab4f3e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-password-smart-lockout.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-password-smart-lockout
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-password-smart-lockout.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 6a1756b0-479d-1347-fa78-0d0a5e394eb5
---

# Prevent Attacks Using Smart Lockout - Microsoft Entra ID | Microsoft Learn

Smart lockout helps lock out bad actors that try to guess your users' passwords or use brute-force methods to get in. Smart lockout can recognize sign-ins that come from valid users and treat them differently than sign-ins from attackers and other unknown sources. Attackers get locked out while your users continue to access their accounts and be productive.

## How smart lockout works

By default, smart lockout locks an account from sign-in after:

- 10 failed attempts in Azure Public and Microsoft Azure operated by 21Vianet tenants
- Three failed attempts for Azure US Government tenants

The account locks again after each subsequent failed sign-in attempt. The lockout period is one minute at first, and longer in subsequent attempts. To minimize the ways an attacker could work around this behavior, we don't disclose the rate at which the lockout period increases after unsuccessful sign-in attempts.

Smart lockout tracks the last three bad password hashes to avoid incrementing the lockout counter for the same password. If someone enters the same bad password multiple times, this behavior doesn't cause the account to lock out.

Note

Hash tracking functionality isn't available for customers with pass-through authentication enabled because authentication happens on-premises and not in the cloud.

Federated deployments that use Active Directory Federation Services (AD FS) 2016 and AD FS 2019 can enable similar benefits by using [AD FS Extranet Lockout and Extranet Smart Lockout](/en-us/windows-server/identity/ad-fs/operations/configure-ad-fs-extranet-smart-lockout-protection). It's recommended to move to [managed authentication](https://www.microsoft.com/security/business/identity-access/upgrade-adfs).

Smart lockout is always on for all Microsoft Entra customers, with these default settings that offer the right mix of security and usability. Customizing the smart lockout settings with values specific to your organization requires Microsoft Entra ID P1 or higher licenses for your users.

Using smart lockout doesn't guarantee that a genuine user is never locked out. When smart lockout locks a user account, we try our best to not lock out the genuine user. The lockout service attempts to ensure that bad actors can't gain access to a genuine user account. The following considerations apply:

- Lockout state across Microsoft Entra data centers is synchronized. However, the total number of failed sign-in attempts allowed before an account is locked out will vary slightly from the configured lockout threshold. Once an account is locked out, it's locked out everywhere across all Microsoft Entra data centers.
- Smart Lockout uses familiar location versus unfamiliar location to differentiate between a bad actor and the genuine user. Both unfamiliar and familiar locations have separate lockout counters.

    To prevent the system from locking out a user signing in from an unfamiliar location, they must use the correct password to avoid being locked out and have a low number of previous lockout attempts from unfamiliar locations. If the user is locked out from an unfamiliar location, they should consider SSPR to reset the lockout counter.

- After an account lockout, the user can initiate self-service password reset (SSPR) to sign in again. SSPR lets users reset or change their own passwords without help desk or administrator assistance. If the user chooses **I forgot my password** during SSPR, the duration of the lockout is reset to 0 seconds, so the user doesn't need to wait for the lockout duration to expire. If the user chooses **I know my password** during SSPR, the lockout timer continues and the duration of the lockout isn't reset. In that case, to regain access the user should either change their password or wait until the configured lockout duration expires.

You can integrate smart lockout with hybrid deployments that use password hash sync or pass-through authentication to protect on-premises Active Directory Domain Services (AD DS) accounts from being locked out by attackers. By setting smart lockout policies in Microsoft Entra ID appropriately, you can filter out attacks before they reach on-premises AD DS.

When using [pass-through authentication](../hybrid/connect/how-to-connect-pta), the following considerations apply:

- The Microsoft Entra lockout threshold must be **less** than the AD DS account lockout threshold. Set the values so that the AD DS account lockout threshold is at least two or three times greater than the Microsoft Entra lockout threshold.
- The Microsoft Entra lockout duration must be **longer** than the AD DS account lockout duration. The Microsoft Entra duration is set in seconds, while the AD DS duration is set in minutes. 
    Tip

    This configuration ensures Microsoft Entra smart lockout stops your on-premises AD DS accounts from being locked out by brute force attacks, like [password spray attacks](../../id-protection/concept-identity-protection-risks#password-spray) on your Microsoft Entra accounts.

For example, if you want your Microsoft Entra smart lockout duration to be higher than AD DS, then Microsoft Entra ID would be 120 seconds (2 minutes) while your on-premises AD is set to 1 minute (60 seconds). If you want your Microsoft Entra lockout threshold to be 10, then you want your on-premises AD DS lockout threshold to 20.

Important

An administrator can unlock a user's cloud account if Smart Lockout has locked them out without waiting for the lockout duration to expire. For more information, see [Reset a user's password](../../fundamentals/users-reset-password-azure-portal).

## Verify on-premises account lockout policy

To verify your on-premises AD DS account lockout policy, complete the following steps from a domain-joined system with administrator privileges:

1. Open the Group Policy Management tool.
2. Edit the group policy that includes your organization's account lockout policy, such as, the **Default Domain Policy**.
3. Browse to **Computer Configuration** &gt; **Policies** &gt; **Windows Settings** &gt; **Security Settings** &gt; **Account Policies** &gt; **Account Lockout Policy**.
4. Verify your **Account lockout threshold** and **Reset account lockout counter after** values.

![Modify the on-premises Active Directory account lockout policy](media/howto-password-smart-lockout/entra-on-premises-account-lockout-policy.png)

## Manage Microsoft Entra smart lockout values

Based on your organizational requirements, you can customize the Microsoft Entra smart lockout values. Customizing the smart lockout settings with values specific to your organization requires Microsoft Entra ID P1 or higher licenses for your users. Customizing the smart lockout settings isn't available for Microsoft Azure operated by 21Vianet tenants.

To check or modify the smart lockout values for your organization, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods** &gt; **Password protection**.
3. Set the **Lockout threshold** based on how many failed sign-ins are allowed on an account before its first lockout.

    The default is 10 for Azure Public tenants and three for Azure US Government tenants.
4. Set the **Lockout duration in seconds**, to the length in seconds of each lockout.

    The default is 60 seconds (one minute).

Note

If the first sign-in after a lockout period has expired also fails, the account locks out again. If an account locks repeatedly, the lockout duration increases.

[![Screenshot that shows how to customize the Microsoft Entra smart lockout policy in the Microsoft Entra admin center.](media/howto-password-smart-lockout/custom-smart-lockout-policy.png)](media/howto-password-smart-lockout/custom-smart-lockout-policy.png#lightbox)

## Testing Smart lockout

When the smart lockout threshold is triggered, you'll get the following message while the account is locked:

*Your account is temporarily locked to prevent unauthorized use. Try again later, and if you still have trouble, contact your admin.*

When you test smart lockout, your sign-in requests might be handled by different datacenters due to the geo-distributed and load-balanced nature of the Microsoft Entra authentication service.

Smart lockout tracks the last three bad password hashes to avoid incrementing the lockout counter for the same password. If someone enters the same bad password multiple times, this behavior doesn't cause the account to lock out.

## Default protections

In addition to Smart lockout, Microsoft Entra ID also protects against attacks by analyzing signals including IP traffic and identifying anomalous behavior. Microsoft Entra ID blocks these malicious sign-ins by default and returns [AADSTS50053 - IdsLocked error code](../../identity-platform/reference-error-codes), regardless of the password validity.