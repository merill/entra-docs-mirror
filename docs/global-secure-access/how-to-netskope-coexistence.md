---
layout: Conceptual
title: Security Service Edge (SSE) Coexistence With Microsoft and Netskope - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-netskope-coexistence
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure and deploy Microsoft Entra and Netskope Security Service Edge (SSE) solutions together for optimized security and connectivity across private applications, Microsoft 365, and internet access.
contributors: 
ms.topic: concept-article
ms.date: 2026-03-13T00:00:00.0000000Z
ms.reviewer: shkhalid
ai-usage: ai-assisted
locale: en-us
document_id: bb0a37dc-f258-3c9b-2e6a-b2c4611fb127
document_version_independent_id: bb0a37dc-f258-3c9b-2e6a-b2c4611fb127
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-netskope-coexistence.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-netskope-coexistence
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-netskope-coexistence.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: d96c1b10-dcd4-e03b-a762-78b415c610f1
---

# Security Service Edge (SSE) Coexistence With Microsoft and Netskope - Global Secure Access | Microsoft Learn

## Overview

In today's rapidly evolving digital landscape, organizations require robust, and unified solutions to ensure secure and seamless connectivity. Microsoft and Netskope offer complementary Secure Access Service Edge (SASE) capabilities that, when integrated, provide enhanced security and connectivity for diverse access scenarios.

This guide outlines how to configure and deploy Microsoft Entra solutions alongside Netskope's Security Service Edge (SSE) offerings. By using the strengths of both platforms, you can optimize your organization's security posture while maintaining high-performance connectivity for private applications, Microsoft 365 traffic, and internet access.

1. **Microsoft Entra Private Access with Netskope Internet Access**

In the first scenario, Global Secure Access handles private application traffic. Netskope only captures Internet traffic.

1. **Microsoft Entra Private Access with Netskope Private Access and Netskope Internet Access**

In the second scenario, both clients handle traffic for separate private applications. Global Secure Access handles private applications in Microsoft Entra Private Access. Private applications in Netskope Private Access are accessed through the Netskope client. Netskope handles Internet traffic.

1. **Microsoft Entra Microsoft Access with Netskope Private Access and Netskope Internet Access**

In the third scenario, Global Secure Access handles all Microsoft 365 traffic. Netskope handles private application and Internet traffic.

1. **Microsoft Entra Internet Access and Microsoft Entra Microsoft Access with Netskope Private Access**

In the fourth scenario, Global Secure Access handles Internet and Microsoft 365 traffic. Netskope only captures Private application traffic.

## Prerequisites

To configure Microsoft and Netskope for a unified SASE solution, start by setting up Microsoft Entra Internet Access and Microsoft Entra Private Access. Next, configure Netskope Private Access and Internet Access. Finally, make sure to establish the required Fully Qualified Domain Name (FQDN) and IP bypasses to ensure smooth integration between the two platforms.

1. Set up Microsoft Entra Internet Access and Microsoft Entra Private Access. These products make up the Global Secure Access solution.
2. Set up Netskope Private Access and Internet Access
3. Configure the Global Secure Access FQDN and IP bypasses

## Microsoft Global Secure Access

To set up Global Secure Access and test all scenarios in this documentation:

1. Enable and disable different Microsoft Global Secure Access traffic forwarding profiles for your Microsoft Entra tenant. For more information about enabling and disabling profiles, see [Global Secure Access traffic forwarding profiles](/en-us/entra/global-secure-access/concept-traffic-forwarding).
2. Install and configure the Microsoft Entra private network connector. For information on how to install and configure the connector, see [How to configure connectors](/en-us/entra/global-secure-access/how-to-configure-connectors). 
    Note

    Private Network Connectors are required for Microsoft Entra Private Access applications.
3. Configure Quick Access to your private resources and set up Private Domain Name System (DNS) and DNS suffixes. For information on how to configure Quick Access, see [How to configure Quick Access](/en-us/entra/global-secure-access/how-to-configure-quick-access).
4. Install and configure the Global Secure Access client on end-user devices. For more information about clients, see [Global Secure Access clients](/en-us/entra/global-secure-access/concept-clients). For information on how to install the Windows client, see [Global Secure Access client for Windows](/en-us/entra/global-secure-access/how-to-install-windows-client). For macOS, see [Global Secure Access Client for macOS](/en-us/entra/global-secure-access/how-to-install-macos-client).

## Netskope Private Access and Internet Access

1. Configure Netskope Private Apps. For more information about configuring Netskope Private Access, see [Netskope One Private Access](https://docs.netskope.com/en/netskope-private-access) documentation.
2. Configure Netskope Steering Configurations for Private and Internet Access. For more information about configuring Netskope, see [Netskope Traffic Steering documentation](https://docs.netskope.com/en/creating-a-steering-configuration/). The steps for creating the required steering configurations for each scenario are listed.
3. Set up and configure Netskope Real-time Protection Policies to allow access to Private Apps. For more information, see [Netskope Real-time Protection Policy for Private Apps](https://docs.netskope.com/en/create-a-real-time-protection-policy-for-private-apps/).
4. Invite users to Netskope and send them an email containing links to the Netskope client install package. To invite users, navigate to the **Netskope portal** &gt; **Settings** &gt; **Security** **Cloud** **Platform** &gt; **Users**.

## Netskope Location Profiles

Create network location profiles to bypass Microsoft SSE service Internet Protocol (IP) addresses and Microsoft 365 destination IPs.

Configure the `Microsoft SSE Service` policy:

1. Navigate to **Policies** &gt; **Profiles** &gt; **Network Location** &gt; **New Network Location** &gt; **Single Object**.
2. Add the routes and save them as `MSFT SSE Service`:`150.171.19.0/24`, `150.171.20.0/24`, `13.107.232.0/24`, `13.107.233.0/24`, `150.171.15.0/24`, `150.171.18.0/24`, `151.206.0.0/16`, `6.6.0.0/16`.

Configure the `MSFT SSE M365` policy:

- Repeat Steps 1 & 2 to Add Microsoft 365 IPs and save them as `MSFT SSE M365`:`132.245.0.0/16`, `204.79.197.215/32`, `150.171.32.0/22`, `131.253.33.215/32`, `23.103.160.0/20`, `40.96.0.0/13`, `52.96.0.0/14`, `40.104.0.0/15`, `13.107.128.0/22`, `13.107.18.10/31`, `13.107.6.152/31`, `52.238.78.88/32`, `104.47.0.0/17`, `52.100.0.0/14`, `40.107.0.0/16`, `40.92.0.0/15`, `150.171.40.0/22`, `52.104.0.0/14`, `104.146.128.0/17`, `40.108.128.0/17`, `13.107.136.0/22`, `40.126.0.0/18`, `20.231.128.0/19`, `20.190.128.0/18`, `20.20.32.0/19`.

The `MSFT SSE Service` and `MSFT SSE M365` profiles are used in steering configurations.

## Microsoft Entra Private Access with Netskope Internet Access

In this scenario, Global Secure Access handles private application traffic. Netskope only captures Internet traffic.

### Microsoft Entra Private Access configuration

For this scenario:

1. [Enable Microsoft Entra Private Access forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-private-access-profile.md#enable-the-private-access-traffic-forwarding-profile).
2. Install a [Private Network Connector](/en-us/entra/global-secure-access/how-to-configure-connectors) for Microsoft Entra Private Access.
3. Configure [Quick Access and set up Private DNS](/en-us/entra/global-secure-access/how-to-configure-quick-access).
4. Install and configure the [Global Secure Access client for Windows](/en-us/entra/global-secure-access/how-to-install-windows-client) or [macOS](/en-us/entra/global-secure-access/how-to-install-macos-client).

### Netskope Internet Access configuration

Netskope portal configuration

1. Set up and configure [Netskope Steering Configuration](https://docs.netskope.com/en/steering-configuration/) to steer Web Traffic.
2. Install the Netskope Client for [Windows](https://docs.netskope.com/en/netskope-client-for-windows), or [macOS](https://docs.netskope.com/en/netskope-client-for-macos).

#### Add Steering Configuration for Internet Access

1. Navigate to **Netskope portal** &gt; **Settings** &gt; **Security Cloud Platform** &gt; **Steering Configuration** &gt; **New Configuration**.
2. Add a Configuration Name such as `MSFTSSEWebTraffic`.
3. Choose a **User Group** or **OU** to apply the configuration to.
4. Under **Cloud, Web and Firewall** &gt; **Web Traffic**
5. **Bypass exception traffic at** &gt; **Client**
6. Under **Private Apps** &gt; **None**.
7. Under **Borderless SD-WAN Apps** &gt; **None**.
8. Set **Status** to **Disabled** and select **Save**.
9. Select the `MSFTSSEWebTraffic` configuration &gt; **Exceptions** &gt; **New Exception** &gt; **Destination Locations**.
10. Select `MSFT SSE Service` (Instructions for creating this object are listed in the Netskope profiles section).
11. The action is **Bypass** &gt; check the box for **Treat it like local IP address** &gt; **Add**.
12. Select **New Exception** &gt; **Domains** and add the Global Secure Access domain exception: \*.globalsecureaccess.microsoft.com &gt; **Save**
13. Ensure that the `MSFTSSEWebTraffic` configuration is at the top of the list of steering configurations in your tenant. Then enable the configuration.
14. Go to the system tray to check that Global Secure Access and Netskope clients are enabled.

#### Verify configurations for clients

1. Right-click on **Global Secure Access Client** &gt; **Advanced Diagnostics** &gt; **Forwarding Profile** and verify that Private access and Private DNS rules are applied to this client.
2. Navigate to **Advanced Diagnostics** &gt; **Health Check** and ensure no checks are failing.
3. Right-click on **Netskope Client** &gt; **Configuration**. Verify **Steering Configuration** matches the name of the configuration. If not, select the **Update** link. 
    Note

    To troubleshoot health check failures, see [Troubleshoot the Global Secure Access client](/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check).

#### Test traffic flow

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browsers: `bing.com`, `salesforce.com`, `Instagram.com`.
3. In the system tray, right-click **Global Secure Access Client** and select **Advanced Diagnostics** &gt; **Traffic** **tab**.
4. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from these websites.
5. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to these sites is missing from the Global Secure Access traffic logs.
6. Sign in to Netskope portal and browse to **Skope IT** &gt; **Events & Alerts** &gt; **Page Events**. Validate traffic related to these sites **is** present in Netskope logs.
7. Access your private application set up in Microsoft Entra Private Access. For example, access a File Share via Server Message Block (SMB).
8. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to File Share **is** captured in the Global Secure Access traffic logs.
9. Sign in to Netskope portal and browse to **Skope IT** &gt; **Events & Alerts** &gt; **Network Events**. Validate traffic related to the private application **is not** present in the traffic logs.
10. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the **Traffic** dialog box, select **Stop collecting**.
11. Scroll to confirm the Global Secure Access client handled only private application traffic.

## Microsoft Entra Private Access with Netskope Private Access and Netskope Internet Access

In this scenario, both clients handle traffic for separate private applications. The Global Secure Access client handles private applications in Microsoft Entra Private Access and the Netskope client handles private applications in Netskope Private Access. Netskope handles internet traffic.

### Microsoft Entra Private Access configuration

For this scenario:

1. [Enable Microsoft Entra Private Access forwarding profile](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-private-access-profile.md#enable-the-private-access-traffic-forwarding-profile).
2. Install a [Private Network Connector](/en-us/entra/global-secure-access/how-to-configure-connectors) for Microsoft Entra Private Access.
3. Configure [Quick Access and set up Private DNS](/en-us/entra/global-secure-access/how-to-configure-quick-access).
4. Install and configure the [Global Secure Access client for Windows](/en-us/entra/global-secure-access/how-to-install-windows-client) or [macOS](/en-us/entra/global-secure-access/how-to-install-macos-client).

### Netskope Private Access and Netskope Internet Access configuration

In the Netskope portal:

1. Set up and configure [Netskope Steering Configuration](https://docs.netskope.com/en/steering-configuration/) to steer Web Traffic and Private Apps.
2. Install the Netskope Client for [Windows](https://docs.netskope.com/en/netskope-client-for-windows), or [macOS](https://docs.netskope.com/en/netskope-client-for-macos).
3. Create [Real-time Protection policy](https://docs.netskope.com/en/inline-policies/) to allow access to Private Apps.
4. Install the [Netskope Private Access Publisher](https://docs.netskope.com/en/deploy-a-publisher).

#### Add Steering Configuration for Internet Access and Private Apps

1. Navigate to **Netskope portal** &gt; **Settings** &gt; **Security Cloud Platform** &gt; **Steering Configuration**&gt; **New Configuration**.
2. Add a **Configuration Name** such as `MSFTSSEWebAndPrivate`.
3. Choose a **User Group** or **OU** to apply the configuration to.
4. Under **Cloud, Web and Firewall** &gt; **Web Traffic**
5. **Bypass exception traffic at** &gt; **Client**
6. Under **Private Apps**, select **Specific Private Apps**.
7. On the next line &gt; **Netskope will** &gt; **Steer**
8. Under **Borderless SD-WAN Apps** &gt; **None**.
9. Set **Status** to **Disabled** and select **Save**.
10. Select the `MSFTSSEWebAndPrivate` configuration &gt; **Exceptions** &gt; **New Exception** &gt; **Destination Locations**.
11. Select `MSFT SSE Service` (Instructions for creating this object are listed in the Netskope profiles section).
12. The action is **Bypass** &gt; check the box for **Treat it like local IP address** &gt; Add.
13. Select **New Exception** &gt; **Domains** and add the Global Secure Access domain exception: \*.globalsecureaccess.microsoft.com &gt; **Save**.
14. Select **Add Steered Item**.
15. Select **Private App** and select the private applications for Netskope to steer &gt; **Add**.
16. Ensure that the `MSFTSSEWebAndPrivate` configuration is at the top of the list of steering configurations in your tenant. Then enable the configuration.

#### Add Netskope Private App Real-time Protection Policy

1. Navigate to **Netskope Portal** &gt; **Policies** &gt; **Real-time Protection**.
2. Select **New** **Policy** &gt; **Private** **App** **Access**.
3. In **Source**, select the **Users**, **Groups**, or **OUs** to grant access.
4. Add any required **Criteria**, like OS or Device Classification.
5. In **Destination** &gt; **Private** **App** &gt; select Private Apps to allow access to.
6. In **Profile & Action** &gt; **Allow**.
7. Give the policy a name such as `Private Apps` and put it in the **Default** group.
8. Set **Status** to Enabled.
9. Go to the system tray to check that Global Secure Access and Netskope clients are enabled.

#### Verify configurations for clients

1. Right-click on **Global Secure Access Client** &gt; **Advanced Diagnostics** &gt; **Forwarding Profile** and verify that Private access and Private DNS rules are applied to this client.
2. Navigate to **Advanced Diagnostics** &gt; **Health Check** and ensure no checks are failing.
3. Right-click on **Netskope Client** &gt; **Configuration**. Verify **Steering Configuration** matches the name of the configuration created. If not, select the **Update** link. 
    Note

    To troubleshoot health check failures, see [Troubleshoot the Global Secure Access client](/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check).

#### Test traffic flow

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browsers: `bing.com`, `salesforce.com`, `yelp.com`.
3. In the system tray, right-click **Global Secure Access Client** and select **Advanced Diagnostics** &gt; **Traffic tab**.
4. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from these websites.
5. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic** **logs**. Validate traffic related to these sites is missing from the Global Secure Access traffic logs.
6. Sign in to Netskope portal and browse to **Skope IT** &gt; **Events & Alerts** &gt; **Page Events**. Validate traffic related to these sites **is** present in Netskope logs.
7. Access your private application set up in Microsoft Entra Private Access. For example, access a File Share via SMB.
8. Access your private application set up in Netskope Private Access. For example, open an RDP session to a private server.
9. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
10. Validate traffic related to the SMB file share private app **is** captured and that traffic related to the RDP session **isn't** captured in the Global Secure Access traffic logs.
11. Sign in to Netskope portal and browse to **Skope IT** &gt; **Events & Alerts** &gt; **Network Events**. Validate traffic related to the **RDP** session **is** present and that traffic related to the **SMB** file share **isn't** in the Netskope logs.
12. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the **Traffic** dialog box, select **Stop collecting**.
13. Scroll to confirm the Global Secure Access client handled private application traffic for the SMB file share and didn't handle the RDP session traffic.

## Microsoft Entra Microsoft Access with Netskope Private Access and Netskope Internet Access

In this scenario, Global Secure Access handles all Microsoft 365 traffic. Netskope Private Access handles Private application traffic and Netskope Internet Access handles Internet traffic.

### Microsoft Entra Microsoft Access configuration

For this scenario:

1. [Enable Microsoft Entra Microsoft Access forwarding profile](how-to-manage-microsoft-profile#enable-the-microsoft-traffic-profile).
2. Install and configure the [Global Secure Access client for Windows](/en-us/entra/global-secure-access/how-to-install-windows-client) or [macOS](/en-us/entra/global-secure-access/how-to-install-macos-client).

### Netskope Private Access and Netskope Internet Access configuration

In the Netskope portal:

1. Set up and configure [Netskope Steering Configuration](https://docs.netskope.com/en/steering-configuration/) to steer Web Traffic and Private Apps.
2. Install the Netskope Client for [Windows](https://docs.netskope.com/en/netskope-client-for-windows), or [macOS](https://docs.netskope.com/en/netskope-client-for-macos).
3. Create [Real-time Protection policy](https://docs.netskope.com/en/inline-policies/) to allow access to Private Apps.
4. Install the [Netskope Private Access Publisher](https://docs.netskope.com/en/deploy-a-publisher).

#### Add Steering Configuration for Internet Access and Private Apps

1. Navigate to **Netskope portal** &gt; **Settings** &gt; **Security Cloud Platform** &gt; **Steering Configuration**&gt; **New Configuration**.
2. Add a **Configuration Name** such as `MSFTSSEWebAndPrivate-NoM365`.
3. Choose a **User Group** or **OU** to apply the configuration to.
4. Under **Cloud, Web and Firewall** &gt; **Web Traffic.**
5. **Bypass exception traffic at** &gt; **Client.**
6. Under **Private Apps**, select **Specific Private Apps**.
7. On the next line &gt; **Netskope will** &gt; **Steer.**
8. Under **Borderless SD-WAN Apps** &gt; **None**.
9. Set **Status** to **Disabled** and select **Save**.
10. Select the `MSFTSSEWebAndPrivate-NoM365` configuration &gt; **Exceptions** &gt; **New Exception** &gt; **Destination Locations** &gt; Select `MSFT SSE Service` and `MSFT SSE M365` (Instructions for creating this object are listed in the Netskope profiles section).
11. Select **Bypass** and **Treat it like local IP address** options.
12. Select **Exceptions** &gt; **New Exception** &gt; **Domains** and add these exceptions: `*.globalsecureaccess.microsoft.com`, `*.auth.microsoft.com`, `*.msftidentity.com`, `*.msidentity.com`, `*.onmicrosoft.com`, `*.outlook.com`, `*.protection.outlook.com`, `*.sharepoint.com`, `*.sharepointonline.com`, `*.svc.ms`, `*.wns.windows.com`, `account.activedirectory.windowsazure.com`, `accounts.accesscontrol.windows.net`, `admin.onedrive.com`, `adminwebservice.microsoftonline.com`, `api.passwordreset.microsoftonline.com`, `autologon.microsoftazuread-sso.com`, `becws.microsoftonline.com`, `ccs.login.microsoftonline.com`, `clientconfig.microsoftonline-p.net`, `companymanager.microsoftonline.com`, `device.login.microsoftonline.com`, `g.live.com`, `graph.microsoft.com`, `graph.windows.net`, `login-us.microsoftonline.com`, `login.microsoft.com`, `login.microsoftonline-p.com`, `login.microsoftonline.com`, `login.windows.net`, `logincert.microsoftonline.com`, `loginex.microsoftonline.com`, `nexus.microsoftonline-p.com`, `officeclient.microsoft.com`, `oneclient.sfx.ms`, `outlook.cloud.microsoft`, `outlook.office.com`, `outlook.office365.com`, `passwordreset.microsoftonline.com`, `provisioningapi.microsoftonline.com`, `spoprod-a.akamaihd.net`.
13. Select **Add Steered Item** &gt; Select **Private App** and select the private applications for Netskope to steer &gt; **Add**.
14. Ensure that the `MSFTSSEWebAndPrivate-NoM365` configuration is at the top of the list of steering configurations in your tenant. Then enable the configuration.

#### Add Netskope Private App Real-time Protection Policy

1. Navigate to **Netskope Portal** &gt; **Policies** &gt; **Real-time Protection**.
2. Select **New** **Policy** &gt; **Private** **App** **Access**.
3. In **Source**, select the **Users**, **Groups**, or **OUs** to grant access.
4. Add any required **Criteria**, like OS or Device Classification.
5. In **Destination** &gt; **Private** **App** &gt; select Private Apps to allow access to.
6. In **Profile & Action** &gt; **Allow**.
7. Give the policy a name such as `Private Apps` and put it in the **Default** group.
8. Set **Status** to Enabled.
9. Go to the system tray to check that Global Secure Access and Netskope clients are enabled.

#### Verify configurations for clients

1. Right-click on **Global Secure Access Client** &gt; **Advanced Diagnostics** &gt; **Forwarding Profile** and verify that only Microsoft 365 rules are applied to this client.
2. Navigate to **Advanced Diagnostics** &gt; **Health Check** and ensure no checks are failing.
3. Right-click on **Netskope Client** &gt; **Configuration**. Verify **Steering Configuration** matches the name of the configuration created. If not, select the **Update** link. 
    Note

    To troubleshoot health check failures, see [Troubleshoot the Global Secure Access client](/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check).

#### Test traffic flow

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browsers: `bing.com`, `salesforce.com`, `yelp.com`.
3. In the system tray, right-click **Global Secure Access Client** and select **Advanced Diagnostics** &gt; **Traffic tab**.
4. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from these websites.
5. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to these sites is missing from the Global Secure Access traffic logs.
6. Sign in to Netskope portal and browse to **Skope IT** &gt; **Events & Alerts** &gt; **Page Events**.
7. Validate traffic related to these sites **is** present in Netskope logs.
8. Access your private application set up in Netskope Private Access. For example, open an RDP session to a private server.
9. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
10. Validate traffic related to the RDP session **isn’t** in the Global Secure Access traffic logs.
11. Sign in to Netskope portal and browse to **Skope IT** &gt; **Events & Alerts** &gt; **Network Events**. Validate traffic related to the **RDP** session **is** present.
12. Access Outlook Online (`outlook.com`, `outlook.office.com`, `outlook.office365.com`), SharePoint Online (`<yourtenantdomain>.sharepoint.com`).
13. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the **Traffic** dialog box, select **Stop collecting**.
14. Scroll to confirm the Global Secure Access client handled only Microsoft 365 traffic.
15. You can also validate that the traffic is captured in the Global Secure Access traffic logs. In the Microsoft Entra admin center, navigate to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
16. Validate traffic related to Outlook Online and SharePoint Online is missing from Netskope portal in **Skope IT** &gt; **Events & Alerts** &gt; **Page Events**.

## Microsoft Entra Internet Access and Microsoft Entra Microsoft Access with Netskope Private Access

In this scenario Netskope only captures private application traffic. Global Secure Access handles all other traffic.

### Microsoft Entra Internet Access and Microsoft Access configuration

For this scenario:

1. [Enable Microsoft Entra Microsoft Access](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-microsoft-profile.md#enable-the-microsoft-traffic-profile) and [Microsoft Entra Internet Access forwarding profiles](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/global-secure-access/how-to-manage-internet-access-profile.md#prerequisites).
2. Install and configure the [Global Secure Access client for Windows](/en-us/entra/global-secure-access/how-to-install-windows-client) or [macOS](/en-us/entra/global-secure-access/how-to-install-macos-client).
3. Add a Microsoft Entra Internet Access traffic forwarding profile custom bypass to exclude Netskope service FQDN and IPs.

#### Add a custom bypass for Netskope in Global Secure Access

1. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding** &gt; **Internet access profile**.
2. Under **Internet access policies** &gt; Select **View**.
3. Expand **Custom Bypass** &gt; Select **Add rule**
4. Leave destination type **FQDN** and in Destination enter `*.goskope.com` &gt; **Save**
5. Select **Add rule** again &gt; **IP Range** &gt; **Add** the IP ranges (each range is a new rule): `163.116.128.0..163.116.255.255`, `162.10.0.0..162.10.127.255`, `31.186.239.0..31.186.239.255`, `8.39.144.0..8.39.144.255`, `8.36.116.0..8.36.116.255`
6. Select **Save**.

### Netskope Private Access configuration

In the Netskope portal:

1. Set up and configure [Netskope Steering Configuration](https://docs.netskope.com/en/steering-configuration/) to steer Web Traffic and Private Apps.
2. Install the Netskope Client for [Windows](https://docs.netskope.com/en/netskope-client-for-windows), or [macOS](https://docs.netskope.com/en/netskope-client-for-macos).
3. Create [Real-time Protection policy](https://docs.netskope.com/en/inline-policies/) to allow access to Private Apps.
4. Install the [Netskope Private Access Publisher](https://docs.netskope.com/en/deploy-a-publisher).

#### Add Steering Configuration for Private Apps

1. Navigate to **Netskope portal** &gt; **Settings** &gt; **Security Cloud Platform** &gt; **Steering Configuration**&gt; **New Configuration**.
2. Add a **Configuration Name** such as `MSFTSSEPrivate`.
3. Choose a **User Group** or **OU** to apply the configuration to.
4. Under **Cloud, Web and Firewall** &gt; **None.**
5. Under **Private Apps**, select **All Private Apps**.
6. On the next line &gt; **Netskope will** &gt; **Steer.**
7. Under **Borderless SD-WAN Apps** &gt; **None**.
8. Set **Status** to **Disabled** and select **Save**.
9. Ensure that the `MSFTSSEPrivate` configuration is at the top of the list of steering configurations in your tenant. Then enable the configuration.

#### Add Netskope Private App Real-time Protection Policy

1. Navigate to **Netskope Portal** &gt; **Policies** &gt; **Real-time Protection**.
2. Select **New** **Policy** &gt; **Private** **App** **Access**.
3. In **Source**, select the **Users**, **Groups**, or **OUs** to grant access.
4. Add any required **Criteria**, like OS or Device Classification.
5. In **Destination** &gt; **Private** **App** &gt; select Private Apps to allow access to.
6. In **Profile & Action** &gt; **Allow**.
7. Give the policy a name such as `Private Apps` and put it in the **Default** group.
8. Set **Status** to Enabled.
9. Go to the system tray to check that Global Secure Access and Netskope clients are enabled.

#### Verify configurations for clients

1. Right-click on **Global Secure Access Client** &gt; **Advanced Diagnostics** &gt; **Forwarding Profile** and verify that Microsoft Access and Internet Access rules are applied to this client.
2. Navigate to **Advanced Diagnostics** &gt; **Health Check** and ensure no checks are failing.
3. Right-click on **Netskope Client** &gt; **Configuration**. Verify **Steering Configuration** matches the name of the configuration created. If not, select the **Update** link. 
    Note

    To troubleshoot health check failures, see [Troubleshoot the Global Secure Access client](/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check).

#### Test traffic flow

1. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. Select the **Traffic** tab and select **Start collecting**.
2. Access these websites from the browsers: `bing.com`, `salesforce.com`, `Instagram.com`, Outlook Online (`outlook.com`, `outlook.office.com`, `outlook.office365.com`), SharePoint Online (`<yourtenantdomain>.sharepoint.com`).
3. Sign in to Microsoft Entra admin center and browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Validate traffic related to these sites **is** captured in the Global Secure Access traffic logs.
4. Access your private application set up in Netskope Private Apps. For example, using Remote Desktop (RDP).
5. Sign in to Netskope portal and browse to **Skope IT** &gt; **Events & Alerts** &gt; **Network Events**. Validate traffic related to the **RDP** session **is** present and that traffic related to Microsoft 365 and Internet Traffic such as Instagram.com, Outlook Online, and SharePoint Online is missing from Netskope Portal.
6. In the system tray, right-click **Global Secure Access Client** and then select **Advanced Diagnostics**. In the network **traffic** dialog box, select **Stop collecting**.
7. Scroll to observe that the Global Secure Access client **isn't** capturing traffic from the private application. Also, observe that the Global Secure Access client is capturing traffic for Microsoft 365 and other internet traffic.