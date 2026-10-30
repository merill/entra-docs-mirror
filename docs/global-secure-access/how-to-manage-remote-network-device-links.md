---
layout: Conceptual
title: How to add device links to remote networks - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-manage-remote-network-device-links
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to add and delete customer premises equipment device links to remote networks for Global Secure Access.
ms.topic: how-to
ms.date: 2026-03-23T00:00:00.0000000Z
ms.reviewer: absinh
ms.custom: sfi-image-nochange
locale: en-us
document_id: 75bdac8b-a033-e875-fc5a-aa8bb4f1ea4e
document_version_independent_id: 22ff5837-17dd-d3f8-8338-0f8d407a3d7d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-manage-remote-network-device-links.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-manage-remote-network-device-links
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-manage-remote-network-device-links.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: be973052-f9f9-a71b-f713-8d69e844af09
---

# How to add device links to remote networks - Global Secure Access | Microsoft Learn

Customer premises equipment, such as routers, are added to the remote network. You can create device links when you create a new remote network or add them after the remote network is created. This article explains how to add and delete device links for remote networks for Global Secure Access.

## Prerequisites

To configure remote networks, you must have:

- A **Global Secure Access Administrator** role in Microsoft Entra ID.
- Created a remote network.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## Add a device link

You can add a device link from the Microsoft Entra admin center or using the Microsoft Graph API.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
You can add a device link to a remote network at any time.

1. Browse to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**.
2. Select a remote network from the list.
3. Select **Links** from the menu.
4. Select **+ Add a link**.

### Add a link - General tab

There are several details to enter on the General tab. Pay close attention to the Peer and Local Border Gateway Protocol (BGP) addresses. *The peer and local details are reversed, depending on where the configuration is completed.*

![Screenshot of the General tab with examples in each field.](media/how-to-manage-remote-network-device-links/add-device-link.png)

1. Enter the following details.
    - **Link name**: Name of your Customer Premises Equipment (CPE).
    - **Device type**: Choose a device option from the dropdown list.
    - **Device IP address**: Public IP address of your CPE (customer premise equipment) device.
    - **Device BGP address**: Enter the BGP IP address of your CPE.
        - This address is entered as the *local* BGP IP address on the CPE.
    - **Device ASN**: Provide the autonomous system number (ASN) of the CPE.
        - A BGP-enabled connection between two network gateways requires that they have different ASNs.
        - For more information, see the **Valid ASNs** section of the [Remote network configurations](reference-remote-network-configurations#valid-asn) article.
    - **Redundancy**: Select either *No redundancy* or *Zone redundancy* for your IPSec tunnel.
    - **Zone redundancy local BGP address**: This optional field shows up only when you select **Zone redundancy**.
        - Enter a BGP IP address that *isn't* part of your on-premises network where your CPE resides and is different from the **Device BGP address**.
    - **Bandwidth capacity (Mbps)**: Specify tunnel bandwidth. Available options are 250, 500, 750, and 1,000 Mbps.
    - **Local BGP address**: Enter a BGP IP address that *isn't*part of your on-premises network where your CPE resides.
        - For example, if your on-premises network is 10.1.0.0/16, then you can use 10.2.0.4 as your Local BGP address.
        - This address is entered as the *peer* BGP​​ IP address on your CPE.
        - Refer to the [valid BGP addresses](reference-remote-network-configurations#valid-bgp-addresses) list for reserved values that can't be used.
2. Select **Next**.

### Add a link - Details tab

The **Details** tab is where you establish the bidirectional communication channel between Global Secure Access and your CPE. Configure your IPSec/IKE policy and select **Next**.

![Screenshot of the default device link details.](media/how-to-manage-remote-network-device-links/default-device-link-details.png)

- **IKEv2** is selected by default. Currently only IKEv2 is supported.
- The IPSec/IKE policy is set to **Default** but you can change to **Custom**.
- If you choose the custom IPSec/IKE policy, first review the [How to create remote network with custom Internet Key Exchange (IKE) policy](how-to-create-remote-network-custom-ike-policy) article.
- If you select **Custom**, you must use a combination of settings that are supported by Global Secure Access. The valid configurations you can use are mapped out in the [Remote network valid configurations](reference-remote-network-configurations) reference article.
- Whether you choose **Default** or **Custom**, the IPSec/IKE policy you specify must match the policy you enter on your CPE.

### Add a link - Security tab

1. Enter the Pre-shared key (PSK) and Zone Redundancy Pre-shared key (PSK). The same secret key must be used on your respective CPE. The Zone Redundancy Pre-shared key (PSK) field only appears if you set up redundancy on the first page in creating the link.
2. Select the **Save** button.

# [Microsoft Graph API](#tab/microsoft-graph-api)
Remote networks with a custom IKE policy can be created using Microsoft Graph on the `/beta` endpoint.

Important

APIs under the `/beta` version in Microsoft Graph are subject to change. Use of these APIs in production applications is not supported. For details, see [Microsoft Graph versioning and support](/en-us/graph/versioning-and-support).

1. Sign in to [Graph Explorer](https://aka.ms/ge).
2. Select `POST` as the HTTP method from the dropdown.
3. Set the API version to beta.
4. Run the following query to get a list of your remote networks and their details.

    ```http
    GET https://graph.microsoft.com/beta/networkAccess/connectivity/remoteNetworks
    ```
5. Run the following query to get the device link details.

    ```http
    POST https://graph.microsoft.com/beta/networkAccess/connectivity/remoteNetworks/{remoteNetworkId}/deviceLinks
    ```

Sample response:

```http
{
    "name": "CPE3",
    "ipAddress": "20.55.91.42",
    "deviceVendor": "ciscoMeraki",
    "bandwidthCapacityInMbps": "mbps1000",
    "bgpConfiguration": {
        "localIpAddress": "192.168.1.2",
        "peerIpAddress": "10.2.2.2",
        "asn": 65533
    },
    "redundancyConfiguration": {
        "redundancyTier": "zoneRedundancy",
        "zoneLocalIpAddress": "192.168.1.3"
    },
    "tunnelConfiguration": {
        "@odata.type": "#microsoft.graph.networkaccess.tunnelConfigurationIKEv2Default",
        "preSharedKey": "<your-preshared-key>"
    }
}
```

---

## How to delete device links

You can delete device links through the Microsoft Entra admin center and using the Microsoft Graph API.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**. Device links appear in the **Links** column on the list of remote networks.
3. Select the device link from the **Links** column to access the device link details page.
4. Select **Delete** for the device link you want to delete. A confirmation dialog appears. Select **Delete** to confirm the deletion.

    ![Screenshot of the delete icon for remote network device links.](media/how-to-manage-remote-network-device-links/delete-device-link.png)

# [Microsoft Graph API](#tab/microsoft-graph-api)
1. Sign in to [Graph Explorer](https://aka.ms/ge).
2. Select `DELETE` as the HTTP method from the dropdown.
3. Set the API version to beta.
4. Enter the following query.

    ```http
    DELETE https://graph.microsoft.com/beta/networkAccess/connectivity/remotenetworks/{remoteNetworkId}/deviceLinks/{deviceLinkId}
    
    ```

---