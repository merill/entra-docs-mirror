---
layout: Conceptual
title: View and remove requests for an access package in entitlement management - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-requests
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to view requests and remove for an access package in entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-06-25T00:00:00.0000000Z
locale: en-us
document_id: 03ed8323-bc00-d453-bf0a-10117fcb5eb0
document_version_independent_id: 6472ff5a-0731-2478-afa3-7a27037170ed
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-requests.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-requests
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-requests.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 6b903db9-41a5-3990-afa5-8880f7a5210d
---

# View and remove requests for an access package in entitlement management - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn

In entitlement management, you can see who has requested access packages, the policy for their request, and the status of their request. This article describes how to view requests for an access package, and remove requests that are no longer needed.

## View requests

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, the Access package manager, and the Access package assignment manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, open the access package you want to view requests of.
4. Select **Requests**.
5. Select a specific request to see more details.

    ![List of requests for an access package](media/entitlement-management-access-package-requests/requests-list.png)
6. You can select on **Request History details** to see who approved a request, what their approval justifications were, and when access was delivered.

If you have a set of users whose requests are in the "Partially Delivered" or "Failed" state, you can retry those requests by using the [reprocess functionality](entitlement-management-reprocess-access-package-requests).

### View requests with Microsoft Graph

You can also retrieve requests for an access package using Microsoft Graph. A user in an appropriate role with an application that has the delegated `EntitlementManagement.Read.All` or `EntitlementManagement.ReadWrite.All` permission can call the API to [list assignmentRequests](/en-us/graph/api/entitlementmanagement-list-assignmentrequests?view=graph-rest-1.0&amp;preserve-view=true). While an Identity Governance Administrator can retrieve access package requests from multiple catalogs, if user or application service principal is assigned only to catalog-specific delegated administrative roles, the request must supply a filter to indicate a specific access package, such as: `$expand=accessPackage&$filter=accessPackage/id eq 'aaaabbbb-0000-cccc-1111-dddd2222eeee'`. An application that has the application permission `EntitlementManagement.Read.All` or `EntitlementManagement.ReadWrite.All` permission can also use this API to retrieve requests across all catalogs.

Microsoft Graph will return the results in pages, and will continue to return a reference to the next page of results in the `@odata.nextLink` property with each response, until all pages of the results have been read. To read all results, you must continue to call Microsoft Graph with the `@odata.nextLink` property returned in each response until the `@odata.nextLink` property is no longer returned, as described in [paging Microsoft Graph data in your app](/en-us/graph/paging).

## Remove request

You can also remove a completed request that is no longer needed. To remove a request:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, open the access package you want to remove requests for.
4. Select **Requests**.
5. Find the request you want to remove from the access package.
6. Select the Remove button.

Note

If you remove a completed request from an access package, this doesn't remove the active assignment, only the data of the request. So the requestor will continue to have access. If you also need to remove an assignment and the resulting access from that access package, in the left menu, click **Assignments**, locate the assignment, and then [remove the assignment](entitlement-management-access-package-assignments).

### Remove a request with Microsoft Graph

You can also remove a request using Microsoft Graph. A user in an appropriate role with an application that has the delegated `EntitlementManagement.ReadWrite.All` permission, an application with the catalog role, or an application with the `EntitlementManagement.ReadWrite.All` application permission, can call the API to [remove an accessPackageAssignmentRequest](/en-us/graph/api/accesspackageassignmentrequest-delete).