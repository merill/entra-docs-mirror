---
layout: Conceptual
title: Check execution user scope of a workflow - Microsoft Entra ID - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/check-workflow-execution-scope
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Describes how to check the users who fall into the execution scope of a Lifecycle Workflow.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: krbain
ms.custom: sfi-image-nochange
locale: en-us
document_id: 539780c9-eab7-f941-d323-fa7f29884fc5
document_version_independent_id: 09d16f29-ea55-248f-8689-a2a422c38d10
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/check-workflow-execution-scope.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/check-workflow-execution-scope
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/check-workflow-execution-scope.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b18f0371-1d1c-1e49-e8ef-9f85507bbbb5
---

# Check execution user scope of a workflow - Microsoft Entra ID - Microsoft Entra ID Governance | Microsoft Learn

Workflow scheduling will automatically process the workflow for users meeting the workflow's execution conditions. This article walks you through the steps to check the users who fall into the execution scope of a workflow. For more information about execution conditions, see: [workflow basics](understanding-lifecycle-workflows#workflow-basics).

## Check execution user scope of a workflow using the Microsoft Entra admin center

To check the users who fall under the execution scope of a workflow, you'd follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. From the list of workflows, select the workflow you want to check the execution scope of.
4. On the workflow overview page, select **Execution conditions**.
5. On the Execution conditions page, select the **Execution User Scope** tab.
6. On this page, you're presented with a list of users who currently meet the scope for execution for the workflow regardless of whether they have already been processed by the workflow. [![Screenshot of users under scope of workflow execution.](media/check-workflow-execution-scope/execution-user-scope-list.png)](media/check-workflow-execution-scope/execution-user-scope-list.png#lightbox)

Note

The workflow engine currently has a retroactive window that allows workflows to run for users who previously met the conditions for the workflow. For more information on this window, see: [Lifecycle workflow catch-up window](lifecycle-workflow-execution-conditions#lifecycle-workflow-catch-up-window).

## Check execution user scope of a workflow using Microsoft Graph

To check execution user scope of a workflow using API via Microsoft Graph, see: [List executionScope](/en-us/graph/api/workflow-list-executionscope).