---
layout: Conceptual
title: Introduction to securing Microsoft Entra service accounts - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/secure-service-accounts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Explanation of the types of service accounts available in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2022-08-26T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 728ac12a-72de-2462-10a0-90e2c385b1bd
document_version_independent_id: 5f911831-f5d2-6d02-577b-b1b951a27f6e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/secure-service-accounts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/secure-service-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/secure-service-accounts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1e452a0d-6422-0362-ef2a-d17a7be5ac26
---

# Introduction to securing Microsoft Entra service accounts - Microsoft Entra | Microsoft Learn

There are three types of service accounts native to Microsoft Entra ID: Managed identities, service principals, and user-based service accounts. Service accounts are a special type of account that is intended to represent a non-human entity such as an application, API, or other service. These entities operate within the security context provided by the service account.

## Types of Microsoft Entra service accounts

For services hosted in Azure, we recommend using a managed identity if possible, and a service principal if not. Managed identities can't be used for services hosted outside of Azure. In that case, we recommend a service principal. If you can use a managed identity or a service principal, do so. We recommend that you not use a Microsoft Entra user account as a service account. See the following table for a summary.

| Service hosting | Managed identity | Service principal | Azure user account |
| --- | --- | --- | --- |
| Service is hosted in Azure. | Yes. Recommended if the service supports a Managed Identity. | Yes. | Not recommended. |
| Service is not hosted in Azure. | No | Yes. Recommended. | Not recommended. |
| Service is multi-tenant | No | Yes. Recommended. | No. |

## Managed identities

Managed identities are secure Microsoft Entra identities created to provide identities for Azure resources. There are [two types of managed identities](../identity/managed-identities-azure-resources/overview#managed-identity-types):

- System-assigned managed identities can be assigned directly to an instance of a service.
- User-assigned managed identities can be created as a standalone resource.

For more information, see [Securing managed identities](service-accounts-managed-identities). For general information about managed identities, see [What are managed identities for Azure resources?](../identity/managed-identities-azure-resources/overview)

## Service principals

If you can't use a managed identity to represent your application, use a service principal. Service principals can be used with both single tenant and multi-tenant applications.

A service principal is the local representation of an application object in a single Microsoft Entra tenant. It functions as the identity of the application instance, defines who can access the application, and what resources the application can access. A service principal is created in (local to) each tenant where the application is used and references the globally unique application object. The tenant secures the service principal's sign-in and access to resources.

There are two mechanisms for authentication using service principals—client certificates and client secrets. Certificates are more secure: use client certificates if possible. Unlike client secrets, client certificates cannot accidentally be embedded in code.

For information on securing service principals, see [Securing service principals](service-accounts-principal).