---
layout: Conceptual
title: Global Secure Access egress IP ranges - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-egress-ip-ranges
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: global-secure-access
manager: dougeby
description: Reference list of the egress IP ranges that Global Secure Access uses for outbound internet traffic, so you can allowlist them on target services.
ms.topic: reference
ms.date: 2025-08-28T00:00:00.0000000Z
ms.custom: references_regions
ai-usage: ai-assisted
locale: en-us
document_id: ab6ef4eb-fae2-b938-4b45-77aed75b66f6
document_version_independent_id: ab6ef4eb-fae2-b938-4b45-77aed75b66f6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-egress-ip-ranges.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-egress-ip-ranges
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-egress-ip-ranges.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8d5f61e0-e5ba-18cc-39c8-00e8b6f594d9
---

# Global Secure Access egress IP ranges - Global Secure Access | Microsoft Learn

Outbound Internet traffic that is acquired by Global Secure Access, including traffic to Microsoft services, will egress from Global Secure Access instances. If the target service uses IP restrictions and access controls, you may need to configure the target service to allow IP connections from Global Secure Access subnets:

- `128.94.0.0/19`
- `151.206.0.0/16`