---
layout: FAQ
title: FAQ for Microsoft-provided SMS and voice retirement - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-sms-voice-retirement-faq
summary: >
  <p>This article answers frequently asked questions about the retirement of Microsoft-provided SMS and voice authentication in Microsoft Entra ID. For the full timeline and migration guidance, see <a href="concept-sms-voice-retirement">Passkeys by default and retirement of Microsoft-provided SMS and voice authentication</a>.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: marinasanchezz1
ms.author: marisanchez
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Frequently asked questions about the retirement of Microsoft-provided SMS and voice authentication in Microsoft Entra ID and the move to passkeys.
ms.topic: faq
ms.date: 2026-09-23T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 7d241049-d1d4-6991-e114-d191c7e423a7
document_version_independent_id: 7d241049-d1d4-6991-e114-d191c7e423a7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-sms-voice-retirement-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-sms-voice-retirement-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-sms-voice-retirement-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 26fcaa0c-2ce8-767b-3f99-979393978ab7
---

# FAQ for Microsoft-provided SMS and voice retirement - Microsoft Entra ID | Microsoft Learn

This article answers frequently asked questions about the retirement of Microsoft-provided SMS and voice authentication in Microsoft Entra ID. For the full timeline and migration guidance, see [Passkeys by default and retirement of Microsoft-provided SMS and voice authentication](concept-sms-voice-retirement).

## Why is Microsoft provided telecom delivery for SMS and Voice ending?

The primary driver is security. As the industry moves toward phishing-resistant authentication, Microsoft Entra ID is making passkeys the default authentication experience. SMS and voice are among the most vulnerable authentication methods available today and provide significantly weaker protection against phishing and account compromise than passkeys.

Organizations that still require SMS or voice will continue to have that option through telephony providers when there is a legitimate business, regulatory, or technical need. This change is intended to modernize authentication while preserving flexibility for those scenarios.

Beginning September 1, 2026, passkeys will be automatically enabled for users currently enabled for SMS or voice. Beginning February 1, 2027, the retirement applies to all users except Global Administrators and external users. If you haven't configured a telephony provider through Microsoft Security Store, users in scope of the February 1 retirement can no longer use SMS or voice for MFA. Users in scope of that retirement whose only MFA method is SMS or voice will be required to register a passkey during sign-in before they can continue accessing their account. Global Administrators and external users follow a later retirement date of July 1, 2027. Internal guest users aren't included in that July 1 group and still follow the February 1, 2027 retirement date. Tenants that have configured a telephony provider can continue using SMS or voice according to their organization's policies.

## Do Global Administrators and external users have a different retirement date?

Yes. Microsoft-provided SMS and voice authentication will be retired on July 1, 2027 for Global Administrators and external users.

Internal guest users aren't included in that July 1 group and still follow the February 1, 2027 retirement date.

## Will there be costs associated with using a telephony provider through Microsoft Security Store?

Yes. Pricing varies by telephony provider and region. Costs depend on your usage, geographic distribution, selected provider, and offer. Review the Soprano and Telesign offers in the [telephony provider FAQ](phone-providers-faq#costs-and-billing) for specific pricing and commercial details.

However, migrating Microsoft provided SMS and voice users to Passkeys incur no additional cost.

## Will my users be auto-migrated, or do I have to do it?

On September 1, 2026, users enabled for SMS or Voice in the Entra Authentication Methods Policy (AMP) will be auto-enabled for passkeys in AMP. Your Registration Campaign settings will also be updated to Microsoft managed state, and will automatically bring these users into scope.

When these users next sign-in and complete MFA, the registration campaign will nudge them to register a passkey. By default, users will have unlimited snoozes of the nudge prompt. If you do not want this to occur, move users out of SMS or Voice AMP before September 1st.

## What about SSPR (self-service password reset)?

The retirement of native SMS and voice applies across Microsoft Entra, including SSPR. However, users can still use SMS and voice through a telephony provider available in Microsoft Security Store.

Microsoft is also planning to introduce support to change password for users who authenticate with passwordless sign in. More details to come.

## What's Microsoft Security Store?

Instead of Microsoft-provided SMS or voice, you can contract directly with a supported telephony provider through Microsoft Security Store. You get regional control and can select a provider that meets your local security and compliance requirements. This option is for customers who have a regulated or operational requirement for a telephony channel.

Soprano and Telesign are the initial telephony providers available during the private preview. More providers will become available by general availability. The configuration experience becomes available beginning October 30, 2026. For provider and offer information, see [Choose a telephony provider for SMS and voice authentication](concept-phone-providers).

## Where can I see if my tenant is in scope?

To find users still using SMS or Voice, run the [PowerShell script](https://github.com/microsoft/entra-sms-voice-usage-analyzer) described in the main retirement article. Any non-zero result means you're in scope.

## Which cloud environments are included in this timeline?

This timeline applies to public cloud environments only. Other cloud environments will follow on a later schedule, and we will provide advance communications to help customers prepare for the transition.

## Will Azure AD B2C or Microsoft Entra External ID tenants be impacted by this announcement?

Azure AD B2C is out of scope and isn't affected. For Microsoft Entra External ID, this change comes next year, and a separate announcement will follow. So there's no change for either Azure AD B2C or Microsoft Entra External ID tenants with this announcement.

## When will passkey support be available for B2B users?

Passkey support for B2B users and internal guest users is planned to be available by the end of calendar year 2026. These users are included in the scope of the retirement of Microsoft-provided SMS and voice authentication.

External users follow the July 1, 2027 retirement date. Internal guest users still follow the February 1, 2027 retirement date.

## Are external MFA methods impacted by SMS and voice retirement?

No, only SMS and voice authentication method policies and legacy MFA policies are retired.

On September 1, 2026, users that are enabled for SMS or voice in the authentication method policies or legacy MFA policies are auto-enabled for passkeys and nudged to register. External MFA users aren't in scope unless they're also enabled for SMS or voice.

## What if I have different plans for my tenant than enabling passkeys for SMS/voice users, such as configuring a telephony provider or migrating users to another authentication method?

A temporary opt-out will be available for the September 1, 2026 through February 1, 2027 changes. This allows you to delay passkey and Registration Campaign enablement while you complete transition activities, such as configuring a telephony provider or migrating to other authentication methods.

To opt out, update your authentication methods policy using Microsoft Graph and set the `passkeyDynamicMigration` property to `true`.

**Request**

```http
PATCH https://graph.microsoft.com/beta/policies/authenticationmethodspolicy
Content-Type: application/json

{
   "optOutSettings": {
     "passkeyDynamicMigration": true
   }
}
```

After this setting is applied, your tenant will be excluded from the automatic passkey enablement and Registration Campaign rollout during the opt-out period. Beginning February 1, 2027, standard passkey migration and enforcement timelines will apply regardless of this setting for users in scope of the February 1 retirement. Global Administrators and external users instead follow the July 1, 2027 retirement date. Internal guest users remain on the February 1, 2027 retirement date.

However, if your tenant still has users enabled for Microsoft-managed SMS or voice on their applicable retirement date, and you haven't configured a telephony provider through Microsoft Security Store, those users will no longer be able to use SMS or voice to satisfy MFA requirements and continue signing in.

After the applicable retirement date, users whose only available MFA method is SMS or voice will be required to register a passkey during sign-in to continue accessing their account.

There is no opt out for enforcement. This requirement applies to all tenants on the applicable retirement date for each user population.

## Will users receive a blocking passkey registration prompt if we configure a telephony provider?

No. If you configure a telephony provider through Microsoft Security Store and migrate all users who need SMS or voice before their applicable retirement date, those users won't receive the blocking passkey registration prompt as part of the SMS and voice retirement enforcement.

Telephony providers are intended for organizations that have a business, regulatory, or technical need to continue using SMS or voice. Make sure that the provider is configured and that all affected users are migrated before their applicable retirement date. Global Administrators and external users follow the July 1, 2027 retirement date. Internal guest users aren't included in that July 1 group and still follow the February 1, 2027 retirement date. Users who remain enabled for Microsoft-provided SMS or voice are still subject to the passkey registration requirement.

## Are customers going to get locked out of their accounts on the retirement date?

No. If customers do not configure a telephony provider by the applicable retirement date, users who still use SMS and voice will receive a blocking registration prompt to register a passkey. They will no longer be able to skip this prompt and will need to complete passkey registration before they can continue to sign in. Global Administrators and external users follow the July 1, 2027 retirement date. Internal guest users aren't included in that July 1 group and still follow the February 1, 2027 retirement date. Organizations that need SMS or voice after retirement can choose a telephony provider through Microsoft Security Store.