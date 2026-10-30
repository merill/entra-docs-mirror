---
layout: Conceptual
title: Block authentication flows with Conditional Access policy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-block-authentication-flows
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Secure your organization by blocking device code flow and authentication transfer. Learn how to configure Conditional Access policies effectively.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: anjusingh, ludwignick
locale: en-us
document_id: b0710a99-ef99-1cff-c29f-6527e432a47d
document_version_independent_id: b0710a99-ef99-1cff-c29f-6527e432a47d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-block-authentication-flows.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-block-authentication-flows
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-block-authentication-flows.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 81e5503b-f93c-51e5-b600-8937b8e97b31
---

# Block authentication flows with Conditional Access policy - Microsoft Entra ID | Microsoft Learn

## Overview

The following steps help you create Conditional Access policies to restrict how [device code flow](concept-authentication-flows#device-code-flow) and [authentication transfer](concept-authentication-flows#authentication-transfer) are used within your organization.

## Device code flow policies

We recommend organizations get as close as possible to a unilateral block on device code flow. Consider creating a policy to audit the existing use of device code flow and determine if it's still necessary. Only allow device code flow in well documented and secured use cases, like legacy tooling that can't be updated.

For organizations that don't use device code flow, block it with the following Conditional Access policy:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select the users you want to be in-scope for the policy (**all users** recommended).
    2. Under **Exclude**:
        1. Select **Users and groups** and choose your organization's emergency access or break-glass accounts and any other necessary users. Audit this exclusion list regularly.
5. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select the apps you want to be in-scope for the policy (**All resources (formerly 'All cloud apps')** recommended).
6. Under **Conditions** &gt; **Authentication Flows**, set **Configure** to **Yes**.
    1. Select **Device code flow**.
    2. Select **Done**.
7. Under **Access controls** &gt; **Grant**, select **Block access**.
    1. Select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

## Authentication transfer policies

Use the **Authentication flows** condition in Conditional Access to manage the feature. Block [authentication transfer](concept-authentication-transfer) if you don't want users to transfer authentication from their PC to a mobile device. For example, block authentication transfer if you don't allow Outlook to be used on personal devices by certain groups. Use the following Conditional Access policy to block authentication transfer:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users** or user groups you want to block for authentication transfer.
    2. Under **Exclude**:
        1. Select **Users and groups** and choose your organization's emergency access or break-glass accounts and any other necessary users. Audit this exclusion list regularly.
5. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All resources (formerly 'All cloud apps')** or apps you want to block for authentication transfer.
6. Under **Conditions** &gt; **Authentication Flows**, set **Configure** to **Yes**
    1. Select **Authentication transfer**.
    2. Select **Done**.
7. Under **Access controls** &gt; **Grant**, select **Block access**.
    1. Select **Select**.
8. Confirm your settings and set **Enable policy** to **Enabled**.
9. Select **Create** to enable your policy.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).