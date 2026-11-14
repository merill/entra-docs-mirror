---
layout: Conceptual
title: 'Quickstart: Assign and test a built-in Microsoft Entra resource policy (preview) - Microsoft Entra ID Governance | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/resource-policy-quickstart-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Assign a built-in resource policy in report-only mode and compare simulated compliant and noncompliant requests without creating applications.
ms.topic: quickstart
ms.date: 2026-11-11T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 9819ab9c-b9da-359f-92bf-a777aba6cc08
document_version_independent_id: 9819ab9c-b9da-359f-92bf-a777aba6cc08
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/resource-policy-quickstart-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/resource-policy-quickstart-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/resource-policy-quickstart-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 90bd4c6e-8178-2bb7-a27c-70b2e1f45a54
---

# Quickstart: Assign and test a built-in Microsoft Entra resource policy (preview) - Microsoft Entra ID Governance | Microsoft Learn

Use the [Microsoft Entra admin center](https://entra.microsoft.com/) to assign a built-in resource policy in report-only mode and [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to test its decisions with simulated requests. You don't need to write a policy, create applications, or enable enforcement.

## Prerequisites

- An approved test environment.
- A Microsoft Entra ID Governance service plan to create and activate the assignment, including report-only assignments. See [licensing requirements](licensing#resource-policy-preview).
- One work or school account in the test tenant. Use this same account and tenant in the Microsoft Entra admin center and Microsoft Graph Explorer throughout the quickstart, including cleanup.

### Microsoft Entra roles for your account

Use an active [Resource Policy Administrator](resource-policy-concepts#roles-and-api-permissions) role to create and delete the assignment and evaluate assigned policies.

If the role is eligible through Privileged Identity Management (PIM), activate it before starting.

### Delegated permissions for Microsoft Graph Explorer

Before starting, have an administrator grant consent in the test tenant for Microsoft Graph Explorer's **delegated**`ResourcePolicyEvaluation.Read.All` permission. This permission lets you run `evaluateAssignedPolicies` without performing the proposed write.

Assignment creation and cleanup use the Microsoft Entra admin center, so you don't need to grant Graph Explorer assignment-management permissions.

## 1. Select a built-in policy and assign it in your tenant

Use the **Require a department prefix for application names** built-in policy. This policy requires application names to use an allowed department prefix and contain no banned words.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with the test-tenant account described in Prerequisites.
2. Browse to **Tenant governance** &gt; **Definitions**.
3. On the **Built in** tab, find the **Require a department prefix for application names** policy definition and review the description.
4. Select **Add assignment** on the chosen policy definition.
5. On **Settings**, use assignment identifier `enforce_application_name_prefix` and policy version `1.0.0`. Set **Status** to **On** and **Enforcement** to **Report-only**. Leave other properties at their defaults.
6. On **Parameters**, select **Edit allowed\_departments** and enter the following case-sensitive prefixes, one value per row:

    - `Engineering-`
    - `Marketing-`
    - `IT-`
    - `HR-`
    - `Finance-`
    - `Sales-`

    Use **Add row** for the additional `Sales-` value, then select **Apply**. Leave `banned_word_list` and `client_appid_exclusion_list` empty.
7. On **Review**, review the summary and add the assignment.

**On** enables evaluation; **Report-only** records results without blocking requests through this assignment.

## 2. Validate without performing a write

Use `evaluateAssignedPolicies` in Graph Explorer to compare names with and without an allowed prefix, without creating applications. The action evaluates all applicable assignments, so find `enforce_application_name_prefix` in `details` to identify this quickstart's results.

The evaluation action reflects saved assignment settings without waiting for [changes to propagate to real requests](resource-policy-evaluation#assignment-propagation).

Sign in to [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) with the same account and tenant you used in the Microsoft Entra admin center. Confirm that Graph Explorer has the delegated permissions listed in Prerequisites.

### Check a noncompliant application name

Use `Inventory-Taker`, which doesn't start with any of the configured department prefixes.

1. In [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), select **POST** and **beta**.
2. Enter the following request URL:

    ```http
    https://graph.microsoft.com/beta/admin/resourcePolicy/evaluateAssignedPolicies
    ```
3. Select **Request Body** and enter the following JSON:

    ```json
    {
      "resourceUri": "/beta/applications",
      "httpMethod": "post",
      "resourceBody": {
        "displayName": "Inventory-Taker"
      },
      "scope": "/",
      "isResultDetailed": true
    }
    ```
4. Select **Run query**.
5. In **Response preview**, inspect the evaluation result. Select **Expand** if you need more space.

With this report-only assignment, expect **200 OK** and the following fields:

| Field | Value |
| --- | --- |
| `appliedPoliciesEffects` | `deny` |
| `isBlocked` | `false` |
| `details[].assignmentUniqueName` | `enforce_application_name_prefix` |
| `details[].assignedPolicyDisplayName` | Require a department prefix for application names |
| `details[].appliedPolicyEffects` | `deny` |

The matching entry in `details` includes this reason:

> 
> The application name needs an allowed department prefix. Add a prefix from allowed\_departments, then try again.

**200 OK** means the evaluation completed, not that the name is compliant. The `deny` effect identifies the violation; `isBlocked: false` reflects report-only mode. Other applicable assignments can affect the overall result.

### Check a compliant application name

Use `Sales-Inventory-Taker`, which starts with the configured `Sales-` prefix.

1. Keep **POST**, **beta**, and the same evaluation request URL.
2. In **Request Body**, change only `displayName` from `Inventory-Taker` to `Sales-Inventory-Taker`. Keep all other values unchanged.
3. Select **Run query**.
4. In **Response preview**, find the result for `enforce_application_name_prefix`.

With this configuration, expect **200 OK** and the following fields:

| Field | Value |
| --- | --- |
| `appliedPoliciesEffects` | `compliant` |
| `isBlocked` | `false` |
| `details[].assignmentUniqueName` | `enforce_application_name_prefix` |
| `details[].appliedPolicyEffects` | `compliant` |

The response message is:

> 
> Resource is compliant with assigned policies.

Both examples return `isBlocked: false`. Compare the policy effects to distinguish compliance from a report-only violation.

## 3. Clean up or continue

To continue with the [tutorial](resource-policy-tutorial-portal), keep `enforce_application_name_prefix`**On** and **Report-only**, with its version and parameters unchanged. Skip deletion.

If you're stopping here, delete the assignment. The simulated tests created no applications to clean up.

1. Browse to **Tenant governance** &gt; **Assignments**.
2. Select the checkbox for `enforce_application_name_prefix`. Confirm that only the intended assignment is selected, including any selections hidden by the current filter.
3. Select **Delete**.
4. In **Remove assignment?**, confirm **Selected items: 1.**, then select **Delete**.

Deleting the assignment stops it from applying the policy and moves it to **Deleted items**. You can restore it for 30 days.