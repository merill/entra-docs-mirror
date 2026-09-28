---
layout: Conceptual
title: Use Azure Front Door as proxy server for SPA with native auth - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-native-authentication-cors-solution-production-environment
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to set up Azure Front Door as a reverse proxy in a production environment for a single-page app that uses native authentication.
manager: dougeby
ms.subservice: external
ms.topic: how-to
ms.date: 2025-02-07T00:00:00.0000000Z
locale: en-us
document_id: 5c1b634c-9551-4e34-0cc5-c0c5a38cc706
document_version_independent_id: 5c1b634c-9551-4e34-0cc5-c0c5a38cc706
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-native-authentication-cors-solution-production-environment.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-native-authentication-cors-solution-production-environment
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-native-authentication-cors-solution-production-environment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b5e53e15-0a76-4936-b270-8b2badca62ac
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6908a4c7-0b59-4f8b-a00e-59c83ae0a04a
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 4c730eaa-825c-d0ec-0874-b76c23d81aa1
---

# Use Azure Front Door as proxy server for SPA with native auth - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this article, you learn how to Use Azure Front Door as a reverse proxy for a single-page app (SPA) that uses [native authentication API](/en-us/entra/identity-platform/reference-native-authentication-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json).

The native authentication API doesn't support Cross-Origin Resource Sharing (CORS). Therefore, a single-page app (SPA) that uses this API for user authentication can't make successful requests from front-end JavaScript code. To resolve this issue, add a proxy server between the SPA and the native authentication API. The proxy server injects the appropriate CORS headers into the response.

In a production environment, we recommended using [Azure Front Door with a Standard/Premium subscription](/en-us/azure/frontdoor/standard-premium/troubleshoot-cross-origin-resources) as a reverse proxy.

## Prerequisites

- An Azure subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A sample SPA that you can access via a URL such as `http://www.contoso.com`:
    - You can use the React app described in [Quickstart: Sign in users into a sample React SPA by using native authentication API](quickstart-native-authentication-single-page-app-react-sign-in). However, don't configure or run the proxy server, as this guide covers that set up.
    - After you run the app, record the app URL for later use in this guide. In production, this URL contains the domain that you want to use as a custom domain URL, such as `http://www.contoso.com`
- Install [Azure Developer CLI (azd)](/en-us/azure/developer/azure-developer-cli/install-azd?tabs=winget-windows%2Cbrew-mac%2Cscript-linux&amp;pivots=os-windows).

## Set up Azure Front Door as a reverse proxy

1. Familiarize yourself with how to use Azure Front Door with CORS by reading the article at [Using Azure Front Door Standard/Premium with CORS](/en-us/azure/frontdoor/standard-premium/troubleshoot-cross-origin-resources).
2. Use the instructions in [Enable custom URL domains for apps in external tenants](../external-id/customers/how-to-custom-url-domain)to add a custom domain name to your external tenant.
    - For creating an Azure Front Door, use azd template.
3. In your sample SPA, open the *API\React\ReactAuthSimple\src\config.ts* file, then replace the value of `BASE_API_URL`, *http://localhost:3001/api*, with `https://Enter_Custom_Domain_URL/Enter_the_Tenant_ID_Here`. Replace the placeholder:
    1. `Enter_Custom_Domain_URL` with your custom domain url, such as `contoso.com`.
    2. `Enter_the_Tenant_ID_Here` with your Directory (tenant) ID. If you don't have your tenant ID, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
4. If necessary, rerun your sample SPA.

## Create Azure Front Door as a reverse proxy by using an Azure Developer CLI (azd) template

1. To initialize the azd template, run the following command:

    ```console
    azd init --template https://github.com/azure-samples/ms-identity-extid-cors-proxy-frontdoor
    ```

    When prompted, enter a name for the azd environment. The name is used as a prefix for the resource group so it should be unique within your Azure subscription.
2. To sign into Azure, run the following command:

    ```console
    azd auth login
    ```
3. To build, provision, and deploy the app resources, run the following command:

    ```console
    azd up
    ```

    When prompted, enter following information to complete resource creation:

    - `Azure Location`: The Azure location where your resources are deployed.
    - `Azure Subscription`: The Azure Subscription where your resources are deployed.
    - `corsAllowedOrigin`: The origin domain to allow CORS requests from in the format of SCHEME://DOMAIN:PORT, for example, http://localhost:3000.
    - `tenantSubdomain`: The subdomain of your external tenant that we're proxying. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant subdomain, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
    - `customDomain`: The full URL of the custom domain configured within External ID, for example, *login.example.com.*

## Guidelines for using Azure Front Door as a reverse proxy

We recommend the following guidelines when you set up Azure Front Door as a reverse proxy to manage the CORS headers in a production environment:

### Restrict origins

When you configure Azure Front Door, only allow your SPA domain url, such as `https://www.contoso.com`, as origin. Avoid configurations that permit all origins, such as `*` which could lead to security vulnerabilities.

### Use simple requests

Native authentication requests already meet all conditions of [simple requests](https://developer.mozilla.org/docs/Web/HTTP/CORS#simple_requests):

- Uses `Http Method: POST`.
- Uses `Content-Type: application/x-www-form-urlencoded`.
- Request doesn't require custom headers.
- Request doesn't involve `ReadableStream` object in the request.
- Request doesn’t require usage of `XMLHttpRequest`.