---
layout: Conceptual
title: Set Up CORS Proxy Server to Manage Headers for SPA With Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-native-authentication-single-page-app-javascript-sdk-set-up-local-cors
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to set up a CORS proxy server for single-page application that uses native authentication JavaScript SDK.
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2025-02-07T00:00:00.0000000Z
locale: en-us
document_id: 93172f6c-4d0e-6559-bedb-4b863c00e0a7
document_version_independent_id: 93172f6c-4d0e-6559-bedb-4b863c00e0a7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-native-authentication-single-page-app-javascript-sdk-set-up-local-cors.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-native-authentication-single-page-app-javascript-sdk-set-up-local-cors
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-native-authentication-single-page-app-javascript-sdk-set-up-local-cors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 79c83fb6-65db-00d0-3ef5-996532ca4f01
---

# Set Up CORS Proxy Server to Manage Headers for SPA With Native Authentication JavaScript SDK - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this guide, you learn how to set up a local CORS proxy server to manage CORS headers while interacting with native authentication API from your single-page app (SPA). The CORS proxy server is a solution to the native authentication API's inability to support [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/docs/Web/HTTP/CORS).

You can use the CORS server you set up in this article for local app development. Alternatively:

- You can [set up a reverse proxy server to manage CORS headers by using Azure Function App](how-to-native-authentication-cors-solution-test-environment) for a test environment.
- In a production environment, you can [use Azure Front Door as a reverse proxy](how-to-native-authentication-cors-solution-production-environment).

## Create the CORS proxy server

1. In the root folder of your SPA, create a file called *cors.js*, then add the following code:

    ```javascript
    const http = require("http");
    const https = require("https");
    const url = require("url");
    const proxyConfig = require("./proxy.config");
    
    const extraHeaders = [
        "x-client-SKU",
        "x-client-VER",
        "x-client-OS",
        "x-client-CPU",
        "x-client-current-telemetry",
        "x-client-last-telemetry",
        "client-request-id",
    ];
    http.createServer((req, res) => {
        const reqUrl = url.parse(req.url);
        const domain = url.parse(proxyConfig.proxy).hostname;
    
        // Set CORS headers for all responses including OPTIONS
        const corsHeaders = {
            "Access-Control-Allow-Origin": "*",
            "Access-Control-Allow-Methods": "GET, POST, PUT, DELETE, OPTIONS",
            "Access-Control-Allow-Headers": "Content-Type, Authorization, " + extraHeaders.join(", "),
            "Access-Control-Allow-Credentials": "true",
            "Access-Control-Max-Age": "86400", // 24 hours
        };
    
        // Handle preflight OPTIONS request
        if (req.method === "OPTIONS") {
            res.writeHead(204, corsHeaders);
            res.end();
            return;
        }
    
        if (reqUrl.pathname.startsWith(proxyConfig.localApiPath)) {
            const targetUrl = proxyConfig.proxy + reqUrl.pathname?.replace(proxyConfig.localApiPath, "") + (reqUrl.search || "");
    
            console.log("Incoming request -> " + req.url + " ===> " + reqUrl.pathname);
    
            const newHeaders = {};
            for (let [key, value] of Object.entries(req.headers)) {
                if (key !== 'origin') {
                    newHeaders[key] = value;
                }
            }
    
            const proxyReq = https.request(
                targetUrl,
                {
                    method: req.method,
                    headers: {
                        ...newHeaders,
                        host: domain,
                    },
                },
                (proxyRes) => {
                    res.writeHead(proxyRes.statusCode, {
                        ...proxyRes.headers,
                        ...corsHeaders,
                    });
    
                    proxyRes.pipe(res);
                }
            );
    
            proxyReq.on("error", (err) => {
                console.error("Error with the proxy request:", err);
                res.writeHead(500, { "Content-Type": "text/plain" });
                res.end("Proxy error.");
            });
    
            req.pipe(proxyReq);
        } else {
            res.writeHead(404, { "Content-Type": "text/plain" });
            res.end("Not Found");
        }
    }).listen(proxyConfig.port, () => {
        console.log("CORS proxy running on http://localhost:3001");
        console.log("Proxying from " + proxyConfig.localApiPath + " ===> " + proxyConfig.proxy);
    });
    ```
2. In the root folder of your SPA, create a file called *proxy.config.js*, then add the following code:

    ```javascript
    const tenantSubdomain = "Enter_the_Tenant_Subdomain_Here";
    const tenantId = "Enter_the_Tenant_Id_Here";
    
    const config = {
        localApiPath: "/api",
        port: 3001,
        proxy: `https://${tenantSubdomain}.ciamlogin.com/${tenantId}`,
    };
    module.exports = config;
    ```

    - Find the placeholder `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant subdomain, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
    - `tenantId` and replace it with the Directory (tenant) ID. If you don't have your tenant ID, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
3. Open *package.json* file of your SPA, then add the following command in the *scripts* object:

    ```json
    "cors": "node cors.js",
    ```

At this point, the CORS proxy server is ready to run.

## Run the CORS server

To start the CORS proxy server, run the following command in your terminal:

```console
npm run cors
```