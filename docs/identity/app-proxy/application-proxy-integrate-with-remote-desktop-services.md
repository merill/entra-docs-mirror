---
layout: Conceptual
title: Publish Remote Desktop with Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-integrate-with-remote-desktop-services
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Publish Remote Desktop Services (RDS) deployments through Microsoft Entra application proxy for secure external access to remote desktops and RemoteApps.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1ecb521c-9c0a-6baf-d25f-2b0fb130b54f
document_version_independent_id: 71d4d2d4-ff30-d592-175f-f1e76d5cc88b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-integrate-with-remote-desktop-services.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-integrate-with-remote-desktop-services
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-integrate-with-remote-desktop-services.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ddab3cd8-636f-4a91-896e-1c23f399a6bd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f409bb5d-e203-40c5-9d95-0ee717231beb
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: cc79189d-d4c1-ac71-1ea1-c57c6b518d87
---

# Publish Remote Desktop with Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

Remote Desktop Service and Microsoft Entra application proxy work together to improve the productivity of workers who are away from the corporate network.

The intended audience for this article is:

- Current application proxy customers who want to offer more applications to their end users by publishing on-premises applications through Remote Desktop Services.
- Current Remote Desktop Services customers who want to reduce the attack surface of their deployment by using Microsoft Entra application proxy. This scenario gives a set of two-step verification and Conditional Access controls to RDS.

## How application proxy fits in the standard RDS deployment

A standard RDS deployment includes various Remote Desktop role services running on Windows Server. Multiple deployment options exist in the [Remote Desktop Services architecture](/en-us/windows-server/remote/remote-desktop-services/Desktop-hosting-logical-architecture). Unlike other RDS deployment options, the [RDS deployment with Microsoft Entra application proxy](/en-us/windows-server/remote/remote-desktop-services/Desktop-hosting-logical-architecture) (shown in the following diagram) has a permanent outbound connection from the server running the connector service. Other deployments leave open inbound connections through a load balancer.

![Diagram that shows how application proxy sits between the RDS VM and the public internet.](media/application-proxy-integrate-with-remote-desktop-services/rds-with-app-proxy.png)

In an RDS deployment, the Remote Desktop (RD) Web role and the RD Gateway role run on Internet-facing machines. These endpoints are exposed for the following reasons:

- RD Web provides the user a public endpoint to sign in and view the various on-premises applications and desktops they can access. When you select a resource, a Remote Desktop Protocol (RDP) connection is created using the native app on the OS.
- RD Gateway comes into the picture once a user launches the RDP connection. The RD Gateway handles encrypted RDP traffic coming over the internet and translates it to the on-premises server that the user is connecting to. In this scenario, the traffic the RD Gateway is receiving comes from the Microsoft Entra application proxy.

Tip

For more information, see [how to seamlessly deploy RDS with Azure Resource Manager and Azure Marketplace](/en-us/windows-server/remote/remote-desktop-services/rds-in-azure).

## Requirements

- Both the RD Web and RD Gateway endpoints must be located on the same machine, and with a common root. RD Web and RD Gateway are published as a single application with application proxy so that you can have a single sign-on experience between the two applications.
- [Deploy RDS](/en-us/windows-server/remote/remote-desktop-services/rds-in-azure), and [enabled application proxy](application-proxy-add-on-premises-application). Enable application proxy and open required ports and URLs, and enable Transport Layer Security (TLS) 1.2 on the server. To learn which ports need to be opened, and other details, see [Tutorial: Add an on-premises application for remote access through application proxy in Microsoft Entra ID](application-proxy-add-on-premises-application).
- Your end users must use a compatible browser to connect to RD Web or the RD Web client. For more information, see Support for client configurations.
- When publishing RD Web, use the same internal and external Fully Qualified Domain Name (FQDN) when possible. If the internal and external Fully Qualified Domain Names (FQDNs) are different, disable Request Header Translation to avoid the client receiving invalid links.
- If you're using the RD Web client, you *must* use the same internal and external FQDN. If the internal and external FQDNs are different, you encounter websocket errors when making a RemoteApp connection through the RD Web client.
- If you're using RD Web on Internet Explorer, you need to enable the RDS ActiveX add-on.
- If you're using the RD Web client, you need to use the application proxy [connector version 1.5.1975 or later](../../global-secure-access/reference-version-history).
- For the Microsoft Entra pre authentication flow, users can only connect to resources published to them in the **RemoteApp and Desktops** pane. Users can't connect to a desktop using the **Connect to a remote PC** pane.
- If you're using Windows Server 2019, you need to disable HTTP2 protocol. For more information, see [Tutorial: Add an on-premises application for remote access through application proxy in Microsoft Entra ID](application-proxy-add-on-premises-application).

## Deploy the joint RDS and application proxy scenario

After setting up RDS and Microsoft Entra application proxy for your environment, follow the steps to combine the two solutions. These steps walk through publishing the two web-facing RDS endpoints (RD Web and RD Gateway) as applications, and then directing traffic on your RDS to go through application proxy.

### Publish the RD host endpoint

1. [Publish a new application proxy application](application-proxy-add-on-premises-application) with the values.

    - Internal URL: `https://<rdhost>.com/`, where `<rdhost>` is the common root that RD Web and RD Gateway share.
    - External URL: This field is automatically populated based on the name of the application, but you can modify it. Your users go to this URL when they access RDS.
    - Pre authentication method: Microsoft Entra ID.
    - Translate URL headers: No.
    - Use HTTP-Only Cookie: No.
2. Assign users to the published RD application. Make sure they all have access to RDS, too.
3. Leave the single sign-on method for the application as **Microsoft Entra single sign-on disabled**.

    Note

    Your users are asked to authenticate once to Microsoft Entra ID and once to RD Web, but they have single sign-on to RD Gateway.
4. Browse to **Entra ID** &gt; **App registrations**. Choose your app from the list.
5. Under **Manage**, select **Branding**.
6. Update the **Home page URL** field to point to your RD Web endpoint (like `https://<rdhost>.com/RDWeb`).

### Direct RDS traffic to application proxy

Connect to the RDS deployment as an administrator and change the RD Gateway server name for the deployment. This configuration ensures that connections go through the Microsoft Entra application proxy service.

1. Connect to the RDS server running the RD Connection Broker role.
2. Launch **Server Manager**.
3. Select **Remote Desktop Services** from the pane on the left.
4. Select **Overview**.
5. In the Deployment Overview section, select the drop-down menu and choose **Edit deployment properties**.
6. In the RD Gateway tab, change the **Server name** field to the External URL that you set for the RD host endpoint in application proxy.
7. Change the **Logon method** field to **Password Authentication**.

    ![Screenshot that shows the Deployment Properties screen on RDS.](media/application-proxy-integrate-with-remote-desktop-services/rds-deployment-properties.png)
8. Run this command for each collection. Replace *&lt;yourcollectionname&gt;* and *&lt;proxyfrontendurl&gt;* with your own information. This command enables single sign-on between RD Web and RD Gateway, and optimizes performance.

    ```powershell
    Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
    ```

    **For example:**

    ```powershell
    Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://remotedesktoptest-aadapdemo.msappproxy.net/`nrequire pre-authentication:i:1"
    ```

    Note

    The command uses a backtick in ``nrequire`.
9. To verify the modification of the custom RDP properties and view the RDP file contents that are downloaded from RDWeb for this collection, run the following command.

    ```powershell
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

Now that Remote Desktop is configured, Microsoft Entra application proxy takes over as the internet-facing component of RDS. Remove the other public internet-facing endpoints on your RD Web and RD Gateway machines.

### Enable the RD Web Client

If you want users to use the RD Web Client follow the steps at [Set up the Remote Desktop web client for your users](/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-web-client-admin).

The Remote Desktop web client provides access for your organization's Remote Desktop infrastructure. An HTML5-compatible web browser such as Microsoft Edge, Google Chrome, Safari, or Mozilla Firefox (v55.0 and later) is required.

## Test the scenario

Test the scenario with Internet Explorer on a Windows 7 or 10 computer.

1. Go to the external URL you set up, or find your application in the [MyApps panel](https://myapps.microsoft.com).
2. Authenticate to Microsoft Entra ID. Use an account that you assigned to the application.
3. Authenticate to RD Web.
4. Once your RDS authentication succeeds, you can select the desktop or application you want, and start working.

## Support for other client configurations

The configuration outlined in this article is for access to RDS via RD Web or the RD Web Client. If you need to, however, you can support other operating systems or browsers. The difference is in the authentication method that you use.

| Authentication method | Supported client configuration |
| --- | --- |
| Pre authentication | RD Web- Windows 7/10/11 using [`Microsoft Edge Chromium IE mode`](/en-us/deployedge/edge-ie-mode) + RDS ActiveX add-on |
| Pre authentication | RD Web Client- HTML5-compatible web browser such as Microsoft Edge, Internet Explorer 11, Google Chrome, Safari, or Mozilla Firefox (v55.0 and later) |
| Passthrough | Any other operating system that supports the Microsoft Remote Desktop application |

Note

`Microsoft Edge Chromium IE` mode is required when the My Apps portal is used for accessing the Remote Desktop app.

The pre authentication flow offers more security benefits than the passthrough flow. With pre authentication you can use Microsoft Entra authentication features like single sign-on, Conditional Access, and two-step verification for your on-premises resources. You also ensure that only authenticated traffic reaches your network.

To use passthrough authentication, there are just two modifications to the steps listed in this article:

1. In Publish the RD host endpoint step 1, set the Preauthentication method to **Passthrough**.
2. In Direct RDS traffic to application proxy, skip step 8 entirely.