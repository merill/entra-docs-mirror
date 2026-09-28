---
layout: Conceptual
title: Remove Microsoft Entra role assignments - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/groups-remove-assignment
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Remove role assignments in Microsoft Entra ID using the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API.
ms.topic: how-to
ms.date: 2025-05-25T00:00:00.0000000Z
ms.reviewer: vincesm
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done
locale: en-us
document_id: cbf87d17-008b-2bd4-434c-fffed196b455
document_version_independent_id: 53b2c900-d874-a75d-88da-0889846f9c16
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/groups-remove-assignment.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/groups-remove-assignment
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/groups-remove-assignment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 386ea5f9-1929-03c6-2f92-cca3ef3b5968
---

# Remove Microsoft Entra role assignments - Microsoft Entra ID | Microsoft Learn

This article describes how to remove Microsoft Entra role assignments using the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API.

You can remove both direct and indirect role assignments for a user. If a user is assigned a role by a group membership, remove the user from the group to remove the role assignment. For more information, see [Use Microsoft Entra groups to manage role assignments](groups-concept).

## Microsoft Entra roles in PIM

If you have a Microsoft Entra ID P2 license and [Privileged Identity Management (PIM)](../../id-governance/privileged-identity-management/pim-configure), you have additional capabilities for role assignments. For information about removing Microsoft Entra role assignments in PIM, see these articles:

| Method | Information |
| --- | --- |
| Microsoft Entra admin center | [Update or remove an existing role assignment in PIM](../../id-governance/privileged-identity-management/pim-how-to-add-role-to-user#update-or-remove-an-existing-role-assignment) |
| Microsoft Graph PowerShell | [Remove an eligible assignment](/en-us/powershell/microsoftgraph/tutorial-pim#step-6-admin-removes-an-eligible-assignment) |
| Microsoft Graph API | [Manage Microsoft Entra role assignments using PIM APIs](/en-us/graph/api/resources/privilegedidentitymanagementv3-overview)[Remove eligible assignment via Microsoft Graph API](../../id-governance/privileged-identity-management/pim-how-to-add-role-to-user#remove-eligible-assignment-via-microsoft-graph-api) |

## Prerequisites

- Microsoft Entra ID P1 or P2 license
- Privileged Role Administrator
- [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) module when using PowerShell
- Admin consent when using Graph explorer for Microsoft Graph API

For more information, see [Prerequisites to use PowerShell or Graph Explorer](prerequisites).

## Remove Microsoft Entra role assignments

# [Admin center](#tab/admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins**.
3. Select a role name to open the role.
4. Add a check mark next to the users or groups from which you want to remove the role assignment.
5. Select **Remove assignment**.

    If your experience is different than the following screenshot, you might have Microsoft Entra ID P2 and PIM. For more information, see [Update or remove an existing role assignment in PIM](../../id-governance/privileged-identity-management/pim-how-to-add-role-to-user#update-or-remove-an-existing-role-assignment).

    [![Screenshot of Assignments page to remove a role assignment.](media/groups-remove-assignment/remove-assignment.png)](media/groups-remove-assignment/remove-assignment.png#lightbox)
6. When asked to confirm your action, select **Yes**.

# [PowerShell](#tab/ms-powershell)
Use the [Get-MgRoleManagementDirectoryRoleAssignment](/en-us/powershell/module/microsoft.graph.identity.governance/get-mgrolemanagementdirectoryroleassignment) command to list the role assignment ID you want to remove. For examples, see [List Microsoft Entra role assignments](view-assignments?tabs=ms-powershell).

With the role assignment ID, use the [Remove-MgRoleManagementDirectoryRoleAssignment](/en-us/powershell/module/microsoft.graph.identity.governance/remove-mgrolemanagementdirectoryroleassignment) command to remove the role assignment.

```powershell
Remove-MgRoleManagementDirectoryRoleAssignment -UnifiedRoleAssignmentId $roleAssignment.Id
```

# [Graph API](#tab/ms-graph)
Use the [List unifiedRoleAssignments](/en-us/graph/api/rbacapplication-list-roleassignments) API to list the role assignment ID you want to remove. For examples, see [List Microsoft Entra role assignments](view-assignments?tabs=ms-graph).

With the role assignment ID, use the [Delete unifiedRoleAssignment](/en-us/graph/api/unifiedroleassignment-delete) API to remove the role assignment.

### Remove a role assignment for a user

```http
DELETE https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments/lAPpYvVpN0KRkAEhdxReEJC2sEqbR_9Hr48lds9SGHI-1
```

Response

```http
HTTP/1.1 204 No Content
```

### Remove a role assignment that no longer exists

```http
DELETE https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments/lAPpYvVpN0KRkAEhdxReEJC2sEqbR_9Hr48lds9SGHI-1
```

Response

```http
HTTP/1.1 404 Not Found
```

### Remove a Global Administrator role assignment for the current user

```http
DELETE https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments/lAPpYvVpN0KRkAEhdxReEJC2sEqbR_9Hr48lds9SGHI-1
```

Response

```http
HTTP/1.1 400 Bad Request
{
    "odata.error":
    {
        "code":"Request_BadRequest",
        "message":
        {
            "lang":"en",
            "value":"Removing self from Global Administrator built-in role is not allowed"},
            "values":null
        }
    }
}
```

You are prevented from removing your own Global Administrator role assignment to avoid a scenario where a tenant has zero Global Administrators. Removing other roles assigned to yourself is allowed.

---