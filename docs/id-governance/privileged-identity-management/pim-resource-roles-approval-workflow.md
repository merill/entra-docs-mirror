---
layout: Conceptual
title: Approve requests for Azure resource roles in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-resource-roles-approval-workflow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to approve or deny requests for Azure resource roles in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: pim
locale: en-us
document_id: 2db25c00-21a0-2be5-7d78-8b66ec675847
document_version_independent_id: aa152389-c2ac-867b-e53d-5af5a92a0572
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-resource-roles-approval-workflow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-resource-roles-approval-workflow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-resource-roles-approval-workflow.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 97379049-938d-fa8c-3671-3198ebf9c3aa
---

# Approve requests for Azure resource roles in PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Microsoft Entra Privileged Identity Management (PIM) enables you to configure roles so that they require approval for activation, and choose users or groups from your Microsoft Entra organization as delegated approvers. Select two or more approvers for each role to reduce workload for the Privileged Role Administrator. Delegated approvers have 24 hours to approve requests. If a request isn't approved within 24 hours, then the eligible user must resubmit a new request. The 24-hour approval time window isn't configurable.

Follow the steps in this article to approve or deny requests for Azure resource roles.

## View pending requests

As a delegated approver, you receive an email notification when an Azure resource role request is pending your approval. You can view these pending requests in Privileged Identity Management.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Approve requests**.

    In the **Requests for role activations** section, you see a list of requests pending your approval.

## Approve requests

1. Find and select the request that you want to approve. An approve or deny page appears.
2. In the **Justification** box, enter the business justification.
3. Select **Approve**. You receive an Azure notification of your approval.

## Approve pending requests with the Microsoft Azure Resource Manager API

Note

Approval for **extend and renew** requests is currently not supported by the Microsoft ARM API.

### Get IDs for the steps that require approval

To get the details of any stage of a role assignment approval, you can use [Role Assignment Approval Step - Get By ID](/en-us/rest/api/authorization/role-assignment-approval-step/get-by-id?tabs=HTTP) REST API.

#### HTTP request

```HTTP
GET https://management.azure.com/providers/Microsoft.Authorization/roleAssignmentApprovals/{approvalId}/stages/{stageId}?api-version=2021-01-01-preview
```

### Approve the activation request step

To approve the activation request step, make the following API call.

#### HTTP request

```HTTP
PATCH https://management.azure.com/providers/Microsoft.Authorization/roleAssignmentApprovals/{approvalId}/stages/{stageId}?api-version=2021-01-01-preview
{ 
    "reviewResult": "Approve", // or "Deny"
    "justification": "Trusted User" 
} 
```

#### HTTP response

Successful PATCH calls generate an empty response.

For more information, see [Use Role Assignment Approvals to approve PIM role activation requests with REST API](/en-us/rest/api/authorization/privileged-approval-sample).

## Deny requests

1. Find and select the request that you want to deny. An approve or deny page appears.
2. In the **Justification** box, enter the business justification.
3. Select **Deny**. A notification appears with your denial.

## Workflow notifications

Here's some information about workflow notifications:

- Approvers are notified by email when a request for a role is pending their review. Email notifications include a direct link to the request, where the approver can approve or deny.
- Requests are resolved by the first approver who approves or denies.
- When an approver responds to the request, all approvers are notified of the action.
- Resource administrators are notified when an approved user becomes active in their role.

Note

A resource administrator who believes that an approved user shouldn't be active can remove the active role assignment in Privileged Identity Management. Although resource administrators aren't notified of pending requests unless they're an approver, they can view and cancel pending requests for all users by viewing pending requests in Privileged Identity Management.