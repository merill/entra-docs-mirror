---
layout: Conceptual
title: View update and sign-in activities for Managed identities - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/how-to-view-managed-identity-activity
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Step-by-step instructions for viewing the activities made to managed identities, and authentications carried out by managed identities
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2024-06-05T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 622b29df-8106-84c8-a97c-6f228a6ca75e
document_version_independent_id: 0da2e472-7858-29f8-72b0-856237056d00
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/how-to-view-managed-identity-activity.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/how-to-view-managed-identity-activity
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/how-to-view-managed-identity-activity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 91473e36-00a9-52db-341c-77c387cc67ed
---

# View update and sign-in activities for Managed identities - Managed identities for Azure resources | Microsoft Learn

This article explains how to view updates carried out to managed identities, and sign-in attempts made by managed identities.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview).
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## View updates made to user-assigned managed identities

This procedure demonstrates how to view updates carried out to user-assigned managed identities.

1. In the Azure portal, browse to **Activity Log**.

    ![Screenshot showing how to browse to the activity log in the Azure portal](media/how-to-view-managed-identity-activity/browse-to-activity-log.png)
2. Select the **Add Filter** search pill and select **Operation** from the list.

    ![Screenshot showing how to start building the search filter](media/how-to-view-managed-identity-activity/start-adding-search-filter.png)
3. In the **Operation** dropdown list, enter these operation names: "Delete User Assigned Identity" and "Write UserAssignedIdentities".

    ![Screenshot showing how to add operations to the search filter](media/how-to-view-managed-identity-activity/add-operations-to-search-filter.png)
4. When matching operations are displayed, select one to view the summary.

    ![Screenshot showing the summary of the operation](media/how-to-view-managed-identity-activity/view-summary-of-operation.png)
5. Select the **JSON** tab to view more detailed information about the operation, and scroll to the **properties** node to view information about the identity that was modified.

    ![Screenshot showing operation details](media/how-to-view-managed-identity-activity/view-json-of-operation.png)

## View role assignments added and removed for managed identities

Note

You'll need to search by the object (principal) ID of the managed identity that you want to view role assignment changes for.

1. Locate the managed identity you wish to view the role assignment changes for. If you're looking for a system-assigned managed identity, the object ID is displayed in the **Identity** screen under the resource. If you're looking for a user-assigned identity, the object ID is displayed in the **Overview** page of the managed identity.

User-assigned identity:

![Screenshot showing how to get the object ID of user-assigned identity](media/how-to-view-managed-identity-activity/get-object-id-of-user-assigned-identity.png)

System-assigned identity:

![Screenshot showing how to get the object ID of system-assigned identity](media/how-to-view-managed-identity-activity/get-object-id-of-system-assigned-identity.png)

1. Copy the object ID.
2. Browse to the **Activity log**.

    ![Screenshot showing how to browse to the activity log in the Azure portal](media/how-to-view-managed-identity-activity/browse-to-activity-log.png)
3. Select the **Add Filter** search pill and select **Operation** from the list.

    ![Screenshot showing how to start building the search filter](media/how-to-view-managed-identity-activity/start-adding-search-filter.png)
4. In the **Operation** dropdown list, enter these operation names: **Create role assignment** and **Delete role assignment**.

    ![Screenshot showing how to add role assignment operations to the search filter](media/how-to-view-managed-identity-activity/add-role-assignment-operations-to-search-filter.png)
5. Paste the object ID in the search box; the results are filtered automatically.

    ![Screenshot showing how to search by object ID](media/how-to-view-managed-identity-activity/search-by-object-id.png)
6. When matching operations are displayed, select one to view the summary.

    ![Screenshot showing the summary of role assignment for managed identity](media/how-to-view-managed-identity-activity/summary-of-role-assignment-for-msi.png)

## View authentication attempts by managed identities

1. Browse to **Microsoft Entra ID**.

    ![Screenshot showing how to browse to active directory](media/how-to-view-managed-identity-activity/browse-to-entra.png)
2. Select **Sign-in logs** from the **Monitoring** section.

    ![Screenshot showing sign-in logs selection](media/how-to-view-managed-identity-activity/sign-in-logs-menu-item.png)
3. Select the **Managed identity sign-ins** tab.

    ![Screenshot of the managed identities activity section showing all columns ](media/how-to-view-managed-identity-activity/sign-in-logs.png)
4. To view the identity's Enterprise application in Microsoft Entra ID, select the "Managed Identity ID" column.
5. To view the Azure resource or user-assigned managed identity, search by name in the search bar of the Azure portal.

    ![Screenshot showing managed identity sign-in events](media/how-to-view-managed-identity-activity/msi-sign-in-events.png)

Note

Since managed identity authentication requests originate within the Azure infrastructure, the IP Address value is excluded here.