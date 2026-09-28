---
layout: Conceptual
title: Configure Microsoft and Zscaler for a Unified SASE Solution - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-zscaler-coexistence
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to deploy Microsoft Global Secure Access alongside Zscaler Private Access and Internet Access. Covers four integration scenarios with step-by-step configuration, verification, and traffic testing procedures.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: shkhalid
ai-usage: ai-assisted
ms.custom:
- ai-gen-docs-bap
- ai-gen-title
- ai-seo-date:04/16/2025
- ai-gen-description
locale: en-us
document_id: 8564f207-7508-26ed-1d79-144f0bc5d099
document_version_independent_id: 8564f207-7508-26ed-1d79-144f0bc5d099
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-zscaler-coexistence.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-zscaler-coexistence
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-zscaler-coexistence.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 27c670db-aaf2-b860-456b-b67fb38c2c21
---

# Configure Microsoft and Zscaler for a Unified SASE Solution - Global Secure Access | Microsoft Learn

## Overview

In today's rapidly evolving digital landscape, organizations require robust, and unified solutions to ensure secure and seamless connectivity. Microsoft and Zscaler offer complementary Secure Access Service Edge (SASE) capabilities that, when integrated, provide enhanced security and connectivity for diverse access scenarios.

This guide outlines how to configure and deploy Microsoft Entra solutions alongside Zscaler's Security Service Edge (SSE) offerings. By using the strengths of both platforms, you can optimize your organization's security posture while maintaining high-performance connectivity for private applications, Microsoft 365 traffic, and internet access.

1. **Microsoft Entra Private Access with Zscaler Internet Access**

    In this scenario, Global Secure Access handles private application traffic. Zscaler only captures Internet traffic. Therefore, the Zscaler Private Access module is disabled from the Zscaler portal.
2. **Microsoft Entra Private Access with Zscaler Private Access and Zscaler Internet Access**

    In this scenario, both clients handle traffic for separate private applications. Global Secure Access handles private applications in Microsoft Entra Private Access. Private applications in Zscaler use the Zscaler Private Access module. Zscaler Internet Access handles Internet traffic.
3. **Microsoft traffic with Zscaler Private Access and Zscaler Internet Access**

    In this scenario, Global Secure Access handles all Microsoft 365 traffic. Zscaler Private Access handles Private application traffic and Zscaler Internet Access handles Internet traffic.
4. **Microsoft Entra Internet Access and Microsoft traffic with Zscaler Private Access**

    In this scenario, Global Secure Access handles Internet and Microsoft 365 traffic. Zscaler only captures Private application traffic. Therefore, the Zscaler Internet Access module is disabled from the Zscaler portal.

## Prerequisites

To configure Microsoft and Zscaler for a unified SASE solution, start by setting up Microsoft Entra Internet Access and Microsoft Entra Private Access. Next, configure Zscaler Private Access and Zscaler Internet Access. Finally, make sure to establish the required FQDN and IP bypasses to ensure smooth integration between the two platforms.

- Set up Microsoft Entra Internet Access and Microsoft Entra Private Access. These products make up the Global Secure Access solution.
- Set up Zscaler Private Access and Internet Access
- Configure the Global Secure Access FQDN and IP bypasses

### Prerequisites for Microsoft Global Secure Access

To set up Microsoft Entra Global Secure Access and test all four scenarios described in this article:

- Enable and disable different Microsoft Global Secure Access traffic forwarding profiles for your Microsoft Entra tenant. For more information about enabling and disabling profiles, see [Global Secure Access traffic forwarding profiles](concept-traffic-forwarding).
- Install and configure the Microsoft Entra private network connector. For information on how to install and configure the connector, see [How to configure connectors](how-to-configure-connectors). 
    Note

    Private Network Connectors are required for Microsoft Entra Private Access applications.
- Configure Quick Access to your private resources and set up Private Domain Name System (DNS) and DNS suffixes. For information on how to configure Quick Access, see [How to configure Quick Access](how-to-configure-quick-access).
- Install and configure the Global Secure Access client on end-user devices. For more information about clients, see [Global Secure Access clients](concept-clients). For information on how to install the Windows client, see [Global Secure Access client for Windows](how-to-install-windows-client). For macOS, see [Global Secure Access Client for macOS](how-to-install-macos-client).

### Prerequisites for Zscaler Private Access and Internet Access

To integrate ZscalerPrivate Access and Zscaler Internet Access with Microsoft Global Secure Access, make sure you complete the following prerequisites. These steps ensure smooth integration, better traffic management, and improved security.

- Configure Zscaler Internet Access. For more information about configuring Zscaler, see [Step-by-Step Configuration Guide for ZIA](https://help.zscaler.com/zia/step-step-configuration-guide-zia).
- Configure Zscaler Private Access. For more information about configuring Zscaler, see [Step-by-Step Configuration Guide for ZPA](https://help.zscaler.com/zpa/step-step-configuration-guide-zpa).
- Set up and configure Zscaler Client Connector forwarding profiles. For more information about configuring Zscaler, see [Configuring Forwarding Profiles for Zscaler Client Connector](https://help.zscaler.com/zscaler-client-connector/configuring-forwarding-profiles-zscaler-client-connector).
- Set up and configure Zscaler Client Connector app profiles with Global Secure Access bypasses. For more information about configuring Zscaler, see [Configuring Zscaler Client Connector App Profiles](https://help.zscaler.com/zscaler-client-connector/configuring-zscaler-client-connector-app-profiles).

### Global Secure Access service FQDNs and IPs bypasses

Configure the Zscaler Client Connector app profile to work with Microsoft Entra service Fully Qualified Domain Names (FQDNs) and Internet Protocol (IP) addresses.

These entries need to be present in the app profiles for every scenario:

- IPs: `150.171.15.0/24`, `150.171.18.0/24`, `150.171.19.0/24`, `150.171.20.0/24`, `13.107.232.0/24`, `13.107.233.0/24`, `151.206.0.0/16`, `6.6.0.0/16`
- FQDNs: `internet.edgediagnostic.globalsecureaccess.microsoft.com`, `m365.edgediagnostic.globalsecureaccess.microsoft.com`, `private.edgediagnostic.globalsecureaccess.microsoft.com`, `aps.globalsecureaccess.microsoft.com`, `auth.edgediagnostic.globalsecureaccess.microsoft.com`, `<tenantid>.internet.client.globalsecureaccess.microsoft.com`, `<tenantid>.m365.client.globalsecureaccess.microsoft.com`, `<tenantid>.private.client.globalsecureaccess.microsoft.com`, `<tenantid>.auth.client.globalsecureaccess.microsoft.com`, `<tenantid>.private-backup.client.globalsecureaccess.microsoft.com`, `<tenantid>.internet-backup.client.globalsecureaccess.microsoft.com`, `<tenantid>.m365-backup.client.globalsecureaccess.microsoft.com`, `<tenantid>.auth-backup.client.globalsecureaccess.microsoft.com`.
- Install and configure Zscaler Client Connector software.

## Microsoft Entra Private Access with Zscaler Internet Access

In this scenario, Microsoft Entra Private Access handles private application traffic, while Zscaler Internet Access manages Internet traffic. The Zscaler Private Access module is disabled in the Zscaler portal. To configure Microsoft Entra Private Access, you need to complete several steps. First, enable the forwarding profile. Next, install the Private Network Connector. After that, set up Quick Access and configure Private DNS. Finally, install the Global Secure Access client. For Zscaler Internet Access, the configuration involves creating a forwarding profile and app profile, adding bypass rules for Microsoft Entra services, and installing the Zscaler Client Connector. Finally, the configurations are verified, and traffic flow are tested to ensure proper handling of private and Internet traffic by the respective solutions.

### Configure Microsoft Entra Private Access

To configure Microsoft Entra Private Access for this scenario:

- [Enable Microsoft Entra Private Access forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-private-access-profile.md#enable-the-private-access-traffic-forwarding-profile).
- Install a [Private Network Connector](how-to-configure-connectors) for Microsoft Entra Private Access.
- Configure [Quick Access and set up Private DNS](how-to-configure-quick-access).
- Install and configure the [Global Secure Access client for Windows](how-to-install-windows-client) or [macOS](how-to-install-macos-client).

### Configure Zscaler Internet Access

Complete the following steps in the Zscaler portal:

- Set up and configure [Zscaler Internet Access](https://help.zscaler.com/zia/step-step-configuration-guide-zia).
- Create a forwarding profile.
- Create an app profile.
- Install the Zscaler Client Connector

#### Add a forwarding profile

Add Forwarding Profile from the Client Connector Portal:

1. Navigate to **Zscaler Client Connector admin portal** &gt; **Administration** &gt; **Forwarding Profile** &gt; **Add Forwarding Profile**.
2. Add a **Profile Name** such as `ZIA Only`.
3. Select **Packet Filter-Based** in **Tunnel Driver Type**.
4. Select forwarding profile action as **Tunnel** and select tunnel version. For example, `Z-Tunnel 2.0`
5. Scroll down to **Forwarding profile action for ZPA**.
6. Select **None** for all options in this section.

#### Add an app profile

Add App Profile from the Client Connector Portal:

1. Navigate to **Zscaler Client Connector admin portal** &gt; **App Profiles** &gt; **Windows (or macOS)** &gt; **Add Windows Policy (or macOS)**.
2. Add **Name**, set **Rule Order** such as **1**, select **Enable**, select **User(s)** to apply this policy, and select the **Forwarding Profile**. For example, select **ZIA Only**.
3. Scroll down and add the Microsoft SSE service Internet Protocol (IP) addresses and Fully Qualified Domain Names (FQDNs) in the Global Secure Access service FQDNs and IPs bypasses section, to “**HOSTNAME OR IP ADDRESS BYPASS FOR VPN GATEWAY**” field.

#### Verify client configurations

Go to the system tray to check that Global Secure Access and Zscaler clients are enabled.

Verify configurations for clients:

1. Right-click on **Global Secure Access Client** &gt; **Advanced Diagnostics** &gt; **Forwarding Profile** and verify that Private access and Private DNS rules are applied to this client.
2. Navigate to **Advanced Diagnostics** &gt; **Health Check** and ensure no checks are failing.
3. Right-click on **Zscaler Client** &gt; **Open Zscaler** &gt; **More**. Verify **App Policy** matches configurations in the earlier steps. Validate that it's up to date or update it.
4. Navigate to **Zscaler Client** &gt; **Internet Security**. Verify **Service Status** is `ON` and Authentication Status is `Authenticated`.
5. Navigate to **Zscaler Client** &gt; **Private Access**. Verify **Service Status** is `DISABLED`.

Note

For information troubleshooting health check failures, see [Troubleshoot the Global Secure Access client diagnostics - Health check](troubleshoot-global-secure-access-client-diagnostics-health-check).

#### Test traffic flow

Test traffic flow:

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browser: `bing.com`, `salesforce.com`, `Instagram.com`.
3. In the system tray, right-click **Global Secure Access Client** and select **Advanced Diagnostics** &gt; **Traffic** tab.
4. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from these websites.
5. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to these sites is missing from the Global Secure Access traffic logs.
6. Sign in to Zscaler Internet Access (ZIA) admin portal and browse to **Analytics** &gt; **Web Insights** &gt; **Logs**. Validate traffic related to these sites is present in Zscaler logs.
7. Access your private application set up in Microsoft Entra Private Access. For example, access a File Share via Server Message Block (SMB).
8. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
9. Validate traffic related to File Share **is** captured in the Global Secure Access traffic logs.
10. Sign in to Zscaler Internet Access (ZIA) admin portal and browse to **Analytics** &gt; **Web Insights** &gt; **Logs**. Validate traffic related to the private application isn't present in the Dashboard or traffic logs.
11. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the **Traffic** dialog box, select **Stop collecting**.
12. Scroll to confirm the Global Secure Access client handled only private application traffic.

## Microsoft Entra Private Access with Zscaler Private Access and Zscaler Internet Access

In this scenario, both clients handle traffic for separate private applications. Global Secure Access handles private applications in Microsoft Entra Private Access. Private applications in Zscaler use the Zscaler Private Access module. Zscaler Internet Access handles Internet traffic.

### Configure Microsoft Entra Private Access

To configure Microsoft Entra Private Access for this scenario:

- [Enable Microsoft Entra Private Access forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-private-access-profile.md#enable-the-private-access-traffic-forwarding-profile).
- Install a [Private Network Connector](how-to-configure-connectors) for Microsoft Entra Private Access.
- Configure [Quick Access and set up Private DNS](how-to-configure-quick-access).
- Install and configure the [Global Secure Access client for Windows](how-to-install-windows-client) or [macOS](how-to-install-macos-client).

### Configure Zscaler Private Access and Internet Access

Complete the following steps in the Zscaler portal:

- Set up and configure both Zscaler Internet Access and Zscaler Private Access.
- Create a forwarding profile.
- Create an app profile.
- Install the Zscaler Client Connector.

#### Add a forwarding profile

Add Forwarding Profile from the Client Connector Portal:

1. Navigate to **Zscaler Client Connector admin portal** &gt; **Administration** &gt; **Forwarding Profile** &gt; **Add Forwarding Profile**.
2. Add a **Profile Name** such as `ZIA and ZPA`.
3. Select **Packet Filter-Based** in **Tunnel Driver Type**.
4. Select forwarding profile action as Tunnel, and select tunnel version. For example, `Z-Tunnel 2.0`.
5. Scroll down to **Forwarding profile action for ZPA**.
6. Select Tunnel for all options in this section.

#### Add an app profile

Add App Profile from the Client Connector Portal:

1. Navigate to **Zscaler Client Connector admin portal** &gt; **App Profiles** &gt; **Windows (or macOS)** &gt; **Add Windows Policy (or macOS)**.
2. Add **Name**, set **Rule Order** such as **1**, select **Enable**, select **User(s)** to apply this policy, and select the **Forwarding Profile**. For example, select **ZIA and ZPA**.
3. Scroll down and add the Microsoft SSE service Internet Protocol (IP) addresses and Fully Qualified Domain Names (FQDNs) in the Global Secure Access service FQDNs and IPs bypasses section, to “**HOSTNAME OR IP ADDRESS BYPASS FOR VPN GATEWAY**” field.

#### Verify client configurations

Go to the system tray to check that Global Secure Access and Zscaler clients are enabled.

Verify configurations for clients:

1. Right-click on **Global Secure Access Client** &gt; **Advanced Diagnostics** &gt; **Forwarding Profile** and verify that Private access and Private DNS rules are applied to this client.
2. Navigate to **Advanced Diagnostics** &gt; **Health Check** and ensure no checks are failing.
3. Right-click on **Zscaler Client** &gt; **Open Zscaler** &gt; **More**. Verify **App Policy** matches configurations in the earlier steps. Validate that it's up to date or update it.
4. Navigate to **Zscaler Client** &gt; **Internet Security**. Verify **Service Status** is `ON` and Authentication Status is `Authenticated`.
5. Navigate to **Zscaler Client** &gt; **Private Access**. Verify **Service Status** is `ON` and Authentication Status is `Authenticated`.

Note

For information troubleshooting health check failures, see [Troubleshoot the Global Secure Access client diagnostics - Health check](troubleshoot-global-secure-access-client-diagnostics-health-check).

#### Test traffic flow

Test traffic flow:

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browser: `bing.com`, `salesforce.com`, `Instagram.com`.
3. In the system tray, right-click **Global Secure Access Client** and select **Advanced Diagnostics** &gt; **Traffic** tab.
4. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from these websites.
5. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to these sites is missing from the Global Secure Access traffic logs.
6. Sign in to Zscaler Internet Access (ZIA) admin portal and browse to **Analytics** &gt; **Web Insights** &gt; **Logs**.
7. Validate traffic related to these sites is present in Zscaler logs.
8. Access your private application set up in Microsoft Entra Private Access. For example, access a File Share via SMB.
9. Access your private application set up in Zscaler Private Access. For example, open an RDP session to a private server.
10. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
11. Validate traffic related to the SMB file share private app is captured and that traffic related to the RDP session **isn't** captured in the Global Secure Access traffic logs
12. Sign in to Zscaler Private Access (ZPA) admin portal and browse to **Analytics** &gt; **Diagnostics** &gt; **Logs**. Validate traffic related to the RDP session is present and that traffic related to the SMB file share **isn't** in the Dashboard or Diagnostic logs.
13. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the **Traffic** dialog box, select **Stop collecting**.
14. Scroll to confirm the Global Secure Access client handled private application traffic for the SMB file share and didn't handle the RDP session traffic.

## Microsoft traffic with Zscaler Private Access and Zscaler Internet Access

In this scenario, Global Secure Access handles all Microsoft 365 traffic. Zscaler Private Access handles Private application traffic and Zscaler Internet Access handles Internet traffic.

### Configure Microsoft traffic

To configure Microsoft traffic for this scenario:

- [Enable Microsoft traffic forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-microsoft-profile.md#enable-the-microsoft-traffic-profile).
- Install and configure the [Global Secure Access client for Windows](how-to-install-windows-client) or [macOS](how-to-install-macos-client).

### Configure Zscaler Private Access and Internet Access

Complete the following steps in the Zscaler portal:

- Set up and configure Zscaler Private Access.
- Create a forwarding profile.
- Create an app profile.
- Install the Zscaler Client Connector.

#### Add a forwarding profile

Add Forwarding Profile from the Client Connector Portal:

1. Navigate to **Zscaler Client Connector admin portal** &gt; **Administration** &gt; **Forwarding Profile** &gt; **Add Forwarding Profile**.
2. Add a **Profile Name** such as `ZIA and ZPA`.
3. Select **Packet Filter-Based** in **Tunnel Driver Type**.
4. Select forwarding profile action as Tunnel, and select tunnel version. For example, `Z-Tunnel 2.0`.
5. Scroll down to **Forwarding profile action for ZPA**.
6. Select Tunnel for all options in this section.

#### Add an app profile

Add App Profile from the Client Connector Portal:

1. Navigate to **Zscaler Client Connector admin portal** &gt; **App Profiles** &gt; **Windows (or macOS)** &gt; **Add Windows Policy (or macOS)**.
2. Add **Name**, set **Rule Order** such as **1**, select **Enable**, select **User(s)** to apply this policy, and select the **Forwarding Profile**. For example, select **ZIA and ZPA**.
3. Scroll down and add the Microsoft SSE service Internet Protocol (IP) addresses and Fully Qualified Domain Names (FQDNs) in the Global Secure Access service FQDNs and IPs bypasses section, to “**HOSTNAME OR IP ADDRESS BYPASS FOR VPN GATEWAY**” field.

#### Verify client configurations

Go to the system tray to check that Global Secure Access and Zscaler clients are enabled.

Verify configurations for clients:

1. Right-click on **Global Secure Access Client** &gt; **Advanced Diagnostics** &gt; **Forwarding Profile** and verify that only Microsoft 365 rules are applied to this client.
2. Navigate to **Advanced Diagnostics** &gt; **Health Check** and ensure no checks are failing.
3. Right-click on **Zscaler Client** &gt; **Open Zscaler** &gt; **More**. Verify **App Policy** matches configurations in the earlier steps. Validate that it's up to date or update it.
4. Navigate to **Zscaler Client** &gt; **Internet Security**. Verify **Service Status** is `ON` and Authentication Status is `Authenticated`.
5. Navigate to **Zscaler Client** &gt; **Private Access**. Verify **Service Status** is `ON` and Authentication Status is `Authenticated`.

Note

For information troubleshooting health check failures, see [Troubleshoot the Global Secure Access client diagnostics - Health check](troubleshoot-global-secure-access-client-diagnostics-health-check).

#### Test traffic flow

##### Verify internet traffic routes through Zscaler

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browser: `bing.com`, `salesforce.com`, `Instagram.com`.
3. In the system tray, right-click **Global Secure Access Client** and select **Advanced Diagnostics** &gt; **Traffic** tab.
4. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from these websites.
5. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to these sites is missing from the Global Secure Access traffic logs.
6. Sign in to Zscaler Internet Access (ZIA) admin portal and browse to **Analytics** &gt; **Web Insights** &gt; **Logs**.
7. Validate traffic related to these sites is present in Zscaler logs.

##### Verify private application traffic routes through Zscaler

1. Access your private application set up in Zscaler Private Access. For example, open an RDP session to a private server.
2. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
3. Validate traffic related to the RDP session **isn’t** in the Global Secure Access traffic logs.
4. Sign in to Zscaler Private Access (ZPA) admin portal and browse to **Analytics** &gt; **Diagnostics** &gt; **Logs**. Validate traffic related to the RDP session is present in the Dashboard or Diagnostic logs.

##### Verify Microsoft 365 traffic routes through Global Secure Access

1. Access Outlook Online (`outlook.com`, `outlook.office.com`, `outlook.office365.com`), SharePoint Online (`<yourtenantdomain>.sharepoint.com`).
2. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the **Traffic** dialog box, select **Stop collecting**.
3. Scroll to confirm the Global Secure Access client handled only Microsoft 365 traffic.
4. You can also validate that the traffic is captured in the Global Secure Access traffic logs. In the Microsoft Entra admin center, navigate to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
5. Validate traffic related to Outlook Online and SharePoint Online is missing from Zscaler Internet Access logs in **Analytics** &gt; **Web Insights** &gt; **Logs**.

## Microsoft Entra Internet Access and Microsoft traffic with Zscaler Private Access

In this scenario, Global Secure Access handles Internet and Microsoft 365 traffic. Zscaler only captures private application traffic. Therefore, the Zscaler Internet Access module is disabled from the Zscaler portal.

### Configure Microsoft Entra Internet Access and Microsoft traffic

For this scenario, you need to configure:

- [Enable Microsoft traffic forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-microsoft-profile.md#enable-the-microsoft-traffic-profile) and [Microsoft Entra Internet Access forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-internet-access-profile.md#prerequisites).
- Install and configure the [Global Secure Access client for Windows](how-to-install-windows-client) or [macOS](how-to-install-macos-client).
- Add an [Microsoft Entra Internet Access traffic forwarding profile policy custom bypass](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-internet-access-profile.md#internet-access-traffic-forwarding-profile-policies) to exclude ZPA service.

Adding a custom bypass for Zscaler in Global Secure Access:

1. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding** &gt; **Internet access profile**. Under **Internet access policies** select **View**.
2. Expand **Custom Bypass** and select **Add rule**.
3. Leave destination type `FQDN` and in **Destination** enter `*.prod.zpath.net`.
4. Select **Save**.

### Configure Zscaler Private Access

Complete the following steps in the Zscaler portal:

- Set up and configure Zscaler Private Access.
- Create a forwarding profile.
- Create an app profile.
- Install the Zscaler Client Connector.

#### Add a forwarding profile

Add Forwarding Profile from the Client Connector Portal:

1. Navigate to the **Zscaler Client Connector admin portal** &gt; **Administration** &gt; **Forwarding Profile** &gt; **Add Forwarding Profile**.
2. Add a **Profile Name** such as `ZPA Only`.
3. Select **Packet Filter-Based** in **Tunnel Driver Type**.
4. Select forwarding profile action as **None**.
5. Scroll down to **Forwarding profile action for ZPA**.
6. Select Tunnel for all options in this section.

#### Add an app profile

Add App Profile from the Client Connector Portal:

1. Navigate to **Zscaler Client Connector admin portal** &gt; **App Profiles** &gt; **Windows (or macOS)** &gt; **Add Windows Policy (or macOS)**.
2. Add **Name**, set **Rule Order** such as **1**, select **Enable**, select **User(s)** to apply this policy, and select the **Forwarding Profile**. For example, select **ZPA Only**.
3. Scroll down and add the Microsoft SSE service Internet Protocol (IP) addresses and Fully Qualified Domain Names (FQDNs) in the Global Secure Access service FQDNs and IPs bypasses section, to “**HOSTNAME OR IP ADDRESS BYPASS FOR VPN GATEWAY**” field.

#### Verify client configurations

Open the system tray to check that Global Secure Access and Zscaler clients are enabled.

Verify configurations for clients:

1. Right-click on **Global Secure Access Client** &gt; **Advanced Diagnostics** &gt; **Forwarding Profile** and verify that Microsoft 365 and Internet Access rules are applied to this client.
2. Expand the Internet access rules &gt; Verify that the custom bypass, `*.prod.zpath.net` exists in the profile.
3. Navigate to **Advanced Diagnostics** &gt; **Health Check** and ensure no checks are failing.
4. Right-click on **Zscaler Client** &gt; **Open Zscaler** &gt; **More**. Verify **App Policy** matches configurations in the earlier steps. Validate that it's up to date or update it.
5. Navigate to **Zscaler Client** &gt; **Private Access**. Verify **Service Status** is `ON` and Authentication Status is `Authenticated`.
6. Navigate to **Zscaler Client** &gt; **Internet Security**. Verify **Service Status** is `DISABLED`.

Note

For information troubleshooting health check failures, see [Troubleshoot the Global Secure Access client diagnostics - Health check](troubleshoot-global-secure-access-client-diagnostics-health-check).

#### Test traffic flow

Test traffic flow:

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browser: `bing.com`, `salesforce.com`, `Instagram.com`, Outlook Online (`outlook.com`, `outlook.office.com`, `outlook.office365.com`), SharePoint Online (`<yourtenantdomain>.sharepoint.com`).
3. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to these sites is captured in the Global Secure Access traffic logs.
4. Access your private application set up in Zscaler Private Access. For example, using Remote Desktop (RDP).
5. Sign in to Zscaler Private Access (ZPA) admin portal and browse to **Analytics** &gt; **Diagnostics** &gt; **Logs**. Validate traffic related to the RDP session is present in the Dashboard or Diagnostic logs.
6. Sign in to Zscaler Internet Access (ZIA) admin portal and browse to **Analytics** &gt; **Web Insights** &gt; **Logs**. Validate traffic related to Microsoft 365 and Internet Traffic such as Instagram.com, Outlook Online, and SharePoint Online is missing from ZIA logs.
7. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the **Traffic** dialog box, select **Stop collecting**.
8. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from the private application. Also, observe that the Global Secure Access client **is** capturing traffic for Microsoft 365 and other internet traffic.