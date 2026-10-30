---
layout: Conceptual
title: Privileged roles and permissions in Microsoft Entra ID (preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/privileged-roles-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Privileged roles and permissions in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2026-06-05T00:00:00.0000000Z
ms.custom: it-pro, sfi-ga-nochange, sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: eb28e967-b483-087e-6060-227289c817e1
document_version_independent_id: 8dc8c4dd-e937-cf14-d12a-f2718042f1a2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/privileged-roles-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/privileged-roles-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/privileged-roles-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 818f2a8b-6cb0-06ec-a948-1a8ecdfdb54e
---

# Privileged roles and permissions in Microsoft Entra ID (preview) - Microsoft Entra ID | Microsoft Learn

Important

The label for privileged roles and permissions is currently in PREVIEW. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Microsoft Entra ID has roles and permissions that are identified as privileged. These roles and permissions can be used to delegate management of directory resources to other users, modify credentials, authentication or authorization policies, or access restricted data. Privileged role assignments can lead to elevation of privilege if not used in a secure and intended manner. This article describes privileged roles and permissions and best practices for how to use.

## Which roles and permissions are privileged?

For a list of privileged roles and permissions, see [Microsoft Entra built-in roles](permissions-reference). You can also use the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API to identify roles, permissions, and role assignments that are identified as privileged.

# [Admin center](#tab/admin-center)
In the Microsoft Entra admin center, look for the **PRIVILEGED** label.

![Privileged label icon.](media/permissions-reference/privileged-label.png)

On the **Roles and administrators** page, privileged roles are identified in the **Privileged** column. The **Assignments** column lists the number of role assignments. You can also filter privileged roles.

[![Screenshot of the Microsoft Entra roles and administrators page that shows the Privileged and Assignments columns.](media/privileged-roles-permissions/privileged-roles-portal.png)](media/privileged-roles-permissions/privileged-roles-portal.png#lightbox)

When you view the permissions for a privileged role, you can see which permissions are privileged. If you view the permissions as a default user, you won't be able to see which permissions are privileged.

[![Screenshot of the Microsoft Entra roles and administrators page that shows the privileged permissions for a role.](media/privileged-roles-permissions/privileged-roles-permissions.png)](media/privileged-roles-permissions/privileged-roles-permissions.png#lightbox)

When you create a custom role, you can see which permissions are privileged and the custom role will be labeled as privileged.

[![Screenshot of the New custom role page that shows a custom role with privileged permissions.](media/privileged-roles-permissions/custom-role-privileged-permissions.png)](media/privileged-roles-permissions/custom-role-privileged-permissions.png#lightbox)

# [PowerShell](#tab/ms-powershell)
In Microsoft Graph PowerShell, check whether the `IsPrivileged` property is set to `True`.

To list privileged roles, use the [Get-MgBetaRoleManagementDirectoryRoleDefinition](/en-us/powershell/module/microsoft.graph.beta.identity.governance/get-mgbetarolemanagementdirectoryroledefinition) command.

```powershell
Get-MgBetaRoleManagementDirectoryRoleDefinition -Filter "isPrivileged eq true" | Format-List
```

```Output
AllowedPrincipalTypes   :
Description             : Can create and manage all aspects of app registrations and enterprise apps.
DisplayName             : Application Administrator
Id                      : 9b895d92-2cd3-44c7-9d02-a6ac2d5ea5c3
InheritsPermissionsFrom : {88d8e3e3-8f55-4a1e-953a-9b9898b8876b}
IsBuiltIn               : True
IsEnabled               : True
IsPrivileged            : True
ResourceScopes          : {/}
RolePermissions         : {Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphUnifiedRolePermission}
TemplateId              : 9b895d92-2cd3-44c7-9d02-a6ac2d5ea5c3
Version                 : 1
AdditionalProperties    : {[assignmentMode, allowed], [categories, identity], [richDescription, Users in this role can
                          add, manage, and configureenterprise applications, app registrations and manage on-premises
                          like app proxy.], [inheritsPermissionsFrom@odata.context, https://graph.microsoft.com/beta/$m
                          etadata#roleManagement/directory/roleDefinitions('9b895d92-2cd3-44c7-9d02-a6ac2d5ea5c3')/inhe
                          ritsPermissionsFrom]}

AllowedPrincipalTypes   :
Description             : Can reset passwords for non-administrators and Helpdesk Administrators.
DisplayName             : Helpdesk Administrator
Id                      : 729827e3-9c14-49f7-bb1b-9608f156bbb8
InheritsPermissionsFrom : {88d8e3e3-8f55-4a1e-953a-9b9898b8876b}
IsBuiltIn               : True
IsEnabled               : True
IsPrivileged            : True
ResourceScopes          : {/}
RolePermissions         : {Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphUnifiedRolePermission}
TemplateId              : 729827e3-9c14-49f7-bb1b-9608f156bbb8
Version                 : 1
AdditionalProperties    : {[assignmentMode, allowed], [categories, identity], [richDescription, Users with this role
                          can change passwords, invalidate refresh tokens, manage service requests, and monitor
                          service health. Invalidating a refresh token forces the user to sign in again. Helpdesk
                          administrators can reset passwords and invalidate refresh tokens of other users who are
                          non-administrators or assigned the following roles only:
                          * Directory Readers
                          * Guest Inviter
                          * Helpdesk Administrator
                          * Message Center Reader
                          * Password Administrator
                          * Reports Reader], [inheritsPermissionsFrom@odata.context, https://graph.microsoft.com/beta/$
                          metadata#roleManagement/directory/roleDefinitions('729827e3-9c14-49f7-bb1b-9608f156bbb8')/inh
                          eritsPermissionsFrom]}

...
```

To list privileged permissions, use the [Get-MgBetaRoleManagementDirectoryResourceNamespaceResourceAction](/en-us/powershell/module/microsoft.graph.beta.identity.governance/get-mgbetarolemanagementdirectoryresourcenamespaceresourceaction) command.

```powershell
Get-MgBetaRoleManagementDirectoryResourceNamespaceResourceAction -UnifiedRbacResourceNamespaceId "microsoft.directory" -Filter "isPrivileged eq true" | Format-List
```

```Output
ActionVerb                      : PATCH
AuthenticationContext           : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphAuthenticationContextClassReference
AuthenticationContextId         :
Description                     : Update all properties (including privileged properties) on single-directory applications
Id                              : microsoft.directory-applications.myOrganization-allProperties-update-patch
IsAuthenticationContextSettable :
IsPrivileged                    : True
Name                            : microsoft.directory/applications.myOrganization/allProperties/update
ResourceScope                   : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphUnifiedRbacResourceScope
ResourceScopeId                 :
AdditionalProperties            : {}

ActionVerb                      : PATCH
AuthenticationContext           : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphAuthenticationContextClassReference
AuthenticationContextId         :
Description                     : Update credentials on single-directory applications
Id                              : microsoft.directory-applications.myOrganization-credentials-update-patch
IsAuthenticationContextSettable :
IsPrivileged                    : True
Name                            : microsoft.directory/applications.myOrganization/credentials/update
ResourceScope                   : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphUnifiedRbacResourceScope
ResourceScopeId                 :
AdditionalProperties            : {}

...
```

To list privileged role assignments, use the [Get-MgBetaRoleManagementDirectoryRoleAssignment](/en-us/powershell/module/microsoft.graph.beta.identity.governance/get-mgbetarolemanagementdirectoryroleassignment) command.

```powershell
Get-MgBetaRoleManagementDirectoryRoleAssignment -ExpandProperty "roleDefinition" -Filter "roleDefinition/isPrivileged eq true" | Format-List
```

```Output
AppScope                : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphAppScope
AppScopeId              :
Condition               :
DirectoryScope          : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphDirectoryObject
DirectoryScopeId        : /
Id                      : <Id>
Principal               : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphDirectoryObject
PrincipalId             : <PrincipalId>
PrincipalOrganizationId : <PrincipalOrganizationId>
ResourceScope           : /
RoleDefinition          : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphUnifiedRoleDefinition
RoleDefinitionId        : 62e90394-69f5-4237-9190-012177145e10
AdditionalProperties    : {}

AppScope                : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphAppScope
AppScopeId              :
Condition               :
DirectoryScope          : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphDirectoryObject
DirectoryScopeId        : /
Id                      : <Id>
Principal               : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphDirectoryObject
PrincipalId             : <PrincipalId>
PrincipalOrganizationId : <PrincipalOrganizationId>
ResourceScope           : /
RoleDefinition          : Microsoft.Graph.Beta.PowerShell.Models.MicrosoftGraphUnifiedRoleDefinition
RoleDefinitionId        : 62e90394-69f5-4237-9190-012177145e10
AdditionalProperties    : {}

...
```

# [Graph API](#tab/ms-graph)
In the Microsoft Graph API, check whether the `isPrivileged` property is set to `true`.

To list privileged roles, use the [List roleDefinitions](/en-us/graph/api/rbacapplication-list-roledefinitions?view=graph-rest-beta&amp;preserve-view=true&amp;branch=pr-en-us-18827) API.

```http
GET https://graph.microsoft.com/beta/roleManagement/directory/roleDefinitions?$filter=isPrivileged eq true
```

**Response**

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#roleManagement/directory/roleDefinitions",
    "value": [
        {
            "id": "aaf43236-0c0d-4d5f-883a-6955382ac081",
            "description": "Can manage secrets for federation and encryption in the Identity Experience Framework (IEF).",
            "displayName": "B2C IEF Keyset Administrator",
            "isBuiltIn": true,
            "isEnabled": true,
            "isPrivileged": true,
            "resourceScopes": [
                "/"
            ],
            "templateId": "aaf43236-0c0d-4d5f-883a-6955382ac081",
            "version": "1",
            "rolePermissions": [
                {
                    "allowedResourceActions": [
                        "microsoft.directory/b2cTrustFrameworkKeySet/allProperties/allTasks"
                    ],
                    "condition": null
                }
            ],
            "inheritsPermissionsFrom@odata.context": "https://graph.microsoft.com/beta/$metadata#roleManagement/directory/roleDefinitions('aaf43236-0c0d-4d5f-883a-6955382ac081')/inheritsPermissionsFrom",
            "inheritsPermissionsFrom": [
                {
                    "id": "88d8e3e3-8f55-4a1e-953a-9b9898b8876b"
                }
            ]
        },
        {
            "id": "be2f45a1-457d-42af-a067-6ec1fa63bc45",
            "description": "Can configure identity providers for use in direct federation.",
            "displayName": "External Identity Provider Administrator",
            "isBuiltIn": true,
            "isEnabled": true,
            "isPrivileged": true,
            "resourceScopes": [
                "/"
            ],
            "templateId": "be2f45a1-457d-42af-a067-6ec1fa63bc45",
            "version": "1",
            "rolePermissions": [
                {
                    "allowedResourceActions": [
                        "microsoft.directory/domains/federation/update",
                        "microsoft.directory/identityProviders/allProperties/allTasks"
                    ],
                    "condition": null
                }
            ],
            "inheritsPermissionsFrom@odata.context": "https://graph.microsoft.com/beta/$metadata#roleManagement/directory/roleDefinitions('be2f45a1-457d-42af-a067-6ec1fa63bc45')/inheritsPermissionsFrom",
            "inheritsPermissionsFrom": [
                {
                    "id": "88d8e3e3-8f55-4a1e-953a-9b9898b8876b"
                }
            ]
        }
    ]
}
```

To list privileged permissions, use the [List resourceActions](/en-us/graph/api/unifiedrbacresourcenamespace-list-resourceactions?view=graph-rest-beta&amp;preserve-view=true&amp;branch=pr-en-us-18827) API.

```http
GET https://graph.microsoft.com/beta/roleManagement/directory/resourceNamespaces/microsoft.directory/resourceActions?$filter=isPrivileged eq true
```

**Response**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#roleManagement/directory/resourceNamespaces('microsoft.directory')/resourceActions",
    "value": [
        {
            "actionVerb": "PATCH",
            "description": "Update application credentials",
            "id": "microsoft.directory-applications-credentials-update-patch",
            "isPrivileged": true,
            "name": "microsoft.directory/applications/credentials/update",
            "resourceScopeId": null
        },
        {
            "actionVerb": null,
            "description": "Manage all aspects of authorization policy",
            "id": "microsoft.directory-authorizationPolicy-allProperties-allTasks",
            "isPrivileged": true,
            "name": "microsoft.directory/authorizationPolicy/allProperties/allTasks",
            "resourceScopeId": null
        }
    ]
}
```

To list privileged role assignments, use the [List unifiedRoleAssignments](/en-us/graph/api/rbacapplication-list-roleassignments?view=graph-rest-beta&amp;preserve-view=true&amp;branch=pr-en-us-18827) API.

```http
GET https://graph.microsoft.com/beta/roleManagement/directory/roleAssignments?$expand=roleDefinition&$filter=roleDefinition/isPrivileged eq true
```

**Response**

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#roleManagement/directory/roleAssignments(roleDefinition())",
    "value": [
        {
            "id": "{id}",
            "principalId": "{principalId}",
            "principalOrganizationId": "{principalOrganizationId}",
            "resourceScope": "/",
            "directoryScopeId": "/",
            "roleDefinitionId": "b1be1c3e-b65d-4f19-8427-f6fa0d97feb9",
            "roleDefinition": {
                "id": "b1be1c3e-b65d-4f19-8427-f6fa0d97feb9",
                "description": "Can manage Conditional Access capabilities.",
                "displayName": "Conditional Access Administrator",
                "isBuiltIn": true,
                "isEnabled": true,
                "isPrivileged": true,
                "resourceScopes": [
                    "/"
                ],
                "templateId": "b1be1c3e-b65d-4f19-8427-f6fa0d97feb9",
                "version": "1",
                "rolePermissions": [
                    {
                        "allowedResourceActions": [
                            "microsoft.directory/namedLocations/create",
                            "microsoft.directory/namedLocations/delete",
                            "microsoft.directory/namedLocations/standard/read",
                            "microsoft.directory/namedLocations/basic/update",
                            "microsoft.directory/conditionalAccessPolicies/create",
                            "microsoft.directory/conditionalAccessPolicies/delete",
                            "microsoft.directory/conditionalAccessPolicies/standard/read",
                            "microsoft.directory/conditionalAccessPolicies/owners/read",
                            "microsoft.directory/conditionalAccessPolicies/policyAppliedTo/read",
                            "microsoft.directory/conditionalAccessPolicies/basic/update",
                            "microsoft.directory/conditionalAccessPolicies/owners/update",
                            "microsoft.directory/conditionalAccessPolicies/tenantDefault/update"
                        ],
                        "condition": null
                    }
                ]
            }
        },
        {
            "id": "{id}",
            "principalId": "{principalId}",
            "principalOrganizationId": "{principalOrganizationId}",
            "resourceScope": "/",
            "directoryScopeId": "/",
            "roleDefinitionId": "c4e39bd9-1100-46d3-8c65-fb160da0071f",
            "roleDefinition": {
                "id": "c4e39bd9-1100-46d3-8c65-fb160da0071f",
                "description": "Can access to view, set and reset authentication method information for any non-admin user.",
                "displayName": "Authentication Administrator",
                "isBuiltIn": true,
                "isEnabled": true,
                "isPrivileged": true,
                "resourceScopes": [
                    "/"
                ],
                "templateId": "c4e39bd9-1100-46d3-8c65-fb160da0071f",
                "version": "1",
                "rolePermissions": [
                    {
                        "allowedResourceActions": [
                            "microsoft.directory/users/authenticationMethods/create",
                            "microsoft.directory/users/authenticationMethods/delete",
                            "microsoft.directory/users/authenticationMethods/standard/restrictedRead",
                            "microsoft.directory/users/authenticationMethods/basic/update",
                            "microsoft.directory/deletedItems.users/restore",
                            "microsoft.directory/users/delete",
                            "microsoft.directory/users/disable",
                            "microsoft.directory/users/enable",
                            "microsoft.directory/users/invalidateAllRefreshTokens",
                            "microsoft.directory/users/restore",
                            "microsoft.directory/users/basic/update",
                            "microsoft.directory/users/manager/update",
                            "microsoft.directory/users/password/update",
                            "microsoft.directory/users/userPrincipalName/update",
                            "microsoft.azure.serviceHealth/allEntities/allTasks",
                            "microsoft.azure.supportTickets/allEntities/allTasks",
                            "microsoft.office365.serviceHealth/allEntities/allTasks",
                            "microsoft.office365.supportTickets/allEntities/allTasks",
                            "microsoft.office365.webPortal/allEntities/standard/read"
                        ],
                        "condition": null
                    }
                ]
            }
        }
    ]
}
```

---

## Best practices for using privileged roles

Here are some best practices for using privileged roles.

- Apply principle of least privilege
- Use Privileged Identity Management to grant just-in-time access
- Turn on multi-factor authentication for all your administrator accounts
- Configure recurring access reviews to revoke unneeded permissions over time
- Limit the number of Global Administrators to less than 5
- Limit the number of privileged role assignments to less than 10

For more information, see [Best practices for Microsoft Entra roles](best-practices).

### Isolate privileged intermediaries as control plane assets

Any system that can manage or broker access to privileged roles is part of the control plane and must be protected at that level. Examples include privileged access management (PAM) solutions, jump hosts and session hosts, automation runbooks, and service principals or applications that hold highly privileged roles.

In the [Enterprise access model](/en-us/security/privileged-access-workstations/privileged-access-access-model), Tier 0 expands to become the control plane, which must be isolated from the management and data/workload planes so that control of higher planes can't be obtained from lower ones. If a lower-tier system can administer a control plane asset, an attacker who compromises that system can escalate privilege. Treat these intermediaries as control plane (Tier 0) assets and administer them only from equally trusted control plane systems.

## Privileged permissions versus protected actions

Privileged permissions and protected actions are security-related capabilities that have different purposes. Permissions that have the **PRIVILEGED** label help you identify permissions that can lead to elevation of privilege if not used in a secure and intended manner. Protected actions are role permissions that have been assigned Conditional Access policies for added security, such as requiring multi-factor authentication. Conditional Access requirements are enforced when a user performs the protected action. Protected actions are currently in Preview. For more information, see [What are protected actions in Microsoft Entra ID?](protected-actions-overview).

| Capability | Privileged permission | Protected action |
| --- | --- | --- |
| Identify permissions that should be used in a secure manner | ✅ |  |
| Require additional security to perform an action |  | ✅ |

## Terminology

To understand privileged roles and permissions in Microsoft Entra ID, it helps to know some of the following terminology.

| Term | Definition |
| --- | --- |
| action | An activity a security principal can perform on an object type. Sometimes referred to as an operation. |
| permission | A definition that specifies the activity a security principal can perform on an object type. A permission includes one or more actions. |
| privileged permission | In Microsoft Entra ID, permissions that can be used to delegate management of directory resources to other users, modify credentials, authentication or authorization policies, or access restricted data. |
| privileged role | A built-in or custom role that has one or more privileged permissions. |
| privileged role assignment | A role assignment that uses a privileged role. |
| elevation of privilege | When a security principal obtains more permissions than their assigned role initially provided by impersonating another role. |
| protected action | Permissions with Conditional Access applied for added security. |

## How to understand role permissions

The schema for permissions loosely follows the REST format of Microsoft Graph:

`<namespace>/<entity>/<propertySet>/<action>`

For example:

`microsoft.directory/applications/credentials/update`

| Permission element | Description |
| --- | --- |
| namespace | Product or service that exposes the task and is prepended with `microsoft`. For example, all tasks in Microsoft Entra ID use the `microsoft.directory` namespace. |
| entity | Logical feature or component exposed by the service in Microsoft Graph. For example, Microsoft Entra ID exposes User and Groups, OneNote exposes Notes, and Exchange exposes Mailboxes and Calendars. There is a special `allEntities` keyword for specifying all entities in a namespace. This is often used in roles that grant access to an entire product. |
| propertySet | Specific properties or aspects of the entity for which access is being granted. For example, `microsoft.directory/applications/authentication/read` grants the ability to read the reply URL, logout URL, and implicit flow property on the application object in Microsoft Entra ID.<br>- `allProperties` designates all properties of the entity, including privileged properties.<br>- `standard` designates common properties, but excludes privileged ones related to `read` action. For example, `microsoft.directory/user/standard/read` includes the ability to read standard properties like public phone number and email address, but not the private secondary phone number or email address used for multifactor authentication.<br>- `basic` designates common properties, but excludes privileged ones related to the `update` action. The set of properties that you can read may be different from what you can update. That’s why there are `standard` and `basic` keywords to reflect that. |
| action | Operation being granted, most typically create, read, update, or delete (CRUD). There is a special `allTasks` keyword for specifying all of the above abilities (create, read, update, and delete). |

## Compare authentication roles

The following table compares the capabilities of authentication-related roles.

| Role | Manage user's auth methods | Manage per-user MFA | Manage MFA settings | Manage auth method policy | Manage password protection policy | Update sensitive properties | Delete and restore users |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [Authentication Administrator](permissions-reference#authentication-administrator) | Yes for [some users](privileged-roles-permissions#who-can-perform-sensitive-actions) | No | No | No | No | Yes for [some users](privileged-roles-permissions#who-can-perform-sensitive-actions) | Yes for [some users](privileged-roles-permissions#who-can-perform-sensitive-actions) |
| [Privileged Authentication Administrator](permissions-reference#privileged-authentication-administrator) | Yes for all users | No | No | No | No | Yes for all users | Yes for all users |
| [Authentication Policy Administrator](permissions-reference#authentication-policy-administrator) | No | Yes | Yes | Yes | Yes | No | No |
| [User Administrator](permissions-reference#user-administrator) | No | No | No | No | No | Yes for [some users](privileged-roles-permissions#who-can-perform-sensitive-actions) | Yes for [some users](privileged-roles-permissions#who-can-perform-sensitive-actions) |

## Who can reset passwords

In the following table, the columns list the roles that can reset passwords and invalidate refresh tokens. The rows list the roles for which their password can be reset. For example, a Password Administrator can reset the password for Directory Readers, Guest Inviter, Password Administrator, and users with no administrator role. If a user is assigned any other role, the Password Administrator cannot reset their password.

The following table is for roles assigned at the scope of a tenant. For roles assigned at the scope of an administrative unit, [further restrictions apply](manage-roles-portal#roles-that-can-be-assigned-with-administrative-unit-scope).

| Role that password can be reset | Password Admin | Helpdesk Admin | Auth Admin | User Admin | Privileged Auth Admin | Global Admin |
| --- | --- | --- | --- | --- | --- | --- |
| Auth Admin |  |  | ✅ |  | ✅ | ✅ |
| Directory Readers | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Global Admin |  |  |  |  | ✅ | ✅\* |
| Groups Admin |  |  |  | ✅ | ✅ | ✅ |
| Guest Inviter | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Helpdesk Admin |  | ✅ |  | ✅ | ✅ | ✅ |
| Message Center Reader |  | ✅ | ✅ | ✅ | ✅ | ✅ |
| Password Admin | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Privileged Auth Admin |  |  |  |  | ✅ | ✅ |
| Privileged Role Admin |  |  |  |  | ✅ | ✅ |
| Reports Reader |  | ✅ | ✅ | ✅ | ✅ | ✅ |
| User(no admin role) | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| User(no admin role, but member or owner of a [role-assignable group](groups-concept)) |  |  |  |  | ✅ | ✅ |
| User with a role scoped to a [restricted management administrative unit](admin-units-restricted-management) |  |  |  |  | ✅ | ✅ |
| User Admin |  |  |  | ✅ | ✅ | ✅ |
| User Experience Success Manager |  | ✅ | ✅ | ✅ | ✅ | ✅ |
| Usage Summary Reports Reader |  | ✅ | ✅ | ✅ | ✅ | ✅ |
| All other built-in and custom roles |  |  |  |  | ✅ | ✅ |

Security Administrator, Security Operator, and Entra SOC Identity Responder are limited to non-administrative user accounts and can't perform actions on privileged accounts.

Important

The [Partner Tier2 Support](permissions-reference#partner-tier2-support) role can reset passwords and invalidate refresh tokens for all non-administrators and administrators (including Global Administrators). The [Partner Tier1 Support](permissions-reference#partner-tier1-support) role can reset passwords and invalidate refresh tokens for only non-administrators. These roles should not be used because they are deprecated.

The ability to reset a password includes the ability to update the following sensitive properties required for [self-service password reset](../authentication/concept-sspr-howitworks):

- businessPhones
- mobilePhone
- otherMails

## Who can perform sensitive actions

Some administrators can perform the following sensitive actions for some users. All users can read the sensitive properties.

| Sensitive action | Sensitive property name |
| --- | --- |
| Disable or enable users | `accountEnabled` |
| Update business phone | `businessPhones` |
| Update mobile phone | `mobilePhone` |
| Update on-premises immutable ID | `onPremisesImmutableId` |
| Update other emails | `otherMails` |
| Update password profile | `passwordProfile` |
| Update user principal name | `userPrincipalName` |
| Delete or restore users | Not applicable |

In the following table, the columns list the roles that can perform sensitive actions. The rows list the roles for which the sensitive action can be performed upon.

The following table is for roles assigned at the scope of a tenant. For roles assigned at the scope of an administrative unit, [further restrictions apply](manage-roles-portal#roles-that-can-be-assigned-with-administrative-unit-scope).

| Role that sensitive action can be performed upon | Auth Admin | User Admin | Privileged Auth Admin | Global Admin |
| --- | --- | --- | --- | --- |
| Auth Admin | ✅ |  | ✅ | ✅ |
| Directory Readers | ✅ | ✅ | ✅ | ✅ |
| Global Admin |  |  | ✅ | ✅ |
| Groups Admin |  | ✅ | ✅ | ✅ |
| Guest Inviter | ✅ | ✅ | ✅ | ✅ |
| Helpdesk Admin |  | ✅ | ✅ | ✅ |
| Message Center Reader | ✅ | ✅ | ✅ | ✅ |
| Password Admin | ✅ | ✅ | ✅ | ✅ |
| Privileged Auth Admin |  |  | ✅ | ✅ |
| Privileged Role Admin |  |  | ✅ | ✅ |
| Reports Reader | ✅ | ✅ | ✅ | ✅ |
| User(no admin role) | ✅ | ✅ | ✅ | ✅ |
| User(no admin role, but member or owner of a [role-assignable group](groups-concept)) |  |  | ✅ | ✅ |
| User with a role scoped to a [restricted management administrative unit](admin-units-restricted-management) |  |  | ✅ | ✅ |
| User Admin |  | ✅ | ✅ | ✅ |
| User Experience Success Manager | ✅ | ✅ | ✅ | ✅ |
| Usage Summary Reports Reader | ✅ | ✅ | ✅ | ✅ |
| All other built-in and custom roles |  |  | ✅ | ✅ |

Security Administrator, Security Operator, and Entra SOC Identity Responder are limited to non-administrative user accounts and can't perform actions on privileged accounts.