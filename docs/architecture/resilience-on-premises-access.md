---
layout: Conceptual
title: Build resilience in application access with Application Proxy - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-on-premises-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: A guide for architects and IT administrators on using Application Proxy for resilient access to on-premises applications
ms.topic: concept-article
ms.date: 2022-11-16T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: e6aaa189-7c4a-cf86-04c4-31fa73b14e6f
document_version_independent_id: 5ee47a3b-921c-3ddf-6946-b8a3ce4f7882
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-on-premises-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-on-premises-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-on-premises-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 008d2d9a-ebc4-b879-56c7-0f9969b2ee30
---

# Build resilience in application access with Application Proxy - Microsoft Entra | Microsoft Learn

Application Proxy is a feature of Microsoft Entra ID that enables users to access on premises web applications from a remote client. Application Proxy includes the Application Proxy service in the cloud and the private network connectors that run on an on-premises server.

Users access on premises resources through a URL published via Application Proxy. They're redirected to the Microsoft Entra sign-in page. The Application Proxy service in Microsoft Entra ID then sends a token to the private network connector in the corporate network that passes the token to the on-premises Active Directory. The authenticated user can then access the on-premises resource. In the diagram below, [connectors](../global-secure-access/concept-connectors) are shown in a [connector group](../global-secure-access/concept-connector-groups).

Important

When you publish your applications via Application Proxy, you must implement [capacity planning and appropriate redundancy for the private network connectors](../global-secure-access/concept-connectors#specifications-and-sizing-requirements).

![Architecture diagram of Application y](media/resilience-on-prem-access/admin-resilience-app-proxy.png))

## How do I implement Application Proxy?

To implement remote access with Microsoft Entra application proxy, see the following resources.

- [Planning an Application Proxy deployment](../identity/app-proxy/conceptual-deployment-plan)
- [High availability and load balancing best practices](../identity/app-proxy/application-proxy-high-availability-load-balancing)
- [Configure proxy servers](../identity/app-proxy/application-proxy-configure-connectors-with-proxy-servers)
- [Design a resilient access control strategy](../identity/authentication/concept-resilient-controls)