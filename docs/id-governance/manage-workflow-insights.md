---
layout: Conceptual
title: Check Workflow Insights - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/manage-workflow-insights
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to check workflow insights within your Microsoft Entra tenant.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: krbain
locale: en-us
document_id: 5d4191b4-6363-f6fe-bac0-acd41e88e806
document_version_independent_id: 5d4191b4-6363-f6fe-bac0-acd41e88e806
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/manage-workflow-insights.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/manage-workflow-insights
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/manage-workflow-insights.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 990b06a2-db0e-a571-6a78-ff4e5a7146ef
---

# Check Workflow Insights - Microsoft Entra ID Governance | Microsoft Learn

With Workflow Insights, you're able to get a quick view of workflow execution within your environment. With Workflow Insights, you can view information such as:

- Numerical summaries of all successful workflows, users processed, and successful tasks that ran in your environment.
- The top workflows of the past time-span that you define from either 7, 14, or 30 days.
- The top tasks of the past time-span that you define from either 7, 14, or 30 days.
- Number of workflows by categories of the past time-span that you define from either 7, 14, or 30 days.

For more information, see: [Workflow Insights](lifecycle-workflow-insights).

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Check Workflow Insights using the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Overview**.
3. On the overview page, select **Workflow Insights**.
4. On the Workflow Insights page, you're able to view workflow information across your environment.
5. When you find the information you want to look further into, you can select the **filter** option and choose which time frame you want to view information from.
6. Along with being able to filter on a time period, for top workflows and tasks, you're also able to filter based on activity.

    ![Screenshot of picking time duration in workflow insights.](media/manage-workflow-insights/timespan-choice.png)
7. With the activity filter, you can choose to see the top processed workflows or tasks by choosing **Total Processed**, only those which were **Successful**, or only the ones that **Failed**.
8. Under **Workflow Runs by Category** you can filter workflows by category. You can filter to see the percentage of workflows **Total Processed**, **Successful** workflows by category, or **Failed** workflows by category.

    ![Screenshot of workflows by category insights.](media/manage-workflow-insights/workflow-filter-category.png)