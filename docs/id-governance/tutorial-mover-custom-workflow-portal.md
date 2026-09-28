---
layout: Conceptual
title: Automate employee mover tasks when they change jobs using the Microsoft Entra admin center - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tutorial-mover-custom-workflow-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Tutorial for moving users that change jobs using Lifecycle workflows with the Microsoft Entra admin center.
ms.subservice: lifecycle-workflows
ms.topic: tutorial
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: template-tutorial, sfi-image-nochange
locale: en-us
document_id: 27ecbf54-d521-be0c-2e58-f8dbb5a4291f
document_version_independent_id: 27ecbf54-d521-be0c-2e58-f8dbb5a4291f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tutorial-mover-custom-workflow-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tutorial-mover-custom-workflow-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tutorial-mover-custom-workflow-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: ae69f52a-013b-e71a-b7d4-c95366c601b6
---

# Automate employee mover tasks when they change jobs using the Microsoft Entra admin center - Microsoft Entra ID Governance | Microsoft Learn

This tutorial provides a step-by-step guide on how to automate mover tasks with Lifecycle workflows using the Microsoft Entra admin center. The use case for this tutorial is an existing user being added to a new department.

This Mover scenario runs a scheduled workflow and accomplishes the following tasks:

1. Sends email to notify manager of user move
2. Removes all access package assignments for the user (scheduled removal defaulting to 15 days)
3. Adds user to groups

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Before you begin

To complete this tutorial, you must satisfy the prerequisites listed in this section before starting the tutorial as they won't be included in the actual tutorial. Two accounts are required, one account for the user becoming a full-time employee (job profile change), and another account that acts as its manager. The user account must have the following attributes set:

- An existing user you want to run the workflow on with a manager attribute set, and the manager account should have a mailbox to receive an email.
- A security group named *Sales* within your tenant.

Detailed breakdown of the relevant attributes:

| Attribute | Description | Set on |
| --- | --- | --- |
| mail | Used to notify manager of the new employee's temporary access pass | Both |
| manager | This attribute is used by the lifecycle workflow | Employee |
| department | Used to provide the scope for the workflow | Employee |

The mover scenario can be broken down into the following steps:

- **Prerequisite:** Create two user accounts, one to represent an employee and one to represent a manager
- **Prerequisite:** Create a group to add the user to
- **Prerequisite:** Edit the attributes required for this scenario in the admin center
- **Prerequisite:** Edit the attributes for this scenario using Microsoft Graph Explorer
- Create the workflow
- Trigger the workflow
- Verify the workflow was successfully executed

## Create a workflow using the mover template

Use the following steps to create a mover workflow for a user making a job change that is triggered by an attribute change.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Create workflow**.
3. From the templates, select **Employee job profile change**. ![Screenshot of selecting the employee job profile change template.](media/tutorial-mover-custom-workflow-portal/job-change-template.png)
4. Next, you configure the basic information about the workflow. This information includes a name, description, and [administrative scope](manage-delegate-workflow). You're also able to choose the **Trigger type** of the workflow, which in this case is the **Attribute changes** trigger. For **Trigger attribute** you're able to define what attribute being changed will trigger the workflow, which in this case is **department**. After the trigger is set, select **Configure scope**. ![Screenshot of setting attribute change membership trigger in template.](media/tutorial-mover-custom-workflow-portal/job-change-template-basics.png)
5. On the next screen you configure the scope. The scope determines which users this workflow runs against. In this case, it is on all users added to the Sales department. On the configure scope screen, under **Rule** add the following settings, and then select **Review tasks**. For a full list of supported user properties, see [Supported user properties and query parameters](/en-us/graph/api/resources/identitygovernance-rulebasedsubjectset?view=graph-rest-beta&amp;preserve-view=true#supported-user-properties-and-query-parameters). ![Screenshot of setting attribute change scope.](media/tutorial-mover-custom-workflow-portal/group-scope.png)
6. On the **Review tasks** screen, you're able to add, edit, or remove tasks. From the default tasks, remove **Remove user from selected groups**, **Remove user from Selected Teams**, and **Request user access package assignment** from the list and add **Add user to groups** from the add task screen. Keep the **Remove all access package assignments for user** task, which is included by default with scheduled removal set to 15 days. Edit the **Add user to groups** task so that the Sales group is selected. Once complete, select **Review + create**. ![Screenshot of job change template tasks.](media/tutorial-mover-custom-workflow-portal/job-change-template-tasks.png)
7. On the review screen, verify the information is correct, and choose to enable the schedule of the workflow. After reviewing, select **Create**. ![Screenshot of reviewing job change template.](media/tutorial-mover-custom-workflow-portal/job-change-template-review.png)

## Run the workflow

Now that the workflow is created, go to the user you want to run the workflow for, and add them to the Sales department. Within 30 minutes, the user appears in the scope of execution conditions for the workflow. Lifecycle workflows check every 3 hours for users in the associated execution condition, and execute the configured tasks for those users.

## Check workflow status and tasks

After setting the attribute for the user, you can check the status of the workflow, who meets its scope, and its tasks. As a reminder, there are three different data pivots: users, runs, and tasks that are currently available. You can learn more in the how-to guide [Check the status of a workflow](check-status-workflow). In this tutorial, you check the status using the user-focused reports.

1. On the workflow you created, select **Execution conditions** and navigate to the **Execution User Scope** section.
2. On the **Execution User Scope** page you're presented with users who currently meet the execution user scope to have the workflow run on them at its next execution time. ![Screenshot of execution user scope.](media/tutorial-mover-custom-workflow-portal/job-change-execution-scope.png)
3. After the workflow runs for the user, select the **Workflow history** tab to view the user summary and associated workflow tasks and statuses.
4. On the **Workflow history** tab you're presented with the workflow history page. ![Screenshot of the workflow history page.](media/tutorial-mover-custom-workflow-portal/job-change-history-page.png)
5. On this page, you're able to see a general summary, based on users, of total processed, successfully processed, failed to process, successful tasks, and failed tasks.
6. From the list of users processed you can also select a user, see which tasks ran for them, and if they ran successfully. If the task failed, you can see the reason. ![Screenshot of task status for a user.](media/tutorial-mover-custom-workflow-portal/job-change-task-status.png)