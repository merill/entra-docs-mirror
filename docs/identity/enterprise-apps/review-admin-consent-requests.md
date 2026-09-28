---
layout: Conceptual
title: Review and take action on admin consent requests - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/review-admin-consent-requests
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to review and take action on admin consent requests that were created after you were designated as a reviewer.
ms.topic: how-to
ms.date: 2025-04-08T00:00:00.0000000Z
ms.reviewer: ergreenl
ai-usage: ai-assisted
ms.custom: enterprise-apps, sfi-image-nochange
locale: en-us
document_id: ae5c5628-61d7-bded-ad8f-57b2a370a693
document_version_independent_id: 9a179bac-cedb-417c-7a30-b617ffc9c935
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/review-admin-consent-requests.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/review-admin-consent-requests
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/review-admin-consent-requests.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 6b92415d-09da-9d6b-9739-1d554f139534
---

# Review and take action on admin consent requests - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to review and take action on admin consent requests. To review and act on consent requests, you must be designated as a reviewer. For more information, check out the [Configure the admin consent workflow](configure-admin-consent-workflow) article. As a reviewer, you can view all admin consent requests but you can only act on those requests that were created after you were designated as a reviewer.

When reviewing admin consent requests, you have several options to choose from:

- **Review**: This option allows administrators to evaluate the request and grant consent if deemed appropriate.
- **Deny**: Selecting this option will reject the request for consent, preventing the application from accessing the requested permissions. This action does not provide feedback to the user who made the request.
- **Block**: This option not only denies the current request but also prevents future requests for the same application from being submitted. This is useful for applications that are deemed untrustworthy or unnecessary for the organization.

For instance, if an application is found to be non-compliant with company policies, an administrator might choose to 'Block' it. Conversely, if an application is legitimate but requires further review, the administrator may opt to 'Deny' the request temporarily while seeking more information.

Note

The "My Pending" tab is where actions can be taken on admin consent requests. The "All (Preview)" tab is to view the history of the admin consent request only.

## Prerequisites

To review and take action on admin consent requests, you need:

- An Azure account. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An administrator role or a designated reviewer with the appropriate role to [review admin consent requests](grant-admin-consent#prerequisites).

## Review and take action on admin consent requests

To review the admin consent requests and take action:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator) who is a designated reviewer.
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Under **Activity**, select **Admin consent requests**.
4. Select **My Pending** tab to view and act on the pending requests.
5. Select the application that is being requested from the list.
6. Review details about the request:
    - To see what permissions are being requested by the application, select **Review permissions and consent**.
    - To view the application details, select the **App details** tab.
    - To see who is requesting access and why, select the **Requested by** tab.
7. Evaluate the request and take the appropriate action:
    - **Approve the request**. To approve a request, grant admin consent to the application. Once a request is approved, all requestors are notified that their request for access is granted. Approving a request allows all users in your tenant to access the application unless otherwise restricted with user assignment.
    - **Deny the request**. To deny a request, you must provide a justification that is provided to all requestors. Once a request is denied, all requestors are notified that their request for access is denied. Denying a request won't prevent users from requesting admin consent to the application again in the future.
    - **Block the request**. To block a request, you must provide a justification that is provided to all requestors. Once a request is blocked, all requestors are notified that their request to access the application is denied. Blocking a request creates a service principal object for the application in your tenant in a disabled state. Users won't be able to request admin consent to the application in the future.

## Review admin consent requests using Microsoft Graph

To review the admin consent requests programmatically, use the [`appConsentRequest` resource type](/en-us/graph/api/resources/appconsentrequest) and [`userConsentRequest` resource type](/en-us/graph/api/resources/userconsentrequest) and their associated methods in Microsoft Graph. You can't approve or deny consent requests using Microsoft Graph.