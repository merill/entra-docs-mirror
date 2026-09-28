---
layout: Conceptual
title: Set Up CORS Proxy Server to Manage Headers for SPA With Native Authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-single-page-app-react-set-up-local-cors
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to set up a CORS proxy server for single-page application that uses native authentication API.
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2025-02-07T00:00:00.0000000Z
locale: en-us
document_id: 81f27cd8-0781-df10-47e2-30fcef567aa1
document_version_independent_id: 81f27cd8-0781-df10-47e2-30fcef567aa1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-single-page-app-react-set-up-local-cors.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-single-page-app-react-set-up-local-cors
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-single-page-app-react-set-up-local-cors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: f33ae63f-891f-d63b-49ff-112a43874b52
---

# Set Up CORS Proxy Server to Manage Headers for SPA With Native Authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to set up the CORS proxy server to manage CORS headers while interacting with native authentication API from a React single-page app (SPA). The CORS proxy server is a solution to the native authentication API's inability to support [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/docs/Web/HTTP/CORS).

In this tutorial, you:

- Create CORS proxy server.
- Set up the CORS proxy server to call the native authentication API.
- Run and test your React app.

## Prerequisites

- Complete the steps in [Tutorial: Create a React single-page app to sign in users into an external tenant using native authentication API](tutorial-native-authentication-single-page-app-react-sign-up).

### Create the CORS proxy server

1. In the root folder of your React app, create a file called *cors.js*, then add the following code:

    ```javascript
    const http = require("http");
    const https = require("https");
    const url = require("url");
    const proxyConfig = require("./proxy.config.js");
    
    http
    .createServer((req, res) => {
        const reqUrl = url.parse(req.url);
        const domain = url.parse(proxyConfig.proxy).hostname;
        if (reqUrl.pathname.startsWith(proxyConfig.localApiPath)) {
    
            const targetUrl = proxyConfig.proxy + reqUrl.pathname?.replace(proxyConfig.localApiPath, "") + (reqUrl.search || "");
    
            console.log("Incoming request -> " + req.url + " ===> " + reqUrl.pathname);
    
            const proxyReq = https.request(
                targetUrl,
                {
                    method: req.method,
                    headers: {
                        ...req.headers,
                        host: domain,
                    },
                },
                (proxyRes) => {
                    res.writeHead(proxyRes.statusCode, {
                        ...proxyRes.headers,
                        "Access-Control-Allow-Origin": "*",
                        "Access-Control-Allow-Methods": "GET, POST, PUT, DELETE, OPTIONS",
                        "Access-Control-Allow-Headers": "Content-Type, Authorization",
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
    })
    .listen(proxyConfig.port, () => {
        console.log("CORS proxy running on http://localhost:3001");
        console.log("Proxying from " + proxyConfig.localApiPath + " ===> " + proxyConfig.proxy);
    });
    ```
2. In the root folder of your React app, create a file called *proxy.config.js*, then add the following code:

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
3. Open *package.json* file, then add the following command in the *scripts* object:

    ```json
    "cors": "node cors.js",
    ```

At this point, the React app and the CORS proxy server are ready to run.

## Run and test you app

1. Open a terminal window and navigate to the root folder of your app:

    ```console
    cd reactspa
    ```
2. To start the CORS proxy server, run the following command in your terminal:

    ```console
    npm run cors
    ```
3. To start the React app, open another terminal window, then run the following command:

    ```console
    cd reactspa
    npm start
    ```
4. Open a web browser and navigate to `http://localhost:3000/`. A sign-up form appears.
5. To sign up for an account, input your details, select the **Sign Up** button, then follow the prompts.

At this point, you've successfully created a React app that can sign up a user by using the native authentication API. Next, you can update the React app to sign in a user or reset the user's password.

## Additional information about CORS proxy server

In this tutorial, you set up a local CORS server. However, you can [set up a reverse proxy server to manage CORS headers by using Azure Function App as explained in a test environment](how-to-native-authentication-cors-solution-test-environment).

In a production environment, you can use the steps in [Set up a reverse proxy for a single-page app that uses native authentication API by using Azure Function App](how-to-native-authentication-cors-solution-production-environment) to set up your CORS proxy server.