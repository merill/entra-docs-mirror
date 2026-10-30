---
layout: Conceptual
title: What is hybrid identity with Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/whatis-hybrid-identity
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Hybrid identity is having a common user identity for authentication and authorization both on-premises and in the cloud.
keywords: introduction to Azure AD Connect, Azure AD Connect overview, what is Azure AD Connect, install active directory
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.topic: overview
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
locale: en-us
document_id: 17b3fb25-936b-0ef1-9423-608c0a2364c5
document_version_independent_id: 42126028-d632-ed78-a8d3-c52758503ed2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/whatis-hybrid-identity.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/whatis-hybrid-identity
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/whatis-hybrid-identity.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bc301a58-70ae-185c-44b8-ff7707ae3f01
---

# What is hybrid identity with Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn

Today, businesses, and corporations are increasingly deploying a combination of on-premises and cloud applications. Users require access to those applications both on-premises and in the cloud. Managing users both on-premises and in the cloud poses challenging scenarios.

Microsoft’s identity solutions span on-premises and cloud-based capabilities. These solutions create a common user identity for authentication and authorization to all resources, regardless of location. We call this **hybrid identity**.

[![Diagram of new hybrid scenario.](media/common-scenarios/scenario-1.png)](media/common-scenarios/scenario-1.png#lightbox)

Hybrid identity is accomplished through provisioning and synchronization. Provisioning is the process of creating an object based on certain conditions, keeping the object up to date and deleting the object when conditions are no longer met. Synchronization is responsible for making sure identity information for your on-premises users and groups is matching the cloud.

For more information, see [What is provisioning?](what-is-provisioning) and [What is inter-directory provisioning?](what-is-inter-directory-provisioning).

## License requirements for using Microsoft Entra Connect

Using this feature is free and included in your Azure subscription.