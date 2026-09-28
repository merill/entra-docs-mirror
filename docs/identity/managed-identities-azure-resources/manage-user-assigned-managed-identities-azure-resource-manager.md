---
layout: Conceptual
title: Manage user-assigned managed identities using Azure Resource Manager - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-resource-manager
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Manage user-assigned managed identities using Azure Resource Manager.
ms.topic: how-to
ms.date: 2025-09-09T00:00:00.0000000Z
locale: en-us
document_id: 985494c4-02d8-56a8-3009-9719b81c69d3
document_version_independent_id: 985494c4-02d8-56a8-3009-9719b81c69d3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-resource-manager.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-resource-manager
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-resource-manager.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: acefebe2-b448-3e54-b2f3-3b817be6ee3f
---

# Manage user-assigned managed identities using Azure Resource Manager - Managed identities for Azure resources | Microsoft Learn

Managed identities for Azure resources eliminate the need to manage credentials in code. You can use them to get a Microsoft Entra token for your applications. The applications can use the token when accessing resources that support Microsoft Entra authentication. Azure manages the identity so you don't have to.

There are two types of managed identities: system-assigned and user-assigned. System-assigned managed identities have their lifecycle tied to the resource that created them. This identity is restricted to only one resource, and you can grant permissions to the managed identity by using Azure role-based access control (RBAC). User-assigned managed identities can be used on multiple resources.

In this article, you create a user-assigned managed identity by using Azure Resource Manager. You can't list and delete a user-assigned managed identity by using a Resource Manager template. Use the other methods to list or delete a user-assigned managed identity.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview). *Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview#managed-identity-types)*.
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you continue.

## Template creation and editing

Resource Manager templates help you deploy new or modified resources defined by an Azure resource group. Several options are available for template editing and deployment, both local and portal-based. You can:

- Use a [custom template from Azure Marketplace](/en-us/azure/azure-resource-manager/templates/deploy-portal#deploy-resources-from-custom-template) to create a template from scratch or base it on an existing common or [quickstart template](https://azure.microsoft.com/resources/templates/).
- Derive from an existing resource group by exporting a template. You can export them from either [the original deployment](/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal#export-resource-groups-to-templates) or from the [current state of the deployment](/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal#export-resource-groups-to-templates).
- Use a local [JSON editor (such as VS Code)](/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-the-portal), and then upload and deploy by using PowerShell or the Azure CLI.
- Use the Visual Studio [Azure Resource Group project](/en-us/azure/azure-resource-manager/templates/create-visual-studio-deployment-project) to create and deploy a template.

## Create a user-assigned managed identity

To create a user-assigned managed identity, your account needs the [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment.

To create a user-assigned managed identity, use the following template. Replace the `<USER ASSIGNED IDENTITY NAME>` value with your own values.

Important

When you create user-assigned managed identities, the name must start with a letter or number, and may include a combination of alphanumeric characters, hyphens (-) and underscores (\_). For the assignment to a virtual machine or virtual machine scale set to work properly, the name is limited to 24 characters. For more information, see [FAQs and known issues](known-issues).

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "resourceName": {
          "type": "string",
          "metadata": {
            "description": "<USER ASSIGNED IDENTITY NAME>"
          }
        }
  },
  "resources": [
    {
      "type": "Microsoft.ManagedIdentity/userAssignedIdentities",
      "name": "[parameters('resourceName')]",
      "apiVersion": "2018-11-30",
      "location": "[resourceGroup().location]"
    }
  ],
  "outputs": {
      "identityName": {
          "type": "string",
          "value": "[parameters('resourceName')]"
      }
  }
}
```