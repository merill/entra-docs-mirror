---
layout: Conceptual
title: Block access for users with elevated insider risk - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-risk-based-insider-block
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create Conditional Access policies using signals from Adaptive protection in Microsoft Purview.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: poulomib
locale: en-us
document_id: d9926de7-b17b-1e56-3cac-92c7b0ff001a
document_version_independent_id: d9926de7-b17b-1e56-3cac-92c7b0ff001a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-risk-based-insider-block.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-risk-based-insider-block
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-risk-based-insider-block.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7d2198e2-d764-607a-71c4-4fe7578017ab
---

# Block access for users with elevated insider risk - Microsoft Entra ID | Microsoft Learn

## Overview

Most users have a normal behavior that can be tracked, when they fall outside of this norm it could be risky to allow them to just sign in. You might want to block that user or ask them to review a specific [terms of use policy](terms-of-use). Microsoft Purview can provide an [insider risk signal](concept-conditional-access-conditions#insider-risk) to Conditional Access to refine access control decisions. Insider risk management is part of [Microsoft Purview](/en-us/purview/insider-risk-management-adaptive-protection). You must enable it before you can use the signal in Conditional Access.

[![Screenshot of an example Conditional Access policy using insider risk as a condition.](media/policy-risk-based-insider-block/insider-risk-based-conditional-access-policy.png)](media/policy-risk-based-insider-block/insider-risk-based-conditional-access-policy.png#lightbox)

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Template deployment

Organizations can deploy this policy by following the steps outlined below or by using the [Conditional Access templates](concept-conditional-access-policy-common).

## Block access with Conditional Access policy

Tip

Configure [adaptive protection](/en-us/purview/insider-risk-management-adaptive-protection) before you create the following policy.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**:
        1. Select **Users and groups** and choose your organization's emergency access or break-glass accounts.
        2. Select **Guest or external users**and choose the following:
            1. **B2B direct connect users**.
            2. **Service provider users**.
            3. **Other external users**.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Conditions** &gt; **Insider risk**, set **Configure** to **Yes**.
    1. Under **Select the risk levels that must be assigned to enforce the policy**.
        1. Select **Elevated**.
        2. Select **Done**.
8. Under **Access controls** &gt; **Grant**, select **Block access**, then select **Select**.
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

Some administrators might create other Conditional Access policies that use other access controls, like terms of use on lower levels of insider risk.