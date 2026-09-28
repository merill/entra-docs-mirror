---
layout: Conceptual
title: Approve or deny access requests - entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-request-approve
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to use the My Access portal to approve or deny requests to an access package in Microsoft Entra entitlement management.
editor: mamtakumar
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-06-18T00:00:00.0000000Z
ms.reviewer: mamkumar
locale: en-us
document_id: 9fde508b-6a5a-9599-f0c3-50431da3d8fc
document_version_independent_id: 16471c4c-f347-c93b-94a1-60b5627c5b79
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-request-approve.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-request-approve
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-request-approve.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 45399bf5-181d-0da8-0368-1772f0463469
---

# Approve or deny access requests - entitlement management - Microsoft Entra ID Governance | Microsoft Learn

With entitlement management, you can configure policies to require approval for access packages, and choose one or more approvers. This article describes how designated approvers can approve or deny requests for access packages.

## Open request

The first step to approve or deny access requests is to find and open the access request pending approval. There are two ways to open the access request.

**Prerequisite role:** Approver

1. Look for an email from Microsoft Azure that asks you to approve or deny a request. Here's an example email:

    ![Approve request to access package email](media/entitlement-management-shared/approver-request-email.png)
2. Select the **Approve or deny request** link to open the access request.
3. Sign in to the My Access portal.

If you don't have the email, you can find the access requests pending your approval by following these steps.

1. Sign in to the My Access portal at https://myaccess.microsoft.com. For US Government, the domain in the My Access portal link is `myaccess.microsoft.us`.
2. In the left menu, select **Approvals** to see a list of access requests pending approval.
3. On the **Pending** tab, find the request.

Note

If you don't see an email to approve request, make sure that the access package doesn't have notifications disabled.

## View requestor's answers to questions

1. Navigate to the **Approvals** tab in My Access.
2. Go to the request you'd like to approve and select **details**. You can also select **Approve** or **Deny** if you're ready to make a decision.
3. Select **Request details**.

    ![My Access portal - Access request- Click request details](media/entitlement-management-request-approve/requestor-information-request-details.png)
4. On the **Request details** page, basic information about the request is present such as who made the request, and whether it was for themselves or for someone else. See [Request access package on-behalf-of other identities (Preview)](entitlement-management-request-behalf) for more details on requesting access for other identities.
5. The information provided by the requestor is at the bottom of the panel.

    ![Screenshot shows the details for the request](media/entitlement-management-request-approve/requestor-information-requestor-answers.png)
6. Based on the information the requestor provided, you can then approve or deny the request. See the steps in Approve or deny request for guidance.

## Approve or deny request

After you open an access request pending approval, you can see details that will help you make an approve or deny decision.

**Prerequisite role:** Approver

1. Select the **View** link to open the Access request pane.
2. Select **Details** to see details about the access request.

    The details include the identity's name, organization, access start and end date if provided, business justification, when the request was submitted, and when the request expires.
3. Select **Approve** or **Deny**.
4. If necessary, enter a reason.

    ![Screenshot shows the page where you accept or deny request.](media/entitlement-management-request-approve/my-access-approve-request.png)
5. Select **Submit** to submit your decision.

    If a policy is configured with multiple approvers in a stage, only one approver needs to make a decision about the pending approval. After an approver submits their decision to the access request, the request is completed and is no longer available for the other approvers to approve or deny the request. The other approvers can see the request decision and the decision maker in their My Access portal.

    If none of the configured approvers in a stage are able to approve or deny the access request, the request expires after the configured request duration. The user gets notified that their access request has expired, and that they need to resubmit the access request.

## Revoke a request

Users with Microsoft Entra ID Governance can undo their approval for an access request that they previously approved. This revokes the approval and the requestor will no longer have access to the access package.

**Prerequisite role:** Approver with Microsoft Entra ID Governance license

1. In My Access, select **Approvals** &gt; **History**.
2. Select an approved request that you'd like to revoke the decision for.
3. Select **Remove** to remove the identity's access to the access package. Include a reason for why you're revoking your decision.
4. Select **Remove** to submit your decision.