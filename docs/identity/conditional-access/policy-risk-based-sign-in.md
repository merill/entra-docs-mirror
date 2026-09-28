---
layout: Conceptual
title: Sign-in risk-based multifactor authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-risk-based-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Protect your organization by implementing Conditional Access policies that address sign-in risks using Microsoft Entra ID Protection.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth, cokoopma
locale: en-us
document_id: 199e51c2-d6f6-ed8f-39a2-4f395155cb50
document_version_independent_id: 66ae328e-38b8-fe84-5ee9-976adbb99135
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-risk-based-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-risk-based-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-risk-based-sign-in.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
platformId: 282ba9d7-8662-1be6-15da-b15cc87a31e3
---

# Sign-in risk-based multifactor authentication - Microsoft Entra ID | Microsoft Learn

## Overview

Most users have normal behavior that can be tracked. When their behavior falls outside this norm, it might be risky to let them sign in. You might want to block the user or ask them to complete multifactor authentication to confirm their identity.

Sign-in risk represents the likelihood that an authentication request isn't from the identity owner. Organizations with Microsoft Entra ID P2 licenses can create Conditional Access policies incorporating [Microsoft Entra ID Protection sign-in risk detections](../../id-protection/concept-identity-protection-risks).

The sign-in risk-based policy prevents users from registering MFA during risky sessions. If users aren't registered for MFA, their risky sign-ins are blocked, and they receive an AADSTS53004 error.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Template deployment

Organizations can deploy this policy by following the steps outlined below or by using the [Conditional Access templates](concept-conditional-access-policy-common).

## Enable with Conditional Access policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **New policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
    3. Select **Done**.
6. Under **Cloud apps or actions** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Conditions** &gt; **Sign-in risk**, set **Configure** to **Yes**.
    1. Under **Select the sign-in risk level this policy will apply to**, select **High** and **Medium**. [This guidance is based on Microsoft recommendations and might be different for each organization](../../id-protection/howto-identity-protection-configure-risk-policies#choosing-acceptable-risk-levels)
    2. Select **Done**.
8. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require authentication strength**, then select the built-in **Multifactor authentication** authentication strength from the list.
    2. Select **Select**.
9. Under **Session**.
    1. Select **Sign-in frequency**.
    2. Ensure **Every time** is selected.
    3. Select **Select**.
10. Confirm your settings and set **Enable policy** to **Report-only**.
11. Select **Create** to create to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

### Passwordless scenarios

For organizations that adopt [passwordless authentication methods](/en-us/entra/identity/authentication/howto-authentication-passwordless-deployment) make the following changes:

#### Update your passwordless sign-in risk policy

1. Under **Users**:
    1. **Include**, select **Users and groups** and target your passwordless users.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
    3. Select **Done**.
2. Under **Cloud apps or actions** &gt; **Include**, select **All resources** (formerly 'All cloud apps').
3. Under **Conditions** &gt; **Sign-in risk**, set **Configure** to **Yes**.
    1. Under **Select the sign-in risk level this policy will apply to**, select **High** and **Medium**. For more information on risk levels, see [Choosing acceptable risk levels](../../id-protection/howto-identity-protection-configure-risk-policies#choosing-acceptable-risk-levels).
    2. Select **Done**.
4. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require authentication strength**, then select the built-in **Passwordless MFA** or **Phishing-resistant MFA** based on which method the targeted users have.
    2. Select **Select**.
5. Under **Session**:
    1. Select **Sign-in frequency**.
    2. Ensure **Every time** is selected.
    3. Select **Select**.