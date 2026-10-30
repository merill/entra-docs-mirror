---
layout: Conceptual
title: Securing managed identities in Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/service-accounts-managed-identities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn to find, assess, and increase the security of managed identities in Microsoft Entra ID
ms.topic: how-to
ms.date: 2023-02-07T00:00:00.0000000Z
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
ms.subservice: architecture
locale: en-us
document_id: 91b207a2-4b94-98ae-28b6-374ac4261762
document_version_independent_id: e7363e79-07d2-49cd-13b9-973a24a2e4f6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/service-accounts-managed-identities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/service-accounts-managed-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/service-accounts-managed-identities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0653474e-5e85-9bef-321c-baf1258187db
---

# Securing managed identities in Microsoft Entra ID - Microsoft Entra | Microsoft Learn

In this article, learn about managing secrets and credentials to secure communication between services. Managed identities provide an automatically managed identity in Microsoft Entra ID. Applications use managed identities to connect to resources that support Microsoft Entra authentication, and to obtain Microsoft Entra tokens, without credentials management.

## Benefits of managed identities

Benefits of using managed identities:

- With managed identities, credentials are fully managed, rotated, and protected by Azure. Identities are provided and deleted with Azure resources. Managed identities enable Azure resources to communicate with services that support Microsoft Entra authentication.
- No one, including those assigned privileged roles, have access to the credentials, which can't be accidentally leaked by being included in code.

## Using managed identities

Managed identities are best for communications among services that support Microsoft Entra authentication. A source system requests access to a target service. Any Azure resource can be a source system. For example, an Azure virtual machine (VM), Azure Function instance, and Azure App Services instances support managed identities.

Learn more in the video, [What can a managed identity be used for?](https://www.youtube.com/embed/5lqayO_oeEo)

### Authentication and authorization

With managed identities, the source system obtains a token from Microsoft Entra ID without owner credential management. Azure manages the credentials. Tokens obtained by the source system are presented to the target system for authentication.

The target system authenticates and authorizes the source system to allow access. If the target service supports Microsoft Entra authentication, it accepts an access token issued by Microsoft Entra ID.

Azure has a control plane and a data plane. You create resources in the control plane, and access them in the data plane. For example, you create an Azure Cosmos DB database in the control plane, but query it in the data plane.

After the target system accepts the token for authentication, it supports mechanisms for authorization for its control plane and data plane.

Azure control plane operations are managed by Azure Resource Manager and use Azure role-based access control (Azure RBAC). In the data plane, target systems have authorization mechanisms. Azure Storage supports Azure RBAC on the data plane. For example, applications using Azure App Services can read data from Azure Storage, and applications using Azure Kubernetes Service can read secrets stored in Azure Key Vault.

Learn more:

- [What is Azure Resource Manager?](/en-us/azure/azure-resource-manager/management/overview)
- [What is Azure role-based Azure RBAC?](/en-us/azure/role-based-access-control/overview)
- [Azure control plane and data plane](/en-us/azure/azure-resource-manager/management/control-plane-and-data-plane)
- [Azure services that can use managed identities to access other services](../identity/managed-identities-azure-resources/managed-identities-status)

## System-assigned and user-assigned managed identities

There are two types of managed identities, system- and user-assigned.

System-assigned managed identity:

- One-to-one relationship with the Azure resource
    - For example, there's a unique managed identity associated with each VM
- Tied to the Azure resource lifecycle. When the resource is deleted, the managed identity associated with it, is automatically deleted.
- This action eliminates the risk from orphaned accounts

User-assigned managed identity

- The lifecycle is independent from an Azure resource. You manage the lifecycle.
    - When the Azure resource is deleted, the assigned user-assigned managed identity isn't automatically deleted
- Assign user-assigned managed identity to zero or more Azure resources
- Create an identity ahead of time, and then assigned it to a resource later

## Find managed identity service principals in Microsoft Entra ID

To find managed identities, you can use:

- Enterprise applications page in the Azure portal
- Microsoft Graph

### The Azure portal

1. In the Azure portal, in the left navigation, select **Microsoft Entra ID**.
2. In the left navigation, select **Enterprise applications**.
3. In the **Application type** column, under **Value**, select the down-arrow to select **Managed Identities**.

    ![Screenshot of the Managed Identities option under Values, in the Application type column.](media/govern-service-accounts/service-accounts-managed-identities.png)

### Microsoft Graph

Use the following GET request to Microsoft Graph to get a list of managed identities in your tenant.

`https://graph.microsoft.com/v1.0/servicePrincipals?$filter=(servicePrincipalType eq 'ManagedIdentity')`

You can filter these requests. For more information, see [GET servicePrincipal](/en-us/graph/api/serviceprincipal-get?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true).

## Assess managed identity security

To assess managed identity security:

- Examine privileges to ensure the least-privileged model is selected

    - Use the following Microsoft Graph cmdlet to get the permissions assigned to your managed identities:

    `Get-MgServicePrincipalAppRoleAssignment -ServicePrincipalId <String>`
- Ensure the managed identity is not part of a privileged group, such as an administrators group.

    - To enumerate the members of your highly privileged groups with Microsoft Graph:

    `Get-MgGroupMember -GroupId <String> [-All <Boolean>] [-Top <Int32>] [<CommonParameters>]`

## Move to managed identities

If you're using a service principal or a Microsoft Entra user account, evaluate the use of managed identities. You can eliminate the need to protect, rotate, and manage credentials.