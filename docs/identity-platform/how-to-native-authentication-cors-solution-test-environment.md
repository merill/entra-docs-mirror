---
layout: Conceptual
title: Set up a reverse proxy for SPA by using Azure Function App - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-native-authentication-cors-solution-test-environment
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to set up a reverse proxy for a single-page app that calls native authentication API by using Azure Function App.
manager: dougeby
ms.subservice: external
ms.topic: how-to
ms.date: 2025-02-07T00:00:00.0000000Z
locale: en-us
document_id: fab75f93-6ea6-b065-b83f-4ec270a7342c
document_version_independent_id: fab75f93-6ea6-b065-b83f-4ec270a7342c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-native-authentication-cors-solution-test-environment.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-native-authentication-cors-solution-test-environment
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-native-authentication-cors-solution-test-environment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/b5e53e15-0a76-4936-b270-8b2badca62ac
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/6908a4c7-0b59-4f8b-a00e-59c83ae0a04a
platformId: 12f2d116-65cc-71ed-ef0e-8ec2e99586cd
---

# Set up a reverse proxy for SPA by using Azure Function App - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this article, you learn how to set up a reverse proxy by using Azure Functions App to manage CORS headers in a test environment for a single-page app (SPA) that uses [native authentication API](/en-us/entra/identity-platform/reference-native-authentication-api?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json).

The native authentication API doesn't support Cross-Origin Resource Sharing (CORS). Therefore, a single-page app (SPA) that uses this API for user authentication can't make successful requests from front-end JavaScript code. To resolve this issue, you need to add a proxy server between the SPA and the native authentication API. This proxy server injects the appropriate CORS headers into the response.

This solution is for testing purposes and should **NOT be used in a production environment**. If you're looking for a solution to use in a production environment, we recommended you use an Azure Front Door solution, see the instructions in [Use Azure Front Door as a reverse proxy to manage CORS headers for SPA in production](how-to-native-authentication-cors-solution-production-environment).

## Prerequisites

- An Azure subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Register `Microsoft.App` resource provider, see [How to register resource provider](/en-us/azure/azure-resource-manager/management/resource-providers-and-types). You only need to complete this step once for each newly created subscription.
- Install [Azure Developer CLI (azd)](/en-us/azure/developer/azure-developer-cli/install-azd?tabs=winget-windows%2Cbrew-mac%2Cscript-linux&amp;pivots=os-windows).
- A sample SPA that you can access via a URL such as `http://www.contoso.com`:
    - You can use the React app described in [Quickstart: Sign in users into a sample React SPA by using native authentication API](quickstart-native-authentication-single-page-app-react-sign-in). However, don't configure or run the proxy server, as this guide covers that set up.
    - Once you run the app, record the app URL for later use in this guide.

## Create reverse proxy in an Azure function app by using Azure Developer CLI (azd) template

1. To initialize the azd template, run the following command:

    ```console
    azd init --template https://github.com/azure-samples/ms-identity-extid-cors-proxy-function
    ```

    When prompted, enter a name for the azd environment. This name is used as a prefix for the resource group so it should be unique within your Azure subscription.
2. To sign into Azure, run the following command:

    ```console
    azd auth login
    ```
3. To build, provision, and deploy the app resources, run the following command:

    ```console
    azd up
    ```

    When prompted, enter the following information to complete resource creation:

    - `Azure Location`: The Azure location where your resources are deployed.
    - `Azure Subscription`: The Azure Subscription where your resources are deployed.
    - `corsAllowedOrigin`: The origin domain to allow CORS requests from in the format of SCHEME://DOMAIN:PORT, for example, *http://localhost:3000*.
    - `tenantSubdomain`: The subdomain of your external tenant that we're proxying. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant subdomain, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).

## Test your sample SPA with the reverse proxy

1. In your sample SPA, open the *API\React\ReactAuthSimple\src\config.ts* file, then replace:

    - the value of `BASE_API_URL`, *http://localhost:3001/api*, with `https://Enter_App_Function_Name_Here.azurewebsites.net`.
    - the placeholder `Enter_App_Function_Name_Here` with the name of your function app. If necessary, rerun your sample SPA.
2. Browse to the sample SPA URL, then test sign-up, sign-in and password reset flows. Your SPA app should work correctly as the reverse proxy manages CORS headers correctly.