---
layout: Conceptual
title: Activate Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-how-to-activate-role
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: tamimsangrar
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to activate eligible Microsoft Entra roles with Privileged Identity Management (PIM) to perform administrative tasks when needed.
ms.reviewer: ilyal
ms.date: 2026-11-17T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom:
- sfi-ga-nochange
- sfi-image-nochange
- msecd-doc-authoring-1032
zone_pivot_groups: pim-entra-role-activation-methods
locale: en-us
document_id: 43125fc1-f1fb-fa8c-69a6-7866a1b3a1fe
document_version_independent_id: 174dbe2c-7469-a63a-ffd6-757272ce5c50
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-how-to-activate-role.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-how-to-activate-role
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-how-to-activate-role.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: caccf3ec-47aa-0504-9acb-caa9bf5a1d9f
---

# Activate Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn

Microsoft Entra Privileged Identity Management (PIM) simplifies how enterprises manage privileged access to resources in Microsoft Entra ID and other Microsoft online services like Microsoft 365 or Microsoft Intune.

If you have an *eligible* administrative role assignment, *activate* it when you need to perform privileged actions. For example, a user who manages Exchange Online might be eligible for Exchange Online Administrator rather than have permanent Global Administrator access.

Choose the method you will use to activate your Microsoft Entra role assignment.

Important

When a role is activated, Microsoft Entra PIM temporarily adds active assignment for the role. Microsoft Entra PIM creates active assignment (assigns user to a role) within seconds. When deactivation (manual or through activation time expiration) happens, Microsoft Entra PIM removes the active assignment within seconds as well.

Application may provide access based on the role the user has. In some situations, application access may not immediately reflect the fact that user got role assigned or removed. If application previously cached the fact that user does not have a role – when user tries to access application again, access may not be provided. Similarly, if application previously cached the fact that user has a role – when role is deactivated, user may still get access. Specific situation depends on the application’s architecture. For some applications, signing out and signing back in may help get access added or removed.

Important

If you activate an administrative role while signed in to Microsoft Teams on a mobile device, Teams sends a notification saying "Open Teams to continue receiving notifications for *&lt;email address&gt;*", or "*&lt;email address&gt;* needs to sign in to see notifications". Open Teams to continue receiving notifications.

::: zone pivot="entra-admin-center"

## Activate a role in the Microsoft Entra admin center

When you need to assume a Microsoft Entra role, you can request activation by opening **My roles** in Privileged Identity Management.

Note

You can use the Azure mobile app on iOS or Android to activate eligible Microsoft Entra and Azure resource role assignments, request renewals, and check pending requests. See [Activate PIM roles using the Azure mobile app](pim-how-to-activate-role?pivots=azure-mobile-app#activate-pim-roles-using-the-azure-mobile-app).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a user who has an eligible role assignment.
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **My roles**. For information about how to add the Privileged Identity Management tile to your dashboard, see [Start using Privileged Identity Management](pim-getting-started).
3. Select **Microsoft Entra roles** to see a list of your eligible Microsoft Entra roles.

    ![Screenshot of the My roles page showing roles you can activate.](media/pim-how-to-activate-role/my-roles.png)
4. In the **Microsoft Entra roles** list, find the role you want to activate.

    ![Screenshot of the Microsoft Entra roles list showing eligible roles.](media/pim-how-to-activate-role/activate-link.png)
5. Select **Activate** to open the Activate pane.

    ![Screenshot of Microsoft Entra role activation details showing duration and scope.](media/pim-how-to-activate-role/activate-page.png)
6. Select **Additional verification required** and follow the instructions to provide security verification. You are required to authenticate only once per session.

    ![Screenshot of the security verification screen for role activation.](media/pim-resource-roles-activate-your-roles/resources-mfa-enter-code.png)
7. After multifactor authentication, select **Activate before proceeding**.

    ![Screenshot of the identity verification prompt before role activation.](media/pim-how-to-activate-role/activate-role-mfa-banner.png)
8. If you want to specify a reduced scope, select **Scope** to open the filter pane. On the filter pane, you can specify the Microsoft Entra resources that you need access to. It's a best practice to request access to the fewest resources that you need.
9. If necessary, specify a custom activation start time. The Microsoft Entra role would be activated after the selected time.
10. In the **Reason** box, enter the reason for the activation request.
11. Select **Activate**.

    If the [role requires approval](pim-approval-workflow) to activate, a notification appears in the upper right corner of your browser informing you the request is pending approval.

    ![Screenshot of the notification that a role activation request is pending approval.](media/pim-resource-roles-activate-your-roles/resources-my-roles-activate-notification.png)

## View the status of activation requests

You can view the status of your pending requests to activate.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **My requests**.
3. When you select **My requests** you see a list of your Microsoft Entra role and Azure resource role requests.

    [![Screenshot of My requests - Microsoft Entra ID page showing your pending requests](media/pim-how-to-activate-role/my-requests-page.png)](media/pim-how-to-activate-role/my-requests-page.png#lightbox)
4. Scroll to the right to view the **Request Status** column.

## Cancel a pending request in the Microsoft Entra admin center

If you don't require activation of a role that requires approval, you can cancel a pending request at any time.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **My requests**.
3. For the role that you want to cancel, select the **Cancel** link.

    When you select Cancel, the request is canceled. To activate the role again, you have to submit a new request for activation.

    ![Screenshot of the My requests list with the Cancel action highlighted.](media/pim-resource-roles-activate-your-roles/resources-my-requests-cancel.png)

::: zone-end

::: zone pivot="my-access"

## Activate a Microsoft Entra role in My Access portal (Preview)

Use [**Roles**](https://aka.ms/pim/roles) under **My Access** in the [My Access portal](../my-access-portal-overview) to activate an eligible Microsoft Entra role assignment.

Microsoft Entra role assignment activation through the My Access portal is in preview. You activate an existing eligible role assignment to obtain temporary role access for your signed-in identity.

1. Sign in to the [My Access portal](https://myaccess.microsoft.com) in the tenant where you have an eligible role assignment.
2. Under **My Access**, select [**Roles**](https://aka.ms/pim/roles), and then select **Entra roles**.
3. Find and select the eligible Microsoft Entra role assignment that you need for your task.

    [![Screenshot of My Access Microsoft Entra roles showing an eligible role assignment and its Activate action.](media/pim-how-to-activate-role/my-access-entra-roles.png)](media/pim-how-to-activate-role/my-access-entra-roles.png#lightbox)
4. Review the activation details and complete the activation requirements shown for your role assignment.
5. Select **Activate** to submit your activation request. If approval is required, wait for approval before using the role.

## View and cancel a pending request in My Access

If you no longer need a pending role assignment activation, cancel the request in the My Access portal.

1. Under **My Access**, select [**Roles**](https://aka.ms/pim/roles), and then select **Entra roles**.
2. In the **Assignment status** dropdown, select **Pending**.
3. Find the request you no longer need, and select **Cancel**.

::: zone-end

::: zone pivot="api"

## Activate a role using Microsoft Graph API

Use Microsoft Graph to list your eligible role assignments and submit a role activation request. The examples show a request that lists eligibility and an activation request with justification, schedule, and ticket information. For API permissions and resource details, see [Overview of role management through the privileged identity management (PIM) API](/en-us/graph/api/resources/privilegedidentitymanagementv3-overview).

### Get all eligible roles that you can activate

The following request lists your eligible role assignments. It doesn't return eligible role assignments obtained through group membership.

#### HTTP request

```HTTP
GET https://graph.microsoft.com/v1.0/roleManagement/directory/roleEligibilityScheduleRequests/filterByCurrentUser(on='principal')  
```

#### HTTP response

The sample response shows one role assignment. The response can include multiple eligible role assignments.

```HTTP
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#Collection(unifiedRoleEligibilityScheduleRequest)",
    "value": [
        {
            "@odata.type": "#microsoft.graph.unifiedRoleEligibilityScheduleRequest",
            "id": "50d34326-f243-4540-8bb5-2af6692aafd0",
            "status": "Provisioned",
            "createdDateTime": "2022-04-12T18:26:08.843Z",
            "completedDateTime": "2022-04-12T18:26:08.89Z",
            "approvalId": null,
            "customData": null,
            "action": "adminAssign",
            "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
            "roleDefinitionId": "8424c6f0-a189-499e-bbd0-26c1753c96d4",
            "directoryScopeId": "/",
            "appScopeId": null,
            "isValidationOnly": false,
            "targetScheduleId": "50d34326-f243-4540-8bb5-2af6692aafd0",
            "justification": "Assign Attribute Assignment Admin eligibility to myself",
            "createdBy": {
                "application": null,
                "device": null,
                "user": {
                    "displayName": null,
                    "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee"
                }
            },
            "scheduleInfo": {
                "startDateTime": "2022-04-12T18:26:08.8911834Z",
                "recurrence": null,
                "expiration": {
                    "type": "afterDateTime",
                    "endDateTime": "2024-04-10T00:00:00Z",
                    "duration": null
                }
            },
            "ticketInfo": {
                "ticketNumber": null,
                "ticketSystem": null
            }
        }
    ]
}
```

### Self-activate a role eligibility with justification

Submit a role activation request for an existing eligible role assignment. The sample includes a justification, activation schedule, and ticket information.

#### HTTP request

```HTTP
POST https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignmentScheduleRequests 

{
    "action": "selfActivate",
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
    "roleDefinitionId": "8424c6f0-a189-499e-bbd0-26c1753c96d4",
    "directoryScopeId": "/",
    "justification": "I need access to the Attribute Administrator role to manage attributes to be assigned to restricted AUs",
    "scheduleInfo": {
        "startDateTime": "2022-04-14T00:00:00.000Z",
        "expiration": {
            "type": "AfterDuration",
            "duration": "PT5H"
        }
    },
    "ticketInfo": {
        "ticketNumber": "CONTOSO:Normal-67890",
        "ticketSystem": "MS Project"
    }
}
```

#### HTTP response

```HTTP
HTTP/1.1 201 Created
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#roleManagement/directory/roleAssignmentScheduleRequests/$entity",
    "id": "911bab8a-6912-4de2-9dc0-2648ede7dd6d",
    "status": "Granted",
    "createdDateTime": "2022-04-13T08:52:32.6485851Z",
    "completedDateTime": "2022-04-14T00:00:00Z",
    "approvalId": null,
    "customData": null,
    "action": "selfActivate",
    "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
    "roleDefinitionId": "8424c6f0-a189-499e-bbd0-26c1753c96d4",
    "directoryScopeId": "/",
    "appScopeId": null,
    "isValidationOnly": false,
    "targetScheduleId": "911bab8a-6912-4de2-9dc0-2648ede7dd6d",
    "justification": "I need access to the Attribute Administrator role to manage attributes to be assigned to restricted AUs",
    "createdBy": {
        "application": null,
        "device": null,
        "user": {
            "displayName": null,
            "id": "071cc716-8147-4397-a5ba-b2105951cc0b"
        }
    },
    "scheduleInfo": {
        "startDateTime": "2022-04-14T00:00:00Z",
        "recurrence": null,
        "expiration": {
            "type": "afterDuration",
            "endDateTime": null,
            "duration": "PT5H"
        }
    },
    "ticketInfo": {
        "ticketNumber": "CONTOSO:Normal-67890",
        "ticketSystem": "MS Project"
    }
}
```

::: zone-end

::: zone pivot="azure-mobile-app"

## Activate PIM roles using the Azure mobile app

Use the Azure mobile app on iOS or Android to activate eligible Microsoft Entra role assignments and view their status.

Note

The signed-in user needs an active Premium P2 or EMS E5 license to use PIM in the Azure mobile app.

1. Download the Azure mobile app for [iOS](https://apps.apple.com/us/app/microsoft-azure/id1219013620) or [Android](https://play.google.com/store/apps/details?id=com.microsoft.azure). You can also select **Open in mobile** from **Privileged Identity Management** &gt; **My roles** &gt; **Microsoft Entra roles** to download it.

    [![Screenshot shows how to download the mobile app.](media/pim-how-to-activate-role/open-mobile.png)](media/pim-how-to-activate-role/open-mobile.png#lightbox)
2. Open the Azure mobile app and sign in. Select the **Privileged Identity Management** card and select **My Microsoft Entra roles** to view your eligible and active role assignments.

    [![Screenshots of the mobile app showing how a user would view available roles.](media/pim-how-to-activate-role/mobile-app-select-part-1.png)](media/pim-how-to-activate-role/mobile-app-select-part-1.png#lightbox)
3. Select the role assignment, and then select **Action &gt; Activate** in its details. Complete the activation requirements, enter any required details, and select **Activate** at the bottom.

    [![Screenshot of the mobile app showing a user how to fill out the required information.](media/pim-how-to-activate-role/mobile-app-select-part-2.png)](media/pim-how-to-activate-role/mobile-app-select-part-2.png#lightbox)
4. View the status of your activation requests and your role assignments under **My Microsoft Entra roles**.

    [![Screenshot of the mobile app showing the user's role status.](media/pim-how-to-activate-role/mobile-app-select-part-3.png)](media/pim-how-to-activate-role/mobile-app-select-part-3.png#lightbox)

::: zone-end

## Deactivate a role assignment

When a role assignment is activated, you see a **Deactivate** option in the portal for the role assignment. Also, you can't deactivate a role assignment within five minutes after activation.

To deactivate your active role assignment by using Microsoft Graph, create a role assignment schedule request with `action` set to `selfDeactivate`. For the request format and permissions, see [Create roleAssignmentScheduleRequests](/en-us/graph/api/rbacapplication-post-roleassignmentschedulerequests).