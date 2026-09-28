---
layout: Conceptual
title: What is the provisioning agent? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/what-is-provisioning-agent
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes the provisioning agent used by cloud sync and on-premsises app provisioning.
ms.topic: concept-article
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: dfbf66e6-b470-d955-ef22-99ce8f6cf50e
document_version_independent_id: 5fa44e03-4e5f-41cf-134f-43750739c4e2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/what-is-provisioning-agent.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/what-is-provisioning-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/what-is-provisioning-agent.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4ac2d27e-d4d3-646a-d376-0995141ff373
---

# What is the provisioning agent? - Microsoft Entra ID | Microsoft Learn

The provisioning agent is the synchronization tool that is used to deliver several features for use with Microsoft Entra ID and is managed from the cloud.

The provisioning agent provides connectivity between Microsoft Entra ID and your on-premises environment.

These features include:

- cloud sync
- on-premises app provisioning

## How it works

The provisioning agent uses SCIM ([System for Cross-domain Identity Management (SCIM) 2.0](https://techcommunity.microsoft.com/t5/identity-standards-blog/provisioning-with-scim-getting-started/ba-p/880010)). The SCIM specification provides a common user schema to help users move into, out of, and around apps. SCIM is becoming the de facto standard for provisioning and, when used in conjunction with federation standards like SAML or OpenID Connect, provides administrators an end-to-end standards-based solution for access management.