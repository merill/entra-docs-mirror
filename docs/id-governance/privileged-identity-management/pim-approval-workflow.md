---
layout: Conceptual
title: Approve or deny requests for Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-approval-workflow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to approve or deny requests for Microsoft Entra roles in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.custom: pim, sfi-ga-nochange
locale: en-us
document_id: 55d8ca0b-4832-abb9-7275-b94a4ab18018
document_version_independent_id: 7ca62916-63cc-2c36-f48f-d09592460647
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-approval-workflow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-approval-workflow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-approval-workflow.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8ea0fba9-29d8-b63f-607d-267f330cdf96
---

# Approve or deny requests for Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Privileged Identity Management (PIM) in Microsoft Entra ID allows you to configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers. Delegated approvers have 24 hours to approve requests. If a request isn't approved within 24 hours, then the eligible user must re-submit a new request. The 24-hour approval time window isn't configurable.

## View pending requests

As a delegated approver, you receive an email notification when a Microsoft Entra role request is pending your approval. You can view these pending requests in Privileged Identity Management.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Approve requests**.

    ![Screenshot showing the Approve requests page showing request to review Microsoft Entra roles.](media/azure-ad-pim-approval-workflow/resources-approve-pane.png)

    In the **Requests for role activations** section, you can see a list of requests pending your approval.

## View pending requests using Microsoft Graph API

### HTTP request

```HTTP
GET https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignmentScheduleRequests/filterByCurrentUser(on='approver')?$filter=status eq 'PendingApproval' 
```

### HTTP response

```HTTP
{ 
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#Collection(unifiedRoleAssignmentScheduleRequest)", 
    "value": [ 
        { 
            "@odata.type": "#microsoft.graph.unifiedRoleAssignmentScheduleRequest", 
            "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee", 
            "status": "PendingApproval", 
            "createdDateTime": "2021-07-15T19:57:17.76Z", 
            "completedDateTime": "2021-07-15T19:57:17.537Z", 
            "approvalId": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee", 
            "customData": null, 
            "action": "SelfActivate", 
            "principalId": "aaaaaaaa-bbbb-cccc-1111-222222222222", 
            "roleDefinitionId": "88d8e3e3-8f55-4a1e-953a-9b9898b8876b", 
            "directoryScopeId": "/", 
            "appScopeId": null, 
            "isValidationOnly": false, 
            "targetScheduleId": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee", 
            "justification": "test", 
            "createdBy": { 
                "application": null, 
                "device": null, 
                "user": { 
                    "displayName": null, 
                    "id": "d96ea738-3b95-4ae7-9e19-78a083066d5b" 
                } 
            }, 
            "scheduleInfo": { 
                "startDateTime": null, 
                "recurrence": null, 
                "expiration": { 
                    "type": "afterDuration", 
                    "endDateTime": null, 
                    "duration": "PT5H30M" 
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

## Approve requests

Note

Approvers aren't able to approve their own role activation requests. Additionally, service principals aren't allowed to approve requests.

1. Find and select the request that you want to approve. An approve or deny page appears.
2. In the **Justification** box, enter the business justification.
3. Select **Submit**. At this point, the system sends an Azure notification of your approval.

## Approve pending requests using Microsoft Graph API

Note

Approval for **extend and renew** requests is currently not supported by the Microsoft Graph API.

### Get IDs for the steps that require approval

For a specific activation request, this command gets all the approval steps that need approval. Multi-step approvals aren't currently supported.

#### HTTP request

```HTTP
GET https://graph.microsoft.com/beta/roleManagement/directory/roleAssignmentApprovals/<request-ID-GUID> 
```

#### HTTP response

```HTTP
{ 
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#roleManagement/directory/roleAssignmentApprovals/$entity", 
    "id": "<request-ID-GUID>",
    "steps@odata.context": "https://graph.microsoft.com/beta/$metadata#roleManagement/directory/roleAssignmentApprovals('<request-ID-GUID>')/steps", 
    "steps": [ 
        { 
            "id": "<approval-step-ID-GUID>", 
            "displayName": null, 
            "reviewedDateTime": null, 
            "reviewResult": "NotReviewed", 
            "status": "InProgress", 
            "assignedToMe": true, 
            "justification": "", 
            "reviewedBy": null 
        } 
    ] 
} 
```

### Approve the activation request step

#### HTTP request

```HTTP
PATCH 
https://graph.microsoft.com/beta/roleManagement/directory/roleAssignmentApprovals/<request-ID-GUID>/steps/<approval-step-ID-GUID> 
{ 
    "reviewResult": "Approve", // or "Deny"
    "justification": "Trusted User" 
} 
```

#### HTTP response

Successful PATCH calls generate an empty response.

## Deny requests

1. Find and select the request that you want to deny. An approve or deny page appears.
2. In the **Justification** box, enter the business justification.
3. Select **Deny**. A notification appears with your denial.

## Workflow notifications

Here's some information about workflow notifications:

- Approvers are notified by email when a request for a role is pending their review. Email notifications include a direct link to the request, where the approver can approve or deny.
- Requests are resolved by the first approver who approves or denies.
- All approvers are notified when an approver responds to an approval request.
- Global Administrators and Privileged Role Administrators are notified when an approved user becomes active in their role.

Note

A Global Administrator or Privileged Role Admin who believes that an approved user shouldn't be active can remove the active role assignment in Privileged Identity Management. Although administrators aren't notified of pending requests unless they're an approver, they can view and cancel any pending requests for all users by viewing pending requests in Privileged Identity Management.