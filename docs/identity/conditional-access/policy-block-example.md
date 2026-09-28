---
layout: Conceptual
title: Conditional Access - Block access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-block-example
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a custom Conditional Access policy to Block access.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: calebb, lhuangnorth
locale: en-us
document_id: 5ab8873e-3b18-fadc-cb98-0e48f819e3e7
document_version_independent_id: 19fb2bc0-2a06-5e4d-a5f3-ea9c1cc2406f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-block-example.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-block-example
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-block-example.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: e336d6ab-1730-1506-0797-9ab6ee56639b
---

# Conditional Access - Block access - Microsoft Entra ID | Microsoft Learn

## Overview

For organizations with a conservative cloud migration approach, the block all policy is an option that can be used.

Caution

Misconfiguration of a block policy can lead to organizations being locked out.

Policies like these can have unintended side effects. Proper testing and validation are vital before enabling. Administrators should utilize tools such as [Conditional Access report-only mode](concept-conditional-access-report-only) and [the What If tool in Conditional Access](what-if-tool) when making changes.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Create a Conditional Access policy

The following steps help create Conditional Access policies to block access to all apps except for [Office 365](concept-conditional-access-cloud-apps#office-365) (Microsoft 365) if users aren't on a trusted network. These policies are put in to [Report-only mode](howto-conditional-access-insights-reporting) to start so administrators can determine the impact on existing users. When administrators are comfortable that the policies apply as they intend, they can switch them to **On**.

The first policy blocks access to all apps except for Microsoft 365 applications if not on a trusted location.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)**, select the following options:
    1. Under **Include**, select **All resources (formerly 'All cloud apps')**.
    2. Under **Exclude**, select **Office 365**, select **Select**.
7. Under **Conditions**:
    1. Under **Conditions** &gt; **Location**.
        1. Set **Configure** to **Yes**
        2. Under **Include**, select **Any location**.
        3. Under **Exclude**, select **All trusted locations**.
    2. Under **Client apps**, set **Configure** to **Yes**, and select **Done**.
8. Under **Access controls** &gt; **Grant**, select **Block access**, then select **Select**.
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

The following policy is created to require multifactor authentication or a compliant device for users of Microsoft 365.

1. Select **Create new policy**.
2. Give your policy a name. Create a meaningful standard for the names of your policies.
3. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
4. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include** &gt; **Select resources**, choose **Office 365**, and select **Select**.
5. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require multifactor authentication** and **Require device to be marked as compliant** select **Select**.
    2. Ensure **Require one of the selected controls** is selected.
    3. Select **Select**.
6. Confirm your settings and set **Enable policy** to **Report-only**.
7. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

Note

Conditional Access policies are enforced after first-factor authentication is completed. Conditional Access isn't intended to be an organization's first line of defense for scenarios like denial-of-service (DoS) attacks, but it can use signals from these events to determine access.