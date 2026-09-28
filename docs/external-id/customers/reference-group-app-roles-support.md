---
layout: Conceptual
title: Groups and app roles support in external tenants - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/reference-group-app-roles-support
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Find out which core Microsoft Entra features related to the user and group management model and application assignment are available in external tenants.
ms.topic: reference
ms.date: 2023-05-01T00:00:00.0000000Z
ms.custom: it-pro, sfi-ga-nochange
locale: en-us
document_id: 14e5e2e3-712e-79f5-e13c-9b5371941ef1
document_version_independent_id: 12b45a3f-c5ef-bf59-1153-a3d9ae579e0f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/reference-group-app-roles-support.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/reference-group-app-roles-support
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/reference-group-app-roles-support.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 093ff550-24b3-aa1e-de37-904567eaafbe
---

# Groups and app roles support in external tenants - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

An external tenant follows the Microsoft Entra user and group management model and application assignment. Many of the core Microsoft Entra features are being phased into external tenants. The following table shows which features are currently available.

| **Feature** | **Currently available?** |
| --- | --- |
| Create an application role for a resource | Yes, by modifying the application manifest |
| Assign an application role to users | Yes |
| Assign an application role to groups | Yes, via Microsoft Graph only |
| Assign an application role to applications | Yes, via application permissions |
| Assign a user to an application role | Yes |
| Assign an application to an application role (application permission) | Yes |
| Add a group to an application/service principal (groups claim) | Yes, via Microsoft Graph only |
| Create/update/delete a customer (local user) via the Microsoft Entra admin center | Yes |
| Reset a password for a customer (local user) via the Microsoft Entra admin center | Yes |
| Create/update/delete a customer (local user) via Microsoft Graph | Yes |
| Reset a password for a customer (local user) via Microsoft Graph | Yes, only if the service principal is added to the Global Administrator role |
| Create/update/delete a security group via the Microsoft Entra admin center | Yes |
| Create/update/delete a security group via the Microsoft Graph API | Yes |
| Change security group members using the Microsoft Entra admin center | Yes |
| Change security group members using the Microsoft Graph API | Yes |