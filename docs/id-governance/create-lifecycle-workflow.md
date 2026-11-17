---
layout: Conceptual
title: Create a lifecycle workflow - Microsoft Entra ID - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/create-lifecycle-workflow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: rogulati
ms.author: rogulati
ms.service: entra-id-governance
manager: dougeby
description: Create a lifecycle workflow from a template, clone an existing workflow, or use Microsoft Graph. Configure a profile for identity verification templates.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-11-03T00:00:00.0000000Z
ms.custom: template-how-to, msecd-doc-authoring-1026
ai-usage: ai-assisted
locale: en-us
document_id: f6e4c9c4-5c16-4af0-8e0f-b0837bf1bdf8
document_version_independent_id: 66313ddc-ea8c-b721-e283-5f6887151367
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/create-lifecycle-workflow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/create-lifecycle-workflow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/create-lifecycle-workflow.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 415d94d0-e127-a520-a994-c74836b4d637
---

# Create a lifecycle workflow - Microsoft Entra ID - Microsoft Entra ID Governance | Microsoft Learn

Lifecycle workflows allow for tasks associated with the lifecycle process to be run automatically for users as they move through their lifecycle in your organization. Workflows consist of:

- **Tasks**: Actions taken when a workflow is triggered.
- **Execution conditions**: The who and when of a workflow. These conditions define which users this workflow should run against, and when (trigger) the workflow should run.

In the Microsoft Entra admin center, you can create and customize workflows for common scenarios by using built-in templates or by cloning an existing workflow. To build a workflow from scratch without using a template or an existing workflow, use Microsoft Graph.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

- An ID verification profile with purpose set to `all` or `onboarding`, if you use either identity-verification template (Preview). You can create a profile before you start or select **Create new verification profile** during workflow creation. For profile configuration, see [Create an ID verification profile](../verified-id/how-to-create-id-verification-profile).

## Create a lifecycle workflow by cloning an existing workflow in the Microsoft Entra admin center

You can use an existing workflow as the starting point for a new workflow. The clone option is available only in the Microsoft Entra admin center.

To start cloning from the workflow list:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. Select the workflow that you want to clone, and then select **Clone**.

    [![Screenshot of a selected workflow and the Clone option on the Lifecycle workflows page.](media/create-lifecycle-workflow/clone-workflow-list.png)](media/create-lifecycle-workflow/clone-workflow-list.png#lightbox)

You can also start cloning from the workflow creation experience:

1. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Create workflow**.
2. On the **Choose a workflow** page, find the **Clone an existing workflow** card, and then select **Browse workflows**.

    [![Screenshot of the Clone an existing workflow card on the Choose a workflow page.](media/create-lifecycle-workflow/clone-workflow-template-card.png)](media/create-lifecycle-workflow/clone-workflow-template-card.png#lightbox)
3. Select the workflow that you want to clone.

After you select a workflow to clone, the **Review + create** tab opens directly. Review the workflow settings, and then select **Create** to create the workflow without making changes.

To customize the workflow before you create it, select the other tabs and update the workflow details or configuration. When you're finished, return to the **Review + create** tab and select **Create**.

## Create a lifecycle workflow by using a template in the Microsoft Entra admin center

Use a built-in template as the starting point for a workflow, and customize it to meet your organization's needs. For available templates and their default settings, see [Lifecycle Workflows templates](lifecycle-workflow-templates).

To create a workflow based on a template:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Create a workflow**.
3. On the **Choose a workflow** page, select the workflow template that you want to use.

    For identity-verification onboarding, select **Pre-hire identity verification initiation (Preview)** or **New Hire employee onboarding with identity verification (Preview)**. See [Lifecycle Workflows templates](lifecycle-workflow-templates).

    [![Screenshot of the workflow template gallery, including the two identity-verification templates in preview.](media/create-lifecycle-workflow/templates-list.png)](media/create-lifecycle-workflow/templates-list.png#lightbox)
4. On the **Basics** tab, enter a unique display name, description, and [administrative scope](manage-delegate-workflow) for the workflow.

    If you selected either identity-verification template, also select **Trigger type** on this tab. When you're finished, select **Next**.

    ![Screenshot of basic information about a workflow template.](media/create-lifecycle-workflow/template-basics.png)
5. On the **Configure scope** tab, configure the execution conditions for the workflow. For other templates, also select the trigger type on this tab. For more information on what you can configure, see [Execution conditions](understanding-lifecycle-workflows#execution-conditions).
6. Under **Rule**, enter values for **Property**, **Operator**, and **Value**. The following screenshot gives an example of a rule being set up for a sales department. For a full list of user properties that lifecycle workflows support, see [Supported user properties and query parameters](/en-us/graph/api/resources/identitygovernance-rulebasedsubjectset?view=graph-rest-beta&amp;preserve-view=true#supported-user-properties-and-query-parameters).

    ![Screenshot of scope configuration options for a lifecycle workflow template.](media/create-lifecycle-workflow/template-scope.png)
7. To view your rule syntax, select the **View rule syntax** button. You can copy and paste multiple user property rules on the panel that appears. For more information on which properties you can include, see [User properties](/en-us/graph/aad-advanced-queries?tabs=http#user-properties). When you finish adding rules, select **Next**.

    ![Screenshot of workflow rule syntax.](media/create-lifecycle-workflow/template-syntax.png)
8. If you selected either identity-verification template, on the **Select identity verification profile** tab, select a profile from **Verified ID Profile**. If you need a new profile, select **Create new verification profile**. The profile's purpose must be set to `all` or `onboarding`. Select **Next: Review tasks**.

    For other templates, skip this step and continue to **Review tasks**.

    [![Screenshot of the identity verification profile selection tab, with the Verified ID Profile dropdown and Create new verification profile link.](media/create-lifecycle-workflow/select-identity-verification-profile.png)](media/create-lifecycle-workflow/select-identity-verification-profile.png#lightbox)
9. On the **Review tasks** tab, you can add a task to the template by selecting **Add task**. To enable an existing task on the list, select **Enable**. To disable a task, select **Disable**. To remove a task from the template, select **Remove**.

    For identity-verification tasks, select or change the profile on the workflow's **Select identity verification profile** tab, not in the task settings. For task settings and email requirements, see [Lifecycle workflow tasks](lifecycle-workflow-tasks).

    When you're finished with tasks for your workflow, select **Next: Review and create**.

    ![Screenshot of adding tasks to templates.](media/create-lifecycle-workflow/template-tasks.png)
10. On the **Review and create** tab, review the workflow's settings. Leave the scheduling checkbox cleared to test the workflow before automatic processing begins. Select it when you're ready to enable scheduled runs. Select **Create** to create the workflow.

    ![Screenshot of reviewing and creating a workflow.](media/create-lifecycle-workflow/template-review.png)

Important

In the Microsoft Entra admin center, a newly created workflow is enabled (`isEnabled` is `true`), but scheduling is disabled (`isSchedulingEnabled` is `false`) unless you select the scheduling checkbox. This lets you [run the workflow on-demand](on-demand-workflow) for a small audience before enabling scheduled processing. Disabling the workflow itself (`isEnabled` is `false`) prevents both scheduled and on-demand runs.

## Create a lifecycle workflow by using Microsoft Graph

To create a lifecycle workflow by using the Microsoft Graph API, see [Create workflow](/en-us/graph/api/identitygovernance-lifecycleworkflowscontainer-post-workflows).

For API creation, explicitly set `isEnabled` and `isSchedulingEnabled` for the intended run mode. The values you set control workflow execution and scheduling; don't assume the admin center's checkbox defaults apply to an API request.

The three Preview tasks used by the two identity-verification templates are available only in Microsoft Graph `/beta`, not `/v1.0`. To create a workflow that includes these tasks, see [Create workflow (beta)](/en-us/graph/api/identitygovernance-lifecycleworkflowscontainer-post-workflows?view=graph-rest-beta&amp;preserve-view=true). For task definitions and arguments, see [Lifecycle workflow tasks](lifecycle-workflow-tasks).

Note

Microsoft Graph beta APIs are subject to change. Use of these APIs in production applications isn't supported.