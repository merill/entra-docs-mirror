---
layout: Conceptual
title: Use Application Gateway WAF to protect your application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-application-gateway-waf
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: How to add Web Application Firewall (WAF) protection for apps published with Microsoft Entra application proxy.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: aa262fef-5348-4345-3d10-f46b4e5a8eb0
document_version_independent_id: 848c6128-9d68-eaad-88dc-e2c7784446ae
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-application-gateway-waf.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-application-gateway-waf
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-application-gateway-waf.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e8fdebed-2921-4997-a75a-fa863723a535
- https://authoring-docs-microsoft.poolparty.biz/devrel/d4cf20b3-3e54-4ed9-8b09-370a52eee81b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf1e63a8-325f-42be-b60c-d84a95a42b1f
- https://authoring-docs-microsoft.poolparty.biz/devrel/9ecc2643-be13-4271-a1f4-87114737d63a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 62b95e1d-1b94-1958-c140-7e35ec57d085
---

# Use Application Gateway WAF to protect your application - Microsoft Entra ID | Microsoft Learn

## Overview

Add Web Application Firewall (WAF) protection for apps published with Microsoft Entra application proxy.

For more information about Web Application Firewall, see [What is Azure Web Application Firewall on Azure Application Gateway?](/en-us/azure/web-application-firewall/ag/ag-overview).

## Deployment steps

This article provides the steps to securely expose a web application on the Internet using Microsoft Entra application proxy with Azure WAF on Application Gateway.

![Architecture diagram showing web application traffic flow from Internet through Azure WAF and Application Gateway to Microsoft Entra application proxy and internal application servers.](media/application-proxy-waf/application-proxy-waf.png)

### Configure Azure Application Gateway to send traffic to your internal application

Some steps of the Application Gateway configuration are omitted in this article. For a detailed guide on creating and configuring an Application Gateway, see [Quickstart: Direct web traffic with Azure Application Gateway - Microsoft Entra admin center](/en-us/azure/application-gateway/quick-create-portal).

### 1. Create a private-facing HTTPS listener

Create a listener so users can access the web application privately when connected to the corporate network.

![Application Gateway listener configuration page showing private access settings for corporate network users.](media/application-proxy-waf/application-gateway-listener.png)

### 2. Create a backend pool with the web servers

In this example, the backend servers have Internet Information Services (IIS) installed.

![Application Gateway backend pool configuration showing IIS web servers.](media/application-proxy-waf/application-gateway-backend.png)

### 3. Create a backend setting

A backend setting determines how requests reach the backend pool servers.

![Application Gateway backend settings configuration page showing request routing parameters.](media/application-proxy-waf/application-gateway-backend-settings.png)

### 4. Create a routing rule that ties the listener, the backend pool, and the backend setting created in the previous steps

![Application Gateway routing rule configuration page showing listener selection step.](media/application-proxy-waf/application-gateway-add-rule-1.png)![Application Gateway routing rule configuration page showing backend pool and backend settings selection.](media/application-proxy-waf/application-gateway-add-rule-2.png)

### 5. Enable the WAF in the Application Gateway and set it to Prevention mode

![Application Gateway WAF configuration page showing WAF enabled with Prevention mode selected.](media/application-proxy-waf/application-gateway-enable-waf.png)

## Configure your application to be remotely accessed through application proxy in Microsoft Entra ID

Both connector VMs, the Application Gateway, and the backend servers are deployed in the same virtual network in Azure. The setup also applies to applications and connectors deployed on-premises.

For a detailed guide on how to add your application to application proxy in Microsoft Entra ID, see [Tutorial: Add an on-premises application for remote access through application proxy in Microsoft Entra ID](application-proxy-add-on-premises-application). For more information about performance considerations concerning the private network connectors, see [Optimize traffic flow with Microsoft Entra application proxy](application-proxy-network-topology).

![Microsoft Entra application proxy configuration showing matching internal and external URLs for port 443 access.](media/application-proxy-waf/application-proxy-configuration.png)

In this example, the same URL was configured as the internal and external URL. Remote clients access the application over the Internet on port 443, through the application proxy. A client connected to the corporate network accesses the application privately. Access is through the Application Gateway directly on port 443. For a detailed step on configuring custom domains in application proxy, see [Configure custom domains with Microsoft Entra application proxy](how-to-configure-custom-domain).

An [Azure Private Domain Name System (DNS) zone](/en-us/azure/dns/private-dns-getstarted-portal) is created with an A record. The A record points `www.fabrikam.one` to the private frontend IP address of the Application Gateway. The record ensures the connector VMs send requests to the Application Gateway.

## Test the application

After [adding a user for testing](application-proxy-add-on-premises-application#add-a-user-for-testing), you can test the application by accessing `https://www.fabrikam.one`. The user is prompted to authenticate in Microsoft Entra ID, and upon successful authentication, accesses the application.

![Microsoft Entra ID sign-in page prompting user for authentication.](media/application-proxy-waf/sign-in-2.png)![Browser showing successful application access after authentication.](media/application-proxy-waf/application-gateway-response.png)

## Simulate an attack

To test if the WAF is blocking malicious requests, you can simulate an attack using a basic SQL injection signature. For example, "https://www.fabrikam.one/api/sqlquery?query=x%22%20or%201%3D1%20--".

![Browser showing HTTP 403 Forbidden error from WAF blocking SQL injection attempt.](media/application-proxy-waf/waf-response.png)

An HTTP 403 response confirms that WAF blocked the request.

The Application Gateway [Firewall logs](/en-us/azure/application-gateway/application-gateway-diagnostics#firewall-log) provide more details about the request and why WAF is blocking it.

![Application Gateway Firewall log entry showing blocked request details and SQL injection rule violation.](media/application-proxy-waf/waf-log.png)