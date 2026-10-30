---
layout: Conceptual
title: Configure execution limits for Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/lifecycle-workflow-execution-limits
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to set tenant-wide and workflow-specific execution limits and manage quarantined workflows in Lifecycle Workflows to prevent large-scale impact.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.custom: msecd-doc-authoring-1015
ms.date: 2026-06-23T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 1cbbacdd-c40b-8ef0-a249-b06f33cc820b
document_version_independent_id: 1cbbacdd-c40b-8ef0-a249-b06f33cc820b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/lifecycle-workflow-execution-limits.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/lifecycle-workflow-execution-limits
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/lifecycle-workflow-execution-limits.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: bfd27b2d-4ece-e5ef-1f60-23de0549803b
---

# Configure execution limits for Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn

Lifecycle Workflows lets you run your workflows with confidence by using built-in guardrails. You can set tenant-wide or per-workflow execution limits and require admin approval to resume execution after a limit is reached. These limits protect your organization from large-scale impact caused by misconfigurations.

When a scheduled run exceeds a configured limit, Lifecycle Workflows places the workflow in quarantine and notifies administrators. A quarantined workflow doesn't run again until an administrator approves its execution.

This article shows you how to set tenant-wide execution limits, set workflow-specific execution limits, and review and clear quarantined workflows in the Microsoft Entra admin center.

Execution limits apply only to scheduled workflow runs. Limits are checked automatically before a workflow runs at its scheduled time. On-demand runs aren't subject to execution limits.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Set tenant-wide execution limits

Tenant-wide limits apply to all workflows that don't have their own workflow-specific limits. Set a tenant-wide limit as a percentage of your user population, a fixed number of users, or both.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflow settings**.
3. Select **Enable execution threshold**.

    [![Screenshot of the Lifecycle workflows Workflow settings page with the Tenant Execution Threshold section and Enable execution threshold toggle.](media/lifecycle-workflow-execution-limits/tenant-execution-threshold.jpg)](media/lifecycle-workflow-execution-limits/tenant-execution-threshold.jpg#lightbox)
4. Select one or both of the following limit options:

    - **Limit to percentage of user population**: Enter the percentage of users you want to allow.
    - **Limit to specific number of users**: Enter the fixed number of users you want to allow.
5. Select **Save**.

When you set both limit options, Lifecycle Workflows evaluates them using OR logic. If either limit is exceeded, the workflow is quarantined.

## Set workflow-specific execution limits

Workflow-specific limits apply to a single workflow and override any tenant-wide limits for that workflow. Only the workflow-specific limits are enforced for that workflow.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**, and then select the workflow you want to update.
3. On the workflow page, select **Settings**.
4. Select **Enable execution threshold**.

    [![Screenshot of a workflow Settings page with the Workflow Execution Threshold section and the limit options for percentage and number of users.](media/lifecycle-workflow-execution-limits/workflow-execution-threshold.png)](media/lifecycle-workflow-execution-limits/workflow-execution-threshold.png#lightbox)
5. Select one or both of the following limit options:

    - **Limit to percentage of user population**: Enter the percentage of users you want to allow.
    - **Limit to specific number of users**: Enter the fixed number of users you want to allow.
6. Select **Save**.

Note

Updating workflow execution limits creates a new workflow version. The new version appears in the Microsoft Entra admin center, but isn't currently reflected in the API.

## View and clear quarantined workflows

When a workflow exceeds its execution limit, Lifecycle Workflows quarantines the workflow and automatically sends an email notification to Lifecycle Workflows administrators. You don't need to configure an email task to receive these notifications. Review the quarantined workflow and approve its execution when you're ready for it to run again.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. To view quarantined workflows, do one of the following:

    - Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Quarantined workflows**.
    - On the **Lifecycle workflows** **Overview** page, in the **Alerts** section, select **View quarantined workflows**.

    [![Screenshot of the Lifecycle workflows Overview page Alerts section showing the In Quarantine count and the View quarantined workflows link.](media/lifecycle-workflow-execution-limits/quarantined-workflows-alert.png)](media/lifecycle-workflow-execution-limits/quarantined-workflows-alert.png#lightbox)
3. Select one or more workflows from the quarantined workflows list.

    [![Screenshot of the Quarantined workflows page listing quarantined workflows with their exceeded threshold, reason, and quarantined date.](media/lifecycle-workflow-execution-limits/quarantined-workflows-list.png)](media/lifecycle-workflow-execution-limits/quarantined-workflows-list.png#lightbox)
4. Select **Approve execution**.

Note

If a workflow is no longer needed, you can delete it from the tenant instead of approving its execution.

Approving execution doesn't trigger an immediate run. The workflow follows its existing schedule:

- If you approve execution before the next scheduled run time and the workflow still meets its execution conditions, it runs at the scheduled time.
- If you approve execution after the scheduled run time, the workflow is evaluated at the next scheduled run.

You can also run a quarantined workflow on demand, which bypasses execution limits. From the workflow history, you can reprocess all users for a specific run while the workflow remains quarantined. Reprocessing individual users isn't supported.

## Frequently asked questions

**Do execution limits apply to on-demand workflow runs?**

No. Execution limits apply only to scheduled workflow runs. Limits are checked automatically before a workflow runs at its scheduled time.

**What happens if I set both a percentage limit and a user count limit?**

Lifecycle Workflows evaluates the limits using OR logic. If either limit is exceeded, the workflow is quarantined.

**What happens if I set both tenant-wide limits and a workflow-specific limit?**

Workflow-specific limits override tenant-wide limits for that workflow. Only the workflow-specific limits are enforced.

**Can quarantine be cleared automatically without approval?**

No. Clearing quarantine requires approval. A quarantined workflow doesn't run until it's cleared.

**Can I put a workflow into quarantine manually?**

No. Quarantine is automatic and is triggered only when execution limits are exceeded.