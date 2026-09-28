---
layout: Conceptual
title: Simulate remote network connectivity using Azure VNG - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-simulate-remote-network
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Configure Azure resources to simulate remote network connectivity to Microsoft's Security Edge Solutions with Global Secure Access.
ms.topic: how-to
ms.date: 2026-04-15T00:00:00.0000000Z
ms.reviewer: abhijeetsinha
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: ab321c77-5d72-1bee-686a-b862883250c2
document_version_independent_id: b2ef2dd9-b4c4-2739-bc41-b45d7e15cb10
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-simulate-remote-network.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-simulate-remote-network
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-simulate-remote-network.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/20ed8455-bc18-4537-87a4-83784e7b2a39
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9a7f703b-30bb-4d62-9eb4-97213f571849
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9c93493d-740e-66ac-4363-b3d1e294af9d
---

# Simulate remote network connectivity using Azure VNG - Global Secure Access | Microsoft Learn

## Overview

Organizations might want to extend the capabilities of Microsoft Entra Internet Access to entire networks, not just individual devices. They can [install the Global Secure Access Client](how-to-install-windows-client) on these devices. This article shows how to extend these capabilities to an Azure virtual network hosted in the cloud. You can apply similar principles to a customer's on-premises network equipment.

## Prerequisites

To complete the steps in this process, you need the following prerequisites:

- An Azure subscription and permission to create resources in the [Azure portal](https://portal.azure.com).
- A basic understanding of [site-to-site VPN connections](/en-us/azure/vpn-gateway/tutorial-site-to-site-portal).
- A Microsoft Entra tenant with the [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator) role assigned.

## Components of the virtual network

When you build this functionality in Azure, your organization can better understand how Microsoft Entra Internet Access works in a broader implementation. The resources you create in Azure correspond to on-premises concepts in the following ways:

[![Diagram showing a virtual network in Azure connected to Microsoft Entra Internet Access simulating a customer's network.](media/how-to-simulate-remote-network/simulate-remote-network.png)](media/how-to-simulate-remote-network/simulate-remote-network.png#lightbox)

| Azure resource | Traditional on-premises component |
| --- | --- |
| **Virtual network** | Your on-premises IP address space |
| **Virtual network gateway** | Your on-premises router, sometimes referred to as customer premises equipment (CPE) |
| **Local network gateway** | The Microsoft gateway that your router (Azure virtual network gateway) creates an IPsec tunnel to |
| **Connection** | IPsec VPN tunnel created between the virtual network gateway and local network gateway |
| **Virtual machine** | Client devices on your on-premises network |

In this article, use the following default values. You can change these settings to fit your own requirements.

- **Subscription:** Visual Studio Enterprise
- **Resource group name:** Network\_Simulation
- **Region:** East US

## High-level steps

Complete the steps to simulate remote network connectivity with Azure virtual networks in the Azure portal and the Microsoft Entra admin center. It might be helpful to have multiple tabs open so you can switch between them easily.

Before creating your virtual resources, you need a resource group and virtual network to use throughout the following sections. If you already have a test resource group and virtual network configured, you can start at step 3.

1. Create a resource group (Azure portal)
2. Create a virtual network (Azure portal)
3. Create a virtual network gateway (Azure portal)
4. Create a remote network with device links (Microsoft Entra admin center)
5. Create local network gateway (Azure portal)
6. Create a site-to-site (S2S) VPN connection (Azure portal)
7. Verify connectivity (Both)

## Create a resource group

Create a resource group to contain all of the necessary resources.

1. Sign in to the [Azure portal](https://portal.azure.com) with permission to create resources.
2. Browse to **Resource groups**.
3. Select **Create**.
4. Select your **Subscription** and **Region**, and enter a name for your **Resource group**.
5. Select **Review + create**.
6. Confirm your details, and then select **Create**.

![Screenshot that shows the create a resource group fields.](media/how-to-simulate-remote-network/create-azure-resource-group.png)

## Create a virtual network

Create a virtual network inside your new resource group.

1. From the Azure portal, browse to **Virtual Networks**.
2. Select **Create**.
3. Select the **Resource group** you just created.
4. Enter your network's **Virtual network Name**.
5. Leave the default values for the other fields.
6. Select **Review + create**.
7. Select **Create**.

![Screenshot that shows the create a virtual network fields.](media/how-to-simulate-remote-network/create-azure-virtual-network.png)

## Create a virtual network gateway

Create a virtual network gateway inside your new resource group.

1. From the Azure portal, browse to **Virtual network gateways**.
2. Select **Create**.
3. Enter a **Name** for your virtual network gateway and select the appropriate region.
4. Select your **Virtual network**.

    [![Screenshot of the Azure portal showing configuration settings for a virtual network gateway.](media/how-to-simulate-remote-network/create-azure-virtual-network-gateway.png)](media/how-to-simulate-remote-network/create-azure-virtual-network-gateway-expanded.png#lightbox)
5. Create a **Public IP address** and enter a descriptive name.

    - **OPTIONAL**: If you want a secondary IPsec tunnel, under the **SECOND PUBLIC IP ADDRESS** section, create another public IP address and enter a name. If you create a second IPsec tunnel, you need to create two device links in the Create a remote network step.
    - Set the **Enable active-active mode** to **Disabled** if you don't need a second public IP address.
    - The sample in this article uses a single IPsec tunnel.
6. Select an **Availability zone**.
7. Set **Configure BGP** to **Enabled**.
8. Set the **Autonomous system number (ASN)** to an appropriate value. Refer to the [valid ASN values](reference-remote-network-configurations#valid-asn) list for reserved values that you can't use.

    ![Screenshot of the IP address fields for creating a virtual network gateway.](media/how-to-simulate-remote-network/create-azure-virtual-network-gateway-ip-addresses.png)
9. Leave all other settings as their defaults or blank.
10. Select **Review + create**. Confirm your settings.
11. Select **Create**.

Note

It might take several minutes to deploy and create the virtual network gateway. You can start the next section while it's being created, but you need the public IP addresses of your virtual network gateway to complete the next step.

To view these IP addresses, browse to the **Configuration** page of your virtual network gateway after it deploys.

![Screenshot that shows how to find the public IP addresses of a virtual network gateway.](media/how-to-simulate-remote-network/virtual-network-gateway-public-ip-addresses.png)

## Create a remote network

You create a remote network in the Microsoft Entra admin center. Enter the information in two sets of tabs.

![Screenshot of the two sets of tabs used in the process.](media/how-to-simulate-remote-network/remote-network-tabs.png)

The following steps provide the basic information needed to create a remote network with Global Secure Access. Two separate articles cover this process in greater detail. To avoid confusion, review these articles:

- [How to create a remote network](how-to-create-remote-networks)
- [How to manage remote network device links](how-to-manage-remote-network-device-links)

### Zone redundancy

Before you create your remote network for Global Secure Access, review the two options about redundancy. You can create remote networks with or without redundancy. Add redundancy in two ways:

- Choose **Zone redundancy**while creating a device link in the Microsoft Entra admin center.
    - In this scenario, you create another gateway in a different availability zone within the same datacenter **Region** you picked while creating your remote network.
    - In this scenario, you need just one public IP address on your virtual network gateway.
    - Two IPSec tunnels are created from the same public IP address of your router to different Microsoft gateways in different availability zones.
- Create a secondary public IP address in the Azure portal and create two device links with different public IP addresses in the Microsoft Entra admin center.
    - You can choose **No redundancy** when adding device links to your remote network in the Microsoft Entra admin center.
    - In this scenario, you need primary and secondary public IP addresses on your virtual network gateway.

### Create the remote network and add device links

For this article, choose the zone redundancy path.

Tip

Local BGP address must be a private IP address that is outside the address space of the virtual network associated with your virtual network gateway. For example, if the address space of your virtual network is 10.1.0.0/16, you can use 10.2.0.0 as your Local BGP address.

Refer to the [**valid BGP addresses**](reference-remote-network-configurations#valid-bgp-addresses) list for reserved values that you can't use.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**.
3. Select **Create remote network** and provide the following details on the **Basics**tab:
    - **Name**
    - **Region**

![Screenshot of the basics tab for creating a remote network.](media/how-to-simulate-remote-network/create-basics-tab.png)

1. On the Connectivity tab, select **Add a link**.
2. On the **Add a link - General** tab, enter the following details:

    - **Link name**: Name of your Customer Premises Equipment (CPE).
    - **Device type**: Choose a device option from the dropdown list.
    - **Device IP address**: Public IP address of your CPE (customer premise equipment) device.
    - **Device BGP address**: Enter the BGP IP address of your CPE.
        - Enter this address as the *local* BGP IP address on the CPE.
    - **Device ASN**: Provide the autonomous system number (ASN) of the CPE.
        - A BGP-enabled connection between two network gateways requires that they have different ASNs.
        - For more information, see the **Valid ASNs** section of the [Remote network configurations](reference-remote-network-configurations#valid-asn) article.
    - **Redundancy**: Select either *No redundancy* or *Zone redundancy* for your IPSec tunnel.
    - **Zone redundancy local BGP address**: This optional field appears only when you select **Zone redundancy**.
        - Enter a BGP IP address that *isn't* part of your on-premises network where your CPE resides and is different from the **Device BGP address**.
    - **Bandwidth capacity (Mbps)**: Specify tunnel bandwidth. Available options are 250, 500, 750, and 1,000 Mbps.
    - **Local BGP address**: Enter a BGP IP address that *isn't*part of your on-premises network where your CPE resides.
        - For example, if your on-premises network is 10.1.0.0/16, you can use 10.2.0.4 as your Local BGP address.
        - Enter this address as the *peer* BGP​​ IP address on your CPE.
        - Refer to the [valid BGP addresses](reference-remote-network-configurations#valid-bgp-addresses) list for reserved values that can't be used.

    ![Screenshot of the Add a link - General tab with examples in each field.](media/how-to-simulate-remote-network/virtual-network-device-link-details.png)
3. On the **Add a link - Details** tab, keep the default values unless you made a different selection previously, and select **Next**.
4. On the **Add a link - Security** tab, enter the pre-shared key (PSK) and select **Save**. You return to the main **Create a remote network** set of tabs.
5. On the **Traffic profiles** tab, select the appropriate traffic forwarding profile.
6. Select **Review + Create**.
7. If everything looks correct, select **Create remote network**.

### View connectivity configuration

After you create a remote network and add a device link, you can view the configuration details in the Microsoft Entra admin center. You need several details from this configuration to complete the next step.

1. Browse to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**.
2. In the last column on the right in the table, select **View configuration** for the remote network you created. The configuration appears as a JSON blob.
3. Locate and save Microsoft's public IP address `endpoint`, `asn`, and `bgpAddress` from the pane that opens.

    - Use these details to set up your connectivity in the next step.
    - For more information about viewing these details, see [Configure customer premises equipment](how-to-configure-customer-premises-equipment).

    ![Screenshot that shows the view configuration panel.](media/how-to-simulate-remote-network/view-configuration-details-panel.png)

The following diagram connects the key details of these configuration details to their correlating role in the simulated remote network. A text description of the diagram follows the image.

[![Diagram of the remote network configurations and where the details correlate to the network.](media/how-to-simulate-remote-network/simulate-remote-networks-diagram.png)](media/how-to-simulate-remote-network/simulate-remote-networks-diagram-expanded.png#lightbox)

The center of the diagram depicts a resource group that contains a virtual machine connected to a virtual network. A virtual network gateway then connects to the local network gateway through a site-to-site redundant VPN connection.

A screenshot of the connectivity details has two sections highlighted. The first highlighted section under `localConfigurations` contains the details of the Global Secure Access gateway, which is your local network gateway.

**Local Network Gateway 1**

- Public IP address/endpoint: 120.x.x.76
- ASN: 65476
- BGP IP address/bgpAddress: 192.168.1.1

**Local Network Gateway 2**

- Public IP address/endpoint: 4.x.x.193
- ASN: 65476
- BGP IP address/bgpAddress: 192.168.1.2

The second highlighted section under `peerConfiguration` contains the details of the virtual network gateway, which is your local router equipment.

**Virtual Network Gateway**

- Public IP address/endpoint: 20.x.x.1
- ASN: 65533
- BGP IP address/bgpAddress: 10.1.1.1

Another callout points to the virtual network you created in your resource group. The address space for the virtual network is 10.2.0.0/16. The Local BGP address and Peer BGP address can't be in the same address space.

## Create local network gateway

Create a local network gateway in the Azure portal. You need several details from the remote network configuration, including the Microsoft gateway endpoint, ASN, and BGP address, to complete this step.

If you select **No redundancy** when creating device links in the Microsoft Entra admin center, create one local network gateway.

If you select **Zone redundancy**, create two local network gateways. You have two sets of `endpoint`, `asn`, and `bgpAddress` in `localConfigurations` for the device links. The **View Configuration** details for that remote network in the Microsoft Entra admin center provide this information.

1. From the Azure portal, browse to **Local network gateways**.
2. Select **Create**.
3. Select your **Resource group** (for example, `Network_Simulation`).
4. Select the appropriate region.
5. Provide your local network gateway with a **Name**.
6. For **Endpoint**, select **IP address**, and then provide the `endpoint` IP address from the Microsoft Entra admin center.
7. Select **Next: Advanced**.
8. Set **Configure BGP** to **Yes**.
9. Enter the **Autonomous system number (ASN)** from the `localConfigurations` section of the **View configuration** details.

    - Refer to the **Local network gateway** section of the graphic in the View connectivity configuration section.
10. Enter the **BGP peer IP address** from the `localConfigurations` section of the **View configuration** details.

    ![Screenshot of the ASN and BGP fields in the local network gateway process.](media/how-to-simulate-remote-network/create-azure-local-network-gateway-bgp.png)
11. Select **Review + create** and confirm your settings.
12. Select **Create**.

If you configured zone redundancy when creating device links (which provides two sets of Microsoft gateway endpoints), repeat these steps to create a second local network gateway by using the second set of endpoint, ASN, and BGP address values.

Go to the **Configurations** to review the details of your local network gateway.

![Screenshot of the Azure portal showing configuration settings for a local network gateway.](media/how-to-simulate-remote-network/local-network-gateway-configuration.png)

## Create a site-to-site (S2S) VPN connection

Create a site-to-site VPN connection in the Azure portal. If you configured zone redundancy, create two connections: one for the primary gateway and one for the secondary. Keep all settings set to the default value unless noted.

1. From the Azure portal, browse to **Connections**.
2. Select **Create**.
3. Select your **Resource group** (for example, `Network_Simulation`).
4. Under **Connection type**, select **Site-to-site (IPsec)**.
5. Enter a **Name** for the connection, and select the appropriate **Region**.
6. Select **Next: Settings**.
7. Select your **Virtual network gateway** and **Local network gateway**.
8. Enter the same **Shared key (PSK)** that you configured for the device link in the Microsoft Entra admin center remote network configuration.
9. Check the box for **Enable BGP**.
10. Select **Review + create**. Confirm your settings.
11. Select **Create**.

Repeat these steps to create another connection with second local network gateway.

[![Screenshot of the Azure portal showing configuration settings for a site-to-site connection.](media/how-to-simulate-remote-network/create-site-to-site-connection.png)](media/how-to-simulate-remote-network/create-site-to-site-connection.png#lightbox)

## Verify connectivity

To verify connectivity, you need to simulate the traffic flow. One method is to create a virtual machine (VM) to initiate the traffic.

### Simulate traffic with a virtual machine

To simulate traffic and verify connectivity, create a VM in the virtual network and initiate traffic to Microsoft services. Leave all settings set to the default value unless noted.

1. From the Azure portal, browse to **Virtual machines**.
2. Select **Create** &gt; **Azure virtual machine**.
3. Select your **Resource group** (for example, `Network_Simulation`).
4. Provide a **Virtual machine name**.
5. Select the image you want to use. For this example, select **Windows 11 Pro, version 22H2 - x64 Gen2**.
6. Select **Run with Azure Spot discount** for this test.
7. Provide a **Username** and **Password** for your VM.
8. Confirm that you have an eligible Windows 10 or 11 license with multitenant hosting rights at the bottom of the page.
9. Move to the **Networking** tab.
10. Select your **Virtual network**.
11. Move to the **Management** tab.
12. Check the box **Login with Microsoft Entra ID**.
13. Select **Review + create**. Confirm your settings.
14. Select **Create**.

You might choose to lock down remote access to the network security group to only a specific network or IP.

### Avoid asymmetric routing when connecting to virtual machines in remote networks

When you connect an Azure virtual machine (VM) to a Global Secure Access remote network, you can't use Remote Desktop Protocol (RDP) as-is to connect to the VM by using its public IP address. If you disconnect the remote network, RDP works again. Asymmetric routing causes this behavior and is expected.

Here's why it happens: the VM has a public IP address, so inbound RDP traffic (the SYN packet) from your PC reaches the VM directly. However, because Global Secure Access advertises the entire internet address range, the VM's return traffic (the SYN-ACK) routes through the IPsec tunnel to Global Secure Access. Global Secure Access receives a SYN-ACK for a session with no corresponding SYN, so it drops the packet and the connection fails. This condition makes the VM's public IP address unusable for inbound connections.

**Workarounds**

To avoid asymmetric routing problems with remote networks, use one of these workarounds:

- Use Azure Bastion

    [Azure Bastion](/en-us/azure/bastion/bastion-overview) eliminates asymmetric routing for remote management scenarios like RDP. By using Bastion, your PC connects to the Bastion service over HTTPS, and Bastion initiates the RDP session to the VM by using its private IP address. The VM responds directly to Bastion within the virtual network. Because both directions of the connection stay inside the virtual network, traffic never passes through the Global Secure Access gateway, and routing remains symmetric.
- Use point-to-site (P2S) VPN with your VNG

    If you configure a virtual network gateway (VNG) for [point-to-site (P2S) connectivity](/en-us/azure/vpn-gateway/point-to-site-about), your client device receives a private IP address from the VNG address pool by using the [Azure VPN Client](/en-us/azure/vpn-gateway/point-to-site-vpn-client-certificate-windows-azure-vpn-client). All traffic to the VM flows through the VNG tunnel and returns the same way, keeping routing symmetric.

### Verify connectivity status

After you create the remote networks and connections, it might take a few minutes for the connection to be established. From the Azure portal, you can validate that the VPN tunnel is connected and that BGP peering is successful.

1. In the Azure portal, browse to the **virtual network gateway** you created and select **Connections**.
2. Each of the connections shows a **Status** of **Connected** once the configuration is applied and successful.
3. Browse to **BGP peers** under the **Monitoring** section to confirm that BGP peering is successful. Look for the peer addresses provided by Microsoft. Once the configuration is applied and successful, the **Status** shows **Connected**.

[![Screenshot showing how to find the connection status for your virtual network gateway.](media/how-to-simulate-remote-network/verify-connectivity.png)](media/how-to-simulate-remote-network/verify-connectivity.png#lightbox)

You can use the virtual machine you created to validate that traffic is flowing to Microsoft services. Browsing to resources in SharePoint or Exchange Online should result in traffic on your virtual network gateway. You can see this traffic by browsing to [Metrics on the virtual network gateway](/en-us/azure/vpn-gateway/monitor-vpn-gateway#analyzing-metrics) or by [Configuring packet capture for VPN gateways](/en-us/azure/vpn-gateway/packet-capture).

Tip

If you're using this article for testing Microsoft Entra Internet Access, clean up all related Azure resources by deleting the new resource group when you're done.