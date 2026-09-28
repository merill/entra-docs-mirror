---
layout: Conceptual
title: Create custom roles to manage enterprise apps in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/custom-enterprise-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Create and assign custom Microsoft Entra roles for enterprise apps access in Microsoft Entra ID
ms.topic: how-to
ms.date: 2025-01-03T00:00:00.0000000Z
ms.reviewer: vincesm
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
locale: en-us
document_id: e3228b41-a76b-9e5a-e4ee-d39d6a004612
document_version_independent_id: f83fa9fe-ee0b-5916-78a8-2b4f4cd93526
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/custom-enterprise-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/custom-enterprise-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/custom-enterprise-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0fe2d47d-4483-ac87-3650-053f430ff3b4
---

# Create custom roles to manage enterprise apps in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article explains how to create a custom role with permissions to manage enterprise app assignments for users and groups in Microsoft Entra ID. For the elements of roles assignments and the meaning of terms such as subtype, permission, and property set, see the [custom roles overview](custom-overview).

## Prerequisites

- Microsoft Entra ID P1 or P2 license
- Privileged Role Administrator
- [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) module when using PowerShell
- Admin consent when using Graph explorer for Microsoft Graph API

For more information, see [Prerequisites to use PowerShell or Graph Explorer](prerequisites).

## Enterprise app role permissions

There are two enterprise app permissions discussed in this article. All examples use the update permission.

- To read the user and group assignments at scope, grant the `microsoft.directory/servicePrincipals/appRoleAssignedTo/read` permission
- To manage the user and group assignments at scope, grant the `microsoft.directory/servicePrincipals/appRoleAssignedTo/update` permission

Granting the update permission results in the assignee being able to manage assignments of users and groups to enterprise apps. The scope of user and/or group assignments can be granted for a single application or granted for all applications. If granted at an organization-wide level, the assignee can manage assignments for all applications. If made at an application level, the assignee can manage assignments for only the specified application.

Granting the update permission is done in two steps:

1. Create a custom role with permission `microsoft.directory/servicePrincipals/appRoleAssignedTo/update`
2. Grant users or groups permissions to manage user and group assignments to enterprise apps. This is when you can set the scope to the organization-wide level or to a single application.

# [Admin center](#tab/admin-center)
### Create a new custom role

In the Microsoft Entra Admin Center, you can create and manage custom roles to control access and permissions for enterprise apps.

Note

Custom roles are created and managed at an organization-wide level and are available only from the organization's Overview page.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins**.
3. Select **New custom role**.

    [![Screenshot of Roles and administrators page in Microsoft Entra admin center.](../../media/common/entra-roles-admins.png)](../../media/common/entra-roles-admins.png#lightbox)
4. On the **Basics** tab, provide "Manage user and group assignments" for the name of the role and "Grant permissions to manage user and group assignments" for the role description, then select **Next**.

    [![Screenshot of Basics tab to provide a name and description for the custom role.](media/custom-enterprise-apps/role-name-and-description.png)](media/custom-enterprise-apps/role-name-and-description.png#lightbox)
5. On the **Permissions** tab, enter "microsoft.directory/servicePrincipals/appRoleAssignedTo/update" in the search box, select the checkboxes next to the desired permissions, then select **Next**.

    [![Screenshot of Permissions tab to add the permissions to the custom role.](media/custom-enterprise-apps/role-custom-permissions.png)](media/custom-enterprise-apps/role-custom-permissions.png#lightbox)
6. On the **Review + create** tab, review the permissions and select **Create**.

    [![Screenshot of Review + create tab to create the custom role.](media/custom-enterprise-apps/role-custom-create.png)](media/custom-enterprise-apps/role-custom-create.png#lightbox)

### Assign the role to a user using the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins**.
3. Select the **Manage user and group assignments** role.

    [![Screenshot of Roles and administrators page to search for the custom role.](media/custom-enterprise-apps/select-custom-role.png)](media/custom-enterprise-apps/select-custom-role.png#lightbox)
4. Select **Add assignment**, select the desired user, and then click **Select** to add role assignment to the user.

    [![Screenshot of Add assignment page to assign the custom role to a user.](media/custom-enterprise-apps/assign-user-to-role.png)](media/custom-enterprise-apps/assign-user-to-role.png#lightbox)

#### Assignment tips

- To grant permissions to assignees to manage users and group access for all enterprise apps organization-wide, start from the organization-wide **Roles and Administrators** list on the Microsoft Entra ID **Overview** page for your organization.
- To grant permissions to assignees to manage users and group access for a specific enterprise app, go to that app in Microsoft Entra ID and open in the **Roles and Administrators** list for that app. Select the new custom role and complete the user or group assignment. The assignees can manage users and group access only for the specific app.
- To test your custom role assignment, sign in as the assignee and open an application’s **Users and groups** page to verify that the **Add user** option is enabled.

    [![Screenshot of Users and groups page to verify the user permissions.](media/custom-enterprise-apps/verify-user-permissions.png)](media/custom-enterprise-apps/verify-user-permissions.png#lightbox)

# [PowerShell](#tab/ms-powershell)
For more detail, see [Create a custom role in Microsoft Entra ID](custom-create) and [Assign Microsoft Entra roles](manage-roles-portal).

### Create a custom role

Create a new role using the following PowerShell script:

```PowerShell
# Basic role information
$description = "Can manage user and group assignments for Applications"
$displayName = "Manage user and group assignments"
$templateId = (New-Guid).Guid

# Set of permissions to grant
$allowedResourceAction = @("microsoft.directory/servicePrincipals/appRoleAssignedTo/update")
$rolePermission = @{'allowedResourceActions'= $allowedResourceAction}
$rolePermissions = $rolePermission

# Create new custom admin role
$customRole = New-MgRoleManagementDirectoryRoleDefinition -Description $description `
   -DisplayName $displayName -RolePermissions $rolePermissions -TemplateId $templateId -IsEnabled
```

### Assign the custom role

Assign the role using this PowerShell script.

```powershell
# Get the user and role definition you want to link
$user =  Get-MgUser -Filter "userPrincipalName eq 'chandra@example.com'"
$roleDefinition = Get-MgRoleManagementDirectoryRoleDefinition -Filter "displayName eq 'Manage user and group assignments'"

# Get app registration and construct scope for assignment.
$appRegistration = Get-MgApplication -Filter "displayName eq 'My Filter Photos'"
$directoryScope = '/' + $appRegistration.Id

# Create a scoped role assignment
$roleAssignment = New-MgRoleManagementDirectoryRoleAssignment -DirectoryScopeId $directoryScope `
   -PrincipalId $user.Id -RoleDefinitionId $roleDefinition.Id
```

# [Graph API](#tab/ms-graph)
Use the [Create unifiedRoleDefinition](/en-us/graph/api/rbacapplication-post-roledefinitions) API to create a custom role. For more information, see [Create a custom role in Microsoft Entra ID](custom-create) and [Assign Microsoft Entra roles](manage-roles-portal).

```http
POST https://graph.microsoft.com/v1.0/roleManagement/directory/roleDefinitions

{
    "description": "Can manage user and group assignments for Applications.",
    "displayName": "Manage user and group assignments",
    "isEnabled": true,
    "rolePermissions":
    [
        {
            "allowedResourceActions":
            [
                "microsoft.directory/servicePrincipals/appRoleAssignedTo/update"
            ]
        }
    ],
    "templateId": "<PROVIDE NEW GUID HERE>",
    "version": "1"
}
```

### Assign the custom role using the Microsoft Graph API

Use the [Create unifiedRoleAssignment](/en-us/graph/api/rbacapplication-post-roleassignments) API to assign the custom role. The role assignment combines a security principal ID (which can be a user or service principal), a role definition ID, and a Microsoft Entra resource scope. For more information on the elements of a role assignment, see the [custom roles overview](custom-overview)

```http
POST https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments

{
    "@odata.type": "#microsoft.graph.unifiedRoleAssignment",
    "principalId": "<PROVIDE OBJECTID OF USER TO ASSIGN HERE>",
    "roleDefinitionId": "<PROVIDE OBJECTID OF ROLE DEFINITION HERE>",
    "directoryScopeId": "/"
}
```

---