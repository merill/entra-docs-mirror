---
layout: Conceptual
title: Enhance Remote Network Resilience with Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/remote-network-resilience
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: This article provides techniques to improve remote network resilience with Global Secure Access.
ms.topic: best-practice
ms.date: 2025-09-02T00:00:00.0000000Z
ms.reviewer: abhijeetsinha
ai-usage: ai-assisted
locale: en-us
document_id: e0056d85-f30b-9d3c-4d0e-382169a46c52
document_version_independent_id: e0056d85-f30b-9d3c-4d0e-382169a46c52
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/remote-network-resilience.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/remote-network-resilience
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/remote-network-resilience.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c5ea9623-391b-a19d-9a9f-6d750e5343c1
---

# Enhance Remote Network Resilience with Global Secure Access - Global Secure Access | Microsoft Learn

This article provides actionable recommendations to enhance the resilience of remote networks. To ensure optimal deployment and performance of Global Secure Access remote network connectivity, follow these best practices:

## Configure redundant tunnels and failovers

Configure multiple Internet Protocol Security (IPsec) tunnels from the customer premises equipment (CPE) to different Global Secure Access edges or POPs.

### Zone redundancy

The **Zone redundancy** option creates two IPsec tunnels in different availability zones, but within the same Azure region.

![Screenshot of the Connectivity step, with the Add a link pane showing the Zone redundancy menu option.](media/remote-network-resilience/zone-redundancy.png)

### Geographic redundancy

You can also achieve redundancy by creating a new remote network in a different geographic region. You can use the same CPE configuration to set up IPsec tunnels in the secondary remote network.

![Screenshot of the list of remote networks in multiple geographic regions.](media/remote-network-resilience/geographic-redundancy.png)

Use the CPE's management console to assign weights to these IPsec tunnels and decide how to route traffic through them.

| Tunnel weighting | Traffic routing |
| --- | --- |
| Equal split | active-active |
| Primary/secondary | active-standby |

### Dynamic route learning

Use Border Gateway Protocol (BGP) for dynamic route learning. If BGP isn't supported on the device, set up static routes with appropriate metrics.

## Set up CPE according to your desired security posture

Configure CPE based on whether your business prioritizes security or productivity.

### Prioritize security

If you prioritize security, prevent user traffic from going to the destination without first going through Global Secure Access. To do so, statically route traffic over the IPsec tunnel with Global Secure Access without setting up the default route.

### Prioritize productivity

If you prioritize productivity, set up a default route for traffic. This way, if a Global Secure Access VPN gateway or backend service goes down, user traffic continues directly through the default route.

Important

**Recommendation**: Set up a default route and configure an IP SLA Layer 7 health probe to monitor the endpoint.

To set up a default route:

1. Configure an IP SLA Layer 7 health probe to monitor the endpoint `http://m365.remote-network.edgediagnostic.globalsecureaccess.microsoft.com:6544/ping`. For guidance, see [How to create a remote network with Global Secure Access](how-to-create-remote-networks).
2. Alternatively, set the probe to monitor IP address `198.18.1.101`. Statically send these IP addresses over the Global Secure Access IPsec tunnel from your CPE. We're adding this IP address to the Microsoft 365 BGP route advertisement.

Note

These endpoints are accessible only through Global Secure Access remote network connectivity.

## Configure monitoring and observability

Monitor traffic logs and remote network health events by exporting them to your Log Analytics workspace. Set up Azure Monitor alert rules to track the health of your workspace. For more information, see [What are remote network health logs?](how-to-remote-network-health-logs).