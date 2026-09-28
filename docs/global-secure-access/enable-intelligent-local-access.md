---
layout: Conceptual
title: Enable Intelligent Local Network - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/enable-intelligent-local-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to enable the Intelligent Local Access (ILA) capability for Microsoft Entra Private Access, which optimizes traffic flow for clients accessing Entra apps via private networks.
ms.topic: how-to
ms.date: 2026-06-03T00:00:00.0000000Z
ms.reviewer: dhruvinshah
ai-usage: ai-assisted
locale: en-us
document_id: 9689060e-96b9-eb3a-933e-bd0d280c71a3
document_version_independent_id: 9689060e-96b9-eb3a-933e-bd0d280c71a3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/enable-intelligent-local-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/enable-intelligent-local-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/enable-intelligent-local-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 1cc14159-50b5-0c8e-cb77-294d3e924bb0
---

# Enable Intelligent Local Network - Global Secure Access | Microsoft Learn

Intelligent Local Access capability can help optimize the traffic flow from Microsoft Entra clients to Microsoft Entra Private Access apps when the client is on a corporate/private network. This article explains how to enable the Intelligent Private Network for Microsoft Entra Private Access.

## Prerequisites

To configure a Global Secure Access (GSA) Private Networks, you must have:

- [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role or the [Privileged Role Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#privileged-role-administrator) role.
- Product licensing. For details, see the licensing section of [What is Global Secure Access](/en-us/entra/global-secure-access/overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## Private Access overview

Today, Entra Private Access (PA) sends all traffic, both application and authentication, over the SSE / Private Access service, regardless of the user's location. This process, represented by the green workflow in the following diagram, results in network backhauling, which negatively impacts user experience by adding latency and slowing down the network significantly. With the Intelligent Local Access (ILA) feature, we aim to address this issue by enabling intelligent network routing. The GSA client determines how traffic is routed to private applications. This feature ensures a consistent security posture for employees, whether they work remote or on-premises. This adaptive local access significantly improves user experience by reducing latency and avoiding network hair pinning, represented by the blue workflow in the following diagram.

[![A diagram showing the workflow between Microsoft Entra Private Access and Intelligent Local Access.](media/enable-intelligent-local-access/microsoft-entra-private-access-intelligent-local-access-workflow.png)](media/enable-intelligent-local-access/microsoft-entra-private-access-intelligent-local-access-workflow.png#lightbox)

The GSA client uses DNS probes to determine if the client is inside the corporate network. Once the client identifies corpnet locations, you can define which Private Access applications should use ILA and bypass the traffic instead of sending it through the cloud backend

## Enable Intelligent local access capability

To enable the Intelligent local access for Microsoft Entra Private Access, complete these steps. This procedure involves creating Private networks and adding application to the private network.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Browse to **Global Secure Access** **&gt; Connect &gt; Private networks**.
3. Select **Add Private network**.

[![A screenshot showing the UI screen where you can add a private network.](media/enable-intelligent-local-access/add-private-network.png)](media/enable-intelligent-local-access/add-private-network.png#lightbox)

1. In the **Add Private network** panel that opens, define following:

    1. Name - The friendly name of the network.
    2. DNS Servers - Server address used for DNS resolution.

        1. Internet Protocol version 4 (IPv4) address, such as 10.10.2.1, that identifies a DNS server on the network.
    3. Fully qualified domain name

        1. The fully qualified domain name (FQDN) that needs to be resolved.
    4. Enter the appropriate details for the selected Resolved to IP address type. Depending on what you select, fill in an appropriate value in the subsequent field **Resolved to IP address value**.

| Resolved to IP address type | Resolved to IP address value |
| --- | --- |
| **IP address** | Internet Protocol version 4 (IPv4) address, such as 10.10.2.1, that identifies a device on the network. |
| **IP address range (CIDR)** | Classless Inter-Domain Routing (CIDR) represents a range of IP addresses where an IP address is followed by a suffix that indicates the number of network bits in the subnet mask.For example, 10.10.2.0/24 indicates that the first 24 bits of the IP address represent the network address, while the remaining 8 bits represents the host address.Provide the starting address and network mask. |
| **IP address range (IP to IP)** | Range of IP addresses from start IP (such as 10.10.2.1) to end IP (such as 10.10.2.10).Provide the IP address start and end. |

1. Select **Target Resource**.

    1. Select Quick Access or PA enterprise app which is locally bypassed when this private network is detected.
2. Select **Create**.

[![A screenshot of the page where you create a private network.](media/enable-intelligent-local-access/create-private-network.png)](media/enable-intelligent-local-access/create-private-network.png#lightbox)

## Best practices

Keep the number of Private networks to a minimum. A Private network identifies that a client is connected to a specific network. It isn't intended to indicate whether an individual application is accessible within that network.

In this context, a network doesn't necessarily refer to a single, restricted physical network. It can represent a logical network that consists of multiple physical networks where the same applications are accessible.

Create a single Private network definition for each logical network. Then assign all Private Access applications that are accessible from that network to that Private network.

## Verify ILA flow on the client

You can use the advanced diagnostic client in Global Secure Access to monitor the ILA network traffic.

Open **Advanced diagnostics** for client.

1. Select **Start Collecting** Network traffic.
2. Filter by Destination IP/FQDN for the end resource.
3. Ensure the default filter for **Action == Tunnel** is removed. [![A screenshot of the Global Secure Access Advanced Diagnostics page showing Network traffic details.](media/enable-intelligent-local-access/advanced-diagnostics-network-traffic.png)](media/enable-intelligent-local-access/advanced-diagnostics-network-traffic.png#lightbox)
4. Access the application.
5. Verify that the Connection Status is **Bypassed** and that Action is **Local** in the Network Traffic. [![A screenshot of the Global Secure Access Advanced Diagnostics page showing Network traffic status and settings.](media/enable-intelligent-local-access/network-traffic-connection-status-and-action-settings.png)](media/enable-intelligent-local-access/network-traffic-connection-status-and-action-settings.png#lightbox)

## Related links

[Understand Private Access](concept-private-access)