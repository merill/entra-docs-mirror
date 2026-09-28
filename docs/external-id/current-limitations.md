---
layout: Conceptual
title: Limitations of B2B collaboration - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/current-limitations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Current limitations for Microsoft Entra B2B collaboration
ms.topic: concept-article
ms.date: 2026-04-24T00:00:00.0000000Z
ms.collection: content-health, M365-identity-device-management
ai-usage: ai-assisted
locale: en-us
document_id: 7476784f-6f44-8aab-3d08-2c813a4e0422
document_version_independent_id: 894d5b3a-a96d-d6c1-d72a-a532191dd5db
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/current-limitations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/current-limitations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/current-limitations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 46cde8ee-8199-d2d2-0cab-45a588d0d3e1
---

# Limitations of B2B collaboration - Microsoft Entra External ID | Microsoft Learn

Microsoft Entra B2B collaboration is currently subject to the limitations described in this article.

## Possible double multifactor authentication

With Microsoft Entra B2B, you can enforce multifactor authentication at the resource organization (the inviting organization). The reasons for this approach are detailed in [Conditional Access for B2B collaboration users](authentication-conditional-access). If a partner already has multifactor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.

## Instant-on

In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on. The updates and writes ordinarily happen in one directory instance and must be replicated across all instances. Replication is completed once all instances are updated. Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur. If that happens, refresh or retry to help. If you're writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.

## Microsoft Entra directories

Microsoft Entra B2B is subject to Microsoft Entra service directory limits. For details about the number of directories a user can create and the number of directories to which a user or guest user can belong, see [Microsoft Entra service limits and restrictions](../identity/users/directory-service-limits-restrictions).