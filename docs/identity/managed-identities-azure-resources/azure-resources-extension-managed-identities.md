---
layout: Conceptual
title: Use Azure Resources Extension in VS Code for Managed Identities - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/azure-resources-extension-managed-identities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Learn how to use VS Code's Azure Resources extension to manage and configure Azure managed identities directly from your development environment.
ms.date: 2024-06-12T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: arluca
locale: en-us
document_id: d6b10289-bbd9-e663-c5eb-6e5f0f408407
document_version_independent_id: d6b10289-bbd9-e663-c5eb-6e5f0f408407
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/azure-resources-extension-managed-identities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/azure-resources-extension-managed-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/azure-resources-extension-managed-identities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/911a44a7-2f6c-477c-810f-dc8b7d425cce
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/14f2b9d5-6f06-45a8-ac5f-313eaa351153
platformId: f145fdac-7c02-2bee-54cb-8a95b7984e93
---

# Use Azure Resources Extension in VS Code for Managed Identities - Managed identities for Azure resources | Microsoft Learn

The Azure Resources extension for Visual Studio Code provides a powerful interface for managing Azure resources directly from your development environment. The extension offers essential capabilities for developers to inspect, and verify their managed identity configurations. This article focuses on three tasks you can accomplish from within VS Code to ensure your managed identities are properly configured and secure.

## Prerequisites

Before starting, ensure you have:

- Visual Studio Code installed
- Appropriate permissions to view Azure resources
- Access to the Azure subscription containing your managed identities

## Install Azure Resources Extension

To work with managed identities in Visual Studio Code, you need the Azure Resources extension. For more information, see [Azure Resources for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureresourcegroups)

## Create a Managed Identity

You need to have a managed identity created in your Azure subscription. For more information, see [create a managed identity](how-manage-user-assigned-managed-identities).

## Discover managed identity properties (Client ID, Object ID, etc.)

The first step in working with managed identities is understanding their key properties and how to access them from VS Code. Every managed identity has several important properties that your application code needs. For example:

- Client ID: The unique identifier used by your application to request tokens
- Object ID (Principal ID): The unique identifier in Microsoft Entra used for role assignments
- Resource ID: The full Azure resource path for the managed identity
- Tenant ID: The Microsoft Entra tenant where the identity exists

These properties can't be directly viewed in the Azure Resources extension. Use Copilot with the `/@azure` command to retrieve them. Here’s how you can do it:

1. Open the Azure Resources extension in the VS Code sidebar
2. Select your subscription
3. Locate the Managed Identities section. Here. you see all your managed identities that you have access to.
4. Right click on the managed identity of interest and select \*\*Ask @Azure\*\*. This opens a chat with Copilot. It requires you to sign in to your Azure account if you haven't already. Ensure you're using Copilot in agent mode since this is required to access Azure resources.
5. Query for any property you're looking for like `Client ID`, `Object ID`, or `Resource ID`. For example, you can type:

    ```
     /@azure get the Client ID of the managed identity named "myManagedIdentity"
    ```

## Confirm source resources using a managed identity

Managed identities can be used as an identity for various Azure resources, such as virtual machines, app services, and more. To confirm which resources are using a specific managed identity, you can check the target services associated with that identity.

1. Open the Azure Resources extension in the VS Code sidebar
2. Select your subscription
3. Locate the Managed Identities section. Here. you see all your managed identities that you have access to.
4. Select a managed identity then select **Source Resources**.
5. All resources using the managed identity are listed here.

## Confirm managed identity assignment to target resource

Managed identities can be assigned to various Azure resources. You can check the resources to which a managed identity is assigned directly from the Azure Resources extension in Visual Studio Code. This is useful for ensuring that your managed identity is correctly configured for the resources it needs to access.

1. Open the Azure Resources extension in the VS Code sidebar
2. Select your subscription
3. Locate the Managed Identities section. Here. you see all your managed identities that you have access to.
4. Select a managed identity then select **Target Services**.
5. All resources that the managed identity is assigned to are listed here.

## Confirm managed identity permissions for a target resource

Permissions are managed through Azure Role-Based Access Control (RBAC), which allows you to assign roles to your managed identity for specific resources.

Follow these steps to confirm the permissions of your managed identity:

1. Open the Azure Resources extension in the VS Code sidebar
2. Select your subscription
3. Locate the Managed Identities section. Here, you see all your managed identities that you have access to.
4. Select a managed identity then select **Target Services**. All resources that the managed identity is assigned to will be listed here.
5. Select a target resource to view its permissions