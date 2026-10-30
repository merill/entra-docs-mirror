---
layout: Conceptual
title: Require Terms of Use at sign-in to Microsoft Admin Portals - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-all-users-require-terms-of-use
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: How to require terms of use acceptance before access to selected cloud apps is granted with Microsoft Entra Conditional Access.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: 
locale: en-us
document_id: 30af6e66-d38a-a461-9b84-33b4e2c562ca
document_version_independent_id: 259c3b11-817b-430d-7fc8-2cb8f7de5193
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-all-users-require-terms-of-use.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-all-users-require-terms-of-use
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-all-users-require-terms-of-use.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 8f91c260-3c53-00ec-2ae6-1859817642fe
---

# Require Terms of Use at sign-in to Microsoft Admin Portals - Microsoft Entra ID | Microsoft Learn

## Overview

Organizations might want to require users to accept [terms of use (ToU)](terms-of-use) before accessing certain applications in their environment. This example helps you create a policy requiring terms of use to be accepted as part of the initial sign in process for administrators who access any of the [Microsoft Admin Portals](concept-conditional-access-cloud-apps#microsoft-admin-portals).

## Create your terms of use

This section provides you with the steps to create a sample terms of use document. When you create a terms of use document, you select a value for **Enforce with Conditional Access policy templates**. Selecting **Custom policy** opens a dialog to create a new Conditional Access policy as soon as your terms of use is created.

1. Create a new terms of use document and save it as a PDF file.
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
3. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Terms of use**.
4. In the menu on the top, select **New terms**.
5. In the **Name** textbox, provide a name for your terms of use policy.
6. Upload your terms of use PDF file.
    1. Select your default language.
    2. In the **Display name** textbox, type the name you want to be displayed.
7. For **Require users to expand the terms of use**, select **On**.
8. For **Enforce with Conditional Access policy templates**, select **Custom policy**.
9. Select **Create**.

## Create a Conditional Access policy

This section shows how to create the required Conditional Access policy.

**To configure your Conditional Access policy:**

1. Give your policy a name. Create a meaningful standard for the names of your policies.
2. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
3. Under **Target resources** &gt; **Resources (formerly cloud apps)**, select the following options:
    1. Under **Include**, choose **Select resources**.
    2. Select **Microsoft Admin Portals**, and then choose **Select**.
4. Under **Access controls**, select **Grant**.
    1. Select **Grant access**.
    2. Select the terms of use you created previously and choose **Select**.
5. Confirm your settings and set **Enable policy** to **Report-only**.
6. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

## Test your Conditional Access policy

In the previous section, you created a Conditional Access policy requiring terms of use be accepted when accessing any of the [Microsoft Admin Portals](concept-conditional-access-cloud-apps#microsoft-admin-portals).

To test your policy, try to sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) using a test account. You should see a dialog that requires you to accept your terms of use.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).