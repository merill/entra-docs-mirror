---
layout: Conceptual
title: Resolve cross-origin resource sharing issues - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-understand-cors-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Learn how to identify and resolve cross-origin resource sharing (CORS) issues in Microsoft Entra application proxy.
ms.topic: troubleshooting
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 1d687983-7232-8dea-8527-d46ea68afb35
document_version_independent_id: 1ea2fd45-18c1-ba82-334d-7acc1152f9eb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-understand-cors-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-understand-cors-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-understand-cors-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5e5aac42-cafb-69be-6176-2f4bf1277d5d
---

# Resolve cross-origin resource sharing issues - Microsoft Entra ID | Microsoft Learn

## Overview

[Cross-origin resource sharing (CORS)](https://www.w3.org/TR/cors/) can present challenges for the apps and APIs you publish through Microsoft Entra application proxy. This article discusses Microsoft Entra application proxy CORS issues and solutions.

Browser security usually prevents a webpage from making requests to another domain. This restriction is called the *same-origin policy*. The policy prevents a malicious site from reading sensitive data from another site. However, sometimes you might want to let other sites call your web API. CORS is a W3C standard that directs a server to allow some cross-origin requests and reject others.

## Identify a CORS issue

Two URLs have the same origin if they have identical schemes, hosts, and ports ([Request For Comments (RFC) 6454](https://tools.ietf.org/html/rfc6454)), such as in this example:

- `http://contoso.com/foo.html`
- `http://contoso.com/bar.html`

These URLs have different origins than the previous two:

- `http://contoso.net`: Different domain
- `http://contoso.com:9000/foo.html`: Different port
- `https://contoso.com/foo.html`: Different scheme
- `http://www.contoso.com/foo.html`: Different subdomain

Same-origin policy prevents apps from accessing resources from other origins unless they use the correct access control headers. If the CORS headers are absent or incorrect, cross-origin requests fail.

You can identify CORS issues by using browser debug tools:

1. Open the browser and go to the web app.
2. Select the **F12** key to open the debug console in DevTools.
3. Try to reproduce the transaction, and review the console message. A CORS violation produces a console error about origin.

In the following screenshot, selecting the **Try It** button caused a CORS error message that `https://corswebclient-contoso.msappproxy.net` wasn't found in the `Access-Control-Allow-Origin` header.

![Screenshot that shows an example of a CORS issue.](media/application-proxy-understand-cors-issues/image3.png)

## CORS challenges with application proxy

The following example shows a typical Microsoft Entra application proxy CORS scenario. The internal server hosts a *CORSWebService* web API controller, and a *CORSWebClient* that calls *CORSWebService*. An Asynchronous JavaScript and XML (AJAX) request is made from *CORSWebClient* to *CORSWebService*.

![Screenshot that shows an on-premises same-origin request.](media/application-proxy-understand-cors-issues/image1.png)

The *CORSWebClient* app works on-premises but fails or shows an error when published through Microsoft Entra application proxy. If *CORSWebClient* and *CORSWebService* are published as separate apps, they're hosted on different domains. The different domains make AJAX requests from *CORSWebClient* to *CORSWebService* cross-origin, causing them to fail.

![Screenshot that shows an application proxy CORS request.](media/application-proxy-understand-cors-issues/image2.png)

## Solutions for application proxy CORS issues

You can resolve the preceding CORS issue in several ways.

### Option 1: Set up a custom domain

Use a Microsoft Entra application proxy [custom domain](how-to-configure-custom-domain) to publish from the same origin, without making any changes to app origins, code, or headers.

### Option 2: Publish the parent directory

Publish the parent directory of both apps. This solution works especially well if you have only two apps on the web server. Instead of publishing each app separately, you can publish the common parent directory, which results in the same origin.

The following examples show the Microsoft Entra application proxy pages for the *CORSWebClient* app. When the internal URL is set to `contoso.com/CORSWebClient`, the app can't make successful requests to the `contoso.com/CORSWebService` directory, because they're cross-origin.

![Screenshot that shows publishing an app individually.](media/application-proxy-understand-cors-issues/image4.png)

Instead, set the value for **Internal URL** to publish the parent directory, which includes both the `CORSWebClient` and `CORSWebService` directories:

![Screenshot that shows publishing a parent directory.](media/application-proxy-understand-cors-issues/image5.png)

The resulting app URLs effectively resolve the CORS issue:

- `https://corswebclient-contoso.msappproxy.net/CORSWebService`
- `https://corswebclient-contoso.msappproxy.net/CORSWebClient`

### Option 3: Update HTTP headers

To match the origin request, add a custom HTTP response header on the web service. Websites running in Internet Information Services (IIS) use IIS Manager to modify the header.

![Screenshot that shows adding a custom response header in IIS Manager.](media/application-proxy-understand-cors-issues/image6.png)

The modification doesn't require any code changes. You can verify it in a Fiddler trace.

```http
**Post the Header Addition**\
HTTP/1.1 200 OK\
Cache-Control: no-cache\
Pragma: no-cache\
Content-Type: text/plain; charset=utf-8\
Expires: -1\
Vary: Accept-Encoding\
Server: Microsoft-IIS/8.5 Microsoft-HTTPAPI/2.0\
**Access-Control-Allow-Origin: https://corswebclient-contoso.msappproxy.net**\
X-AspNet-Version: 4.0.30319\
X-Powered-By: ASP.NET\
Content-Length: 17
```

### Option 4: Modify the application

You can change your application to support CORS by adding the `Access-Control-Allow-Origin` header, with appropriate values. The way to add the header depends on the application's code language. Changing the code requires the most effort.

### Option 5: Extend the lifetime of the access token

Some CORS issues can't be resolved. For example, your application redirects to `login.microsoftonline.com` to authenticate, and the access token expires. The CORS call then fails. A workaround for this scenario is to extend the lifetime of the access token, to prevent it from expiring during a user’s session. For more information, see [Configurable token lifetimes in Microsoft Entra ID](../../identity-platform/configurable-token-lifetimes).

### Option 6: Complex application

For applications that contain multiple individual web applications where preflight (`OPTIONS`) requests are used, you can publish the apps by using the complex application feature. For more information, see [Understand complex applications in Microsoft Entra application proxy](application-proxy-configure-complex-application).