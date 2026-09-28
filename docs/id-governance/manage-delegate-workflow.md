---
layout: Conceptual
title: Delegated Workflow Management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/manage-delegate-workflow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article informs a user about delegating management of workflows using Lifecycle workflows.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: 736aabd6-9f3c-d883-aa1e-d4437c538f1c
document_version_independent_id: 736aabd6-9f3c-d883-aa1e-d4437c538f1c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/manage-delegate-workflow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/manage-delegate-workflow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/manage-delegate-workflow.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 416a3f8e-7671-d18a-6c73-01e89c799da0
---

# Delegated Workflow Management - Microsoft Entra ID Governance | Microsoft Learn

Workflows by default, unless specified during creation, are managed by users with either the Lifecycle Workflows, or Global, administrator roles. As workflows grow and change to meet the needs of members of your organization, so does the need to limit who can manage them. With delegated workflow management, you can scope management of workflows using [Administrative Units](../identity/role-based-access-control/administrative-units). When scoped, specific admins are only granted access to manage specific workflows. Scoping allows for greater security within your environment by following Microsoft's least privileged access guidelines by only giving access to specifically what's needed.

The following table shows the differences between the Lifecycle Workflows Administrator role, and the scoped workflow administrator role in terms of Lifecycle workflow capabilities:

| Capability | Lifecycle Workflows Administrator | Workflow Administrator |
| --- | --- | --- |
| [Create Workflow](create-lifecycle-workflow) | Yes | No |
| [Edit Workflow](manage-workflow-properties) | Yes | Yes (only assigned workflows) |
| [Custom Task Extensions](trigger-custom-task) | Yes | No |
| [Delete Workflow](delete-lifecycle-workflow#delete-a-workflow-by-using-the-microsoft-entra-admin-center) | Yes | Yes (only assigned workflows) |
| [Restore Workflow](delete-lifecycle-workflow#view-deleted-workflows-in-the-microsoft-entra-admin-center) | Yes | Yes (only assigned workflows) |
| [View workflow history](lifecycle-workflow-history) | Yes | Yes (only assigned workflows) |
| [Run Workflow on-demand](on-demand-workflow) | Yes | Yes (only assigned workflows) |
| [Scope Workflows](manage-delegate-workflow#edit-the-administrative-scopes-of-an-existing-workflow-using-the-microsoft-entra-admin-center) | Yes | No |

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals). You must also have at least one administrative unit within your tenant. For steps on creating an administrative unit, see [Create an administrative unit](../identity/role-based-access-control/admin-units-manage#create-an-administrative-unit).

## Assign Lifecycle Workflows Administrator role to administrative unit

To delegate workflow management using administrative scopes, you must first assign the Lifecycle Workflows administrator role to the administrative unit. To do so, you'd follow these steps:

Tip

While the following steps walk you through setting the role for a specific user, you can set the role to a group within the administrative unit to delegate management within a scope to multiple users.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. On the users page, select the user you want to assign the admin scope to.
4. From the user overview page, select **Assigned roles**.
5. On the assigned roles page, select **Add assignments**.
6. On the add assignments page select the following:**Select role**: Lifecycle Workflows Administrator**Scope type**: Administrative unit ![Screenshot of adding administrative unit.](media/manage-delegate-workflow/add-administrative-unit.png)
7. On the **Selected scope** pane, select the administrative unit where your workflow will be scoped to, and select **Next**.
8. On the **Setting** tab, you can set the assignment as either **Eligible** or **Active**.

    Note

    Assignment must be active to run for users in the administrative unit.
9. Select **Save**.

## Add administrative scopes to a new workflow

To add an administrative scope to a new workflow, set the administrative scope during workflow creation by doing the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Create a workflow**.
3. On the **Choose a workflow** page, select the workflow template that you want to use.
4. On the **Basics** tab, enter a unique display name, description, and administrative scope for the workflow, and then select **Next**. ![Screenshot of setting admin scope of a new workflow.](media/manage-delegate-workflow/create-admin-scope.png)
5. Finish setting the execution conditions, tasks, and create the workflow.

Note

You can assign up to five administrative scopes per workflow.

## Edit the administrative scopes of an existing workflow using the Microsoft Entra admin center

With the role set for admins over the administrative unit, you must edit the workflow to be assigned within the scope of that administrative unit. To edit the properties of a workflow to be in an administrative unit's scope using the Microsoft Entra admin center, you do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. On the list of workflows page, select the workflow that you want to edit the administrative scopes of.
4. On the workflow overview page, select **Administration Scope**.

    Tip

    You can also select the **Administration scope** card on the overview page to get to the administration scope page.
5. On the administration scope page, select **Assign Administration scope**.
6. From the administration scope pane, you can see the list of all administrative units in your tenant.
7. Select the administrative unit(s) you want to scope the workflow to.
8. Select **Save**.

## Assign Lifecycle Workflows Administrator role to administrative unit programmatically

To assign Lifecycle workflow admins to an administrative unit scope via API, you must have the following information:

- Lifecycle Workflow admin role ID: 59d46f88-662b-457b-bceb-5c3809e5908f
- User ID for the user you want to assign the scope to
- ID of the administrative unit you want to assign

With this information, you can make the following API call:

POST `https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments`

```
{
    "@odata.type": "#microsoft.graph.unifiedRoleAssignment",
    "principalId": "<Object ID of user>",
    "roleDefinitionId": "59d46f88-662b-457b-bceb-5c3809e5908f",
    "directoryScopeId": "/administrativeUnits/<Object ID of administrative unit>"
}
```

## View the administrative scopes of a workflow using the Microsoft Entra admin center

When managing workflows, it's important to see what administrative scopes they fall under. This allows you to quickly see who can manage each specific workflow. To see the administrative scopes of a workflow, do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. On the workflow list screen, you can see the number of scopes assigned to the workflow under the **Administration scope assigned** column.
4. Select the number in the column to see the list of scopes assigned to that workflow.

## Remove the administrative scopes of a workflow using the Microsoft Entra admin center

Administration scopes can be removed from a workflow at any time. To remove an administrative unit scope from a workflow, do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. On the list of workflows page, select the workflow that you want to remove an administrative scope from.
4. On the workflow overview page, select **Properties**.
5. Under properties, select **Administrative Scope**.
6. From the administrative scope pane, you can see the list of all administrative scopes of the workflow.
7. Select the administration scope you want to remove the workflow from.
8. Select **Save**.

## Edit the administrative scopes of a workflow using Microsoft Graph

To edit the administrative scopes of a workflow via API using Microsoft Graph, see: [Update workflow](/en-us/graph/api/identitygovernance-workflow-createnewversion).

## View the administrative scopes of a workflow using Microsoft Graph

To view the administrative scopes of a workflow via API using Microsoft Graph, see: [Get workflow](/en-us/graph/api/identitygovernance-workflow-get).

## Remove the administrative scopes of a workflow using Microsoft Graph

To remove the administrative scopes of a workflow via API using Microsoft Graph, see: [Update workflow](/en-us/graph/api/identitygovernance-workflow-createnewversion).