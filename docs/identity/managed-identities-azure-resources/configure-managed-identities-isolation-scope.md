---
layout: Conceptual
title: Configure Isolation Scope For User Assigned Managed Identities - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/configure-managed-identities-isolation-scope
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Learn how to configure isolation scope for user-assigned managed identities to improve security and resilience.
ms.reviewer: arluca
ms.topic: how-to
ms.date: 2025-07-17T00:00:00.0000000Z
locale: en-us
document_id: 39480634-3643-5c92-5ab7-97c7dc269d73
document_version_independent_id: 39480634-3643-5c92-5ab7-97c7dc269d73
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/configure-managed-identities-isolation-scope.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/configure-managed-identities-isolation-scope
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/configure-managed-identities-isolation-scope.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 1e0ff726-e566-282e-34a2-d23ca388a3c6
---

# Configure Isolation Scope For User Assigned Managed Identities - Managed identities for Azure resources | Microsoft Learn

This article shows you how to configure isolation scope for user-assigned managed identities in the Azure portal. You can either enable regional isolation scope or set your isolation scope to none. Regional isolation helps improve security and resilience by restricting where managed identities can be used, ensuring they can only be assigned to source resources in the same region.

## Prerequisites

Before you begin, ensure you have the following:

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Read the [Isolation scope for user-assigned managed identities](managed-identities-isolation-scope) concept article to understand the benefits and implications.

## Configure isolation scope in Azure portal

Use the following steps to configure isolation scope for a user-assigned managed identity.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Managed Identities**. In the search box, type *Managed Identities*. Under **Services**, select **Managed Identities**.
3. Create a new managed identity. Select **+ Create** to add a new user-assigned managed identity. Configure the basic settings:

    - **Subscription**: Select your subscription
    - **Resource Group**: Choose an existing resource group or create a new one
    - **Region**: Select the specific region for deployment
    - **Isolation Scope**: Select *Regional* to set the isolation scope to regional or *None* to set it to none
    - **Name**: Enter the name of the managed identity
4. Review and create. Select **Review + create** to validate your configuration.
5. Select **Create** to deploy the managed identity.

Once you set the value for isolation scope, you can only update it via Azure Resource Manager deployment template or REST API. The Azure portal doesn't yet support changing the isolation scope after creation.