---
layout: Conceptual
title: Lifecycle Workflow Insights - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/lifecycle-workflow-insights
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Conceptual article about Lifecycle Workflows reporting and history capabilities.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: krbain
locale: en-us
document_id: 1abb23f1-0ce0-5525-a7c2-f477ab48b387
document_version_independent_id: 1abb23f1-0ce0-5525-a7c2-f477ab48b387
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/lifecycle-workflow-insights.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/lifecycle-workflow-insights
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/lifecycle-workflow-insights.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: a9ded9db-0aef-d100-658e-f8dab6a0d523
---

# Lifecycle Workflow Insights - Microsoft Entra ID Governance | Microsoft Learn

Workflows created using Lifecycle Workflows allow for the automation of lifecycle tasks for users no matter where they fall in the Joiner-Mover-Leaver (JML) model of their identity lifecycle in your organization. Making sure workflows are processed correctly is an important part of an organization's lifecycle management process. With the Lifecycle Workflows Workflow Insights feature, you're able to see aggregate information about all workflows across your tenant.

![Screenshot of the Workflow Insights page.](media/lifecycle-workflow-insights/workflow-insights-view.png)

With Workflow Insights, you're also able to view aggregate workflow information across your tenant. Workflow Insights allows you to quickly view the following information:

- Summary
- Top Workflows
- Top Tasks
- Workflow by Category

More details about insights found in these sections are discussed in the following sections of this article. For a step by step guide on checking the insights for workflows in your tenant, see: [Check Workflow Insights](manage-workflow-insights).

## Workflow Insights summary

The Workflow Insights summary provides a numerical view of successful workflows, users, and tasks processed within a tenant.

![Screenshot of a workflow insights summary.](media/lifecycle-workflow-insights/workflow-insights-summary.png)

This summary can be filtered to show information from the past 7, 14, or 30 days.

## Top Workflow Insights summary

The Top Workflows Insights summary lists the top workflows ran in the tenant for a time-span that can be 7, 14, or 30 days. The top workflows can also filter in order by total processed, successful runs, or failed runs.

![Screenshot of top workflows processed insight summary.](media/lifecycle-workflow-insights/workflow-insights-workflows.png)

When you view the top workflow insights summary, the following information is shown:

| Detail | Information |
| --- | --- |
| Workflow | The name of the workflow. |
| Total Processed | The total runs of the workflow. |
| Successful | The successful runs for the workflow. |
| Failed | The failed runs for the workflow. |
| Category | The workflow's category. |
| Total Users | The total number of users processed by the workflow. |
| Successful Users | The number of successful users processed by the workflow. |
| Failed Users | The number of failed users processed by the workflow. |

Note

Users, who the workflow ran successfully for with errors, might affect the count of users processed.

## Top Tasks Insights summary

The Top Tasks Insights summary lists the top tasks ran in the tenant for a time-span that can be 7, 14, or 30 days. The top tasks can also filter in order by total processed, successful runs, or failed runs.

![Screenshot of workflow insights top tasks summary.](media/lifecycle-workflow-insights/workflow-insights-tasks.png)

When you view the top tasks insights summary, the following information is shown:

| Detail | Information |
| --- | --- |
| Task | The name of the task. |
| Total Processed | The total runs of the task. |
| Successful | The successful runs for the task. |
| Failed | The failed runs for the task. |
| Total Users | The total number of users processed by the task. |
| Successful Users | The number of successful users processed by the task. |
| Failed Users | The number of failed users processed by the task. |

## Workflow Category Insights summary

The Workflow Category Insights summary lists the top workflows run by category using a percentage for a time-span that can be 7, 14, or 30 days. The category can also filter by total processed, successful workflows, or failed workflows.

![Screenshot of workflow insights by category summary.](media/lifecycle-workflow-insights/workflow-insights-category.png)

When you view the workflows run by category insights summary, the following information is shown:

| Detail | Information |
| --- | --- |
| Joiner | The percentage of workflows that have the category of *Joiner*. If the filter is set as successful, the percentage of Joiner is the number of Joiner workflows by percentage that were successful during the filtered time span. |
| Mover | The percentage of workflows that have the category of *Mover*. If the filter is set as total, the percentage of Mover is the number of mover workflows by percentage that were processed during the filtered time span. |
| Leaver | The percentage of workflows that have the category of *Leaver*. If the filter is set as failed, the percentage of Leaver is the number of Leaver workflows by percentage that failed during the filtered time span. |