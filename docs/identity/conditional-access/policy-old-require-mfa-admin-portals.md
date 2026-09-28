---
layout: Conceptual
title: Require multifactor authentication for Microsoft admin portals - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-old-require-mfa-admin-portals
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a Conditional Access policy requiring multifactor authentication for admins accessing Microsoft admin portals.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth
locale: en-us
document_id: 91ad3afe-2622-48fe-2290-b2ef42013eb7
document_version_independent_id: 76d2e793-c43f-85de-a613-c009b38a01b2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-old-require-mfa-admin-portals.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-old-require-mfa-admin-portals
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-old-require-mfa-admin-portals.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 2b447f3d-3cb2-a99e-725f-8ba26e119f4d
---

# Require multifactor authentication for Microsoft admin portals - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft recommends securing access to any Microsoft admin portals like Microsoft Entra, Microsoft 365, Exchange, and Azure. Using the [Microsoft Admin Portals](concept-conditional-access-cloud-apps#microsoft-admin-portals) app organizations can control interactive access to Microsoft admin portals.

Microsoft recommends you require phishing-resistant multifactor authentication on the following roles at a minimum:

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
    1. Under **Include**, select **Directory roles** and choose at least the previously listed roles.

        Warning

        Conditional Access policies support built-in roles. Conditional Access policies are not enforced for other role types including [administrative unit-scoped](../role-based-access-control/manage-roles-portal) or [custom roles](../role-based-access-control/custom-create).
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, **Select resources**, select **Microsoft Admin Portals**.
7. Under **Access controls** &gt; **Grant**, select **Grant access**, **Require authentication strength**, select **Multifactor authentication**, then select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.