---
layout: Conceptual
title: Check status of a Lifecycle workflow - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/check-status-workflow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article guides a user on checking the status of a Lifecycle workflow
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: template-how-to, sfi-image-nochange
locale: en-us
document_id: 1ef53d6a-1553-edae-f82d-6382bd9539a1
document_version_independent_id: c0520f95-a2cc-4861-40b8-84b6a8aa2399
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/check-status-workflow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/check-status-workflow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/check-status-workflow.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 9ba5fafb-f43a-a55e-619e-374ba390e78a
---

# Check status of a Lifecycle workflow - Microsoft Entra ID Governance | Microsoft Learn

When a workflow is created, it's important to check its status and run history to make sure it ran properly for the users it processed both by schedule and by on-demand. To get information about the status of workflows, Lifecycle Workflows allows you to check run and user processing history. This history also gives you summaries to see how often a workflow has run, and who it ran successfully for. You're also able to check the status of both the workflow, and its tasks. Checking the status of workflows and their tasks allows you to troubleshoot potential problems that could come up during their execution.

## Run workflow history using the Microsoft Entra admin center

You're able to retrieve run information of a workflow using Lifecycle Workflows. To check the runs of a workflow using the Microsoft Entra admin center, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. Select the workflow whose run history you want to check.
4. On the workflow overview screen, select **Workflow history**.
5. On the history page, select the **Runs** button.
6. Here you see a summary of workflow runs. ![Screenshot of a workflow Runs list.](media/check-status-workflow/run-list.png)
7. The runs summary cards include the total number of processed runs, the number of successful runs, the number of failed runs, and the total number of failed tasks.

## User workflow history using the Microsoft Entra admin center

To get further information than just the runs summary for a workflow, you're also able to get information about users processed by a workflow. To check the status of users a workflow has processed using the Microsoft Entra admin center, follow these steps:

1. In the left menu, select **Lifecycle Workflows**.
2. Select **Workflows**.
3. Select the workflow you want to see user processing information for.
4. On the workflow overview screen, select **Workflow history**. ![Screenshot of a workflow overview history.](media/check-status-workflow/workflow-history.png)
5. On the workflow history page, you're presented with a summary of every user processed by the workflow along with counts of successful and failed users and tasks. ![Screenshot of a list of workflow summaries.](media/check-status-workflow/workflow-history-list.png)
6. By selecting total tasks for a user, you can see which tasks successfully completed, or are currently in progress. ![Screenshot of workflow task history status.](media/check-status-workflow/task-history-status.png)
7. By selecting failed tasks, you're able to see which tasks failed for a specific user. ![Screenshot of workflow failed tasks history.](media/check-status-workflow/task-history-failed.png)
8. By selecting unprocessed tasks, you're able to see which tasks are unprocessed. ![Screenshot of unprocessed tasks of a workflow.](media/check-status-workflow/task-history-unprocessed.png)

## User workflow history using Microsoft Graph

### List user processing results using Microsoft Graph

To view a status list of users processed by a workflow, which are UserProcessingResults, you'd make the following API call:

To view a list of user processing results using API via Microsoft Graph, see: [List userProcessingResults](/en-us/graph/api/identitygovernance-workflow-list-userprocessingresults)

### User processing results using Microsoft Graph

To view a summary of user processing results via API using Microsoft Graph, see: [userProcessingResult: summary](/en-us/graph/api/identitygovernance-userprocessingresult-summary)

## Run workflow history via Microsoft Graph

### List runs using Microsoft Graph

To view runs of a workflow via API using Microsoft Graph, see: [runs](/en-us/graph/api/resources/identitygovernance-run)

### Get a summary of runs using Microsoft Graph

To view run summary via API using Microsoft Graph, see: [run summary of a lifecycle workflow](/en-us/graph/api/identitygovernance-run-summary)

### List user and task processing results of a given run using Microsoft Graph

To get user processing result for a run of a lifecycle workflow via API using Microsoft Graph, see: [Get userProcessingResult (for a run of a lifecycle workflow)](/en-us/graph/api/identitygovernance-userprocessingresult-get)

To list task processing results for a user processing result via API using Microsoft Graph, see: [List taskProcessingResults (for a userProcessingResult)](/en-us/graph/api/identitygovernance-userprocessingresult-list-taskprocessingresults)

Note

A workflow must have activity in the past 7 days to get **userProcessingResults ID**. If there isn't any activity in that time-frame, the **userProcessingResults** call returns no value.