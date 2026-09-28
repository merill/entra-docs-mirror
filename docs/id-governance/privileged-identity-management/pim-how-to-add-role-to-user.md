---
layout: Conceptual
title: Assign Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-how-to-add-role-to-user
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to assign Microsoft Entra roles in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: subject-rbac-steps, sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: 5251782e-04ce-449d-8756-50baf40a17b5
document_version_independent_id: e7453008-05a8-4ff9-0406-b0ee278866ba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-how-to-add-role-to-user.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-how-to-add-role-to-user
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-how-to-add-role-to-user.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9e400368-9d7a-caaf-75d2-7b4b51f0f727
---

# Assign Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

With Microsoft Entra ID, a Global Administrator can make **permanent** Microsoft Entra admin role assignments. These role assignments can be created using the [Microsoft Entra admin center](../../identity/role-based-access-control/permissions-reference) or using [PowerShell commands](/en-us/powershell/module/azuread/#directory_roles).

The Microsoft Entra Privileged Identity Management (PIM) service also allows Privileged Role Administrators to make permanent admin role assignments. Additionally, Privileged Role Administrators can make users **eligible** for Microsoft Entra admin roles. An eligible administrator can activate the role when they need it, and then their permissions expire once they're done.

Privileged Identity Management supports both built-in and custom Microsoft Entra roles. For more information on Microsoft Entra custom roles, see [Role-based access control in Microsoft Entra ID](../../identity/role-based-access-control/custom-overview).

Note

When a role is assigned, the assignment:

- Can't be assigned for a duration of less than five minutes
- Can't be removed within five minutes of it being assigned

## Assign a role

Follow these steps to make a user eligible for a Microsoft Entra admin role.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Microsoft Entra roles**.
3. Select **Roles** to see the list of roles for Microsoft Entra permissions.

    ![Screenshot of the Roles page with the Add assignments action selected.](media/pim-how-to-add-role-to-user/roles-list.png)
4. Select **Add assignments** to open the **Add assignments** page.
5. Select **Select a role** to open the **Select a role** page.

    ![Screenshot showing the new assignment pane.](media/pim-how-to-add-role-to-user/select-role.png)
6. Select a role you want to assign, select a member you want to assign to the role, and then select **Next**.

    You can select users, groups, or agent identities. For a list of roles that you can assign to agent identities, see [Authorization in Microsoft Entra Agent ID](../../agent-id/authorization-agent-id).

    Note

    If you assign a Microsoft Entra built-in role to a guest user, the guest user will be elevated to have the same permissions as a member user. For information about member and guest user default permissions, see [What are the default user permissions in Microsoft Entra ID?](../../fundamentals/users-default-permissions)
7. In the **Assignment type** list on the **Membership settings** pane, select **Eligible** or **Active**.

    - **Eligible** assignments require the member of the role to perform an action to use the role. Actions might include performing a multifactor authentication (MFA) check, providing a business justification, or requesting approval from designated approvers.
    - **Active** assignments don't require the member to perform any action to use the role. Members assigned as active always have the privileges assigned to the role.
8. To specify a specific assignment duration, add a start and end date and time boxes. When finished, select **Assign** to create the new role assignment.

    - **Permanent** assignments have no expiration date. Use this option for permanent workers who frequently need the role permissions.
    - **Time-bound** assignments expire at the end of a specified period. Use this option with temporary or contract workers, for example, whose project end date and time are known.

    Note

    Active time-bound role assignment for the Global Administrator role isn't removed at expiration time if there are no other assigned active role assignments for Global Administrator present. In other words, if it’s last assigned active role assignment for Global Administrator role, it will remain. Similarly, eligible time-bound role assignment for Global Administrator role isn't removed at expiration time if there are no other assigned role assignments for Global Administrator role present, that is, if it’s the last Global Administrator role assignment. This is done to minimize the risk of administrators locking themselves out of the tenant by accident.

    ![Screenshot showing Memberships settings - date and time.](media/pim-how-to-add-role-to-user/start-and-end-dates.png)
9. After the role is assigned, an assignment status notification is displayed.

    ![Screenshot showing a new assignment notification.](media/pim-how-to-add-role-to-user/assignment-notification.png)

## Assign a role with restricted scope

For certain roles, the scope of the granted permissions can be restricted to a single admin unit, service principal, or application. This procedure is an example of assigning a role that has the scope of an administrative unit. For a list of roles that support scope via administrative unit, see [Assign roles with administrative unit scope](../../identity/role-based-access-control/manage-roles-portal). This feature is currently being rolled out to Microsoft Entra organizations.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins**.
3. Select the **User Administrator**.

    ![Screenshot showing the Add assignment command is available when you open a role in the portal.](media/pim-how-to-add-role-to-user/add-assignment.png)
4. Select **Add assignments**.

    ![Screenshot showing when a role supports scope, you can select a scope.](media/pim-how-to-add-role-to-user/add-scope.png)
5. On the **Add assignments** page, you can:

    - Select a user or group to be assigned to the role.
    - Select the role scope (in this case, administrative units).
    - Select an administrative unit for the scope.

If you try to assign a custom role that is compatible with administrative units, you aren't able to assign the role with administrative unit scope by starting from the **Roles & admins** page. To assign the custom role with administrative unit scope, you must first open the administrative unit and then assign the role. For more information, see [Assign roles with administrative unit scope](../../identity/role-based-access-control/manage-roles-portal). For information about creating administrative units, see [Create or delete administrative units](../../identity/role-based-access-control/admin-units-manage).

## Assign a role using Microsoft Graph API

For more information about Microsoft Graph APIs for PIM, see [Overview of role management through the privileged identity management (PIM) API](/en-us/graph/api/resources/privilegedidentitymanagementv3-overview).

For permissions required to use the PIM API, see [Understand the Privileged Identity Management APIs](pim-apis).

### Eligible with no end date

This example shows an HTTP request to create an eligible assignment with no end date. For details on the API commands including request samples in languages such as C# and JavaScript, see [Create roleEligibilityScheduleRequests](/en-us/graph/api/rbacapplication-post-roleeligibilityschedulerequests).

#### HTTP request

```HTTP
POST https://graph.microsoft.com/v1.0/roleManagement/directory/roleEligibilityScheduleRequests
Content-Type: application/json

{
    "action": "adminAssign",
    "justification": "Permanently assign the Global Reader to the auditor",
    "roleDefinitionId": "f2ef992c-3afb-46b9-b7cf-a126ee74c451",
    "directoryScopeId": "/",
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
    "scheduleInfo": {
        "startDateTime": "2022-04-10T00:00:00Z",
        "expiration": {
            "type": "noExpiration"
        }
    }
}
```

#### HTTP response

This example shows a response. The response object shown here might be shortened for readability.

```HTTP
HTTP/1.1 201 Created
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#roleManagement/directory/roleEligibilityScheduleRequests/$entity",
    "id": "42159c11-45a9-4631-97e4-b64abdd42c25",
    "status": "Provisioned",
    "createdDateTime": "2022-05-13T13:40:33.2364309Z",
    "completedDateTime": "2022-05-13T13:40:34.6270851Z",
    "approvalId": null,
    "customData": null,
    "action": "adminAssign",
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
    "roleDefinitionId": "f2ef992c-3afb-46b9-b7cf-a126ee74c451",
    "directoryScopeId": "/",
    "appScopeId": null,
    "isValidationOnly": false,
    "targetScheduleId": "42159c11-45a9-4631-97e4-b64abdd42c25",
    "justification": "Permanently assign the Global Reader to the auditor",
    "createdBy": {
        "application": null,
        "device": null,
        "user": {
            "displayName": null,
            "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee"
        }
    },
    "scheduleInfo": {
        "startDateTime": "2022-05-13T13:40:34.6270851Z",
        "recurrence": null,
        "expiration": {
            "type": "noExpiration",
            "endDateTime": null,
            "duration": null
        }
    },
    "ticketInfo": {
        "ticketNumber": null,
        "ticketSystem": null
    }
}
```

### Active and time-bound

The example shows an HTTP request to create a time-bound active assignment. For details on the API commands including request samples in languages such as C# and JavaScript, see [Create roleAssignmentScheduleRequests](/en-us/graph/api/rbacapplication-post-roleassignmentschedulerequests).

#### HTTP request

```HTTP
POST https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignmentScheduleRequests 

{
    "action": "adminAssign",
    "justification": "Assign the Exchange Recipient Administrator to the mail admin",
    "roleDefinitionId": "31392ffb-586c-42d1-9346-e59415a2cc4e",
    "directoryScopeId": "/",
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
    "scheduleInfo": {
        "startDateTime": "2022-04-10T00:00:00Z",
        "expiration": {
            "type": "afterDuration",
            "duration": "PT3H"
        }
    }
}
```

#### HTTP response

This example shows the response. The response object shown here might be shortened for readability.

```HTTP
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#roleManagement/directory/roleAssignmentScheduleRequests/$entity",
    "id": "ac643e37-e75c-4b42-960a-b0fc3fbdf4b3",
    "status": "Provisioned",
    "createdDateTime": "2022-05-13T14:01:48.0145711Z",
    "completedDateTime": "2022-05-13T14:01:49.8589701Z",
    "approvalId": null,
    "customData": null,
    "action": "adminAssign",
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
    "roleDefinitionId": "31392ffb-586c-42d1-9346-e59415a2cc4e",
    "directoryScopeId": "/",
    "appScopeId": null,
    "isValidationOnly": false,
    "targetScheduleId": "ac643e37-e75c-4b42-960a-b0fc3fbdf4b3",
    "justification": "Assign the Exchange Recipient Administrator to the mail admin",
    "createdBy": {
        "application": null,
        "device": null,
        "user": {
            "displayName": null,
            "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee"
        }
    },
    "scheduleInfo": {
        "startDateTime": "2022-05-13T14:01:49.8589701Z",
        "recurrence": null,
        "expiration": {
            "type": "afterDuration",
            "endDateTime": null,
            "duration": "PT3H"
        }
    },
    "ticketInfo": {
        "ticketNumber": null,
        "ticketSystem": null
    }
}
```

## Update or remove an existing role assignment

Follow these steps to update or remove an existing role assignment. You can't remove the last active role assignment for Global Administrators. Consider having an emergency access account with active permanent role assignment for Global Administrator role. For more information, see [emergency access accounts](../../identity/role-based-access-control/security-emergency-access). You can't remove the eligible role assignment for Global Administrators if there would be no assigned role assignments for the Global Administrator role left. This is done to minimize risks of administrators locking themselves out of the tenant inadvertently.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Microsoft Entra roles**.
3. Select **Roles** to see the list of roles for Microsoft Entra ID.
4. Select the role that you want to update or remove.
5. Find the role assignment on the **Eligible roles** or **Active roles** tabs.

    ![Screenshot showing how to update or remove role assignment.](media/pim-how-to-add-role-to-user/remove-update-assignments.png)
6. Select **Update** or **Remove** to update or remove the role assignment.

## Remove eligible assignment via Microsoft Graph API

This example shows an HTTP request to revoke an eligible assignment to a role from a principal. For details on the API commands including request samples in languages such as C# and JavaScript, see [Create roleEligibilityScheduleRequests](/en-us/graph/api/rbacapplication-post-roleeligibilityschedulerequests).

### Request

```HTTP
POST https://graph.microsoft.com/v1.0/roleManagement/directory/roleEligibilityScheduleRequests 

{ 
    "action": "AdminRemove", 
    "justification": "abcde", 
    "directoryScopeId": "/", 
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222", 
    "roleDefinitionId": "88d8e3e3-8f55-4a1e-953a-9b9898b8876b" 
} 
```

### Response

```HTTP
{ 
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#roleManagement/directory/roleEligibilityScheduleRequests/$entity", 
    "id": "fc7bb2ca-b505-4ca7-ad2a-576d152633de", 
    "status": "Revoked", 
    "createdDateTime": "2021-07-15T20:23:23.85453Z", 
    "completedDateTime": null, 
    "approvalId": null, 
    "customData": null, 
    "action": "AdminRemove", 
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222", 
    "roleDefinitionId": "88d8e3e3-8f55-4a1e-953a-9b9898b8876b", 
    "directoryScopeId": "/", 
    "appScopeId": null, 
    "isValidationOnly": false, 
    "targetScheduleId": null, 
    "justification": "test", 
    "scheduleInfo": null, 
    "createdBy": { 
        "application": null, 
        "device": null, 
        "user": { 
            "displayName": null, 
            "id": "5d851eeb-b593-4d43-a78d-c8bd2f5144d2" 
        } 
    }, 
    "ticketInfo": { 
        "ticketNumber": null, 
        "ticketSystem": null 
    } 
} 
```