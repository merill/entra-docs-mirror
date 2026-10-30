---
layout: Conceptual
title: How to find your tenant ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/how-to-find-tenant
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Instructions about how to find your Microsoft Entra tenant ID for an existing Azure subscription.
ms.topic: how-to
ms.date: 2025-01-14T00:00:00.0000000Z
ms.reviewer: jeffsta
ms.custom: it-pro, ge-structured-content-pilot, sfi-image-nochange
locale: en-us
document_id: 4a2c79bd-0887-2f50-f67e-57e580b0b5f9
document_version_independent_id: 2d054a79-8ff1-dbe4-51da-6e99db97457b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/how-to-find-tenant.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurepowershell,azurecli
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/how-to-find-tenant
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/how-to-find-tenant.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0923294f-2d2e-d604-adcf-43c36e27fc69
---

# How to find your tenant ID - Microsoft Entra | Microsoft Learn

## Overview

Azure subscriptions have a trust relationship with Microsoft Entra ID. Microsoft Entra ID is trusted to authenticate the subscription's users, services, and devices. Each subscription has a tenant ID associated with it, and there are a few ways you can find the tenant ID for your subscription.

## Find tenant ID through the Microsoft Entra admin center

Follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Reader](../identity/role-based-access-control/permissions-reference#global-reader).
2. Browse to **Entra ID** &gt; **Overview** &gt; **Properties**.

    ![Screenshot of Microsoft Entra ID - Identity Properties overview.](media/how-to-find-tenant/identity-overview-properties.png)
3. Scroll down to the **Tenant ID** section and you can find your tenant ID in the box.

## Find tenant ID through the Azure portal

Follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Browse to **Microsoft Entra ID** &gt; **Properties**.
3. Scroll down to the **Tenant ID** section and you can find your tenant ID in the box.

    ![Screenshot of Microsoft Entra ID - Properties - Tenant ID - Tenant ID field.](media/how-to-find-tenant/portal-tenant-id.png)

## Find tenant ID with PowerShell

To find the tenant ID with Azure PowerShell, use the cmdlet `Get-AzTenant`.

```azurepowershell
Connect-AzAccount
Get-AzTenant
```

For more information, see the [Get-AzTenant](/en-us/powershell/module/az.accounts/get-aztenant) cmdlet reference.

## Find tenant ID with CLI

Use the [Azure CLI](/en-us/cli/azure/install-azure-cli) or [Microsoft 365 CLI](https://github.com/pnp/cli-microsoft365) to find the tenant ID.

For Azure CLI, use one of the commands `az login`, `az account list`, or `az account tenant list`. All commands included below return the `tenantId` property for each of your subscriptions.

```azurecli
az login
az account list
az account tenant list
```

For more information, see [az login](/en-us/cli/azure/reference-index#az-login) command reference, [az account](/en-us/cli/azure/account) command reference, or [az account tenant](/en-us/cli/azure/account/tenant) command reference.

For Microsoft 365 CLI, use the cmdlet `tenant id` as shown in the following example:

```cli
m365 tenant id get
```