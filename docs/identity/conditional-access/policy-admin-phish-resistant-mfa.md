---
layout: Conceptual
title: Require phishing-resistant multifactor authentication for Microsoft Entra administrator roles - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-admin-phish-resistant-mfa
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a Conditional Access policy requiring stronger authentication methods for highly privileged roles in your organization.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth
locale: en-us
document_id: c548806f-fcaf-bded-3c16-18e4b9b0024d
document_version_independent_id: d9ea3205-5261-f83d-1f14-67fb1ea661ec
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-admin-phish-resistant-mfa.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-admin-phish-resistant-mfa
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-admin-phish-resistant-mfa.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a4ba6069-d5a4-ab15-f36b-9ae3c96b3fb6
---

# Require phishing-resistant multifactor authentication for Microsoft Entra administrator roles - Microsoft Entra ID | Microsoft Learn

## Overview

Accounts with privileged administrative roles are frequent targets of attackers. Requiring phishing-resistant multifactor authentication (MFA) for these accounts reduces the risk of compromise.

Caution

Before creating a policy requiring phishing-resistant multifactor authentication, make sure your administrators register the appropriate methods. Enabling this policy without completing this step risks locking you out of your tenant. Administrators can [configure Temporary Access Pass to register passwordless authentication methods](../authentication/howto-authentication-temporary-access-pass) or follow the steps in [register a passkey (FIDO2)](../authentication/how-to-register-passkey-with-security-key).

Microsoft recommends requiring phishing-resistant multifactor authentication for at least the following roles:

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

Organizations can include or exclude roles based on their requirements.

Organizations can use this policy with features like Privileged Identity Management (PIM), which lets you [require MFA for role activation](/en-us/entra/id-governance/privileged-identity-management/pim-how-to-change-default-settings#on-activation-require-multifactor-authentication).

## Authentication strength

This article helps your organization create an MFA policy for your environment using authentication strengths. Microsoft Entra ID offers three [built-in authentication strengths](/en-us/entra/identity/authentication/concept-authentication-strengths):

- Multifactor authentication strength (less restrictive)
- Passwordless MFA strength
- **Phishing-resistant MFA strength** (most restrictive), recommended in this article

Use one of the built-in strengths or create a [custom authentication strength](/en-us/entra/identity/authentication/concept-authentication-strength-advanced-options) based on the authentication methods you want to require.

For external user scenarios, the MFA authentication methods that a resource tenant accepts vary depending on whether the user completes MFA in their home tenant or in the resource tenant. For more information, see [Authentication strength for external users](/en-us/entra/identity/authentication/concept-authentication-strength-external-users).

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Template deployment

Organizations can deploy this policy by following the steps outlined below or by using the [Conditional Access templates](concept-conditional-access-policy-common).

## Create a Conditional Access policy

Warning

If you use [external authentication methods](/en-us/entra/identity/authentication/how-to-authentication-external-method-manage), these methods are currently incompatible with authentication strengths. Use the **[Require multifactor authentication](concept-conditional-access-grant#require-multifactor-authentication)** grant control instead.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Name your policy. Create a meaningful naming standard for your organization's policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **Directory roles** and choose at least the previously listed roles.

        Warning

        Conditional Access policies support built-in roles. Conditional Access policies aren't enforced for other role types including [administrative unit-scoped](../role-based-access-control/manage-roles-portal) or [custom roles](../role-based-access-control/custom-create).
    2. Under **Exclude**, select **Users and groups**, and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require authentication strength**, then select **Phishing-resistant MFA strength** from the list.
    2. Select **Select**.
8. Confirm your settings, and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.