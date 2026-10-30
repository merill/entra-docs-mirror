---
layout: Conceptual
title: Request an access package - entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-request-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to use the My Access portal to request access to an access package in Microsoft Entra entitlement management.
editor: mamtakumar
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2026-06-17T00:00:00.0000000Z
ms.reviewer: mamkumar
locale: en-us
document_id: 52f03984-fb13-e5b4-7033-19375ad86f32
document_version_independent_id: 67387f31-273f-1f56-0133-a4c425d6fc49
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-request-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-request-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-request-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 48f7fbe1-075d-8b22-3233-97e3cae0a68c
---

# Request an access package - entitlement management - Microsoft Entra ID Governance | Microsoft Learn

With entitlement management, an access package enables a one-time setup of resources and policies that automatically administers access for the life of the access package.

An access package manager can configure policies to require approval for users to have access to access packages. A user that needs access to an access package can submit a request to get access. This article describes how to submit an access request.

## Sign in to the My Access portal

The first step is to sign in to the My Access portal where you can request access to an access package.

**Prerequisite role:** Requestor

1. Look for an email or a message from the project or business manager you're working with. The email should include a link to the access package you need access to. The link starts with `myaccess`, includes a directory hint, and ends with an access package ID. For US Government, the domain might be `https://myaccess.microsoft.us` instead.

    `https://myaccess.microsoft.com/@<directory_hint>#/access-packages/<access_package_id>`

    Note

    When signing into My Access via your directory hint link, you're required to reauthenticate with your sign-in credentials.
2. Open the link.
3. Sign in to the My Access portal.

    Be sure you use your organizational (work or school) account. If you're unsure, check with your project or business manager.

## Request an access package

Once you find the access package in the My Access portal, you can submit a request for either yourself, or a direct employee.

**Prerequisite role:** Requestor

1. Find the access package in the list. If necessary, you can search by typing a search string. You can search by name, description, or resources.
2. To request access, you can either select the row or select **Request**.
3. On the Request details pane, select whether or not you're requesting the access package for yourself, or a direct employee. ![Screenshot of manager requesting package.](media/entitlement-management-request-behalf/manager-request-package.png)
4. Review the details of the access package, then select **Continue**.
5. You might have to answer questions and provide business justification for your request. If there are questions that you need to answer, type in your responses in the fields.
6. If the **Business justification** box is displayed, type a justification for needing access.
7. Set the **Request for specific period?** toggle to request access to the access package for a set duration of time:

    1. If you don't need access for a specific period, set the **Request for specific period?** toggle to **No**.
    2. If you need access for a certain time period, set the **Request for specific period?** toggle to **Yes**. Then, specify the start date and end date for access.

        ![My Access portal - Request access](media/entitlement-management-shared/my-access-request-access.png)
8. When finished, select **Submit request** to submit your request.
9. Select **Request history** to see a list of your requests and the status.

    If the access package requires approval, the request is now in a pending approval state.

### Select a policy

If you request access to an access package that has multiple policies that apply, you might be asked to select a policy. For example, an access package manager might configure an access package with two policies for two groups of employees. The first policy might allow access for 60 days and require approval. The second policy might allow access for two days and not require approval. If you encounter this scenario, you must select the policy you want to use.

![My Access portal - Request access - multiple policies](media/entitlement-management-request-access/my-access-multiple-policies.png)

### Fill out requestor information

You can request access to an access package that requires business justification and extra requestor information before granting you access to the access package. Fill out all the requestor information required to access the access package.

![My Access portal - Request access](media/entitlement-management-shared/my-access-request-access.png)

If you're a manager requesting access on behalf of an employee, keep in mind that you're filling out the requestor information section on behalf of the employee, as well:

![Screenshot of manager requesting question.](media/entitlement-management-request-behalf/manager-request-questions.png)

For more information on this process, see: [Request access packages on-behalf-of other users (Preview)](entitlement-management-request-behalf)

Note

You might notice that some of the additional requestor information has pre-populated values. This generally occurs if your account already has attribute information set, either from a previous request or other process. These values can be editable or not depending on the settings of the policy selected.

## Resubmit a request

When you request access to an access package, your request might be denied or your request might expire if approvers don't respond in time. If you need access, you can try again and resubmit your request. The following procedure explains how to resubmit an access request:

**Prerequisite role:** Requestor

1. Sign in to the **My Access** portal.
2. Select **Request history** from the navigation menu to the left.
3. Find the access package for which you're resubmitting a request.
4. Select the check mark to select the access package.
5. Select the blue **View** link of the selected access package.

    ![Select access package and view link](media/entitlement-management-request-access/resubmit-request-select-request-and-view.png)

    A pane opens with the request history for the access package.

    ![Select resubmit button](media/entitlement-management-request-access/resubmit-request-select-resubmit.png)
6. Select the **Resubmit** button at the bottom of the pane.

## Cancel a request

If you submit an access request and the request is still in the **pending approval** state, you can cancel the request.

**Prerequisite role:** Requestor

1. In the My Access portal, select **Request history** to see a list of your requests and the status.
2. Select the **View** link for the request you want to cancel.
3. If the request is still in the **pending approval** state, you can select **Cancel request** to cancel the request.

    ![My Access portal - Cancel request](media/entitlement-management-request-access/my-access-cancel-request.png)
4. Select **Request history** to confirm the request was canceled.

## View approver information for pending requests

If the access package is configured to display approver details, you can view who your approver is for any pending requests.

**Prerequisite role:** Requestor

1. In the My Access portal, select **Request history** to see a list of your requests and the status.
2. Select the **View** link for the request that is pending approval.
3. In the request details pane, select **Details** under pending approval. The approver information will be displayed if the access package policy allows it.