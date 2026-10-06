---
layout: Conceptual
title: Security Service Edge (SSE) coexistence with Microsoft and Palo Alto Networks - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-palo-alto-coexistence
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Deploy Microsoft Entra Private Access alongside Palo Alto Prisma Access. Includes configuration steps for secure internet access and private application connectivity.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: shkhalid
ai-usage: ai-assisted
locale: en-us
document_id: 65873ebb-ffe8-3ec6-c197-e348119c11c2
document_version_independent_id: 65873ebb-ffe8-3ec6-c197-e348119c11c2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-palo-alto-coexistence.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-palo-alto-coexistence
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-palo-alto-coexistence.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: b3845034-bb12-7587-8efd-7f4c8499aaf6
---

# Security Service Edge (SSE) coexistence with Microsoft and Palo Alto Networks - Global Secure Access | Microsoft Learn

## Overview

Microsoft and Palo Alto Networks SSE solutions can be used together in a unified environment. When used together, you harness a robust set of capabilities from both platforms to elevate your SASE journey. The synergy between these platforms enhances security and provides seamless connectivity.

This document contains steps to deploy these solutions side by side across several different access scenarios.

1. **Microsoft Entra Private Access with Palo Alto Prisma Access for secure Internet Access**

In this scenario Global Secure Access will handle private application traffic. Prisma Access will only capture Internet traffic.

1. **Microsoft Entra Private Access with Palo Alto Prisma Access for Private Application and Internet Access**

In this scenario both clients will handle traffic for separate private applications. Private applications in Microsoft Entra Private Access will be handled by Global Secure Access while private applications in Prisma Access service connections, or ZTNA connectors, will be accessed through GlobalProtect client. Internet traffic will be handled by Prisma Access.

1. **Microsoft traffic with Palo Alto Prisma Access for Private Application and Internet Access**

In this scenario Global Secure Access will handle all Microsoft 365 traffic. Prisma Access will handle Private applications via service connection or ZTNA connectors. Internet traffic will be handled by Prisma Access.

1. **Microsoft Entra Internet Access and Microsoft traffic with Palo Alto Prisma Access for Private Application Access**

In this scenario Global Secure Access will handle Internet and Microsoft 365 traffic. Prisma Access will only capture private application traffic via service connection or ZTNA connectors.

Note

The following configurations were tested for Palo Alto Prisma Access and managed with Strata Cloud Manager. Private application access was tested through Service Connections and ZTNA connectors. Connectivity to Prisma Access service was provided by GlobalProtect and tested with SSL and IPsec VPN configurations.

**Prerequisites**

To configure Microsoft and Palo Alto Prisma Access for a unified SASE solution, start by setting up Microsoft Entra Internet Access and Microsoft Entra Private Access. Next, configure Prisma Access for private application access by service connection or ZTNA connector. Finally, make sure to establish the required FQDN and IP bypasses to ensure smooth integration between the two platforms.

- Set up Microsoft Entra Internet Access and Microsoft Entra Private Access. These products make up the Global Secure Access solution.
- Set up Palo Alto Prisma Access for Private Access and Internet Access
- Configure the Global Secure Access FQDN and IP bypasses

**Microsoft Global Secure Access**

To set up Global Secure Access and test all scenarios in this documentation you will need to perform the following.

- Enable and disable different Global Secure Access traffic forwarding profiles for your Microsoft Entra tenant. For more information about enabling and disabling profiles, see [Global Secure Access traffic forwarding profiles](/en-us/entra/global-secure-access/concept-traffic-forwarding).
- Install and configure the Microsoft Entra private network connector. For information on how to install and configure the connector, see [How to configure connectors](/en-us/entra/global-secure-access/how-to-configure-connectors).

Note

Private Network Connectors are required for Microsoft Entra Private Access applications.

- Configure Quick Access to your private resources and set up Private Domain Name System (DNS) and DNS suffixes. For information on how to configure Quick Access, see [How to configure Quick Access](/en-us/entra/global-secure-access/how-to-configure-quick-access).
- Install and configure the Global Secure Access client on end-user devices. For more information about clients, see [Global Secure Access clients](/en-us/entra/global-secure-access/concept-clients). For information on how to install the Windows client, see [Global Secure Access client for Windows](/en-us/entra/global-secure-access/how-to-install-windows-client). For macOS, see [Global Secure Access Client for macOS](/en-us/entra/global-secure-access/how-to-install-macos-client).

**Palo Alto Prisma Access**

To integrate Palo Alto Prisma Access with Microsoft Global Secure Access, make sure you complete the following prerequisites. These steps ensure smooth integration, better traffic management, and improved security.

- Set up a service connection or ZTNA Connector for Prisma Access to allow access to private applications. To learn about setting up a service connection see the [Palo Alto documentation for configuring a service connection](https://docs.paloaltonetworks.com/prisma-access/administration/prisma-access-service-connections/configure-a-service-connection). For the ZTNA Connector see the [Palo Alto documentation for configuring a ZTNA Connector](https://docs.paloaltonetworks.com/prisma-access/administration/ztna-connector-in-prisma-access/configure-a-ztna-connector).
- Set up GlobalProtect for mobile users to allow remote access to private applications. For more information see the documentation for [GlobalProtect setup](https://docs.paloaltonetworks.com/prisma-access/administration/prisma-access-mobile-users/mobile-users-globalprotect/set-up-globalprotect-mobile-users).
- Configure the GlobalProtect tunnel settings and app settings to work with Microsoft Entra Private DNS and bypass Microsoft Entra service Fully Qualified Domain Name (FQDN) and Internet Protocol (IP) addresses.

Tunnel Settings:

1. In the **Strata Cloud Manager portal**, go to **Workflows** &gt; **Prisma Access Setup** &gt; **GlobalProtect** &gt; **GlobalProtect App** &gt; **Tunnel Settings**.
2. In the **Split Tunneling** section, exclude traffic by adding the domain and routes: `*.globalsecureaccess.microsoft.com`, `150.171.19.0/24`, `150.171.20.0/24`, `13.107.232.0/24`, `13.107.233.0/24`, `150.171.15.0/24`, `150.171.18.0/24`, `151.206.0.0/16`, `6.6.0.0/16`.

App Settings:

1. In the **Strata Cloud Manager portal**, go to **Workflows** &gt; **Prisma Access Setup** &gt; **GlobalProtect** &gt; **GlobalProtect App** &gt; **App Settings**
2. Scroll to **App Configuration** &gt; **Show Advanced Options** &gt; **DNS** and **uncheck** the box for **Resolve All FQDNs Using DNS Servers Assigned by the Tunnel (Windows Only)**
    Note

    The setting **"Resolve All FQDNs Using DNS Servers Assigned by the Tunnel (Windows Only)"** should be **disabled** when using Microsoft Entra Private DNS (Configurations 1 and 2). During testing, this setting was **enabled** (checked) for Configurations 3 and 4.
3. Navigate to **Workflows** &gt; **Prisma Access Setup** &gt; **GlobalProtect** &gt; **GlobalProtect App**. Select **Push Config** and select **Push** on the top right side of your screen.
4. Verify that the configuration pushed to the GlobalProtect client. Navigate to **Manage** &gt; **Operations** &gt; **Push Status**.
5. Install the Palo Alto Networks GlobalProtect client. For more information on installing the Palo Alto Networks GlobalProtect client, for Windows see [GlobalProtect App for Windows](https://docs.paloaltonetworks.com/globalprotect/6-2/globalprotect-app-user-guide/globalprotect-app-for-windows). For macOS see, [GlobalProtect App for macOS](https://docs.paloaltonetworks.com/globalprotect/6-2/globalprotect-app-user-guide/globalprotect-app-for-mac). To set up the GlobalProtect client there are a lot of options like tying in Microsoft Entra ID to create your accounts. For more information about the options, see [Microsoft Entra single sign-on (SSO) integration with Palo Alto Networks - GlobalProtect](/en-us/entra/identity/saas-apps/palo-alto-networks-globalprotect-tutorial). For the most basic setup, add a local user to the GlobalProtect from Palo Alto Networks’ Strata Cloud Manager.
6. Browse to **Manage** &gt; **Configuration** &gt; **NGFW and Prisma Access**.
7. Select **Configuration Scope** &gt; **GlobalProtect** and then select **Identity Services** &gt; **Local Users & Groups** &gt; **Local Users**. Add a user and password for testing.
8. After the client is installed, users enter the portal address and their credentials.
9. After users sign in, the connection icon turns blue, and clicking on shows it in a connected state. 
    Note

    In Configuration 4, if you face issues connecting with GlobalProtect using local users, try setting up Microsoft Entra SSO.

## Microsoft Entra Private Access with Palo Alto Prisma Access for secure Internet Access

In this scenario Global Secure Access will handle private application traffic. Prisma Access will only capture Internet traffic.

**Microsoft Entra Private Access configuration**

For this scenario you will need to do the following.

- [Enable Microsoft Entra Private Access forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-private-access-profile.md#enable-the-private-access-traffic-forwarding-profile).
- Install a [Private Network Connector](/en-us/entra/global-secure-access/how-to-configure-connectors) for Microsoft Entra Private Access.
- Configure [Quick Access and set up Private DNS](/en-us/entra/global-secure-access/how-to-configure-quick-access).
- Install and configure the [Global Secure Access client for Windows](/en-us/entra/global-secure-access/how-to-install-windows-client) or [macOS](/en-us/entra/global-secure-access/how-to-install-macos-client).

**Palo Alto Prisma Access configuration**

For this scenario you will need to perform the following in the Palo Alto Strata Cloud Manager portal.

- Set up and configure [GlobalProtect for mobile users](https://docs.paloaltonetworks.com/prisma-access/administration/prisma-access-mobile-users/mobile-users-globalprotect/set-up-globalprotect-mobile-users).
- Configure the GlobalProtect tunnel settings and app settings to work with Global Secure Access. Follow the instructions listed in the Tunnel Settings and App Settings above.
- Install the Palo Alto Networks GlobalProtect client for Windows, [GlobalProtect App for Windows](https://docs.paloaltonetworks.com/globalprotect/6-2/globalprotect-app-user-guide/globalprotect-app-for-windows) or macOS, [GlobalProtect App for macOS](https://docs.paloaltonetworks.com/globalprotect/6-2/globalprotect-app-user-guide/globalprotect-app-for-mac).

After both clients are installed and running side by side and configurations from admin portals are complete, go to the system tray to check that Global Secure Access and GlobalProtect clients are enabled.

Verify configuration for Global Secure Access client.

1. Right click on the **Global Secure Access client &gt; Advanced Diagnostics &gt; Forwarding Profile** and verify that Private Access and Private DNS rules are applied to this client.
2. Navigate to **Advanced Diagnostics &gt; Health Check** and ensure no checks are failing.

Note

For information about troubleshooting health check failures, see [Troubleshoot the Global Secure Access client: Health check - Global Secure Access | Microsoft Learn](/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check).

**Test traffic flow**

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browsers: `salesforce.com`, `Instagram.com`, `yelp.com`.
3. In the system tray, right-click **Global Secure Access Client** and select **Advanced Diagnostics** &gt; **Traffic tab**.
4. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from these websites
5. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to these sites is missing from the Global Secure Access traffic logs.
6. Sign in to Palo Alto Networks’ Strata Cloud Manager and browse to **Incidents & Alerts** &gt; **Log Viewer**.
7. Validate traffic related to these sites **is** present in the Prisma Access logs.
8. Access your private application set up in Microsoft Entra Private Access. For example, access a File Share via Server Message Block (SMB).
9. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
10. Validate traffic related to the File Share **is** captured in the Global Secure Access traffic logs.
11. Sign in to Palo Alto Networks’ Strata Cloud Manager and browse to **Incidents & Alerts** &gt; **Log Viewer**. Validate traffic related to the private application isn’t present in the logs.
12. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the **Traffic** dialog box, select **Stop collecting**.
13. Scroll to confirm the Global Secure Access client handled only private application traffic.

## Microsoft Entra Private Access with Palo Alto Prisma Access for Private Application and Internet Access

In this scenario both clients will handle traffic for separate private applications. Private applications in Microsoft Entra Private Access will be handled by Global Secure Access while private applications in Prisma Access service connections, or ZTNA connectors, will be accessed through GlobalProtect client. Internet traffic will be handled by Prisma Access.

**Microsoft Entra Private Access configuration**

For this scenario you will need to:

- [Enable Microsoft Entra Private Access forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-private-access-profile.md#enable-the-private-access-traffic-forwarding-profile).
- Install a [Private Network Connector](/en-us/entra/global-secure-access/how-to-configure-connectors) for Microsoft Entra Private Access.
- Configure [Quick Access and set up Private DNS](/en-us/entra/global-secure-access/how-to-configure-quick-access).
- Install and configure the [Global Secure Access client for Windows](/en-us/entra/global-secure-access/how-to-install-windows-client) or [macOS](/en-us/entra/global-secure-access/how-to-install-macos-client).

**Palo Alto Networks configuration**

For this scenario you will need to perform the following in the Palo Alto Strata Cloud Manager portal.

- Set up and configure [GlobalProtect for mobile users](https://docs.paloaltonetworks.com/prisma-access/administration/prisma-access-mobile-users/mobile-users-globalprotect/set-up-globalprotect-mobile-users).
- Configure the GlobalProtect tunnel settings and app settings to work with Global Secure Access. Follow the instructions listed in the Tunnel Settings and App Settings above.
- Install the Palo Alto Networks GlobalProtect client for Windows, [GlobalProtect App for Windows](https://docs.paloaltonetworks.com/globalprotect/6-2/globalprotect-app-user-guide/globalprotect-app-for-windows) or macOS, [GlobalProtect App for macOS](https://docs.paloaltonetworks.com/globalprotect/6-2/globalprotect-app-user-guide/globalprotect-app-for-mac).

After both clients are installed and running side by side and configurations from admin portals are complete, go to the system tray to check that Global Secure Access and GlobalProtect clients are enabled.

Verify configuration for Global Secure Access client.

1. Right click on the **Global Secure Access client &gt; Advanced Diagnostics &gt; Forwarding Profile** and verify that Private Access and Private DNS rules are applied to this client.
2. Navigate to **Advanced Diagnostics &gt; Health Check** and ensure no checks are failing.

Note

For information about troubleshooting health check failures, see [Troubleshoot the Global Secure Access client: Health check - Global Secure Access | Microsoft Learn](/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check).

**Test traffic flow**

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browsers: `salesforce.com`, `Instagram.com`, `yelp.com`.
3. In the system tray, right-click **Global Secure Access Client** and select **Advanced Diagnostics** &gt; **Traffic tab**.
4. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from these websites.
5. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to these sites is missing from the Global Secure Access traffic logs.
6. Sign in to Palo Alto Networks’ Strata Cloud Manager and browse to **Incidents & Alerts** &gt; **Log Viewer**.
7. Validate traffic related to these sites **is** present in the Prisma Access logs.
8. Access your private application set up in Microsoft Entra Private Access. For example, access a File Share via Server Message Block (SMB).
9. Access your private application set up in Prisma Access through a service connection or ZTNA connector. For example, open an RDP session to a private server.
10. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
11. Validate traffic related to the SMB file share private app is captured and that traffic related to the RDP session **isn’t** captured in the Global Secure Access traffic logs.
12. Sign in to Palo Alto Networks’ Strata Cloud Manager and browse to **Incidents & Alerts** &gt; **Log Viewer**. Validate traffic related to the private RDP session **is** present and that traffic related to the SMB file share **isn’t** in the logs.
13. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the network traffic dialog box, select **Stop collecting**.
14. Scroll to confirm the Global Secure Access client handled private application traffic for the SMB file share and didn't handle the RDP session traffic.

## Microsoft traffic with Palo Alto Prisma Access for Private Application and Internet Access

In this scenario Global Secure Access will handle all Microsoft 365 traffic. Prisma Access will handle Private applications via service connection or ZTNA connectors and Internet traffic.

**Microsoft traffic configuration**

For this scenario you will need to:

- [Enable Microsoft traffic forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-microsoft-profile.md#enable-the-microsoft-traffic-profile).
- Install and configure the [Global Secure Access client for Windows](/en-us/entra/global-secure-access/how-to-install-windows-client) or [macOS](/en-us/entra/global-secure-access/how-to-install-macos-client).

**Palo Alto Networks configuration**

For this scenario you will need to perform the following in the Palo Alto Strata Cloud Manager portal.

- Set up and configure [GlobalProtect for mobile users](https://docs.paloaltonetworks.com/prisma-access/administration/prisma-access-mobile-users/mobile-users-globalprotect/set-up-globalprotect-mobile-users).
- Configure the GlobalProtect tunnel settings and app settings to work with Global Secure Access. Follow the instructions listed in the Tunnel Settings and App Settings above.
- Install the Palo Alto Networks GlobalProtect client for Windows, [GlobalProtect App for Windows](https://docs.paloaltonetworks.com/globalprotect/6-2/globalprotect-app-user-guide/globalprotect-app-for-windows) or macOS, [GlobalProtect App for macOS](https://docs.paloaltonetworks.com/globalprotect/6-2/globalprotect-app-user-guide/globalprotect-app-for-mac).

Note

For this configuration, enable **Resolve All FQDNs Using DNS Servers Assigned by the Tunnel (Windows Only)** in the App Settings.

After both clients are installed and running side by side and configurations from admin portals are complete, go to the system tray to check that Global Secure Access and GlobalProtect clients are enabled.

Verify configuration for Global Secure Access client.

1. Right click on the **Global Secure Access client &gt; Advanced Diagnostics &gt; Forwarding Profile** and verify that Microsoft 365 rules are applied to this client.
2. Navigate to **Advanced Diagnostics &gt; Health Check** and ensure no checks are failing.

Note

For information about troubleshooting health check failures, see [Troubleshoot the Global Secure Access client: Health check - Global Secure Access | Microsoft Learn](/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check).

**Test traffic flow**

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browsers: `salesforce.com`, `Instagram.com`, `yelp.com`.
3. In the system tray, right-click **Global Secure Access Client** and select **Advanced Diagnostics** &gt; **Traffic tab**.
4. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from these websites.
5. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to these sites is missing from the Global Secure Access traffic logs.
6. Sign in to Palo Alto Networks’ Strata Cloud Manager and browse to **Incidents & Alerts** &gt; **Log Viewer**.
7. Validate traffic related to these sites **is** present in the Prisma Access logs.
8. Access your private application set up in Prisma Access through a service connection or ZTNA connector. For example, open an RDP session to a private server.
9. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
10. Validate traffic related to the RDP session **isn’t** in the Global Secure Access traffic logs
11. Sign in to Palo Alto Networks’ Strata Cloud Manager and browse to **Incidents & Alerts** &gt; **Log Viewer**. Validate traffic related to the RDP session is present in the Prisma Access logs.
12. Access Outlook Online (`outlook.com`, `outlook.office.com`, `outlook.office365.com`), SharePoint Online (`<yourtenantdomain>.sharepoint.com`).
13. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the **Traffic** dialog box, select **Stop collecting**.
14. Scroll to confirm the Global Secure Access client handled only Microsoft 365 traffic.
15. You can also validate that the traffic is captured in the Global Secure Access traffic logs. In the Microsoft Entra admin center, navigate to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
16. Validate traffic related to Outlook Online and SharePoint Online is missing from Prisma Access logs in Strata Cloud Manager **Incidents & Alerts** &gt; **Log Viewer**.

## Microsoft Entra Internet Access and Microsoft traffic with Palo Alto Prisma Access for Private Application Access

In this scenario Global Secure Access will handle Internet and Microsoft traffic. Prisma Access will only capture private application traffic via service connection or ZTNA connectors.

**Microsoft Entra Internet Access and Microsoft traffic configuration**

For this scenario you will need to do the following.

- [Enable Microsoft traffic forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-microsoft-profile.md#enable-the-microsoft-traffic-profile) and [Microsoft Entra Internet Access forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-internet-access-profile.md#prerequisites).
- Install and configure the [Global Secure Access client for Windows](/en-us/entra/global-secure-access/how-to-install-windows-client) or [macOS](/en-us/entra/global-secure-access/how-to-install-macos-client).
- Add a Microsoft Entra Internet Access traffic forwarding profile custom bypass to exclude Prisma Access service FQDN.

Add a custom bypass for Prisma Access in Global Secure Access:

1. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding** &gt; **Internet access profile** &gt; Under **Internet access policies** &gt; Select “**View**”.
2. Expand **Custom Bypass** &gt; Select **Add rule**.
3. Leave destination type **FQDN** and in **Destination** enter `*.gpcloudservice.com`.
4. Select **Save.**

**Palo Alto Networks configuration**

For this scenario you will need to perform the following in the Palo Alto Strata Cloud Manager portal.

- Set up and configure [GlobalProtect for mobile users](https://docs.paloaltonetworks.com/prisma-access/administration/prisma-access-mobile-users/mobile-users-globalprotect/set-up-globalprotect-mobile-users).
- Configure the GlobalProtect tunnel settings and app settings to work with Global Secure Access. Follow the instructions listed in the Tunnel Settings and App Settings above.
- Install the Palo Alto Networks GlobalProtect client for Windows, [GlobalProtect App for Windows](https://docs.paloaltonetworks.com/globalprotect/6-2/globalprotect-app-user-guide/globalprotect-app-for-windows) or macOS, [GlobalProtect App for macOS](https://docs.paloaltonetworks.com/globalprotect/6-2/globalprotect-app-user-guide/globalprotect-app-for-mac).

Note

For this configuration, enable **Resolve All FQDNs Using DNS Servers Assigned by the Tunnel (Windows Only)** in the App Settings.

After both clients are installed and running side by side and configurations from admin portals are complete, go to the system tray to check that Global Secure Access and GlobalProtect clients are enabled.

Verify configuration for Global Secure Access client.

1. Right click on the **Global Secure Access client &gt; Advanced Diagnostics &gt; Forwarding Profile** and verify that Microsoft 365 and Internet Access rules are applied to this client.
2. Navigate to **Advanced Diagnostics &gt; Health Check** and ensure no checks are failing.

Note

For information about troubleshooting health check failures, see [Troubleshoot the Global Secure Access client: Health check - Global Secure Access | Microsoft Learn](/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check).

**Test traffic flow**

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browser: `bing.com`, `salesforce.com`, `Instagram.com`, Outlook Online (`outlook.com`, `outlook.office.com`, `outlook.office365.com`), SharePoint Online (`<yourtenantdomain>.sharepoint.com`).
3. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to these sites is captured in the Global Secure Access traffic logs.
4. Access your private application set up in Prisma Access through a service connection or ZTNA connector. For example, open an RDP session to a private server.
5. Sign in to Palo Alto Networks’ Strata Cloud Manager and browse to **Incidents & Alerts** &gt; **Log Viewer**. Validate traffic related to the RDP session is present and that traffic related to Microsoft 365 and Internet Traffic such as `Instagram.com`, Outlook Online, and SharePoint Online is missing from the Prisma Access logs.
6. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the network traffic dialog box, select **Stop collecting**.
7. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from the private application. Also, observe that the Global Secure Access client **is** capturing traffic for Microsoft 365 and other internet traffic.