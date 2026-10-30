---
layout: Conceptual
title: Manage user-assigned managed identities using the Azure portal - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Manage user-assigned managed identities using the Azure portal.
ms.topic: how-to
ms.date: 2025-09-09T00:00:00.0000000Z
locale: en-us
document_id: fcdcb291-fe1d-e2b9-7f11-228cd4c66ee3
document_version_independent_id: fcdcb291-fe1d-e2b9-7f11-228cd4c66ee3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-portal.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: e8b8bdeb-d9f0-fd9d-e1e6-7b03863cb630
---

# Manage user-assigned managed identities using the Azure portal - Managed identities for Azure resources | Microsoft Learn

Managed identities for Azure resources eliminate the need to manage credentials in code. You can use them to get a Microsoft Entra token for your applications. The applications can use the token when accessing resources that support Microsoft Entra authentication. Azure manages the identity so you don't have to.

There are two types of managed identities: system-assigned and user-assigned. System-assigned managed identities have their lifecycle tied to the resource that created them. This identity is restricted to only one resource, and you can grant permissions to the managed identity by using Azure role-based access control (RBAC). User-assigned managed identities can be used on multiple resources.

In this article, you learn how to create, list, delete, or assign a role to a user-assigned managed identity by using the Azure portal.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview). Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview#managed-identity-types).
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you continue.

## Create a user-assigned managed identity

To create a user-assigned managed identity, your account needs the [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. In the search box, enter **Managed Identities**. Under **Services**, select **Managed Identities**.
3. Select **Add**, and enter values in the following boxes in the **Create User Assigned Managed Identity** pane:

    - **Subscription**: Choose the subscription to create the user-assigned managed identity under.
    - **Resource group**: Choose a resource group to create the user-assigned managed identity in, or select **Create new** to create a new resource group.
    - **Region**: Choose a region to deploy the user-assigned managed identity, for example, **West US**.
    - **Name**: Enter the name for your user-assigned managed identity, for example, UAI1.

    Important

    When you create user-assigned managed identities, the name must start with a letter or number, and may include a combination of alphanumeric characters, hyphens (-) and underscores (\_). For the assignment to a virtual machine or virtual machine scale set to work properly, the name is limited to 24 characters. For more information, see [FAQs and known issues](known-issues).

    ![Screenshot that shows the Create User Assigned Managed Identity pane.](media/how-manage-user-assigned-managed-identities/create-user-assigned-managed-identity-portal.png)
4. Select **Review + create** to review the changes.
5. Select **Create**.

## List user-assigned managed identities

To list or read a user-assigned managed identity, your account needs to have either [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) or [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignments.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. In the search box, enter **Managed Identities**. Under **Services**, select **Managed Identities**.
3. A list of the user-assigned managed identities for your subscription is returned. To see the details of a user-assigned managed identity, select its name.
4. You can now view the details about the managed identity as shown in the image.

    ![Screenshot that shows the list of user-assigned managed identity.](media/how-manage-user-assigned-managed-identities/list-user-assigned-managed-identity-portal.png)

## Delete a user-assigned managed identity

To delete a user-assigned managed identity, your account needs the [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment. Deleting a user-assigned identity doesn't remove it from the resource it was assigned to.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Select the user-assigned managed identity, and select **Delete**.
3. Under the confirmation box, select **Yes**.

    ![Screenshot that shows the Delete user-assigned managed identities.](media/how-manage-user-assigned-managed-identities/delete-user-assigned-managed-identity-portal.png)

## Manage access to user-assigned managed identities

In some environments, administrators choose to limit who can manage user-assigned managed identities. Administrators can implement this limitation using [built-in](/en-us/azure/role-based-access-control/built-in-roles#identity) RBAC roles. You can use these roles to grant a user or group in your organization rights over a user-assigned managed identity.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. In the search box, enter **Managed Identities**. Under **Services**, select **Managed Identities**.
3. A list of the user-assigned managed identities for your subscription is returned. Select the user-assigned managed identity that you want to manage.
4. Select **Access control (IAM)**.
5. Choose **Add role assignment**.

    ![Screenshot that shows the user-assigned managed identity access control screen.](media/how-manage-user-assigned-managed-identities/role-assign.png)
6. In the **Add role assignment** pane, choose the role to assign and choose **Next**.
7. Choose who should have the role assigned.