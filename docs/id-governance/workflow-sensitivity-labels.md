---
layout: Conceptual
title: Sensitivity Labels in Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/workflow-sensitivity-labels
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article describes sensitivity labels in Workflows, and how to see them during the task creation process.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: 03baab5c-0ca6-94a8-96b5-a029ad257e06
document_version_independent_id: 03baab5c-0ca6-94a8-96b5-a029ad257e06
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/workflow-sensitivity-labels.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/workflow-sensitivity-labels
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/workflow-sensitivity-labels.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ead09300-b7aa-2587-d8c6-f6c78c929e07
---

# Sensitivity Labels in Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn

Maintaining and classifying data within your environment is an important part in maintaining a secure environment. Sensitivity labels from Microsoft Purview Information Protection let you classify and protect your organization's data, while making sure that user productivity and their ability to collaborate isn't hindered. With sensitivity labels in Lifecycle Workflows, administrators are able to quickly view the sensitivity labels of groups and teams during workflow creation, and editing.

The following tasks support viewing sensitivity labels:

- [Add user to groups](lifecycle-workflow-tasks#add-user-to-groups)
- [Add user to teams](lifecycle-workflow-tasks#add-user-to-teams)
- [Remove user from selected groups](lifecycle-workflow-tasks#remove-user-from-selected-groups)
- [Remove user from selected teams](lifecycle-workflow-tasks#remove-user-from-selected-teams)

## License requirements

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Prerequisites

Along with Microsoft Entra licenses required for Lifecycle workflows, you must also have:

- [A created sensitivity label](/en-us/purview/create-sensitivity-labels?tabs=classic-label-scheme#create-and-configure-sensitivity-labels)
- [A sensitivity label applied to the group or team you want to use with a Lifecycle workflow](/en-us/purview/sensitivity-labels-teams-groups-sites#using-sensitivity-labels-for-microsoft-teams-microsoft-365-groups-and-sharepoint-sites)

## View assigned sensitivity labels during workflow creation

To view the sensitivity labels of groups and teams using Lifecycle workflows during workflow creation, do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Create a workflow**.
3. On the **Choose a workflow** page, select the workflow template that you want to use.
4. Add Basic information, Trigger type, and scope details for the workflow.
5. On the tasks page, add the task you want to use to view sensitivity labels with. Task availability is based on which template you selected to create your workflow. For more information on workflow templates, see: [Lifecycle Workflows templates and categories](lifecycle-workflow-templates).
6. After adding the group-related tasks to the workflow, select the task, and then select **select groups**. ![Screenshot of selecting group in workflows.](media/workflow-sensitivity-labels/select-groups-workflow.png)
7. On the list pane, you're able to see a list of groups or teams that can be selected, and their sensitivity labels. ![Screenshot of adding groups to workflow along with their sensitivity labels.](media/workflow-sensitivity-labels/add-group-sensitivity-label.png)
8. After adding the group or team to the task, select **Next** to move to the review screen, and **Create** to create the workflow.

## View assigned sensitivity labels on existing workflow tasks

Sensitivity labels of groups and teams used within existing tasks of a workflow can be viewed by doing the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. Select the workflow that has the task that you want to view.
4. On the workflow overview screen, select **Tasks**.
5. On the tasks screen, select the specific task related to sensitivity you want to view.
6. On the task overview screen, select the group or teams selection option.
7. On the list screen, you're able to see the group currently assigned to the task, a list of groups or teams that can be added to the task, and also their sensitivity labels. ![Screenshot of teams and sensitivity labels within a task for an existing workflow.](media/workflow-sensitivity-labels/sensitivity-label-existing-workflow.png)