---
layout: Conceptual
title: How to Create Remote Networks - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-create-remote-networks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to create remote networks, for remote locations such as branch offices, for Global Secure Access.
ms.topic: how-to
ms.date: 2026-04-15T00:00:00.0000000Z
ms.reviewer: abhijeetsinha
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0122c559-94d6-ce59-ff5c-423663b03dfa
document_version_independent_id: eb82f9e3-6a80-a989-9c77-8c146382f037
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-create-remote-networks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-create-remote-networks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-create-remote-networks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: daffe440-36a7-cdc1-aa59-a847f0d0c7d9
---

# How to Create Remote Networks - Global Secure Access | Microsoft Learn

Remote networks are remote locations, such as a branch office, or networks that require internet connectivity. Setting up remote networks connects your users in remote locations to Global Secure Access. Once you configure a remote network, you can assign a traffic forwarding profile to manage your corporate network traffic. Global Secure Access provides remote network connectivity so you can apply network security policies to your outbound traffic.

You can connect remote networks to Global Secure Access in several ways. In a nutshell, you're creating an Internet Protocol Security (IPSec) tunnel between a core router, known as the customer premises equipment (CPE), at your remote network and the nearest Global Secure Access endpoint. All internet-bound traffic routes through the core router of the remote network for security policy evaluation in the cloud. You don't need to install the client on individual devices.

This article explains how to create a remote network for Global Secure Access.

## Prerequisites

To configure remote networks, you must have:

- A **Global Secure Access Administrator** role in Microsoft Entra ID.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).
- Customer premises equipment (CPE) must support the following protocols:
    - Internet Protocol Security (IPSec)
    - GCMEAES128, GCMAES 192, or GCMAES256 algorithms for Internet Key Exchange (IKE) phase 2 negotiation
    - Internet Key Exchange Version 2 (IKEv2)
    - Border Gateway Protocol (BGP)
- [Review the valid configurations for setting up remote networks](reference-remote-network-configurations).
- Remote network connectivity solution uses *RouteBased* VPN configuration with *any-to-any* (wildcard or 0.0.0.0/0) traffic selectors. Make sure that your CPE has the correct traffic selector set.
- Remote network connectivity solution uses *Responder* modes. Your CPE must initiate the connection.

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## High-level steps

You can create a remote network in the Microsoft Entra admin center or through the Microsoft Graph API.

At a high level, there are five steps for creating a remote network and configuring an active IPsec tunnel:

1. **Basics**: Enter the basic details like the **Name** and **Region** of your remote network. **Region** specifies where you want your other end of IPsec tunnel. The other end of the tunnel is your router or CPE.
2. **Connectivity**: Add a device link (or IPsec tunnel) to the remote network. In this step, you enter your router's details in the Microsoft Entra admin center, which tells Microsoft where to expect IKE negotiations to come from.
3. **Traffic forwarding profile**: Associate a traffic forwarding profile with the remote network, which specifies what traffic to acquire over the IPsec tunnel. Global Secure Access uses dynamic routing through BGP.
4. **View CPE connectivity configuration**: Retrieve the IPsec tunnel details of Microsoft's end of the tunnel. On the **Connectivity** step, you provided your router's details to Microsoft. In this step, you retrieve Microsoft's side of the connectivity configuration.
5. **Set up your CPE**: Take Microsoft's connectivity configuration from the previous step and enter it in the management console of your router or CPE. This step *isn't* in the Microsoft Entra admin center.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
You configure remote networks on three tabs. Complete each tab in order. After you complete each tab, either select the next tab from the top of the page, or select the **Next** button at the bottom of the page.

### Basics

On the **Basics** tab, enter the name and location of your remote network. You must complete this tab.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**.
3. Select **Create remote network**and enter the details.
    - **Name**
    - **Region**

![Screenshot of the basics tab of the create device link process.](media/how-to-create-remote-networks/create-basics-tab.png)

### Connectivity

Add the device links for the remote network on the **Connectivity** tab. You can add device links *after* creating the remote network. For each device link, enter the device type, public IP address of your CPE, border gateway protocol (BGP) address, and autonomous system number (ASN).

The details required to complete the **Connectivity** tab can be complex. For more information, see [How to manage remote network device links](how-to-manage-remote-network-device-links).

### Traffic forwarding profiles

You can assign the remote network to a traffic forwarding profile when you create the remote network. You can also assign the remote network at a later time. For more information, see [Traffic forwarding profiles](concept-traffic-forwarding).

1. Either select the **Next** button or select the **Traffic profiles** tab.
2. Select the appropriate traffic forwarding profile.
3. Select the **Review + create** button.

    ![Screenshot of the Create a remote network page, open to the Traffic profiles tab, with Microsoft traffic profile selected.](media/how-to-create-remote-networks/microsoft-traffic-profile-selected.png)

#### Traffic profile enforcement on remote network device links

Global Secure Access enforces traffic forwarding profiles for all device links, such as IPsec tunnels, associated with a remote network. It forwards only traffic types that match an enabled and associated traffic forwarding profile. The Global Secure Access gateway drops all other traffic.

This enforcement means:

- If you associate only the **Microsoft traffic profile** with a remote network, the Global Secure Access gateway drops any non-Microsoft traffic (such as general internet traffic) sent over the device link.
- If you associate only the **Internet Access traffic profile** with a remote network, the Global Secure Access gateway drops any Microsoft traffic sent over the device link.

Important

To avoid unintended traffic loss, associate **both** the **Microsoft traffic profile** and the **Internet Access traffic profile** with your remote network if your license permits. This configuration ensures that the appropriate profile handles all traffic forwarded over the IPsec tunnel rather than silently dropping it at the gateway.

For details on available traffic forwarding profiles and their configuration, see [Global Secure Access traffic forwarding profiles](/en-us/entra/global-secure-access/concept-traffic-forwarding).

The final tab in the process is to review all of the settings that you provided. Review the details provided here and select the **Create remote network** button.

### View CPE connectivity configuration

All your remote networks appear on the **Remote network** page. Select the **View configuration** link in the **Connectivity details** column to view your configuration details.

These details contain the connectivity information from Microsoft's side of the bidirectional communication channel that you use to set up your CPE.

This process is covered in detail in the [How to configure your customer premises equipment](how-to-configure-customer-premises-equipment).

### Set up your CPE

You perform this step in the management console of your CPE, not in Microsoft Entra admin center. Until you complete this step, your IPsec *isn't* set up. IPsec is a bidirectional communication. IKE negotiations occur between two parties before the tunnel is successfully set up. Don't skip this step.

Tip

For guidance on enhancing the resilience of remote networks, see [Best practices for Global Secure Access remote network resilience](remote-network-resilience).

# [Microsoft Graph API](#tab/microsoft-graph-api)
You can use Microsoft Graph on the `/beta` endpoint to view and manage Global Secure Access remote networks. Creating a remote network and assigning a traffic forwarding profile are separate API calls.

1. Sign in to [Graph Explorer](https://aka.ms/ge).
2. Select `POST` as the `HTTP` method.
3. Select `BETA` as the `API` version.
4. Run the query.

    ```http
    POST https://graph.microsoft.com/beta/networkAccess/connectivity/remoteNetworks
    Content-Type: application/json
    
    {
        "name": "Bellevue branch w/ device link",
        "region": "canadaEast",
        "forwardingProfiles": [
            {
                "id": "1adaf535-1e31-4e14-983f-2270408162bf"
            }
        ],
        "deviceLinks": [
            {
                "name": "CPE1",
                "ipAddress": "52.13.21.25",
                "bandwidthCapacityInMbps": "mbps500",
                "deviceVendor": "barracudaNetworks",
                "bgpConfiguration": {
                    "localIpAddress": "192.168.1.2",
                    "peerIpAddress": "10.1.1.2",
                    "asn": 65533
                },
                "redundancyConfiguration": {
                    "zoneLocalIpAddress": null,
                    "redundancyTier": "noRedundancy"
                },
                "tunnelConfiguration": {
                    "@odata.type": "#microsoft.graph.networkaccess.tunnelConfigurationIKEv2Default",
                    "preSharedKey": "test123"
                }
            }
        ]
    }
    ```

### Assign a traffic forwarding profile

Associating a traffic forwarding profile to your remote network by using the Microsoft Graph API is a two-step process. First, locate the ID of the traffic profile. The ID is different for all tenants. Second, associate the traffic forwarding profile with your desired remote network.

1. Sign in to [Graph Explorer](https://aka.ms/ge).
2. Select `PATCH` as the `HTTP` method from the dropdown.
3. Select the `API` version to **beta**.
4. Enter the query.

    ```
    GET https://graph.microsoft.com/beta/networkaccess/forwardingprofiles 
    ```
5. Select **Run query**.
6. Find the `ID` of the desired traffic forwarding profile.
7. Select `PATCH` as the `HTTP` method from the dropdown.
8. Enter the query.

    ```http
        PATCH https://graph.microsoft.com/beta/networkAccess/connectivity/remoteNetworks/dc6a7efd-6b2b-4c6a-84e7-5dcf97e62e04
        Content-Type: application/json
    
        {
            "name": "Test Redmond branch"
        }
    ```

### Traffic profile enforcement on remote network device links

Global Secure Access enforces traffic forwarding profiles for all device links, such as IPsec tunnels, associated with a remote network. It forwards only traffic types that match an enabled and associated traffic forwarding profile. The Global Secure Access gateway drops all other traffic.

This enforcement means:

- If you associate only the **Microsoft traffic profile** with a remote network, the Global Secure Access gateway drops any non-Microsoft traffic (such as general internet traffic) sent over the device link.
- If you associate only the **Internet Access traffic profile** with a remote network, the Global Secure Access gateway drops any Microsoft traffic sent over the device link.

Important

To avoid unintended traffic loss, associate **both** the **Microsoft traffic profile** and the **Internet Access traffic profile** with your remote network if your license permits. This configuration ensures that the appropriate profile handles all traffic forwarded over the IPsec tunnel rather than silently dropping it at the gateway.

For details on available traffic forwarding profiles and their configuration, see [Global Secure Access traffic forwarding profiles](/en-us/entra/global-secure-access/concept-traffic-forwarding).

---

## Verify your remote network configurations

Consider and verify a few settings when creating remote networks. You might need to double-check some settings.

- **Verify IKE crypto profile**: The crypto profile (IKE phase 1 and phase 2 algorithms) set for a device link should match the CPE setting. If you choose the **default IKE policy**, ensure that your CPE is set up with the crypto profile specified in the [Remote network configurations](reference-remote-network-configurations) reference article.
- **Verify pre-shared key**: Compare the pre-shared key (PSK) you specified when creating the device link in Microsoft Global Secure Access with the PSK you specify on your CPE. Add this detail on the **Security** tab during the **Add a link** process. For more information, see [How to manage remote network device links](how-to-manage-remote-network-device-links#add-a-link---security-tab).
- **Verify local and peer BGP IP addresses**: The public IP and BGP address you use to configure the CPE must match what you use when you create a device link in Microsoft Global Secure Access.

    - Refer to the [valid BGP addresses](reference-remote-network-configurations#valid-bgp-addresses)list for reserved values that you can't use.
        - The local and peer BGP addresses are reversed between the CPE and what you entered in Global Secure Access.
        - **CPE**: Local BGP IP address = IP1, Peer BGP IP address = IP2
        - **Global Secure Access**: Local BGP IP address = IP2, Peer BGP IP address = IP1
    - Choose an IP address for Global Secure Access that doesn't overlap with your on-premises network.
- **Verify ASN**: Global Secure Access uses BGP to advertise routes between two autonomous systems: your network and Microsoft's. These autonomous systems should have different Autonomous System Numbers (ASNs).

    - Refer to the [valid ASN values](reference-remote-network-configurations#valid-asn) list for reserved values that you can't use.
    - When creating a remote network in the Microsoft Entra admin center, use your network's ASN.
    - When configuring your CPE, use Microsoft's ASN. Go to **Global Secure Access** &gt; **Devices** &gt; **Remote Networks**. Select **Links** and confirm the value in the **Link ASN** column.
- **Verify your public IP address**: In a test environment or lab setup, the public IP address of your CPE might change unexpectedly. This change can cause the IKE negotiation to fail even though everything remains the same.

    - If you encounter this scenario, complete the following steps:
        - Update the public IP address in the crypto profile of your CPE.
        - Go to the **Global Secure Access** &gt; **Devices** &gt; **Remote Networks**.
        - Select the appropriate remote network, delete the old tunnel, and recreate a new tunnel with the updated public IP address.
- **Verify Microsoft's public IP address**: When you delete a device link and/or create a new one, you might get another public IP endpoint of that link in **View configuration** for that remote network. This change can cause the IKE negotiation to fail. If you encounter this scenario, update the public IP address in the crypto profile of your CPE.
- **Verify BGP connectivity setting on your CPE**: Suppose you create a device link for a remote network. Microsoft provides you with the public IP address, say PIP1, and BGP address, say BGP1, of its gateway. This connectivity information is available under `localConfigurations` in the jSON blob you see when you select **View Configuration** for that remote network. On your CPE, make sure that you have a static route destined to BGP1 sent over the tunnel interface created with PIP1. The route is necessary so that CPE can learn the BGP routes we publish over the IPsec tunnel you created with Microsoft.
- **Verify firewall rules**: Allow User Datagram Protocol (UDP) port 500 and 4500 and Transmission Control Protocol (TCP) port 179 for IPsec tunnel and BGP connectivity in your firewall.
- **Port forwarding**: In some situations, the Internet Service Provider (ISP) router is also a network address translation (NAT) device. A NAT converts the private IP addresses of home devices to a public internet-routable device.

    - Generally, a NAT device changes both the IP address and the port. This port changing is the root of the problem.
    - For IPsec tunnels to work, Global Secure Access uses port 500. This port is where IKE negotiation happens.
    - If the ISP router changes this port to something else, Global Secure Access can't identify this traffic and negotiation fails.
    - As a result, phase 1 of IKE negotiation fails and the tunnel isn't established.
    - To fix this failure, complete the port forwarding on your device, which tells the ISP router to not change the port and forward it as-is.