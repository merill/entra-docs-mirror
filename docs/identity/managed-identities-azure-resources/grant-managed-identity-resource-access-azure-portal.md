---
layout: Conceptual
title: Use Azure portal to grant a managed identity access to a resource - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/grant-managed-identity-resource-access-azure-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Step-by-step instructions on using Azure portal to assign a managed identity access to an Azure resource or another resource.
ms.topic: how-to
ms.date: 2025-09-09T00:00:00.0000000Z
locale: en-us
document_id: e3e35653-7858-d441-21b4-97f6116c30bc
document_version_independent_id: e3e35653-7858-d441-21b4-97f6116c30bc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/grant-managed-identity-resource-access-azure-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/grant-managed-identity-resource-access-azure-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/grant-managed-identity-resource-access-azure-portal.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: c8060bb8-7d98-a2f5-150c-2800105964f4
---

# Use Azure portal to grant a managed identity access to a resource - Managed identities for Azure resources | Microsoft Learn

This article shows you how to use the Azure portal to give a managed identity access to an Azure resource. In this article, we use the example of an Azure virtual machine (Azure VM) managed identity accessing an Azure storage account. Once you've configured an Azure resource with a managed identity, you can then give the managed identity access to another resource, similar to any security principal.

## Prerequisites

- Be sure you've enabled managed identity on an Azure resource, such as an [Azure virtual machine](how-to-configure-managed-identities).
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before continuing.

## Use Azure RBAC to assign a managed identity access to another resource using the Azure portal

The steps outlined below show how you grant access to a service using Azure RBAC. Check specific service documentation on how to grant access; for example, check [Azure Data Explorer](/en-us/azure/data-explorer/data-explorer-overview) for instructions. Some Azure services are in the process of adopting Azure RBAC on the data plane.

1. Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription for which you've configured the managed identity.
2. Navigate to the desired resource that you want to modify access control. In this example, you'll give an Azure virtual machine (VM) access to a storage account, then you can navigate to the storage account.
3. Select **Access control (IAM)**.
4. Select **Add** &gt; **Add role assignment** to open the **Add role assignment** page.
5. Select the role and managed identity. For detailed steps, see [Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal).

    ![Screenshot that shows the page for adding a role assignment.](../../media/common/add-role-assignment-page.png)