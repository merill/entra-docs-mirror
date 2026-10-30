---
layout: Conceptual
title: Multi-Geo for Microsoft Entra Private Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-enable-multi-geo
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to enable Multi-Geo Capability for Microsoft Entra Private Access to optimize traffic flow from Microsoft Entra Clients to Microsoft Entra Apps.
ms.topic: how-to
ms.date: 2025-08-18T00:00:00.0000000Z
ms.reviewer: katabish
locale: en-us
document_id: 8723573a-5011-146e-b503-e02b07dd0af9
document_version_independent_id: 8723573a-5011-146e-b503-e02b07dd0af9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-enable-multi-geo.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-enable-multi-geo
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-enable-multi-geo.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: d8517683-f08c-0798-8e79-c12cf13efde2
---

# Multi-Geo for Microsoft Entra Private Access - Global Secure Access | Microsoft Learn

Multi-Geo capability can help optimize the traffic flow from Microsoft Entra clients to Microsoft Entra apps through private access. This article explains how to enable the multi-Geo capability for Microsoft Entra Private Access.

## Prerequisites

- You must have a Microsoft Entra Private Access license.
- You must have a Microsoft Entra Private Access connector group. For more information, see [How to configure private network connectors for Microsoft Entra Private Access and Microsoft Entra application proxy](how-to-configure-connectors).
- You must have the **Global Secure Access Administrator** role or the **Privileged Role Administrator** role. For more information, see [Microsoft Entra Built-in Roles](../identity/role-based-access-control/permissions-reference).

## Overview

Multi-Geo capability helps optimize traffic flow from Microsoft Entra clients to Microsoft Entra apps through private access. Currently, the tenant's default geo location determines the Microsoft Entra routing for private access. For instance, if a tenant's default region is North America, all connector groups must connect to the Microsoft Entra backend in North America, even if some applications and connector groups are in different regions. Multi-Geo support lets customers optimize traffic flow by assigning connector groups according to their preferred geo locations instead of relying solely on the tenant's geo location. Each connector group connects to the SSE backend in the selected area, enhancing overall efficiency. This arrangement provides customers with the flexibility to direct connections to the SSE backend of their choice.

![Diagram that illustrates how Multi-Geo support routes traffic with Microsoft Entra private network connectors.](media/how-to-enable-multi-geo/multi-geo-support-diagram.svg)

## Enable multi-Geo capability

To enable the multi-Geo capability for Microsoft Entra Private Access, complete the following steps. This procedure involves creating connector group in different geographic region, installing connectors, and adding application segments to the connector group.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Applications** &gt; **Enterprise applications** &gt; **Private Network connectors**.
3. Create a connector group, associate it with a geographic region of your choice.
    1. Select **+ New Connector Group**.
    2. In the **New Connector Group** pane, enter a name for the connector group.
    3. Under Advanced settings, select the optimized **country/region** for the connector group. The region you select determines the backend that the connector group connects to.
4. Install a connector. The connector installation require working with an admin in the associated region. For more information, see [How to configure private network connectors for Microsoft Entra Private Access and Microsoft Entra application proxy](how-to-configure-connectors).
5. Add an application segment to the connector group.
    1. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications** &gt; **Network access properties**.
    2. Select **+ Add application segment**.
    3. Select the application segment you want to add to the connector group.
    4. Select **Save**.
6. After about 30 minutes, the multi-Geo configuration takes effect and traffic begins flowing.

Note

- Multi-Geo connectors aren't available through Quick Access. Multi-Geo supports only private enterprise apps.
- Multi-Geo doesn't support the Domain Name System (DNS) experience.
- Multi-Geo doesn't support Japan region selection through Microsoft Entra admin center.