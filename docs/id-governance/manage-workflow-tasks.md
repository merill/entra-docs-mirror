---
layout: Conceptual
title: Manage workflow versions - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/manage-workflow-tasks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article guides a user on managing workflow versions with Lifecycle Workflows.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: template-how-to, sfi-image-nochange
locale: en-us
document_id: 851a0bb4-359d-2006-b9cb-ea482a5e491a
document_version_independent_id: 5e8163cc-4f0c-1bce-056f-8dc436858e98
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/manage-workflow-tasks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/manage-workflow-tasks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/manage-workflow-tasks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 6d4a0ad1-747e-3a8c-bdb4-ec143c5425e3
---

# Manage workflow versions - Microsoft Entra ID Governance | Microsoft Learn

Workflows created with Lifecycle Workflows are able to grow and change with the needs of your organization. Workflows exist as versions from creation. When you make changes to anything other than basic information, you create a new version of the workflow. For more information, see [Manage a workflow's properties](manage-workflow-properties).

Changing a workflow's tasks or execution conditions requires the creation of a new version of that workflow. Tasks within workflows can be added, reordered, and removed at will. Updating a workflow's tasks or execution conditions within the Microsoft Entra admin center triggers the creation of a new version of the workflow automatically. Making these updates in Microsoft Graph requires the new workflow version to be created manually.

## Edit the tasks of a workflow using the Microsoft Entra admin center

Tasks within workflows can be added, edited, reordered, and removed at will. To edit the tasks of a workflow using the Microsoft Entra admin center, you complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. Select the workflow that you want to edit the tasks of and on the left side of the screen, select **Tasks**.
4. You can add a task to the workflow by selecting the **Add task** button.

    [![Screenshot of adding a task to a workflow.](media/manage-workflow-tasks/manage-tasks.png)](media/manage-workflow-tasks/manage-tasks.png#lightbox)
5. You can enable and disable tasks as needed by using the **Enable** and **Disable** buttons.
6. You can reorder the order in which tasks are executed in the workflow by selecting the **Reorder** button. You can also remove a task from a workflow by using the **Remove** button.

    ![Screenshot of reordering tasks in a workflow.](media/manage-workflow-tasks/manage-tasks-reorder.png)
7. After making changes, select **save** to capture changes to the tasks.

## Edit the execution conditions of a workflow using the Microsoft Entra admin center

To edit the execution conditions of a workflow using the Microsoft Entra admin center, you do the following steps:

1. On the left menu of Lifecycle Workflows, select **Workflows**.
2. On the left side of the screen, select **Execution conditions**. [![Screenshot of the execution condition details of a workflow.](media/manage-workflow-tasks/execution-conditions-details.png)](media/manage-workflow-tasks/execution-conditions-details.png#lightbox)
3. On this screen, you're presented with **Trigger details**. You see a trigger type and attribute details. In the template you can edit the attribute details to define when a workflow runs.
4. Select the **Scope details** tab. [![Screenshot of the execution scope page of a workflow.](media/manage-workflow-tasks/execution-conditions-scope.png)](media/manage-workflow-tasks/execution-conditions-scope.png#lightbox)
5. On this screen you can define rules for who the workflow runs. If the trigger **Scope type** is set as Rule-Based, you can define the rule using expressions on user properties. For more information on supported user properties, see [supported queries on user properties](/en-us/graph/aad-advanced-queries#user-properties). If the trigger scope type is group-based, you're able to select which group is the scope of the workflow.
6. After making changes, select **save** to capture changes to the execution conditions.

## See versions of a workflow using the Microsoft Entra admin center

1. On the left menu of Lifecycle Workflows, select **Workflows**.
2. On this page, you see a list of all of your current workflows. Select the workflow that you want to see versions of.
3. On the left side of the screen, select **Versions**.

    [![Screenshot of versions of a workflow.](media/manage-workflow-tasks/manage-versions.png)](media/manage-workflow-tasks/manage-versions.png#lightbox)
4. On this page, you see a list of the workflow versions.

    [![Screenshot of managing version list of lifecycle workflows.](media/manage-workflow-tasks/manage-versions-list.png)](media/manage-workflow-tasks/manage-versions-list.png#lightbox)

## Create a new version of an existing workflow using Microsoft Graph

To create a new version of a workflow via API using Microsoft Graph, see: [workflow: createNewVersion](/en-us/graph/api/identitygovernance-workflow-createnewversion)

### List workflow versions using Microsoft Graph

To list workflow versions via API using Microsoft Graph, see: [List versions (of a lifecycle workflow)](/en-us/graph/api/identitygovernance-workflow-list-versions)