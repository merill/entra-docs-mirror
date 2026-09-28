---
layout: Conceptual
title: Require MFA for guest users with Conditional Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-old-require-mfa-guest
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a custom Conditional Access policy requiring guest users perform multifactor authentication.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth
locale: en-us
document_id: 96bc699d-bc1d-519e-61f0-efb4d14f321f
document_version_independent_id: ff3c955a-13f9-eff5-70f8-d562e3d555a7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-old-require-mfa-guest.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-old-require-mfa-guest
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-old-require-mfa-guest.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7cd61db3-938c-6d0f-f122-f0fd1be695ed
---

# Require MFA for guest users with Conditional Access - Microsoft Entra ID | Microsoft Learn

## Overview

Warning

This article describes a Conditional Access policy that uses the **Require multifactor authentication** grant control. For external users who authenticate with Microsoft Entra ID, consider using **authentication strength** policies to specify which MFA methods are accepted. For more information, see [Require multifactor authentication strength for external users](policy-guests-mfa-strength). Authentication strength policies don't apply to email one-time passcode, SAML/WS-Fed, or Google federation users — for those scenarios, continue using the **Require multifactor authentication** grant control.

Require guest users perform multifactor authentication when accessing your organization's resources. Some organizations might be ready to move to stronger authentication methods for their guest users. These organizations might choose to implement a policy like the one described in the article [Require multifactor authentication strength for external users](policy-guests-mfa-strength).

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Template deployment

Organizations can deploy this policy by following the steps outlined below or by using the [Conditional Access templates](concept-conditional-access-policy-common).

## Create a Conditional Access policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All guest and external users**
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
    1. Under **Exclude**, select any applications that don't require multifactor authentication.
7. Under **Access controls** &gt; **Grant**, select **Grant access**, **Require multifactor authentication**, and select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.