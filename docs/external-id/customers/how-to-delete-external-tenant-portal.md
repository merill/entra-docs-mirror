---
layout: Conceptual
title: Delete an external tenant - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-delete-external-tenant-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to delete an external tenant in the  Microsoft Entra admin center.
ms.topic: how-to
ms.date: 2025-02-06T00:00:00.0000000Z
ms.custom: it-pro, sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: 2c566517-6a03-bdc6-9c03-97a26492efd0
document_version_independent_id: 2c566517-6a03-bdc6-9c03-97a26492efd0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-delete-external-tenant-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-delete-external-tenant-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-delete-external-tenant-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 8602906b-3275-79fa-ae63-15f466dad3a9
---

# Delete an external tenant - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

You can't delete an external tenant until it passes several checks. These checks reduce the risk that deleting an external tenant negatively affects user access. For example, if the tenant associated with a subscription is unintentionally deleted, users can't access the Azure resources for that subscription.

## Prerequisites

- A Microsoft Entra External ID external tenant that you want to delete.
- There are no users in the external tenant, except one [Global Administrator](../../identity/role-based-access-control/permissions-reference#global-administrator) who will delete the tenant. You must delete any other users before you can delete the tenant.
- There are no applications in the tenant. Make sure that you remove all applications including the **b2c-extensions-app**. You must delete all apps listed under **App registrations** in the **All applications** section before proceeding with the deletion.

## Delete the external tenant

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **Overview** &gt; **Manage tenants**.
4. Select the tenant you want to delete, and then select **Delete**.

    ![Screenshot that shows how to delete the tenant.](media/how-to-create-external-tenant-portal/delete-tenant.png)
5. You might need to complete required actions before you can delete the tenant. For example, you might need to delete all user flows in the tenant. If you're ready to delete the tenant, select **Delete**.

The tenant and its associated information are deleted.