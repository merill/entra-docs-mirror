---
layout: Conceptual
title: How to configure routers for remote networks - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-customer-premises-equipment
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure the connectivity between your customer premises equipment and the Global Secure Access network.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0287f97f-6a32-c6a5-f65c-b0566662c770
document_version_independent_id: 5a318e5b-af36-c848-3a91-170acd992f98
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-configure-customer-premises-equipment.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-configure-customer-premises-equipment
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-configure-customer-premises-equipment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 85140613-b067-613d-8086-f9b1852b2ca0
---

# How to configure routers for remote networks - Global Secure Access | Microsoft Learn

## Overview

IPSec tunnel is a bidirectional communication. One side of the communication is established when [adding a device link to a remote network](how-to-manage-remote-network-device-links) in Global Secure Access. During that process, you enter your public IP address and border gateway protocol (BGP) addresses in the Microsoft Entra admin center to tell us about your network configurations.

This article provides the steps to set up the other side of the communication channel.

## Prerequisites

To configure your customer premises equipment (CPE), you must have:

- A **Global Secure Access Administrator** role in Microsoft Entra ID.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).
- To configure your CPE, you must have completed the Global Secure Access onboarding process.

## How to configure your customer premises equipment

You can set up the CPE using the Microsoft Entra admin center or using the Microsoft Graph API. When you create a remote network and add your device link information, configuration details are generated. These details are needed to configure your CPE.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a **Global Secure Access Administrator**.
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**.
3. Select **View configuration** for the remote network you need to configure.

    [![Screenshot of the configuration details with the Microsoft information highlighted.](media/how-to-configure-customer-premises-equipment/remote-network-view-configuration.png)](media/how-to-configure-customer-premises-equipment/remote-network-view-configuration.png#lightbox)
4. Locate and save Microsoft's public IP address `endpoint` from the panel that opens.

    ![Screenshot that shows the view configuration details panel.](media/how-to-configure-customer-premises-equipment/view-configuration-details-panel.png)
5. In the preferred interface for *your CPE*, enter the IP address you saved in the previous step. This step completes the IPSec tunnel configuration.

The following diagram highlights each of the major sections of the device configuration details. Text descriptions of each section follow the diagram.

[![Diagram of the configuration details with each section highlighted.](media/how-to-configure-customer-premises-equipment/device-configuration-map.png)](media/how-to-configure-customer-premises-equipment/device-configuration-map-expanded.png#lightbox)

- The `branchId` and `branchName` represent the remote network details.
- The `displayName` is the device link name.
- The `endpoint`, `asn`, `bgpAddress`, and `region` represent the Microsoft connectivity details. Enter these details on your CPE.
- For zone redundant device links, a second set of details are generated.
- `PeerConfiguration` and the subsequent details represent the CPE connectivity details.
- If you've configured more devices, their details follow.

Important

The crypto profile you specified for the device link should match with what you specify on your CPE. If you chose the "default" IKE policy when configuring the device link, use the configurations described in the **[Remote network configurations](reference-remote-network-configurations)** article.

# [Microsoft Graph API](#tab/microsoft-graph-api)
Follow these instructions to download the connectivity information for your remote network.

1. Sign in to [Graph Explorer](https://aka.ms/ge).
2. Select **GET** as the HTTP method from the dropdown.
3. Set the API version to **beta**.
4. Run the following query to list your remote networks and their device links:

    ```http
    GET https://graph.microsoft.com/beta/networkaccess/connectivity/branches
    ```
5. Run the following query to get the connectivity information, replacing `{branchSiteId}` with the ID of your remote network and `{deviceLinkId}` with the ID of your device link:

    ```http
    GET https://graph.microsoft.com/beta/networkAccess/connectivity/branches/{branchSiteId}/deviceLinks/{deviceLinkId}
    ```

The details in the response are similar to the device configuration details found in the Microsoft Entra admin center.

---