---
layout: Conceptual
title: Automate employee offboarding tasks after their last day of work with the Microsoft Entra admin center - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tutorial-scheduled-leaver-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Tutorial for post off-boarding users from an organization using Lifecycle workflows with the Microsoft Entra admin center.
ms.subservice: lifecycle-workflows
ms.topic: tutorial
ms.date: 2024-11-25T00:00:00.0000000Z
ms.reviewer: krbain
ms.custom: template-tutorial, sfi-image-nochange
locale: en-us
document_id: edf949be-c8b3-418d-c0f7-3b8c1cf48626
document_version_independent_id: fc00095e-3273-46de-6d9d-5ded6fd78157
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tutorial-scheduled-leaver-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tutorial-scheduled-leaver-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tutorial-scheduled-leaver-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: acd61d2b-59d0-8944-3eb9-1c7470a116d2
---

# Automate employee offboarding tasks after their last day of work with the Microsoft Entra admin center - Microsoft Entra ID Governance | Microsoft Learn

This tutorial provides a step-by-step guide on how to configure off-boarding tasks for employees after their last day of work with Lifecycle workflows using the Microsoft Entra admin center.

This post off-boarding scenario runs a scheduled workflow and accomplishes the following tasks:

1. Remove all licenses for user
2. Remove user from all Teams
3. Delete user account

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Before you begin

To complete this tutorial, you must satisfy the prerequisites listed in this section before starting the tutorial as they aren't included in the actual tutorial. As part of the prerequisites for completing this tutorial, you need an account that has licenses and Teams memberships that can be deleted during the tutorial. For more comprehensive instructions on how to complete these prerequisite steps, you can refer to the [Preparing user accounts for Lifecycle workflows tutorial](tutorial-prepare-user-accounts).

The scheduled leaver scenario can be broken down into the following sections:

- **Prerequisite:** Create a user account that represents an employee leaving your organization
- **Prerequisite:** Prepare the user account with licenses and Teams memberships
- Create the lifecycle management workflow
- Run the scheduled workflow after last day of work
- Verify that the workflow was successfully executed

## Create a workflow using scheduled leaver template

Use the following steps to create a scheduled leaver workflow that will automatically perform off-boarding tasks for employees after their last day of work with Lifecycle workflows using the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Select **ID Governance**.
3. Select **Lifecycle workflows**.
4. On the **Overview** page, select **New workflow**. [![Screenshot of selecting a new workflow.](media/tutorial-lifecycle-workflows/new-workflow.png)](media/tutorial-lifecycle-workflows/new-workflow.png#lightbox)
5. From the templates, select **Select** under **Post-offboarding of an employee**. [![Screenshot of selecting a leaver workflow.](media/tutorial-lifecycle-workflows/select-leaver-template.png)](media/tutorial-lifecycle-workflows/select-leaver-template.png#lightbox)
6. Next, you configure the basic information about the workflow. This information includes when the workflow triggers, known as **Days from event**. So in this case, the workflow will trigger seven days after the employee's leave date. On the post-offboarding of an employee screen, add the following settings and then select **Next: Configure Scope**. [![Screenshot of leaver template basics information for a workflow.](media/tutorial-lifecycle-workflows/leaver-basics.png)](media/tutorial-lifecycle-workflows/leaver-basics.png#lightbox)
7. Next, you configure the scope. The scope determines which users this workflow runs against. In this case, it is on all users in the Marketing department. On the configure scope screen, under **Rule** add the following, and then select **Next: Review tasks**. For a full list of supported user properties, see [Supported user properties and query parameters](/en-us/graph/api/resources/identitygovernance-rulebasedsubjectset?view=graph-rest-beta&amp;preserve-view=true#supported-user-properties-and-query-parameters)[![Screenshot of reviewing scope details for a leaver workflow.](media/tutorial-lifecycle-workflows/leaver-scope.png)](media/tutorial-lifecycle-workflows/leaver-scope.png#lightbox)
8. On the following page, you can inspect the tasks if desired but no additional configuration is needed. Select **Next: Select users** when you're finished. [![Screenshot of leaver workflow tasks.](media/tutorial-lifecycle-workflows/review-leaver-tasks.png)](media/tutorial-lifecycle-workflows/review-leaver-tasks.png#lightbox)
9. On the review screen, verify the information is correct and select **Create**. [![Screenshot of a leaver workflow being created.](media/tutorial-lifecycle-workflows/create-leaver-workflow.png)](media/tutorial-lifecycle-workflows/create-leaver-workflow.png#lightbox)

Note

Select **Create** with the **Enable schedule** box unchecked to run the workflow on-demand. You may enable this setting later after checking the tasks and workflow status.

## Run the workflow

Now that the workflow is created, it automatically runs every 3 hours. This means lifecycle workflows check every 3 hours for users in the associated execution condition, and executes the configured tasks for those users. However, for the tutorial, we would like to run it immediately. To run a workflow immediately, we can use the on-demand feature.

Note

Be aware that you currently cannot run a workflow on-demand if it is set to disabled. You need to set the workflow to enabled to use the on-demand feature.

To run a workflow on-demand, for users using the Microsoft Entra admin center, do the following steps:

1. On the workflow screen, select the specific workflow you want to run.
2. Select **Run on demand**.
3. On the **select users** tab, select **add users**.
4. Add a user.
5. Select **Run workflow**.

## Check tasks and workflow status

At any time, you can monitor the status of the workflows and the tasks. As a reminder, there are three different data pivots, users runs, and tasks that are currently available. You can learn more in the how-to guide [Check the status of a workflow](check-status-workflow). In the course of this section, we look at the status using the user focused reports.

1. To begin, select the **Workflow history** tab to view the user summary and associated workflow tasks and statuses. [![Screenshot of the workflow history summary.](media/tutorial-lifecycle-workflows/workflow-history-post-offboard.png)](media/tutorial-lifecycle-workflows/workflow-history-post-offboard.png#lightbox)
2. Once the **Workflow history** tab is selected, you land on the workflow history page as shown: [![Screenshot of the workflow history overview.](media/tutorial-lifecycle-workflows/user-summary-post-offboard.png)](media/tutorial-lifecycle-workflows/user-summary-post-offboard.png#lightbox)
3. Next, you can select **Total tasks** for the user Jane Smith to view the total number of tasks created and their statuses. In this example, there are three total tasks assigned to the user Jane Smith.[![Screenshot of workflow's total tasks.](media/tutorial-lifecycle-workflows/total-tasks-post-offboard.png)](media/tutorial-lifecycle-workflows/total-tasks-post-offboard.png#lightbox)
4. To add an extra layer of granularity, you can select **Failed tasks** for the user Wade Warren to view the total number of failed tasks assigned to the user Wade Warren. [![Screenshot of workflow failed tasks.](media/tutorial-lifecycle-workflows/failed-tasks-post-offboard.png)](media/tutorial-lifecycle-workflows/failed-tasks-post-offboard.png#lightbox)
5. Similarly, you can select **Unprocessed tasks** for the user Wade Warren to view the total number of unprocessed or canceled tasks assigned to the user Wade Warren. [![Screenshot of workflow unprocessed tasks.](media/tutorial-lifecycle-workflows/canceled-tasks-post-offboard.png)](media/tutorial-lifecycle-workflows/canceled-tasks-post-offboard.png#lightbox)

## Enable the workflow schedule

After running your workflow on-demand and checking that everything is working fine, you might want to enable the workflow schedule. To enable the workflow schedule, you select the **Enable Schedule** checkbox on the Properties page.

[![Screenshot of workflow enabled schedule.](media/tutorial-lifecycle-workflows/enable-schedule.png)](media/tutorial-lifecycle-workflows/enable-schedule.png#lightbox)