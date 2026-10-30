---
layout: Conceptual
title: Configure assignment restriction for user-assigned managed identities (preview) - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/configure-managed-identities-assignment-restriction
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: mmacy-msft
ms.author: marshmacy
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Learn how to configure assignment restriction for a user-assigned managed identity in the Azure portal to scope it to specific resource providers.
ms.topic: how-to
ms.custom: msecd-doc-authoring-10012
ms.date: 2026-07-10T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: bc275bc4-3249-9c45-8ed6-c7a3c974f59a
document_version_independent_id: bc275bc4-3249-9c45-8ed6-c7a3c974f59a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/configure-managed-identities-assignment-restriction.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/configure-managed-identities-assignment-restriction
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/configure-managed-identities-assignment-restriction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 829ebfe3-334c-a6ee-ef93-44cdff28e2e1
---

# Configure assignment restriction for user-assigned managed identities (preview) - Managed identities for Azure resources | Microsoft Learn

This article describes how to configure assignment restrictions (also referred to as resource restrictions) for a user-assigned managed identity by using the Azure portal. This is a feature in preview.

Assignment restrictions let you explicitly define the resource providers or resource types that a managed identity can be assigned to. Enforcing assignment restrictions keeps managed identities within their intended scope, which strengthens security and operational boundaries. By restricting where a managed identity can be assigned, you limit identity reuse and reduce blast radius.

## Prerequisites

Before you begin, make sure you have the following:

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/free).

## Create assignment restrictions in the Azure portal

You configure assignment restrictions when you create a user-assigned managed identity. To create a user-assigned managed identity with assignment restrictions, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com) with at least the [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role.
2. Go to **Managed Identities**. In the search box, enter *Managed Identities*. Under **Services**, select **Managed Identities**.
3. Select **+ Create** to add a new user-assigned managed identity and configure the basic settings:

    - **Subscription**: Select your subscription.
    - **Resource group**: Choose an existing resource group or create a new one.
    - **Name**: Enter a name for the managed identity.
    - **Region**: Select the region for deployment.
    - **Isolation Scope**: Select the isolation scope. We recommend setting this value to **Regional** for regional isolation. For more information, see [Isolation scope for user-assigned managed identities](managed-identities-isolation-scope).
    - **Resource**: Select **Add resource**. In the **Select Resource Types** panel that opens, search for and select the resource provider or resource type that the identity is restricted to.

    Note

    If **Resource** is left unconfigured, the value shows as **None**, which represents an empty array.
4. Select **Review + create** to validate your configuration.
5. Select **Create** to deploy the managed identity.

## Update assignment restrictions in the Azure portal

You can update the isolation scope and assignment restrictions of an existing user-assigned managed identity at any time. To update assignment restrictions, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com) with at least the [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role.
2. Go to **Managed Identities**, and then select the user-assigned managed identity that you want to update.
3. Under **Settings**, select **Properties**.
4. Update the assignment restrictions:

    - **Isolation Scope**: Select **Regional** or **None**.
    - **Resource**: Select the edit (pencil) icon. In the **Select Resource Types** panel that opens, add or remove the resource providers or resource types that the identity is restricted to.
5. Select **Save** to apply your changes.

Note

If your update removes a resource provider from the assignment restrictions list, unassign the user-assigned managed identity from the source resource *first*, before you remove the resource provider from the list.

## Supported resource providers and resource types in the Azure portal

Note

Selecting **None** for resource assignment restrictions leaves the identity unrestricted, allowing it to be assigned to resources from any resource provider that supports managed identities.

Configure resource assignment restrictions only when you want to limit identity assignment to specific resource providers. Be aware that the **Select Resource Types** list in the Azure portal may not include all supported resource providers and resource types.

The **Select Resource Types** pane in the Azure portal does not display all resource providers and resource types that support managed identities. If the resource you want to configure is not listed, use the Azure CLI to create or update the identity assignment. Refer to the Azure CLI examples below for resources that are not currently available in the **Select Resource Types** list.

Warning

In Azure CLI commands and infrastructure-as-code (IaC) templates, specify the resource provider namespace on its own, for example `Microsoft.Storage`. Don't use `Microsoft.Storage/*`.

The **Select Resource Types** pane in the Azure portal displays a provider-wide selection as `Microsoft.Storage/*`. The `/*` suffix is a portal display convention and isn't part of the value that the API accepts. Even when the portal shows `Microsoft.Storage/*`, use `Microsoft.Storage` in Azure CLI commands and IaC templates. To restrict the identity to a single resource type instead of the whole provider, specify the full resource type, for example `Microsoft.Storage/storageAccounts`.

### Create an identity with resource assignment restrictions

```bash
az identity create \
  --name MyIdentity \
  --resource-group MyResourceGroup \
  --resource-restriction '{"providers": ["Microsoft.Compute", "Microsoft.Storage"]}'
```

### Update an identity to restrict assignment to specific resources

```bash
az identity update \
  --name MyIdentity \
  --resource-group MyResourceGroup \
  --resource-restriction '{"providers": ["Microsoft.Compute", "Microsoft.Storage"]}'
```

### List the associated resources for an identity

```bash
az identity list-resources \
  --name MyIdentity \
  --resource-group MyResourceGroup
```

### Create an unrestricted identity

```bash
az identity create \
--name MyIdentity \
--resource-group MyResourceGroup \
--resource-restriction '{"providers": []}'
```

### Remove all resource provider restrictions from an identity

```bash
az identity update \
--name MyIdentity \
--resource-group MyResourceGroup \
--resource-restriction '{"providers": []}'
```