---
layout: Conceptual
title: Conditional Access - Authentication strength for external users - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-guests-mfa-strength
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a custom Conditional Access policy with authentication strength to require specific multifactor authentication (MFA) methods for external users.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: inbarc
locale: en-us
document_id: 0ba58bcf-88ef-a65e-7994-09c57594caf6
document_version_independent_id: 9594aa07-f112-f0cd-7bbc-72bfbd115809
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-guests-mfa-strength.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-guests-mfa-strength
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-guests-mfa-strength.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: f1181fcb-b337-628a-5ef0-ab280337dc98
---

# Conditional Access - Authentication strength for external users - Microsoft Entra ID | Microsoft Learn

## Overview

Authentication strength is a Conditional Access control that lets you define a specific combination of multifactor authentication (MFA) methods that an external user must complete to access your resources. This control is especially useful for restricting external access to sensitive apps in your organization. For example, you can create a Conditional Access policy, require a phishing-resistant authentication strength in the policy, and assign it to guests and external users.

Microsoft Entra ID provides three [built-in authentication strengths](/en-us/entra/identity/authentication/concept-authentication-strengths):

- **Multifactor authentication strength** (less restrictive) recommended in this article
- Passwordless MFA strength
- Phishing-resistant MFA strength (most restrictive)

You can use one of the built-in strengths or create a [custom authentication strength](/en-us/entra/identity/authentication/concept-authentication-strength-advanced-options) based on the authentication methods you want to require.

In external user scenarios, the MFA authentication methods that a resource tenant can accept vary depending on whether the user is completing MFA in their home tenant or in the resource tenant. For details, see [Authentication strength for external users](/en-us/entra/identity/authentication/concept-authentication-strength-external-users).

Note

Currently, you can only apply authentication strength policies to external users who authenticate with Microsoft Entra ID. For email one-time passcode, SAML/WS-Fed, Google federation, and Microsoft personal (MSA) users, use the [MFA grant control](concept-conditional-access-grant#require-multifactor-authentication) to require MFA.

## Configure cross-tenant access settings to trust MFA

Authentication strength policies work together with [MFA trust settings](../../external-id/cross-tenant-access-settings-b2b-collaboration#to-change-inbound-trust-settings-for-mfa-and-device-claims) in your cross-tenant access settings to determine where and how the external user must perform MFA. A Microsoft Entra user first authenticates with their own account in their home tenant. Then when this user tries to access your resource, Microsoft Entra ID applies the authentication strength Conditional Access policy and checks to see if you enabled MFA trust.

- **If MFA trust is enabled**, Microsoft Entra ID checks the user's authentication session for a claim indicating that MFA was fulfilled in the user's home tenant.
- **If MFA trust is disabled**, the resource tenant presents the user with a challenge to complete MFA in the resource tenant using an acceptable authentication method.

The authentication methods that external users can use to satisfy MFA requirements are different depending on whether the user is completing MFA in their home tenant or the resource tenant. See the table in [Conditional Access authentication strength](https://aka.ms/b2b-auth-strengths).

Important

Before you create the Conditional Access policy, check your cross-tenant access settings to make sure your inbound MFA trust settings are configured as intended.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Create a Conditional Access policy

Use the following steps to create a Conditional Access policy that applies an authentication strength to external users.

Warning

If you use [external authentication methods](/en-us/entra/identity/authentication/how-to-authentication-external-method-manage), these are currently incompatible with authentication strength and you should use the **[Require multifactor authentication](concept-conditional-access-grant#require-multifactor-authentication)** grant control.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, choose **Select users and groups**, and then select **Guest or external users**.
        1. Select the types of [guest or external users](../../external-id/authentication-conditional-access#assign-conditional-access-policies-to-external-user-types) you want to apply the policy to.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)**, under **Include** or **Exclude**, select any applications you want to include in or exclude from the authentication strength requirements.
7. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require authentication strength**, then select the appropriate built-in or custom authentication strength from the list.
    2. Select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.