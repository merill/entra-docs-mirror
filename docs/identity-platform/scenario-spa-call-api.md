---
layout: Conceptual
title: Build single-page app calling a web API - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-spa-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a single-page application that calls a web API
manager: pmwongera
ms.custom: 
ms.date: 2025-05-12T00:00:00.0000000Z
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: 686d6ca6-916e-3039-a840-b9d02f7dbba8
document_version_independent_id: dd40f329-27f7-9a46-43c5-b239a6fd7534
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-spa-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-spa-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-spa-call-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 5f71e10d-b092-2062-0e0e-6b155688a27c
---

# Build single-page app calling a web API - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

We recommend that you call the `acquireTokenSilent` method to acquire or renew an access token before calling a web API. After you have a token, you can call a protected web API.

## Call a web API

# [JavaScript](#tab/javascript)
Use the acquired access token as a bearer in an HTTP request to call any web API, such as Microsoft Graph API. For example:

```javascript
    var headers = new Headers();
    var bearer = "Bearer " + access_token;
    headers.append("Authorization", bearer);
    var options = {
         method: "GET",
         headers: headers
    };
    var graphEndpoint = "https://graph.microsoft.com/v1.0/me";

    fetch(graphEndpoint, options)
        .then(function (response) {
             //do something with response
        })
```

# [Angular](#tab/angular)
The MSAL Angular wrapper takes advantage of the HTTP interceptor to automatically acquire access tokens silently and attach them to the HTTP requests to APIs. For more information, see [Acquire a token to call an API](scenario-spa-acquire-token).

---