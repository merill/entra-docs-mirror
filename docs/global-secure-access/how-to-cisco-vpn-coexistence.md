---
layout: Conceptual
title: Security Service Edge (SSE) Coexistence With Microsoft and Cisco VPNs - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-cisco-vpn-coexistence
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Configure Microsoft Global Secure Access alongside Cisco AnyConnect and ASA VPNs for unified SASE. Covers deployment scenarios with step-by-step configuration for private access, Microsoft 365 traffic, and internet access.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: shkhalid
ai-usage: ai-assisted
locale: en-us
document_id: c7af86c8-7102-6ab3-1201-761fae3e51f3
document_version_independent_id: c7af86c8-7102-6ab3-1201-761fae3e51f3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-cisco-vpn-coexistence.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-cisco-vpn-coexistence
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-cisco-vpn-coexistence.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bad69977-db6a-44f3-b752-d2bee7de49ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/440fefb2-823b-44b8-a593-35604cde23b7
- https://authoring-docs-microsoft.poolparty.biz/devrel/9f747546-6aa0-47b1-90d7-ee9646fdb207
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31d7aff-61be-45e2-a324-a578cf0c3360
- https://authoring-docs-microsoft.poolparty.biz/devrel/1b2df129-9f07-41b8-9038-0761a41d8a21
- https://authoring-docs-microsoft.poolparty.biz/devrel/c49cc9cb-c0e4-4c7c-8e26-9ab61f52e8b0
platformId: ba88a2f9-0022-f405-f93c-4be55c9caff2
---

# Security Service Edge (SSE) Coexistence With Microsoft and Cisco VPNs - Global Secure Access | Microsoft Learn

## Overview

Organizations require robust, unified solutions to ensure secure and seamless connectivity. Microsoft Secure Access Service Edge (SASE) capabilities that, when integrated with Cisco Virtual Private Networks (VPN), provide enhanced security and connectivity for diverse access scenarios.

This guide outlines how to configure and deploy Microsoft Entra solutions alongside Cisco VPN offerings. By using both platforms, you can optimize your organization's security posture while maintaining high-performance connectivity for private applications, Microsoft 365 traffic, and internet access.

## Cisco remote access VPN platforms

This guide focuses on two Cisco remote access VPN platforms:

- **Cisco Secure Access VPN-as-a-Service (VPNaaS)**
- **Cisco Adaptive Security Appliance (ASA) Remote Access VPN**

## Cisco Secure Access VPNaaS

### Cisco Secure Access VPNaaS - scenarios

1. **Microsoft Entra Internet Access and Microsoft Access with Cisco Secure Access VPNaaS for private access.** Global Secure Access handles internet and Microsoft traffic. Cisco Secure Access VPNaaS captures only private application traffic.
2. **Microsoft Entra Private Access, Internet Access, and Microsoft Access with Cisco Secure Access VPNaaS.** Both clients handle traffic for separate private applications. Global Secure Access handles private applications in Microsoft Entra Private Access, while private applications hosted through Cisco Secure Access VPNaaS are accessed through Cisco Secure Client VPN. Global Secure Access handles internet and Microsoft traffic.

### Cisco Secure Access VPNaaS - prerequisites

To configure Microsoft and Cisco Secure Access VPNaaS for a unified SASE solution:

1. Set up Microsoft Entra Internet Access and Microsoft Entra Private Access. These products make up the Global Secure Access solution.
2. Establish connectivity to Cisco Secure Access VPNaaS.
3. Set up a Cisco remote access VPN profile.
4. Configure fully qualified domain name (FQDN) and IP bypasses (instructions below).

### Cisco Secure Access VPNaaS - Global Secure Access setup

1. Enable and disable different traffic forwarding profiles for your Microsoft Entra tenant. For more information, see [Global Secure Access traffic forwarding profiles](concept-traffic-forwarding).
2. Install and configure the Microsoft Entra private network connector. See [How to configure connectors](how-to-configure-connectors). 
    Note

    Private network connectors are required for Microsoft Entra Private Access applications.
3. Configure Quick Access to private resources and set up private Domain Name System (DNS) and DNS suffixes. See [How to configure Quick Access](how-to-configure-quick-access).
4. Install and configure the Global Secure Access client on end-user devices. See [Global Secure Access clients](concept-clients).
5. Add an Internet Access traffic forwarding profile custom bypass to exclude Cisco Secure Access VPNaaS service FQDN.
    1. Sign in to Microsoft Entra admin center and browse to **Global Secure Access &gt; Connect &gt; Traffic forwarding &gt; Internet access profile**.
    2. Under Internet access policies, select **View**.
    3. Expand **Custom Bypass** and select **Add rule**.
    4. Leave destination type as FQDN and enter the Cisco Secure Access VPN head end service domain, `*.vpn.sse.cisco.com` in Destination.
    5. Select **Save**.

### Cisco Secure Access VPNaaS - Cisco Secure Access setup

#### Split-Include configuration

1. Configure the VPN profile Traffic Steering:
    1. From the Cisco Secure Access portal, go to **Connect &gt; End User Connectivity &gt; Virtual Private Network**.
    2. Select your VPN Profile, then **Traffic Steering**.
    3. In Tunnel Mode, select **Bypass Secure Access** and add exceptions (what to tunnel) for your private application subnets and the Global Secure Access synthetic IP range, `6.6.0.0/16`.
    4. In DNS Mode, select **Split DNS** and add the domain suffix of your private applications.
2. Install the Cisco Secure Client software.

Note

Currently **Split-Include** is the only supported Cisco Secure Access VPNaaS configuration.

## Cisco Secure Access VPNaaS - configuration scenarios

### 1. Microsoft Entra Internet Access and Microsoft Access with Cisco Secure Access VPNaaS for private access

Important

A side-build of the Global Secure Access client for macOS is required for this specific scenario. Contact support for more information.

**Global Secure Access configuration:**

1. Enable Microsoft Entra Internet Access and Microsoft Access forwarding profiles.
2. Install and configure the Global Secure Access client for Windows or macOS.
3. Add an Internet Access traffic forwarding profile custom bypass to exclude Cisco Secure Access VPNaaS service. Add a custom bypass rule for `*.vpn.sse.cisco.com` in the Internet Access profile. For detailed steps, see Adding a custom bypass.

**Cisco configuration:**

1. Set up remote access VPN profile as described previously.
2. Install Cisco Secure Client with VPN.

**Validation:**

1. Ensure both clients are enabled.
2. To verify rules are applied and health checks pass, use Advanced Diagnostics in the Global Secure Access client.
3. Test traffic flow by accessing various sites and validating traffic logs in both platforms.
    1. In the system tray, right-click **Global Secure Access Client** &gt; **Advanced Diagnostics** &gt; **Traffic tab** &gt; **Start collecting**.
    2. Access websites: `bing.com`, `salesforce.com`, `outlook.office365.com`.
    3. Verify Global Secure Access client captures traffic from these sites.
    4. In Microsoft Entra admin center, go to **Global Secure Access &gt; Monitor &gt; Traffic logs**. Validate traffic is logged.
    5. In Cisco Secure Access portal, go to **Monitor &gt; Activity Search**. Validate traffic to these websites **isn't** captured.
    6. Access private resources via Cisco Secure Client (for example, RDP session).
    7. Validate RDP traffic is missing from Global Secure Access traffic logs and present in Cisco Secure Access logs.
    8. Stop collecting traffic in Global Secure Access client and validate no private application traffic was captured.

### 2. Microsoft Entra Private Access, Internet Access, and Microsoft Access with Cisco Secure Access VPN for private access

**Global Secure Access configuration:**

1. Enable Microsoft Entra Internet Access, Private Access, and Microsoft Access forwarding profiles.
2. Install a private network connector for Microsoft Entra Private Access.
3. Configure Quick Access and set up Private DNS.
4. Create an app segment, for example an SMB file share. This will be the application you want to access through Global Secure Access and not Cisco VPN.
5. Add an Internet Access traffic forwarding profile custom bypass to exclude the Cisco Secure Access VPNaaS endpoint. Add a custom bypass rule for `*.vpn.sse.cisco.com` in the Internet Access profile. For detailed steps, see Adding a custom bypass.
6. Install and configure the Global Secure Access client for Windows or macOS.

**Cisco configuration:**

1. Set up remote access VPN profile using Split-Include mode to tunnel your private app subnets and `6.6.0.0/16`. For detailed steps, see Split-Include configuration.
2. Ensure that you configured applications to access through Cisco ASA VPN, for example an RDP server. These apps should be different from the apps configured in Global Secure Access.
3. Install Cisco Secure Client with VPN.

**Validation:**

1. Ensure both clients are enabled.
2. To verify rules are applied and health checks pass, use Advanced Diagnostics in the Global Secure Access client.
3. Test traffic flow by accessing various sites and validating traffic logs in both platforms.
    1. Start collecting traffic in Global Secure Access client.
    2. Access websites: `bing.com`, `salesforce.com`, `outlook.office365.com`.
    3. Verify Global Secure Access client captures traffic from these sites.
    4. Validate traffic in Microsoft Entra admin center traffic logs.
    5. Validate traffic **isn't** captured in Cisco Secure Access portal.
    6. Access private resources via Cisco Secure Client (e.g, RDP session).
    7. Validate RDP traffic is missing from Global Secure Access logs and present in Cisco Secure Access logs.
    8. Access private application in Microsoft Entra Private Access (for example, SMB file share).
    9. Validate SMB traffic is captured in Global Secure Access logs and not in Cisco Secure Access logs.
    10. Stop collecting traffic in Global Secure Access client.

## Cisco ASA Remote Access VPN

### Cisco ASA Remote Access VPN - scenarios

1. **Microsoft Entra Internet Access and Microsoft Access with Cisco ASA Remote Access VPN for private access.** Global Secure Access handles internet and Microsoft traffic. Cisco ASA captures only private application traffic.
2. **Microsoft Entra Private Access, Internet Access, and Microsoft Access with Cisco ASA Remote Access VPN.** Both clients handle traffic for separate private applications. Global Secure Access handles private applications in Microsoft Entra Private Access, while private applications hosted through Cisco ASA are accessed through Cisco Secure Client VPN. Global Secure Access handles internet and Microsoft traffic.

### Cisco ASA Remote Access VPN - prerequisites

To configure Microsoft and Cisco ASA remote access VPN for a unified SASE solution:

1. Set up Microsoft Entra Internet Access and Microsoft Entra Private Access. These products make up the Global Secure Access solution.
2. Establish remote access connectivity to your Cisco ASA.
3. Configure fully qualified domain name (FQDN) and IP bypasses (instructions below).

### Cisco ASA Remote Access VPN - Global Secure Access setup

1. Enable and disable different traffic forwarding profiles for your Microsoft Entra tenant. For more information, see [Global Secure Access traffic forwarding profiles](concept-traffic-forwarding).
2. Install and configure the Microsoft Entra private network connector. See [How to configure connectors](how-to-configure-connectors).

    Note

    Private network connectors are required for Microsoft Entra Private Access applications.
3. Configure Quick Access to private resources and set up private Domain Name System (DNS) and DNS suffixes. See [How to configure Quick Access](how-to-configure-quick-access).
4. Install and configure the Global Secure Access client on end-user devices. See [Global Secure Access clients](concept-clients).
5. Add an Internet Access traffic forwarding profile custom bypass to exclude Cisco ASA remote access VPN endpoint IP and FQDN.

    1. Sign in to Microsoft Entra admin center and browse to **Global Secure Access &gt; Connect &gt; Traffic forwarding &gt; Internet access profile**.
    2. Under Internet access policies, select **View**.
    3. Expand **Custom Bypass** and select **Add rule**.
    4. Leave destination type as FQDN and enter the FQDN used to connect to your Cisco ASA VPN in Destination.
    5. Set destination type as IP and enter the public IP address of your Cisco ASA.
    6. Select **Save**.

## Cisco ASA VPN setup

### Split-Include configuration (ASA)

Configure split-include for Cisco ASA Remote Access VPN:

1. Sign in to Cisco ASA using the Cisco Adaptive Security Device Manager (ASDM) software.
2. Navigate to **Configuration &gt; Remote Access VPN &gt; Network (Client) Access &gt; Secure Client Connection Profiles**.
3. Select an existing connection profile or create a new one, then select **Edit**.
4. Under **Group Policy**, specify the private IP address of the DNS server used for private traffic.
5. In the group policy settings, expand **Advanced &gt; Split Tunneling** and configure the following:

- **DNS Names**: `Inherit`
- **Send All DNS Lookups Through Tunnel**: `No`
- **Policy**: `Tunnel Network List Below`
- **Network List**: Select the access list that includes your private application IP ranges.

1. Edit the access control list (ACL) to permit the private application IP ranges (for example, `10.101.0.0/16`) and the Global Secure Access synthetic IP range `6.6.0.0/16`.
2. Save and apply your changes.

Note

Currently **Split-Include** is the only supported Cisco ASA VPN configuration.

## Cisco ASA Remote Access VPN - configuration scenarios

### Cisco ASA Remote Access VPN

#### 1. Microsoft Entra Internet Access and Microsoft Access with Cisco ASA Remote Access VPN for private access

**Global Secure Access configuration:**

1. Enable Microsoft Entra Internet Access and Microsoft Access forwarding profiles.
2. Install and configure the Global Secure Access client for Windows or macOS.
3. Add an Internet Access traffic forwarding profile custom bypass to exclude the Cisco ASA remote access URL and public IP address. For detailed steps, see Adding a custom bypass for Cisco ASA.

**Cisco configuration:**

1. Configure Cisco ASA remote access VPN connection profile for split-include mode to tunnel your private app subnets. For detailed steps, see Split-Include configuration (ASA).
2. Install Cisco Secure Client or AnyConnect software.
3. Connect to your VPN endpoint.

**Validation:**

1. Ensure both clients are enabled.
2. To verify rules are applied and health checks pass, use Advanced Diagnostics in the Global Secure Access client.
3. Test traffic flow by accessing various sites and validating traffic logs in both platforms.
    1. Start collecting traffic in Global Secure Access client.
    2. Access websites: `bing.com`, `salesforce.com`, `outlook.office365.com`.
    3. Verify Global Secure Access client captures traffic from these sites.
    4. Validate traffic in Microsoft Entra admin center traffic logs.
    5. Validate website traffic **isn't** captured by your Cisco ASA.
    6. Access private resources via Cisco Secure Client (for example, RDP session).
    7. Validate RDP traffic is missing from Global Secure Access logs and present in Cisco logs.
    8. Stop collecting traffic in Global Secure Access client.

#### 2. Microsoft Entra Private Access, Internet Access, and Microsoft Access with Cisco ASA Remote Access VPN for private access

**Global Secure Access configuration:**

1. Enable Microsoft Entra Internet Access, Private Access, and Microsoft Access forwarding profiles.
2. Install a Private Network Connector for Microsoft Entra Private Access.
3. Configure Quick Access and set up Private DNS.
4. Create an app segment, for example an SMB file share. This will be the application you want to access through Global Secure Access and not Cisco ASA VPN.
5. Add an Internet Access traffic forwarding profile custom bypass to exclude the Cisco ASA remote access URL and public IP address. For detailed steps, see Adding a custom bypass for Cisco ASA.
6. Install and configure the Global Secure Access client for Windows or macOS.

**Cisco configuration:**

1. Configure Cisco ASA remote access VPN connection profile for split-include mode to tunnel your private app subnets. For detailed steps, see Split-Include configuration (ASA).
2. Ensure that you configured applications to access through Cisco ASA VPN, for example an RDP server. These apps should be different from the apps configured in Global Secure Access.
3. Install Cisco Secure Client software.
4. Connect to your VPN endpoint.

**Validation:**

1. Ensure both clients are enabled.
2. To verify rules are applied and health checks pass, use Advanced Diagnostics in the Global Secure Access client.
3. Test traffic flow by accessing various sites and validating traffic logs in both platforms.
    1. Start collecting traffic in Global Secure Access client.
    2. Access websites: `bing.com`, `salesforce.com`, `outlook.office365.com`.
    3. Verify Global Secure Access client captures traffic from these sites.
    4. Validate traffic in Microsoft Entra admin center traffic logs.
    5. Validate website traffic **isn't** captured by your Cisco ASA.
    6. Access private resources via Cisco Secure Client (for example, RDP session).
    7. Validate RDP traffic is missing from Global Secure Access logs and present in Cisco logs.
    8. Access private application in Microsoft Entra Private Access (for example, SMB file share).
    9. Validate SMB traffic is captured in Global Secure Access logs and not in Cisco logs.
    10. Stop collecting traffic in Global Secure Access client.

Note

For troubleshooting health check failures, see [Troubleshoot the Global Secure Access client: Health check](troubleshoot-global-secure-access-client-diagnostics-health-check).