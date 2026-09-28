---
layout: HowTo
title: Activate Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-how-to-activate-role
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to activate Microsoft Entra roles in Privileged Identity Management (PIM).
ms.reviewer: ilyal
ms.date: 2026-04-23T00:00:00.0000000Z
ms.topic: how-to
ms.custom:
- ge-structured-content-pilot
- sfi-ga-nochange
- sfi-image-nochange
locale: en-us
document_id: 43125fc1-f1fb-fa8c-69a6-7866a1b3a1fe
document_version_independent_id: 174dbe2c-7469-a63a-ffd6-757272ce5c50
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-how-to-activate-role.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: HowTo
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-how-to-activate-role
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-how-to-activate-role.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: caccf3ec-47aa-0504-9acb-caa9bf5a1d9f
---

# Activate Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn

Microsoft Entra Privileged Identity Management (PIM) simplifies how enterprises manage privileged access to resources in Microsoft Entra ID and other Microsoft online services like Microsoft 365 or Microsoft Intune.

If you have been made *eligible* for an administrative role, then you must *activate* the role assignment when you need to perform privileged actions. For example, if you occasionally manage Microsoft 365 features, your organization's Privileged Role Administrators might not make you a permanent Global Administrator, since that role impacts other services, too. Instead, they would make you eligible for Microsoft Entra roles such as Exchange Online Administrator. You can request to activate that role when you need its privileges, and then have administrator control for a predetermined time period.

This article is for administrators who need to activate their Microsoft Entra role in Privileged Identity Management. Although any user can submit a request for the role they need through PIM without having the Privileged Role Administrator (PRA) role, this role is required for managing and assigning roles to others within the organization.

Important

When a role is activated, Microsoft Entra PIM temporarily adds active assignment for the role. Microsoft Entra PIM creates active assignment (assigns user to a role) within seconds. When deactivation (manual or through activation time expiration) happens, Microsoft Entra PIM removes the active assignment within seconds as well.

Application may provide access based on the role the user has. In some situations, application access may not immediately reflect the fact that user got role assigned or removed. If application previously cached the fact that user does not have a role – when user tries to access application again, access may not be provided. Similarly, if application previously cached the fact that user has a role – when role is deactivated, user may still get access. Specific situation depends on the application’s architecture. For some applications, signing out and signing back in may help get access added or removed.

Important

If a user activating an administrative role is signed in to Microsoft Teams on a mobile device, they will receive a notification from the Teams app saying "Open Teams to continue receiving notifications for *&lt;email address&gt;*", or "*&lt;email address&gt;* needs to sign in to see notifications". The user will need to open the Teams app to continue receiving notifications. This behavior is by design.

## Prerequisites

None

## Activate a role

When you need to assume a Microsoft Entra role, you can request activation by opening **My roles** in Privileged Identity Management.

Note

PIM is now available in the Azure mobile app (iOS | Android) for Microsoft Entra ID and Azure resource roles. Easily activate eligible assignments, request renewals for ones that are expiring, or check the status of pending requests. Read more

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a user who has an eligible role assignment.
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **My roles**. For information about how to add the Privileged Identity Management tile to your dashboard, see [Start using Privileged Identity Management](pim-getting-started).
3. Select **Microsoft Entra roles** to see a list of your eligible Microsoft Entra roles.

    ![My roles page showing roles you can activate](media/pim-how-to-activate-role/my-roles.png)
4. In the **Microsoft Entra roles** list, find the role you want to activate.

    ![Microsoft Entra roles - My eligible roles list](media/pim-how-to-activate-role/activate-link.png)
5. Select **Activate** to open the Activate pane.

    ![Microsoft Entra roles - activation page contains duration and scope](media/pim-how-to-activate-role/activate-page.png)
6. Select **Additional verification required** and follow the instructions to provide security verification. You are required to authenticate only once per session.

    ![Screen to provide security verification such as a PIN code](media/pim-resource-roles-activate-your-roles/resources-mfa-enter-code.png)
7. After multifactor authentication, select **Activate before proceeding**.

    ![Verify my identity with MFA before role activates](media/pim-how-to-activate-role/activate-role-mfa-banner.png)
8. If you want to specify a reduced scope, select **Scope** to open the filter pane. On the filter pane, you can specify the Microsoft Entra resources that you need access to. It's a best practice to request access to the fewest resources that you need.
9. If necessary, specify a custom activation start time. The Microsoft Entra role would be activated after the selected time.
10. In the **Reason** box, enter the reason for the activation request.
11. Select **Activate**.

    If the [role requires approval](pim-resource-roles-approval-workflow) to activate, a notification appears in the upper right corner of your browser informing you the request is pending approval.

    ![Activation request is pending approval notification](media/pim-resource-roles-activate-your-roles/resources-my-roles-activate-notification.png)

## Activate a role using Microsoft Graph API

    For more information about Microsoft Graph APIs for PIM, see [Overview of role management through the privileged identity management (PIM) API](/en-us/graph/api/resources/privilegedidentitymanagementv3-overview).

### Get all eligible roles that you can activate

    When a user gets their role eligibility via group membership, this Microsoft Graph request doesn't return their eligibility.

#### HTTP request

    ```HTTP
    GET https://graph.microsoft.com/v1.0/roleManagement/directory/roleEligibilityScheduleRequests/filterByCurrentUser(on='principal')  
    ```

#### HTTP response

    To save space we're showing only the response for one role, but all eligible role assignments that you can activate will be listed.

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

## View the status of activation requests

You can view the status of your pending requests to activate.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **My requests**.
3. When you select **My requests** you see a list of your Microsoft Entra role and Azure resource role requests.

    [![Screenshot of My requests - Microsoft Entra ID page showing your pending requests](media/pim-how-to-activate-role/my-requests-page.png)](media/pim-how-to-activate-role/my-requests-page.png#lightbox)
4. Scroll to the right to view the **Request Status** column.

## Cancel a pending request for new version

If you don't require activation of a role that requires approval, you can cancel a pending request at any time.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **My requests**.
3. For the role that you want to cancel, select the **Cancel** link.

    When you select Cancel, the request is canceled. To activate the role again, you have to submit a new request for activation.

    ![My request list with Cancel action highlighted](media/pim-resource-roles-activate-your-roles/resources-my-requests-cancel.png)

## Deactivate a role assignment

When a role assignment is activated, you see a **Deactivate** option in the PIM portal for the role assignment. Also, you can't deactivate a role assignment within five minutes after activation.

## Activate PIM roles using the Azure mobile app

PIM is now available in the Microsoft Entra ID and Azure resource roles mobile apps in both iOS and Android.

Note

An active Premium P2 or EMS E5 license is required for the signed-in user to use this inside the app.

1. To activate an eligible Microsoft Entra role assignment, start by downloading the Azure mobile app ([iOS](https://apps.apple.com/us/app/microsoft-azure/id1219013620) | [Android](https://play.google.com/store/apps/details?id=com.microsoft.azure)). You can also download the app by selecting ‘Open in mobile’ from Privileged Identity Management &gt; My roles &gt; Microsoft Entra roles.

    [![Screenshot shows how to download the mobile app.](media/pim-how-to-activate-role/open-mobile.png)](media/pim-resource-roles-assign-roles/resources-abac-update-remove.png#lightbox)
2. Open the Azure mobile app and sign in. Select the **Privileged Identity Management** card and select **My Microsoft Entra roles** to view your eligible and active role assignments.

    [![Screenshots of the mobile app showing how a user would view available roles.](media/pim-how-to-activate-role/mobile-app-select-part-1.png)](media/pim-how-to-activate-role/mobile-app-select-part-1.png#lightbox)
3. Select the role assignment and click on **Action &gt; Activate** under the role assignment details. Complete the steps to active and fill in any required details before clicking ‘Activate’ at the bottom.

    [![Screenshot of the mobile app showing a user how to fill out the required information](media/pim-how-to-activate-role/mobile-app-select-part-2.png)](media/pim-how-to-activate-role/mobile-app-select-part-2.png#lightbox)
4. View the status of your activation requests and your role assignments under **My Microsoft Entra roles**.

    [![Screenshot of the mobile app showing the user's role status.](media/pim-how-to-activate-role/mobile-app-select-part-3.png)](media/pim-how-to-activate-role/mobile-app-select-part-3.png#lightbox)