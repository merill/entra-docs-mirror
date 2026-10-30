---
layout: Conceptual
title: Manage user-assigned managed identities using REST - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-rest
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Manage user-assigned managed identities using REST.
ms.topic: how-to
ms.date: 2025-09-09T00:00:00.0000000Z
locale: en-us
document_id: 353f3d72-5a56-d23c-405c-88a9668ec220
document_version_independent_id: 353f3d72-5a56-d23c-405c-88a9668ec220
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-rest.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-rest
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-rest.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b3737ff6-a4df-5786-b241-816345c3dd43
---

# Manage user-assigned managed identities using REST - Managed identities for Azure resources | Microsoft Learn

Managed identities for Azure resources eliminate the need to manage credentials in code. You can use them to get a Microsoft Entra token for your applications. The applications can use the token when accessing resources that support Microsoft Entra authentication. Azure manages the identity so you don't have to.

There are two types of managed identities: system-assigned and user-assigned. System-assigned managed identities have their lifecycle tied to the resource that created them. This identity is restricted to only one resource, and you can grant permissions to the managed identity by using Azure role-based access control (RBAC). User-assigned managed identities can be used on multiple resources.

In this article, you learn how to create, list, and delete a user-assigned managed identity by using REST.

## Prerequisites

- If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview). *Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview#managed-identity-types)*.
- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you continue.
- You can run all the commands in this article either in the cloud or locally:
    - To run in the cloud, use [Azure Cloud Shell](/en-us/azure/cloud-shell/overview).
    - To run locally, install [curl](https://curl.se/download.html) and the [Azure CLI](/en-us/cli/azure/install-azure-cli).

## Obtain a bearer access token

1. If you're running locally, sign in to Azure through the Azure CLI.

    ```azurecli
    az login
    ```
2. Obtain an access token by using [az account get-access-token](/en-us/cli/azure/account#az-account-get-access-token).

    ```azurecli
    az account get-access-token
    ```

## Create a user-assigned managed identity

To create a user-assigned managed identity, your account needs the [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment.

Important

When you create user-assigned managed identities, the name must start with a letter or number, and may include a combination of alphanumeric characters, hyphens (-) and underscores (\_). For the assignment to a virtual machine or virtual machine scale set to work properly, the name is limited to 24 characters. For more information, see [FAQs and known issues](known-issues).

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroup
s/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>?api-version=2015-08-31-preview' -X PUT -d '{"location": "<LOCATION>"}' -H "Content-Type: application/json" -H "Authorization: Bearer <ACCESS TOKEN>"
```

```HTTP
PUT https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroup
s/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>?api-version=2015-08-31-preview HTTP/1.1
```

**Request headers**

| Request header | Description |
| --- | --- |
| *Content-Type* | Required. Set to `application/json`. |
| *Authorization* | Required. Set to a valid `Bearer` access token. |

**Request body**

| Name | Description |
| --- | --- |
| Location | Required. Resource location. |

## List user-assigned managed identities

To list or read a user-assigned managed identity, your account needs the [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) or [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment.

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities?api-version=2015-08-31-preview' -H "Authorization: Bearer <ACCESS TOKEN>"
```

```HTTP
GET https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities?api-version=2015-08-31-preview HTTP/1.1
```

| Request header | Description |
| --- | --- |
| *Content-Type* | Required. Set to `application/json`. |
| *Authorization* | Required. Set to a valid `Bearer` access token. |

## Delete a user-assigned managed identity

To delete a user-assigned managed identity, your account needs the [Managed Identity Contributor](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role assignment.

Deleting a user-assigned managed identity won't remove the reference from any resource it was assigned to.

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroup
s/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>?api-version=2015-08-31-preview' -X DELETE -H "Authorization: Bearer <ACCESS TOKEN>"
```

```HTTP
DELETE https://management.azure.com/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/TestRG/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>?api-version=2015-08-31-preview HTTP/1.1
```

| Request header | Description |
| --- | --- |
| *Content-Type* | Required. Set to `application/json`. |
| *Authorization* | Required. Set to a valid `Bearer` access token. |