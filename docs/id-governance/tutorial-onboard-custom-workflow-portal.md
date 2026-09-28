---
layout: Conceptual
title: Automate employee onboarding tasks before their first day of work with the Microsoft Entra admin center - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tutorial-onboard-custom-workflow-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Tutorial for onboarding users to an organization using Lifecycle workflows with the Microsoft Entra admin center.
ms.subservice: lifecycle-workflows
ms.topic: tutorial
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: krbain
ms.custom: template-tutorial, sfi-image-nochange
locale: en-us
document_id: 3ad524f4-0406-9dd0-bfc4-32506a2080f8
document_version_independent_id: 66cf5abb-dab4-9d78-c8aa-3417ff2ad211
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tutorial-onboard-custom-workflow-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tutorial-onboard-custom-workflow-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tutorial-onboard-custom-workflow-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
2PlusCloud:
- Azure
- M365
- Power
__autotagging_hash:
- 246706C453D5C5C94C3011718E71B1BF3A9473A8C2C358EF6F1975B2DD2686EF
platformId: 52f9f0d2-f603-1bdc-90a9-74f17a9fbf01
---

# Automate employee onboarding tasks before their first day of work with the Microsoft Entra admin center - Microsoft Entra ID Governance | Microsoft Learn

This tutorial provides a step-by-step guide on how to automate prehire tasks with Lifecycle workflows using the Microsoft Entra admin center.

This prehire scenario generates a temporary access pass for the new employee and sends it via email to the user's new manager.

[![Screenshot of the lifecycle workflow scenario.](media/tutorial-lifecycle-workflows/arch-2.png)](media/tutorial-lifecycle-workflows/arch-2.png#lightbox)

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Before you begin

To complete this tutorial, you must satisfy the prerequisites listed in this section before starting the tutorial as they aren't included in the actual tutorial. Two accounts are required for this tutorial, one account for the new hire and another account that acts as the manager of the new hire. The new hire account must have the following attributes set:

- employeeHireDate must be set to today
- Department must be set to sales
- Manager attribute must be set, and the manager account should have a mailbox to receive an email

For more comprehensive instructions on how to complete these prerequisite steps, you can refer to the [Preparing user accounts for Lifecycle workflows tutorial](tutorial-prepare-user-accounts). The [TAP policy](../identity/authentication/howto-authentication-temporary-access-pass#enable-the-temporary-access-pass-policy) must also be enabled to run this tutorial.

Detailed breakdown of the relevant attributes:

| Attribute | Description | Set on |
| --- | --- | --- |
| mail | Used to notify manager of the new employee's temporary access pass | Both |
| manager | This attribute is used by the lifecycle workflow | Employee |
| employeeHireDate | Used to trigger the workflow | Employee |
| department | Used to provide the scope for the workflow | Employee |

The pre-hire scenario can be broken down into the following sections:

- **Prerequisite:** Create two user accounts, one to represent an employee and one to represent a manager
- **Prerequisite:** Editing the attributes required for this scenario in the admin center
- **Prerequisite:** Edit the attributes for this scenario using Microsoft Graph Explorer
- **Prerequisite:** Enabling and using Temporary Access Pass (TAP)
- Creating the lifecycle management workflow
- Triggering the workflow
- Verifying the workflow was successfully executed

## Create a workflow using the prehire template

Use the following steps to create a pre-hire workflow that generates a TAP and sends it via email to the user's manager using the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Select **ID Governance**.
3. Select **Lifecycle workflows**.
4. On the **Overview** page, select **New workflow**. [![Screenshot of selecting a new workflow.](media/tutorial-lifecycle-workflows/new-workflow.png)](media/tutorial-lifecycle-workflows/new-workflow.png#lightbox)
5. From the templates, select **select** under **Onboard pre-hire employee**. [![Screenshot of selecting workflow template.](media/tutorial-lifecycle-workflows/select-template.png)](media/tutorial-lifecycle-workflows/select-template.png#lightbox)
6. Next, you configure the basic information about the workflow that includes when the workflow triggers, known as **Days from event**. In this case, the workflow triggers two days before the employee's hire date. On the onboard pre-hire employee screen, add the following settings and then select **Next: Configure Scope**.

    [![Screenshot of selecting a configuration scope.](media/tutorial-lifecycle-workflows/configure-scope.png)](media/tutorial-lifecycle-workflows/configure-scope.png#lightbox)
7. Next, you configure the scope. The scope determines which users this workflow runs against. In this case, it is on all users in the Sales department. On the configure scope screen, under **Rule**, add the following settings and select **Next: Review tasks**. For a full list of supported user properties, see [Supported user properties and query parameters](/en-us/graph/api/resources/identitygovernance-rulebasedsubjectset?view=graph-rest-beta&amp;preserve-view=true#supported-user-properties-and-query-parameters).

    [![Screenshot of selecting review tasks.](media/tutorial-lifecycle-workflows/review-tasks.png)](media/tutorial-lifecycle-workflows/review-tasks.png#lightbox)
8. On the following page, you can inspect the task if desired but no additional configuration is needed. Select **Next: Review + Create** when you're finished. [![Screenshot of reviewing an on-board workflow.](media/tutorial-lifecycle-workflows/onboard-review-create.png)](media/tutorial-lifecycle-workflows/onboard-review-create.png#lightbox)
9. On the review screen, verify the information is correct and select **Create**. [![Screenshot of creating an onboard workflow.](media/tutorial-lifecycle-workflows/onboard-create.png)](media/tutorial-lifecycle-workflows/onboard-create.png#lightbox)

## Run the workflow

Now that the workflow is created, it automatically runs every 3 hours. This means lifecycle workflows check every 3 hours for users in the associated execution condition, and execute the configured tasks for those users. However, for this tutorial, you run it immediately. To run a workflow immediately, you can use the on-demand feature.

Note

Be aware that you currently cannot run a workflow on-demand if it is set to disabled. You need to set the workflow to enabled to use the on-demand feature.

To run a workflow on-demand for users using the Microsoft Entra admin center, complete the following steps:

1. On the workflow screen, select the specific workflow you want to run.
2. Select **Run on demand**.
3. On the **select users** tab, select **Add users**.
4. Add a user.
5. Select **Run workflow**.

## Check tasks and workflow status

At any time, you can monitor the status of the workflows and the tasks. As a reminder, there are three different data pivots: users, runs, and tasks that are currently available. You can learn more in the how-to guide [Check the status of a workflow](check-status-workflow). In this tutorial, you check the status using the user-focused reports.

1. To begin, select the **Workflow history** tab to view the user summary and associated workflow tasks and statuses.[![Screenshot of workflow History status.](media/tutorial-lifecycle-workflows/workflow-history.png)](media/tutorial-lifecycle-workflows/workflow-history.png#lightbox)
2. Once the **Workflow history** tab is selected, you land on the workflow history page as shown: [![Screenshot of workflow history overview](media/tutorial-lifecycle-workflows/user-summary.png)](media/tutorial-lifecycle-workflows/user-summary.png#lightbox)
3. Next, you can select **Total tasks** for the user Jane Smith to view the total number of tasks created and their statuses. In this example, there are three total tasks assigned to the user Jane Smith.[![Screenshot of workflow total task summary.](media/tutorial-lifecycle-workflows/total-tasks.png)](media/tutorial-lifecycle-workflows/total-tasks.png#lightbox)
4. To add an extra layer of granularity, you can select **Failed tasks** for the user Jeff Smith to view the total number of failed tasks assigned to the user Jeff Smith. [![Screenshot of workflow failed tasks.](media/tutorial-lifecycle-workflows/failed-tasks.png)](media/tutorial-lifecycle-workflows/failed-tasks.png#lightbox)
5. Similarly, you can select **Unprocessed tasks** for the user Jeff Smith to view the total number of unprocessed or canceled tasks assigned to the user Jeff Smith. [![Screenshot of workflow unprocessed tasks summary.](media/tutorial-lifecycle-workflows/canceled-tasks.png)](media/tutorial-lifecycle-workflows/canceled-tasks.png#lightbox)

## Enable the workflow schedule

After running your workflow on-demand and checking that everything is working fine, you might want to enable the workflow schedule. To enable the workflow schedule, you select the **Enable Schedule** checkbox on the Properties page.

[![Screenshot of enabling workflow schedule.](media/tutorial-lifecycle-workflows/enable-schedule.png)](media/tutorial-lifecycle-workflows/enable-schedule.png#lightbox)