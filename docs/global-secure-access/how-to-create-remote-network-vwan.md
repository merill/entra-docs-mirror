---
layout: Conceptual
title: Simulate remote network connectivity using Azure vWAN - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-create-remote-network-vwan
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Use Global Secure Access to configure Azure and Microsoft Entra resources to create a virtual wide area network to connect to your resources in Azure.
ms.topic: how-to
ms.date: 2026-04-15T00:00:00.0000000Z
ms.reviewer: abhijeetsinha
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2463e92e-9a82-c81f-3df1-e7cb8c82538d
document_version_independent_id: 2463e92e-9a82-c81f-3df1-e7cb8c82538d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-create-remote-network-vwan.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-create-remote-network-vwan
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-create-remote-network-vwan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1f65811f-19b7-4374-b6b1-7dab3f416544
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/70626ef6-54d7-4e8b-8405-9b018e6f8179
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 11c6345d-3d98-5fbc-ed44-db4e968c1ed9
---

# Simulate remote network connectivity using Azure vWAN - Global Secure Access | Microsoft Learn

This article explains how to simulate remote network connectivity by using a remote virtual wide-area network (vWAN). To simulate remote network connectivity by using an Azure virtual network gateway (VNG), see [Simulate remote network connectivity using Azure VNG](/en-us/entra/global-secure-access/how-to-simulate-remote-network).

## Prerequisites

To complete the steps in this process, you need the following prerequisites:

- An Azure subscription and permission to create resources in the [Azure portal](https://portal.azure.com).
- A basic understanding of virtual wide area networks (vWAN).
- A basic understanding of [site-to-site VPN connections](/en-us/azure/vpn-gateway/tutorial-site-to-site-portal).
- A Microsoft Entra tenant with the [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role assigned.
- A basic understanding of Azure virtual desktops or Azure virtual machines.

This document uses the following example values, along with the values in the images and steps. Feel free to configure these settings according to your own requirements.

- Subscription: Visual Studio Enterprise
- Resource group name: GlobalSecureAccess\_Documentation
- Region: South Central US

## High-level steps

To create a remote network using Azure vWAN, you need access to both the Azure portal and the Microsoft Entra admin center. To easily switch between them, keep Azure and Microsoft Entra open in separate tabs. Because certain resources can take more than 30 minutes to deploy, set aside at least two hours to complete this process. Reminder: Resources left running can cost you money. When done testing, or at the end of a project, remove the resources that you no longer need.

1. Set up a vWAN in the Azure portal
    1. Create a vWAN
    2. Create a virtual hub with a site-to-site VPN gateway*The virtual hub takes about 30 minutes to deploy.*
    3. Obtain VPN gateway information
2. Create a remote network in the Microsoft Entra admin center
3. Create a VPN site using the Microsoft gateway
    1. Create a VPN site
    2. Create a site-to-site connection*The site-to-site connection takes about 30 minutes to deploy.*
    3. Check border gateway protocol connectivity and learned routes in Microsoft Azure portal
    4. Check connectivity in Microsoft Entra admin center
4. Configure security features for testing
    1. Create a virtual network
    2. Add a virtual network connection to the vWAN
    3. Create an Azure virtual Desktop*The Azure virtual Desktop takes about 30 minutes to deploy. The Bastion takes another 30 minutes.*
5. Test security features with Azure virtual Desktop (AVD)
    1. Test the tenant restriction
    2. Test source IP restoration

## Set up a vWAN in the Azure portal

There are three main steps to set up a vWAN:

1. Create a vWAN
2. Create a virtual hub with a site-to-site VPN gateway
3. Obtain VPN gateway information

### Create a vWAN

Create a vWAN to connect to your resources in Azure. For more information about vWAN, see the [vWAN Overview](/en-us/azure/virtual-wan/virtual-wan-about).

1. From the Microsoft Azure portal, in the **Search resources** bar, type **vWAN** in the search box and select **Enter**.
2. Select **vWANs** from the results. On the vWANs page, select **+ Create** to open the **Create WAN** page.
3. On the **Create WAN** page, on the **Basics**tab, fill in the fields. Modify the example values to apply to your environment.
    - **Subscription**: Select the subscription that you want to use.
    - **Resource group**: Create new or use existing.
    - **Resource group location**: Choose a resource location from the dropdown. A WAN is a global resource and doesn't live in a particular region. However, you must select a region to manage and locate the WAN resource that you create.
    - **Name**: Type the name that you want to call your vWAN.
    - **Type**: Basic or Standard. Select **Standard**. If you select Basic, understand that Basic vWANs can only contain Basic hubs. Basic hubs can only be used for site-to-site connections.
4. After filling out the fields, at the bottom of the page, select **Review + create**. [![Screenshot of the Create WAN page with completed fields.](media/how-to-create-remote-network-vwan/create-vwan.png)](media/how-to-create-remote-network-vwan/create-vwan-expanded.png#lightbox)
5. Once validation passes, select the **Create** button.

### Create a virtual hub with a VPN gateway

Next, create a virtual hub with a site-to-site virtual private network (VPN) gateway:

1. Within the new vWAN, under **Connectivity**, select **Hubs**.
2. Select **+ New Hub**.
3. On the **Create virtual hub** page, on the **Basics**tab, fill in the fields according to your environment.
    - **Region**: Select the region in which you want to deploy the virtual hub.
    - **Name**: Enter the name for the virtual hub.
    - **Hub private address space**: Use 10.101.0.0/24 for this example. To create a hub, the address range must be in Classless Inter-Domain Routing (CIDR) notation and have a minimum address space of /24.
    - **Virtual hub capacity**: For this example, select **2 Routing Infrastructure Units, 3 Gbps Router, Supports 2000 VMs**. For more information, see [Virtual hub settings](/en-us/azure/virtual-wan/hub-settings).
    - **Hub routing preference**: Leave as default. For more information, see [Virtual hub routing preference](/en-us/azure/virtual-wan/about-virtual-hub-routing-preference).
    - Select **Next : Site to site &gt;**. [![Screenshot of the Create virtual hub page, on the Basics tab, with completed fields.](media/how-to-create-remote-network-vwan/vwan-create-new-hub-basics.png)](media/how-to-create-remote-network-vwan/vwan-create-new-hub-basics-expanded.png#lightbox)
4. On the **Site to site**tab, complete the following fields:
    - Select **Yes**to create a Site-to-site (VPN gateway).
        - **AS Number**: You can't edit the **AS Number** field.
    - **Gateway scale units**: Select **1 scale unit - 500 Mbps x 2** for this example. This value should align with the aggregate throughput of the VPN gateway being created in the virtual hub.
    - **Routing preference**: For this example, select **Microsoft network** for how to route your traffic between Azure and the internet. For more information about routing preference via a Microsoft network or Internet Service Provider (ISP), see the [Routing preference](/en-us/azure/virtual-network/ip-services/routing-preference-overview) article. [![Screenshot of the Create virtual hub page, on the Site to site tab, with completed fields.](media/how-to-create-remote-network-vwan/vwan-create-new-hub-site-to-site.png)](media/how-to-create-remote-network-vwan/vwan-create-new-hub-site-to-site-expanded.png#lightbox)
5. Leave the remaining tab options set to their defaults and select **Review + create** to validate.
6. Select **Create** to create the hub and gateway. *This process can take up to 30 minutes*.
7. After 30 minutes, **Refresh** to view the hub on the **Hubs** page, and then select **Go to resource** to go to the resource.

### Obtain VPN gateway information

To create a remote network in the Microsoft Entra admin center, you need to view and record the VPN gateway information for the virtual hub you created in the previous step.

1. Within the new vWAN, under **Connectivity**, select **Hubs**.
2. Select the virtual hub.
3. Select **VPN (Site to site)**.
4. On the Virtual Hub page, select the **VPN Gateway** link. [![Screenshot of the VPN (Site to site) page, with the VPN Gateway link visible.](media/how-to-create-remote-network-vwan/vwan-create-new-hub-access-hub-hub-1-vpn-gateway.png)](media/how-to-create-remote-network-vwan/vwan-create-new-hub-access-hub-hub-1-vpn-gateway-expanded.png#lightbox)
5. On the VPN Gateway page, select **JSON View**.
6. Copy the JSON text into a file for reference in upcoming steps. Make note of the **autonomous system number (ASN)**, device **IP address**, and the device **border gateway protocol (BGP) address** to use in the Microsoft Entra admin center in the next step. 

    ```json
       "bgpSettings": {
            "asn": 65515,
            "peerWeight": 0,
            "bgpPeeringAddresses": [
                {
                    "ipconfigurationId": "Instance0",
                    "defaultBgpIpAddresses": [
                        "10.101.0.12"
                    ],
                    "customBgpIpAddresses": [],
                    "tunnelIpAddresses": [
                        "203.0.113.250",
                        "10.101.0.4"
                    ]
                },
                {
                    "ipconfigurationId": "Instance1",
                    "defaultBgpIpAddresses": [
                        "10.101.0.13"
                    ],
                    "customBgpIpAddresses": [],
                    "tunnelIpAddresses": [
                        "203.0.113.251",
                        "10.101.0.5"
                    ]
                }
            ]
        }
    ```

Tip

You can't change the ASN value.

## Create a remote network in the Microsoft Entra admin center

In this step, use the network information from the VPN gateway to create a remote network in the Microsoft Entra admin center. The first step is to provide the name and location of your remote network.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator).
2. Navigate to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**.
3. Select the **Create remote network**button and provide the details.
    - **Name**: For this example, use Azure\_vWAN.
    - **Region**: For this example, select **South Central US**.
4. Select **Next: Connectivity** to proceed to the **Connectivity** tab. [![Screenshot of the Create a remote network page on the Basics tab, with the Next: Connectivity button highlighted.](media/how-to-create-remote-network-vwan/entra-create-remote-network-basics-tab.png)](media/how-to-create-remote-network-vwan/entra-create-remote-network-basics-tab-expanded.png#lightbox)
5. On the **Connectivity** tab, add device links for the remote network. Create one link for the VPN gateway's *Instance0* and another link for the VPN gateway's *Instance1*:
    1. Select **+ Add a link**.
    2. Complete the fields on the **General** tab in the **Add a link** form, using the VPN gateway's *Instance0*configuration from the JSON view:
        - **Link name**: Name of your Customer Premises Equipment (CPE). For this example, **Instance0**.
        - **Device type**: Choose a device option from the dropdown list. Set to **Other**.
        - **Device IP address**: Public IP address of your device. For this example, use **203.0.113.250**.
        - **Device BGP address**: Enter the Border Gateway Protocol (BGP) IP address of your CPE. For this example, use **10.101.0.4**.
        - **Device ASN**: Provide the autonomous system number (ASN) of the CPE. For this example, the ASN is **65515**.
        - **Redundancy**: Set to **No redundancy**.
        - **Zone redundant local BGP address**: This optional field shows up only when you select **Zone redundancy**.

            - Enter a BGP IP address that *isn't* part of your on-premises network where your CPE resides and is different from the **Local BGP address**.
        - **Bandwidth capacity (Mbps)**: Specify tunnel bandwidth. For this example, set to **250 Mbps**.
        - **Local BGP address**: Use a BGP IP address that *isn't* part of your on-premises network where your CPE resides, such as **192.168.10.10**.

            - Refer to the [valid BGP addresses](reference-remote-network-configurations#valid-bgp-addresses) list for reserved values that can't be used.

            ![Screenshot of the Add a link form with arrows showing the relationship between the JSON code and the link information.](media/how-to-create-remote-network-vwan/vwan-json-add-a-link-general-crop.png)
    3. Select the **Next** button to view the **Details** tab. Keep the default settings.
    4. Select the **Next** button to view the **Security** tab.
    5. Enter the **Preshared key (PSK)**. The same secret key must be used on your CPE.
    6. Select the **Save** button.

For more information about links, see the article, [How to manage remote network device links](how-to-manage-remote-network-device-links).

1. Repeat the above steps to create a second device link using the VPN gateway's *Instance1*configuration.
    1. Select **+ Add a link**.
    2. Complete the fields on the **General** tab in the **Add a link** form, using the VPN gateway's *Instance1*configuration from the JSON view:
        - **Link name**: Instance1
        - **Device type**: Other
        - **Device IP address**: 203.0.113.251
        - **Device BGP address**: 10.101.0.5
        - **Device ASN**: 65515
        - **Redundancy**: No redundancy
        - **Bandwidth capacity (Mbps)**: 250 Mbps
        - **Local BGP address**: 192.168.10.11
    3. Select the **Next** button to view the **Details** tab. Keep the default settings.
    4. Select the **Next** button to view the **Security** tab.
    5. Enter the **Preshared key (PSK)**. The same secret key must be used on your CPE.
    6. Select the **Save** button.
2. Proceed to the **Traffic profiles** tab to select the traffic profile to link to the remote network.
3. Select **Microsoft 365 traffic profile**.
4. Select **Review + create**.
5. Select **Create remote network**.

Navigate to the Remote network page to view the details of the new remote network. There should be one **Region** and two **Links**.

1. Under **Connectivity details**, select the **View configuration** link. [![Screenshot of the Remote network page with the newly created region, its two links, and the View configuration link highlighted.](media/how-to-create-remote-network-vwan/vwan-view-configuration.png)](media/how-to-create-remote-network-vwan/vwan-view-configuration-expanded.png#lightbox)
2. Copy the Remote network configuration text into a file for reference in upcoming steps. Make note of the **Endpoint**, **ASN**, and **BGP address** for each of the links (**Instance0** and **Instance1**). 

    ```json
       {
      "id": "68d2fab0-0efd-48af-bb17-d793f8ec8bd8",
      "displayName": "Instance0",
      "localConfigurations": [
        {
          "endpoint": "203.0.113.32",
          "asn": 65476,
          "bgpAddress": "192.168.10.10",
          "region": "southCentralUS"
        }
      ],
      "peerConfiguration": {
        "endpoint": "203.0.113.250",
        "asn": 65515,
        "bgpAddress": "10.101.0.4"
      }
    },
    {
      "id": "26500385-b1fe-4a1c-a546-39e2d0faa31f",
      "displayName": "Instance1",
      "localConfigurations": [
        {
          "endpoint": "203.0.113.34",
          "asn": 65476,
          "bgpAddress": "192.168.10.11",
          "region": "southCentralUS"
        }
      ],
      "peerConfiguration": {
        "endpoint": "203.0.113.251",
        "asn": 65515,
        "bgpAddress": "10.101.0.5"
      }
    }
    ```

## Create a VPN site using the Microsoft gateway

In this step, create a VPN site, associate the VPN site with the hub, and then validate the connection.

### Create a VPN site

1. In the Microsoft Azure portal, sign in the virtual hub created in the previous steps.
2. Navigate to **Connectivity** &gt; **VPN (Site to site)**.
3. Select **+ Create new VPN site**.
4. On the **Create VPN site** page, complete the fields on the **Basics** tab.
5. Proceed to the **Links**tab. For each link, enter the Microsoft gateway configuration from the Remote network configuration noted in the "view details" step:
    - **Link name**: For this example, **Instance0**; **Instance1**.
    - **Link speed**: For this example, **250** for both links.
    - **Link provider name**: Set to **Other** for both links.
    - **Link IP address / FQDN**: Use the Endpoint address. For this example, **203.0.113.32**; **203.0.113.34**.
    - **Link BGP address**: Use the BGP address, **192.168.10.10**; **192.168.10.11**.
    - **Link ASN**: Use the ASN. For this example, **65476** for both links. ![Screenshot of the Create VPN page, on the Links tab, with completed fields.](media/how-to-create-remote-network-vwan/create-vwan-create-new-vpn-site-links-enhanced.png)
6. Select **Review + create**.
7. Select **Create**.

### Create a site-to-site connection

In this step, associate the VPN site from the previous step with the hub. Next, remove the default hub association:

1. Navigate to **Connectivity** &gt; **VPN (Site to site)**.
2. Select the **X** to remove the default **Hub association : Connected to this hub** filter so the VPN site appears on the list of available VPN sites. [![Screenshot of the VPN (Site to site) page with the X highlighted for the hub association filter.](media/how-to-create-remote-network-vwan/clear-hub-association-filter.png)](media/how-to-create-remote-network-vwan/clear-hub-association-filter-expanded.png#lightbox)
3. Select the VPN site from the list and select **Connect VPN sites**.
4. In the Connect sites form, type the same **Pre-shared key (PSK)** used for the Microsoft Entra admin center.
5. Select **Connect**.
6. After about 30 minutes, the VPN site updates to show success icons for both the **Connection provisioning status** and **Connectivity status**. [![Screenshot of the VPN (Site to site) page showing a successful status for both Connection provisioning and Connectivity.](media/how-to-create-remote-network-vwan/provisioning-status-succeeded.png)](media/how-to-create-remote-network-vwan/provisioning-status-succeeded-expanded.png#lightbox)

### Check BGP connectivity and learned routes in Microsoft Azure portal

In this step, use the BGP Dashboard to check the list of learned routes that the site-to-site gateway is learning.

1. Navigate to **Connectivity** &gt; **VPN (Site to site)**.
2. Select the VPN site created the previous steps.
3. Select **BGP Dashboard**.

    The BGP dashboard lists the **BGP Peers** (VPN gateways and VPN site), which should have a **Status** of **Connected**.
4. To view the list of learned routes, select **Routes the site-to-site gateway is learning**.

The list of **Learned Routes** shows that the site-to-site gateway is learning the Microsoft 365 routes listed in the Microsoft 365 traffic profile. [![Screenshot of the Learned Routes page with the learned Microsoft 365 routes highlighted.](media/how-to-create-remote-network-vwan/list-of-bgp-learned-routes.png)](media/how-to-create-remote-network-vwan/list-of-bgp-learned-routes-expanded.png#lightbox)

The following image shows the traffic profile **Policies & rules** for the Microsoft 365 profile, which should match the routes learned from the site-to-site gateway. [![Screenshot of the Microsoft 365 traffic forwarding profiles, showing the matching learned routes.](media/how-to-create-remote-network-vwan/traffic-profile-match.png)](media/how-to-create-remote-network-vwan/traffic-profile-match-expanded.png#lightbox)

### Check connectivity in Microsoft Entra admin center

View the Remote network health logs to validate connectivity in the Microsoft Entra admin center.

1. In Microsoft Entra admin center, navigate to **Global Secure Access** &gt; **Monitor** &gt; **Remote network health logs**.
2. Select **Add Filter**.
3. Select **Source IP** and type the source IP address for the VPN gateway's *Instance0* or *Instance1* IP address. Select **Apply**.
4. The connectivity should be **"Remote network alive"**.

You can also validate by filtering by **tunnelConnected** or **BGPConnected**. For more information, see [What are remote network health logs?](/en-us/entra/global-secure-access/how-to-remote-network-health-logs).

## Configure security features for testing

In this step, we prepare for testing by configuring a virtual network, adding a virtual network connection to the vWAN, and creating an Azure Virtual Desktop.

### Create a virtual network

In this step, use the Azure portal to create a virtual network.

1. In the Azure portal, search for and select **Virtual networks**.
2. On the **Virtual networks** page, select **+ Create**.
3. Complete the **Basics** tab, including the **Subscription**, **Resource group**, **Virtual network name**, and the **Region**.
4. Select **Next** to proceed to the **Security** tab.
5. In the **Azure Bastion** section, select **Enable Bastion**.

    - Type the **Azure Bastion host name**. For this example, use **Virtual\_network\_01-bastion**.
    - Select the **Azure Bastion public IP address**. For this example, select **(New) default**. ![Screenshot of the Create virtual network screen, on the Security tab, showing the Bastion settings.](media/how-to-create-remote-network-vwan/vwan-bastion-settings.png)
6. Select **Next** to proceed to the **IP addresses tab** tab. Configure the address space of the virtual network with one or more IPv4 or IPv6 address ranges.

    Tip

    Don't use an overlapping address space. For example, if the virtual hub created in the previous steps uses the address space 10.0.0.0/16, create this virtual network with the address space 10.2.0.0/16.
7. Select **Review + create**. When validation passes, select **Create**.

### Add a virtual network connection to the vWAN

In this step, connect the virtual network to the vWAN.

1. Open the vWAN created in the previous steps and navigate to **Connectivity** &gt; **Virtual network connections**.
2. Select **+ Add connection**.
3. Complete the **Add connection**form, selecting the values from the virtual hub and virtual network created in previous sections:
    - **Connection name**: VirtualNetwork
    - **Hubs**: hub1
    - **Subscription**: Contoso Azure Subscription
    - **Resource group**: GlobalSecureAccess\_Documentation
    - **Virtual network**: VirtualNetwork
4. Leave the remaining fields set to their default values and select **Create**. [![Screenshot of the Add connection form with example information in the required fields.](media/how-to-create-remote-network-vwan/vwan-add-connection.png)](media/how-to-create-remote-network-vwan/vwan-add-connection-expanded.png#lightbox)

### Create an Azure Virtual Desktop

In this step, create a virtual desktop and host it with Bastion.

1. In the Azure portal, search for and select **Azure Virtual Desktop**.
2. On the **Azure Virtual Desktop** page, select **Create a host pool**.
3. Complete the **Basics**tab with the following:
    - The **Host pool name**. For this example, **VirtualDesktops**.
    - The **Location** of the Azure Virtual Desktop object. In this case, **South Central US**.
    - **Preferred app group type**: select **Desktop**.
    - **Host pool type**: select **Pooled**.
    - **Load balancing algorithm**: select **Breadth-first**.
    - **Max session limit**: select **2**.
4. Select **Next: Virtual Machines**.
5. Complete the **Next: Virtual Machines**tab with the following:
    - **Add virtual machines**: Yes
    - The desired **Resource group**. For this example, **GlobalSecureAccess\_Documentation**.
    - **Name prefix**: avd
    - **Virtual machine type**: select **Azure virtual machine**.
    - **Virtual machine location**: **South Central US**.
    - **Availability options**: select **No infrastructure redundancy required**.
    - **Security type**: select **Trusted launch virtual machine**.
    - **Enable secure boot**: Yes
    - **Enable vTPM**: Yes
    - **Image**: For this example, select **Windows 11 Enterprise multi-session + Microsoft 365 apps version 22H2**.
    - **Virtual machine size**: select **Standard D2s v3, 2 vCPU's, 8-GB memory**.
    - **Number of VMs**: 1
    - **Virtual network**: select the virtual network created in previous step, **VirtualNetwork**.
    - **Domain to join**: select **Microsoft Entra ID**.
    - Enter the admin account credentials.
6. Leave other options to default and select **Review + create**.
7. When validation passes, select **Create**.
8. After about 30 minutes, the host pool will update to show that the deployment is complete.
9. Navigate to Microsoft Azure **Home** and select **Virtual machines**.
10. Select the virtual machine created in the previous steps.
11. Select **Connect** &gt; **Connect via Bastion**.
12. Select **Deploy Bastion**. The system takes about 30 minutes to deploy the Bastion host.
13. After the Bastion is deployed, enter the same admin credentials used to create the Azure Virtual Desktop.
14. Select **Connect**. The virtual desktop launches.

## Test security features with Azure Virtual Desktop (AVD)

In this step, we use the AVD to test access restrictions to the virtual network.

### Avoid asymmetric routing when connecting to virtual machines in remote networks

When you connect an Azure virtual machine (VM) to a Global Secure Access remote network, you can't use Remote Desktop Protocol (RDP) as-is to connect to the VM by using its public IP address. If you disconnect the remote network, RDP works again. Asymmetric routing causes this behavior and is expected.

Here's why it happens: the VM has a public IP address, so inbound RDP traffic (the SYN packet) from your PC reaches the VM directly. However, because Global Secure Access advertises the entire internet address range, the VM's return traffic (the SYN-ACK) routes through the IPsec tunnel to Global Secure Access. Global Secure Access receives a SYN-ACK for a session with no corresponding SYN, so it drops the packet and the connection fails. This condition makes the VM's public IP address unusable for inbound connections.

**Workarounds**

To avoid asymmetric routing problems with remote networks, use one of these workarounds:

- Use Azure Bastion

    [Azure Bastion](/en-us/azure/bastion/bastion-overview) eliminates asymmetric routing for remote management scenarios like RDP. By using Bastion, your PC connects to the Bastion service over HTTPS, and Bastion initiates the RDP session to the VM by using its private IP address. The VM responds directly to Bastion within the virtual network. Because both directions of the connection stay inside the virtual network, traffic never passes through the Global Secure Access gateway, and routing remains symmetric.
- Use point-to-site (P2S) VPN with your VNG

    If you configure a virtual network gateway (VNG) for [point-to-site (P2S) connectivity](/en-us/azure/vpn-gateway/point-to-site-about), your client device receives a private IP address from the VNG address pool by using the [Azure VPN Client](/en-us/azure/vpn-gateway/point-to-site-vpn-client-certificate-windows-azure-vpn-client). All traffic to the VM flows through the VNG tunnel and returns the same way, keeping routing symmetric.

### Test the tenant restriction

Before testing, enable tenant restrictions on the virtual network.

1. In Microsoft Entra admin center, navigate to **Global Secure Access** &gt; **Settings** &gt; **Session management**.
2. Set the **Enable tagging to enforce tenant restrictions on your network** toggle to on.
3. Select **Save**.
4. You can modify the cross-tenant access policy by navigating to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**. For more information, see the article, [Cross-tenant access overview](../external-id/cross-tenant-access-overview).
5. Keep the default settings, which prevent users from logging in with external accounts on managed devices.

To test:

1. Sign in to the Azure Virtual Desktop virtual machine created in the previous steps.
2. Go to https://www.office.com and sign in with an internal organization ID. This test should pass successfully.
3. Repeat the previous step, but with an *external account*. This test should fail due to blocked access.![Screenshot of the 'Access is blocked' message.](media/how-to-create-remote-network-vwan/access-blocked-troubleshooting-details-without-highlight.png)

### Test source IP restoration

Before testing, enable Conditional Access.

1. In Microsoft Entra admin center, navigate to **Global Secure Access** &gt; **Settings** &gt; **Session management**.
2. Select the **Adaptive Access** tab.
3. Set the **Enable Global Secure Access signaling in Conditional Access** toggle to on.
4. Select **Save**. For more information, see the article, [Source IP restoration](how-to-source-ip-restoration).

To test (option 1): Repeat the tenant restriction test from the previous section:

1. Sign in to the Azure Virtual Desktop virtual machine created in the previous steps.
2. Go to https://www.office.com and sign in with an internal organization ID. This test should pass successfully.
3. Repeat the previous step, but with an *external account*. This test should fail because the source **IP address** in the error message is coming from the VPN gateway public IP address instead of the Microsoft SSE proxying the request to Microsoft Entra.![Screenshot of the 'Access is blocked' message with the IP address highlighted.](media/how-to-create-remote-network-vwan/access-blocked-troubleshooting-details-with-highlight.png)

To test (option 2):

1. In Microsoft Entra admin center, navigate to **Global Secure Access** &gt; **Monitor** &gt; **Remote network health logs**.
2. Select **Add Filter**.
3. Select **Source IP** and type the VPN gateway public IP address. Select **Apply**. ![Screenshot of the Remote network health logs page with the Add filter menu open ready to type the Source IP.](media/how-to-create-remote-network-vwan/remote-network-health-logs-filter.png)

The system restores the branch office's customer premises equipment (CPE) IP address. Because the VPN gateway represents the CPE, the health logs show the public IP address of the VPN gateway, not the proxy's IP address.

## Remove unneeded resources

When done testing, or at the end of a project, it's a good idea to remove the resources that you no longer need. Resources left running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.