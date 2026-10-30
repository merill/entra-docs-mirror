---
layout: Conceptual
title: Require MFA for all users with Conditional Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-all-users-mfa-strength
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a custom Conditional Access policy to require all users do multifactor authentication.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth
locale: en-us
document_id: d2195c05-13ee-5f82-d5dd-93a36ce0191d
document_version_independent_id: 300ffcd7-1ec7-d610-bf4b-49ea4cd0f1b7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-all-users-mfa-strength.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-all-users-mfa-strength
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-all-users-mfa-strength.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e4c80db0-6186-2e35-1ec3-8eca4e778e7b
---

# Require MFA for all users with Conditional Access - Microsoft Entra ID | Microsoft Learn

## Overview

As Alex Weinert, the Director of Identity Security at Microsoft, mentions in his blog post [Your Pa$$word doesn't matter](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Your-Pa-word-doesn-t-matter/ba-p/731984):

> 
> Your password doesn't matter, but MFA does! Based on our studies, your account is more than 99.9% less likely to be compromised if you use MFA.

## Authentication strength

The guidance in this article helps your organization create an MFA policy for your environment using authentication strengths. Microsoft Entra ID provides three [built-in authentication strengths](/en-us/entra/identity/authentication/concept-authentication-strengths):

- **Multifactor authentication strength** (less restrictive) recommended in this article
- Passwordless MFA strength
- Phishing-resistant MFA strength (most restrictive)

You can use one of the built-in strengths or create a [custom authentication strength](/en-us/entra/identity/authentication/concept-authentication-strength-advanced-options) based on the authentication methods you want to require.

For external user scenarios, the MFA authentication methods that a resource tenant can accept vary depending on whether the user is completing MFA in their home tenant or in the resource tenant. For more information, see [Authentication strength for external users](/en-us/entra/identity/authentication/concept-authentication-strength-external-users).

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Template deployment

Organizations can deploy this policy by following the steps outlined below or by using the [Conditional Access templates](concept-conditional-access-policy-common).

## Create a Conditional Access policy

The following steps help create a Conditional Access policy to require all users do multifactor authentication, using the authentication strength policy, [without any app exclusions](concept-conditional-access-cloud-apps#conditional-access-for-all-resources).

Warning

[External authentication methods](/en-us/entra/identity/authentication/how-to-authentication-external-method-manage) are currently incompatible with authentication strength. You should use the **[Require multifactor authentication](concept-conditional-access-grant#require-multifactor-authentication)** grant control.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.

    1. Under **Include**, select **All users**
    2. Under **Exclude**:
        1. Select **Users and groups**
            1. Choose your organization's emergency access or break-glass accounts.
            2. If you use hybrid identity solutions like Microsoft Entra Connect or Microsoft Entra Connect Cloud Sync, select **Directory roles**, then select **Directory Synchronization Accounts**
        2. You might choose to exclude your guest users if you're targeting them with a [guest user specific policy](policy-guests-mfa-strength).
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.

    Tip

    Microsoft recommends all organizations create a baseline Conditional Access policy that targets: All users, all resources without any app exclusions, and requires multifactor authentication.
7. Under **Access controls** &gt; **Grant**, select **Grant access**.

    1. Select **Require authentication strength**, then select the built-in **Multifactor authentication strength** from the list.
    2. Select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

### Named locations

Organizations might choose to incorporate known network locations known as **Named locations** in their Conditional Access policies. These named locations might include trusted IP networks like those for a main office location. For more information about configuring named locations, see the article [What is the location condition in Microsoft Entra Conditional Access?](concept-assignment-network#ipv4-and-ipv6-address-ranges)

In the previous example policy, an organization might choose to not require multifactor authentication if accessing a cloud app from their corporate network. In this case they could add the following configuration to the policy:

1. Under **Assignments**, select **Network**.
    1. Configure **Yes**.
    2. Include **Any network or location**.
    3. Exclude **All trusted networks and locations**.
2. **Save** your policy changes.