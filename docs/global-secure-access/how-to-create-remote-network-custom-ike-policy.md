---
layout: Conceptual
title: Create a remote network with a custom IKE policy - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-create-remote-network-custom-ike-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to set up the bidirectional communication tunnel between Global Secure Access and your router.
ms.topic: how-to
ms.date: 2026-03-23T00:00:00.0000000Z
ms.reviewer: absinh
ms.custom: sfi-image-nochange
locale: en-us
document_id: 71cbbd86-875a-88cf-bfa6-d1caed214532
document_version_independent_id: 0f2784da-0597-f3ae-0e36-e3b8e7fbf8b4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-create-remote-network-custom-ike-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-create-remote-network-custom-ike-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-create-remote-network-custom-ike-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: bc555c61-e2fa-0b64-7161-cbb2fc32d1a2
---

# Create a remote network with a custom IKE policy - Global Secure Access | Microsoft Learn

IPSec tunnel is a bidirectional communication. This article provides the steps to set up the communication channel in Microsoft Entra admin center and the Microsoft Graph API. The other side of the communication is configured on your customer premises equipment (CPE).

## Prerequisites

To create a remote network with a custom Internet Key Exchange (IKE) policy, you must have:

- A **Global Secure Access Administrator** role in Microsoft Entra ID.
- Received the connectivity information from Global Secure Access onboarding.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## How to create a remote network with a custom IKE policy

If you prefer to add custom IKE policy details to your remote network, you can do so when you add the device link to your remote network. You can complete this step in the Microsoft Entra admin center or using the Microsoft Graph API.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
To create a remote network with a custom IKE policy in the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**.
3. Select **Create remote network**.
4. Provide a name and region for your remote network and select **Next: Connectivity**.
5. Select **+ Add a link** to add the connectivity details of your CPE.

### Add a link - General tab

There are several details to enter on the General tab. Pay close attention to the Peer and Local Border Gateway Protocol (BGP) addresses. *The peer and local details are reversed, depending on where the configuration is completed.*

![Screenshot of the General tab with examples in each field.](media/how-to-create-remote-network-custom-ike-policy/add-device-link.png)

1. Enter the following details:

    - **Link name**: Name of your CPE.
    - **Device type**: Choose a device option from the dropdown list.
    - **Device IP address**: Public IP address of your device.
    - **Device BGP address**: Enter the BGP IP address of your CPE.
        - This address is entered as the *local* BGP IP address on the CPE.
    - **Device ASN**: Provide the autonomous system number (ASN) of the CPE.
        - A BGP-enabled connection between two network gateways requires that they have different ASNs.
        - Refer to the [valid ASN values](reference-remote-network-configurations#valid-asn) list for reserved values that can't be used.
    - **Redundancy**: Select either *No redundancy* or *Zone redundancy* for your IPSec tunnel.
    - **Zone redundancy local BGP address**: This optional field shows up only when you select **Zone redundancy**.
        - Enter a BGP IP address that *isn't* part of your on-premises network where your CPE resides *and* is different from **Local BGP address**.
    - **Bandwidth capacity (Mbps)**: Specify tunnel bandwidth. Available options are 250, 500, 750, and 1,000 Mbps.
    - **Local BGP address**: Enter a BGP IP address that *isn't*part of your on-premises network where your CPE resides.
        - For example, if your on-premises network is 10.1.0.0/16, then you can use 10.2.0.4 as your Local BGP address.
        - This address is entered as the *peer* BGP​​ IP address on your CPE.
        - Refer to the [valid BGP addresses](reference-remote-network-configurations#valid-bgp-addresses) list for reserved values that can't be used.
2. Select **Next**.

### Add a link - Details tab

Important

You must specify both a Phase 1 *and* Phase 2 combination on your CPE.

1. **IKEv2** is selected by default. Currently only IKEv2 is supported.
2. Change the **IPSec/IKE policy** to **Custom**.
3. Select your Phase 1 combination details for **Encryption**, **IKEv2 integrity**, and **DHGroup**.

    - The combination of details you select must align with the available options listed in the [Remote network valid configurations](reference-remote-network-configurations) reference article.
4. Select your Phase 2 combinations for **IPsec encryption**, **IPsec integrity**, **PFS group**, and **SA lifetime (seconds)**.

    - The combination of details you select must align with the available options listed in the [Remote network valid configurations](reference-remote-network-configurations) reference article.
5. Whether you choose Default or Custom, the IPSec/IKE policy you specify must match the crypto policy on your CPE.
6. Select **Next**.

    ![Screenshot of the custom details for the device link.](media/how-to-create-remote-network-custom-ike-policy/device-link-details.png)

### Add a link Security tab

1. Enter the Pre-shared key (PSK) and Zone Redundancy Pre-shared key (PSK). The same secret key must be used on your respective CPE. The Zone Redundancy Pre-shared key (PSK) field only appears if redundancy is set on the first page in creating the link.
2. Select **Save**.

![Screenshot of the Security tab for adding a device link.](media/how-to-create-remote-network-custom-ike-policy/pre-shared-key.png)

# [Microsoft Graph API](#tab/microsoft-graph-api)
Remote networks with a custom IKE policy can be created using Microsoft Graph on the `/beta` endpoint.

Important

APIs under the `/beta` version in Microsoft Graph are subject to change. Use of these APIs in production applications is not supported. For details, see [Microsoft Graph versioning and support](/en-us/graph/versioning-and-support).

1. Sign in to [Graph Explorer](https://aka.ms/ge).
2. Select **POST** as the HTTP method from the dropdown.
3. Set the API version to **beta**.
4. Add the following query, then select **Run query**.

```http
    POST https://graph.microsoft.com/beta/networkAccess/connectivity/remoteNetworks/{remoteNetworkId}/deviceLinks
Content-Type: application/json

{
    "name": "custom link",
    "ipAddress": "114.20.4.14",
    "deviceVendor": "ciscoMeraki",
    "tunnelConfiguration": {
        "saLifeTimeSeconds": 300,
        "ipSecEncryption": "gcmAes128",
        "ipSecIntegrity": "gcmAes128",
        "ikeEncryption": "aes128",
        "ikeIntegrity": "sha256",
        "dhGroup": "ecp384",
        "pfsGroup": "ecp384",
        "@odata.type": "#microsoft.graph.networkaccess.tunnelConfigurationIKEv2Custom",
        "preSharedKey": "SHAREDKEY"
    },
    "bgpConfiguration": {
        "localIpAddress": "10.1.1.11",
        "peerIpAddress": "10.6.6.6",
        "asn": 65000
    },
    "redundancyConfiguration": {
        "redundancyTier": "zoneRedundancy",
        "zoneLocalIpAddress": "10.1.1.12"
    },
    "bandwidthCapacityInMbps": "mbps250"
}
```

---