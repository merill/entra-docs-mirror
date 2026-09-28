---
layout: Conceptual
title: Delete a lifecycle workflow - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/delete-lifecycle-workflow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to delete a lifecycle workflow.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: krbain
locale: en-us
document_id: 1d7e87e5-e7c3-d804-1140-f0c24917613a
document_version_independent_id: deef760c-0e66-c834-6e87-d249cdd0d3ad
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/delete-lifecycle-workflow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/delete-lifecycle-workflow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/delete-lifecycle-workflow.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 785c8f8e-c533-5f67-15f3-f49757dcaadb
---

# Delete a lifecycle workflow - Microsoft Entra ID Governance | Microsoft Learn

You can remove workflows that you no longer need. Deleting these workflows helps keep your lifecycle strategy up to date.

When a workflow is deleted, it enters a soft-delete state. During this period, you can still view it in the list of deleted workflows and restore it if needed. A workflow is permanently removed 30 days after it enters a soft-delete state. If you don't want to wait 30 days for a workflow to be permanently deleted, you can manually delete it.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Delete a workflow by using the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. On the **Workflows** page, select the workflow that you want to delete. Then select **Delete**.

    ![Screenshot of a list of workflows with one selected, along with the Delete button.](media/delete-lifecycle-workflow/delete-button.png)
4. Confirm that you want to delete the workflow by selecting the **Delete** button.

    ![Screenshot of confirming the deletion of a workflow.](media/delete-lifecycle-workflow/delete-workflow.png)

## View deleted workflows in the Microsoft Entra admin center

After you delete workflows, you can view them on the **Deleted workflows** page.

1. On the left pane, select **Deleted workflows**.
2. On the **Deleted workflows** page, check the list of deleted workflows. Each workflow has a description, the date of deletion, and a permanent delete date. By default, the permanent delete date for a workflow is 30 days after it was originally deleted.

    ![Screenshot of a list of deleted workflows.](media/delete-lifecycle-workflow/deleted-list.png)
3. To restore a deleted workflow, select it and then select **Restore workflow**.

    To permanently delete a workflow immediately, select it and then select **Delete permanently**.

## Delete a workflow by using Microsoft Graph

To delete a workflow by using an API via Microsoft Graph, see [Delete a lifecycle workflow](/en-us/graph/api/identitygovernance-workflow-delete?view=graph-rest-beta&amp;preserve-view=true).

## View deleted workflows by using Microsoft Graph

To view a list of deleted workflows by using an API via Microsoft Graph, see [List deleted workflows](/en-us/graph/api/identitygovernance-lifecycleworkflowscontainer-list-deleteditems).

## Permanently delete a workflow by using Microsoft Graph

To permanently delete a workflow by using an API via Microsoft Graph, see [Permanently delete a deleted workflow](/en-us/graph/api/identitygovernance-deleteditemcontainer-delete).

## Restore a deleted workflow by using Microsoft Graph

To restore a deleted workflow by using an API via Microsoft Graph, see [Restore a deleted workflow](/en-us/graph/api/identitygovernance-workflow-restore).

Note

You can't restore permanently deleted workflows.