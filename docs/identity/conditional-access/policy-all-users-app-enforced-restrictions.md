---
layout: Conceptual
title: Use application enforced restrictions to protect access from unmanaged devices - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-all-users-app-enforced-restrictions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a custom Conditional Access policy for unmanaged devices.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth
locale: en-us
document_id: 7748fc00-fbc7-df50-de8e-f04839e09a11
document_version_independent_id: b3a4e4e4-f291-99d8-c7e5-3c273828a8bb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-all-users-app-enforced-restrictions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-all-users-app-enforced-restrictions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-all-users-app-enforced-restrictions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/7428317a-e6c2-4461-ad3e-8a8ad3608734
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/e4f59707-f107-48f2-8d75-0afd91868cd7
platformId: efd7ff03-ce7b-6c5c-c030-3f3c86dd0cf3
---

# Use application enforced restrictions to protect access from unmanaged devices - Microsoft Entra ID | Microsoft Learn

## Overview

This policy can help organizations accomplish the following initiatives:

- [Block or limit access to a specific SharePoint site or OneDrive](/en-us/sharepoint/control-access-from-unmanaged-devices#block-or-limit-access-to-a-specific-sharepoint-site-or-onedrive)
- [Limit access to email attachments in Outlook on the web and the new Outlook for Windows](/en-us/security/zero-trust/zero-trust-identity-device-access-policies-exchange#limit-access-to-exchange-online-from-outlook-on-the-web)
- [Enforce idle session timeout on unmanaged devices](/en-us/microsoft-365/admin/manage/idle-session-timeout-web-apps#idle-session-timeout-on-unmanaged-devices)

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
    1. Under **Include**, select **All users**
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)**, select the following options:
    1. Under **Include**, choose **Select resources**.
    2. Choose **Office 365**, then select **Select**.
7. Under **Access controls** &gt; **Session**, select **Use app enforced restrictions**, then select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.