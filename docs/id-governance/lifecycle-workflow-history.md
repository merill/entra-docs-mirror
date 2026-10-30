---
layout: Conceptual
title: Lifecycle Workflow History - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/lifecycle-workflow-history
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Conceptual article about Lifecycle Workflows reporting and history capabilities
ms.subservice: lifecycle-workflows
ms.topic: concept-article
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: template-concept, sfi-image-nochange
locale: en-us
document_id: c0d159e3-04d9-5819-6a91-f61eadf948db
document_version_independent_id: c2187544-2d5c-1648-da3b-b3b48358a466
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/lifecycle-workflow-history.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/lifecycle-workflow-history
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/lifecycle-workflow-history.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 6d3a9543-ec6f-f58a-287d-fc1b0f924fcc
---

# Lifecycle Workflow History - Microsoft Entra ID Governance | Microsoft Learn

Workflows created using Lifecycle Workflows allow for the automation of lifecycle tasks for users no matter where they fall in the Joiner-Mover-Leaver (JML) model of their identity lifecycle in your organization. Making sure workflows are processed correctly is an important part of an organization's lifecycle management process. Workflows that aren't processed correctly can lead to many issues in terms of security and compliance. With Lifecycle Workflow's history features, you can specify which workflow events you want to view a history of based on users, runs, or task summaries. This reporting feature allows you to quickly see what ran for whom, and whether or not it was successful. Along with the summaries in these specific areas, you're also able to view detailed information about each specific event recorded in their respective section. You're also able to [download these reports as CSV files](download-workflow-history). In this article, you learn when you would use each of these features when getting more information about how workflows were utilized for users in your organization. For aggregate workflow information across your tenant, see: [Lifecycle workflow Insights](lifecycle-workflow-insights). For detailed information about every action Lifecycle Workflows takes, see: [Auditing Lifecycle Workflows](lifecycle-workflow-audits).

## Lifecycle Workflow History Summaries

Lifecycle Workflows introduce a history feature based on summaries and details. These history summaries allow you to quickly get information about for whom a workflow ran, and whether or not this run was successful. This is valuable because the large set of information given by audit logs might become too numerous to be efficiently used. To make a large set of information processed easier to read, Lifecycle Workflows provide summaries for quick use. You can view these history summaries in three ways:

- **Users summary**: Shows a summary of users processed by a workflow. Successful, failed, and total ran information for each specific user is shown.
- **Runs summary**: Shows a summary of workflow runs in terms of the workflow. Successful, failed, and total task information when workflow runs are noted.
- **Tasks summary**: Shows a summary of tasks processed by a workflow, including how many tasks succeeded, failed, and ran in total.

Summaries allow you to quickly gain details about how a workflow ran for itself, or users, without going into further details in logs. For a step-by-step guide on getting this information, see [Check the status of a workflow](check-status-workflow).

## Users Summary information

User summaries allow you to view workflow information through the lens of users processed.

![Screenshot of a workflow user summary.](media/lifecycle-workflow-history/users-summary-concept.png)

Within the user summary, you're able to find the following information:

| Parameter | Description |
| --- | --- |
| Total Processed | The total number of users processed by a workflow during the selected time frame. |
| Successful | The total number of successful users processed by a workflow during the selected time frame. |
| Failed | The total number of failed users processed by a workflow during the selected time frame. |
| Total tasks | The total number of tasks processed for users in a workflow during the selected time frame. |
| Failed tasks | The total number of failed tasks processed for users in a workflow during the selected time frame. |

### User history details

User detailed history information allows you to filter for specific information based on:

- **Date**: You can filter a specific range from as short as 24 hours up to 30 days of when workflow ran.
- **Status**: You can filter a specific status of the user processed. The supported statuses are: **Completed**, **In Progress**, **Queued**, **Canceled**, **Completed with errors**, and **Failed**.
- **Workflow execution type**: You can filter on workflow execution type such as **Scheduled** or **on-demand**
- **Completed date**: You can filter a specific range from as short as 24 hours up to 30 days of when the user was processed in a workflow.

### User history status details

When you view the status of user processing history, the status values correspond to the following information:

| Status | Details |
| --- | --- |
| Completed | This state is reported if all of the workflow's tasks process successfully for a user. |
| In Progress | This state is reported when a workflow begins running tasks for a user. The status remains in this state until all the workflow's tasks are processed for the user, or it fails. |
| Queued | This state is reported when a user is identified by the Lifecycle Workflow engine that meets the execution conditions of a workflow. From here a user either enters a state of *In progress* if the workflow begins running for them, or canceled if the admin manually cancels the workflow. |
| Canceled | This state is reported for the following reasons: **1.** If the workflow was deleted, all scheduled users it's set to run for are canceled.**2.** If the workflow was disabled, all scheduled users it's set to run for are canceled.**3**. If the workflow's schedule was disabled, all scheduled users it's set to run for are canceled.**4.** If the workflow had a new version created and all tasks were disabled, all scheduled users it's set to run for are canceled.**5.** If users don't meet the current execution conditions of the workflow's new version, the scheduled runs are canceled.**6.** If the user was queued to have the workflow run for them, but has a profile change and no longer meet the current execution conditions of the workflow immediately before it runs, the processing is canceled. |
| Completed with errors | This state is reported if the workflow completed, but one or more tasks that are set have **continueOnError** set as *true* have failed. |
| Failed | This state is reported if a task with **continueOnError** set as *false* fails. |

For a complete guide on getting user processed summary information, see: [User workflow history using the Microsoft Entra admin center](check-status-workflow#user-workflow-history-using-the-microsoft-entra-admin-center).

## Runs Summary

Runs summaries allow you to view workflow information through the lens of its run history.

![Screenshot of a workflow runs summary.](media/lifecycle-workflow-history/runs-status-concept.png)

Within the runs summary, you're able to find the following information:

| Parameter | Description |
| --- | --- |
| Total Processed | The total number of workflows that have run. |
| Successful | Workflows that successfully ran. |
| Failed | Workflows that failed to run. |
| Failed tasks | Workflows that ran with failed tasks. |

### Runs history details

Runs detailed history information allows you to filter for specific information based on:

- **Date**: You can filter a specific range from as short as 24 hours up to 30 days of when workflow ran.
- **Status**: You can filter a specific status of the workflow run. The supported statuses are: **Completed**, **In Progress**, **Queued**, **Canceled**, **Completed with errors**, and **Failed**.
- **Workflow execution type**: You can filter on workflow execution type such as **Scheduled** or **On-demand**.
- **Completed date**: You can filter a specific range from as short as 24 hours up to 30 days of when the workflow ran.

### Runs history status details

When you view the status of run history, the status values correspond to the following information:

| Status | Details |
| --- | --- |
| Queued | This state is reported the first time a workflow is set to run. |
| In Progress | This state is reported as soon as the workflow begins processing its first task. |
| Canceled | This state is reported if it was *In Progress* at one point of time, and is now frozen in that state. |
| Completed with errors | This state is reported if the workflow runs successfully for some, but not others. If a workflow enters the queued state, but all of its instances are canceled before executing, then it also shows this state before ever entering a state of *In Progress*. |
| Completed | This state is reported if the workflow ran successfully for every user. |
| Failed | This state is reported if all tasks failed for all users the workflow runs for. Canceled users aren't counted as failures in the report. |

For a complete guide on getting runs information, see: [Run workflow history using the Microsoft Entra admin center](check-status-workflow#run-workflow-history-using-the-microsoft-entra-admin-center).

## Tasks summary

Task summaries allow you to view workflow information through the lens of its tasks.

![Screenshot of a workflow task summary.](media/lifecycle-workflow-history/task-summary-concept.png)

Within the tasks summary, you're able to find the following information:

| Parameter | Description |
| --- | --- |
| Total Processed | The total number of tasks processed by a workflow. |
| Successful | The number of successfully processed tasks by a workflow. |
| Failed | The number of failed processed tasks by a workflow. |
| Unprocessed | The number of unprocessed tasks by a workflow. |

### Task history details

Task detailed history information allows you to filter for specific information based on:

- **Date**: You can filter a specific range from as short as 24 hours up to 30 days of when workflow ran.
- **Status**: You can filter a specific status of the workflow run. The supported statuses are: **Completed**, **In Progress**, **Queued**, **Canceled**, **Completed with errors**, and **Failed**.
- **Completed date**: You can filter a specific range from as short as 24 hours up to 30 days of when the workflow ran.
- **Tasks**: You can filter based on specific task names.

### Task history status details

When you view the status of task history, the status values correspond to the following information:

| Status | Details |
| --- | --- |
| Queued | This state is reported once a workflow instance is scheduled for execution, task reports for all of the tasks within the workflow are also created with this status with Run record. Each task report includes all users but represents a specific task. |
| In Progress | This state is reported as soon as the first task begins being processed. |
| Canceled | This state is reported if no tasks are processed before the workflow is canceled. If a workflow that contains the tasks is deleted, then the status also shows as canceled. |
| Completed with errors | This state is reported if a task is processed for a user, but not every task succeeds. |
| Completed | This state is reported if all tasks ran successfully for every user. |
| Failed | This state is reported if all tasks failed. |

Separating processing of the workflow from the tasks is important because, in a workflow, processing a user certain tasks could be successful, while others could fail. Whether or not a task runs after a failed task in a workflow depends on parameters such as enabling continue On Error, and their placement within the workflow. For more information, see [Common task parameters](lifecycle-workflow-tasks#common-task-parameters).