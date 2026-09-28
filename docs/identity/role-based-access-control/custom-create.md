---
layout: Conceptual
title: Create a custom role in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/custom-create
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Learn how to create a custom role to manage access to Microsoft Entra resources using the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API
ms.reviewer: vincesm
ms.date: 2026-06-27T00:00:00.0000000Z
ms.topic: how-to
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done
locale: en-us
document_id: 649bef7e-a492-d5b1-183a-be12c8994a51
document_version_independent_id: d79544a5-4b92-185e-0bcc-83660ecee475
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/custom-create.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/custom-create
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/custom-create.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 9c70ae72-d64c-0f12-7939-c0944bbef2f7
---

# Create a custom role in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes how to create a custom role to manage access to Microsoft Entra resources using the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API. If you want to instead create a custom role to manage access to Azure resources, see [Create or update Azure custom roles using the Azure portal](/en-us/azure/role-based-access-control/custom-roles-portal).

For the basics of custom roles, see the [custom roles overview](custom-overview). The role can be assigned either at the directory-level scope or an app registration resource scope only. For information about the maximum number of custom roles that can be created in a Microsoft Entra organization, see [Microsoft Entra service limits and restrictions](../users/directory-service-limits-restrictions).

Custom roles can only include permissions that are enabled for custom use. The available categories are [app registrations](custom-available-permissions), [enterprise applications](custom-enterprise-app-permissions), [consent](custom-consent-permissions), [devices](custom-device-permissions), [users](custom-user-permissions), and [groups](custom-group-permissions).

## Prerequisites

- Microsoft Entra ID P1 or P2 license
- Privileged Role Administrator
- [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) module when using PowerShell
- Admin consent when using Graph explorer for Microsoft Graph API

For more information, see [Prerequisites to use PowerShell or Graph Explorer](prerequisites).

# [Admin center](#tab/admin-center)
### Create a custom role

These steps describe how to create a custom role in the Microsoft Entra admin center to manage app registrations.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins**.
3. Select **New custom role**.

    [![Screenshot of Roles and administrators page in Microsoft Entra admin center.](../../media/common/entra-roles-admins.png)](../../media/common/entra-roles-admins.png#lightbox)
4. On the **Basics** tab, provide a name and description for the role.

    You can clone the baseline permissions from a custom role but you can't clone a built-in role.

    [![Screenshot of Basics tab to provide a name and description for a custom role.](media/custom-create/basics-tab.png)](media/custom-create/basics-tab.png#lightbox)
5. On the **Permissions** tab, select the permissions necessary to manage basic properties and credential properties of app registrations. For a detailed description of each permission, see [Application registration subtypes and permissions in Microsoft Entra ID](custom-available-permissions).

    1. First, enter "credentials" in the search bar and select the `microsoft.directory/applications/credentials/update` permission.

        [![Screenshot of Permissions tab to select the permissions for a custom role.](media/custom-create/permissions-tab.png)](media/custom-create/permissions-tab.png#lightbox)
    2. Next, enter "basic" in the search bar, select the `microsoft.directory/applications/basic/update` permission, and then click **Next**.
6. On the **Review + create** tab, review the permissions and select **Create**.

    Your custom role will show up in the list of available roles to assign.

# [PowerShell](#tab/ms-powershell)
### Sign in

Use the [Connect-MgGraph](/en-us/powershell/module/microsoft.graph.authentication/connect-mggraph) command to sign in to your tenant.

```PowerShell
Connect-MgGraph -Scopes "RoleManagement.ReadWrite.Directory"
```

### Create a custom role

Create a new role using the following PowerShell script:

```PowerShell
# Basic role information
$displayName = "Application Support Administrator"
$description = "Can manage basic aspects of application registrations."
$templateId = (New-Guid).Guid
      
# Set of permissions to grant
$rolePermissions = @{
    "allowedResourceActions" = @(
        "microsoft.directory/applications/basic/update",
        "microsoft.directory/applications/credentials/update"
    )
}
      
# Create new custom admin role
$customAdmin = New-MgRoleManagementDirectoryRoleDefinition -RolePermissions $rolePermissions `
    -DisplayName $displayName -Description $description -TemplateId $templateId -IsEnabled:$true
```

### Update a custom role

```powershell
# Update role definition
# This works for any writable property on role definition. You can replace display name with other
# valid properties.
Update-MgRoleManagementDirectoryRoleDefinition -UnifiedRoleDefinitionId c4e39bd9-1100-46d3-8c65-fb160da0071f `
   -DisplayName "Updated DisplayName"
```

### Delete a custom role

```powershell
# Delete role definition
Remove-MgRoleManagementDirectoryRoleDefinition -UnifiedRoleDefinitionId c4e39bd9-1100-46d3-8c65-fb160da0071f
```

# [Graph API](#tab/ms-graph)
### Create a custom role

Follow these steps:

1. Use the [Create unifiedRoleDefinition](/en-us/graph/api/rbacapplication-post-roledefinitions) API to create a custom role.

    ```HTTP
    POST https://graph.microsoft.com/v1.0/roleManagement/directory/roleDefinitions
    ```

    Body

    ```HTTP
    {
        "description": "Can manage basic aspects of application registrations.",
        "displayName": "Application Support Administrator",
        "isEnabled": true,
        "templateId": "<GUID>",
        "rolePermissions": [
            {
                "allowedResourceActions": [
                    "microsoft.directory/applications/basic/update",
                    "microsoft.directory/applications/credentials/update"
                ]
            }
        ]
    }
    ```

    Note

    The `"templateId": "GUID"` is an optional parameter that's sent in the body depending on the requirement. If you have a requirement to create multiple different custom roles with common parameters, it's best to create a template and define a `templateId` value. You can generate a `templateId` value beforehand by using the PowerShell cmdlet `(New-Guid).Guid`.
2. Use the [Create unifiedRoleAssignment](/en-us/graph/api/rbacapplication-post-roleassignments) API to assign the custom role.

    ```http
    POST https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignments
    ```

    Body

    ```http
    {
    "principalId":"<GUID OF USER>",
    "roleDefinitionId":"<GUID OF ROLE DEFINITION>",
    "directoryScopeId":"/<GUID OF APPLICATION REGISTRATION>"
    }
    ```

---