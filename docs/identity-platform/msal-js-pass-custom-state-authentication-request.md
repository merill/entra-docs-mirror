---
layout: Conceptual
title: Pass custom state in authentication requests (MSAL.js) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-js-pass-custom-state-authentication-request
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to pass a custom state parameter value in authentication request using the Microsoft Authentication Library for JavaScript (MSAL.js).
manager: dougeby
ms.date: 2026-01-09T00:00:00.0000000Z
ms.reviewer: jo.arroyo
ms.topic: how-to
locale: en-us
document_id: 9bbc905f-7d33-4403-d9bf-35b96d759095
document_version_independent_id: 18d853d3-53ed-1739-dcf2-67fd8c6a66ab
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-js-pass-custom-state-authentication-request.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-js-pass-custom-state-authentication-request
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-js-pass-custom-state-authentication-request.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fe39cd45-39de-4047-953d-db268d7c71d9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ca56ff04-5597-4109-9f5d-17812bae2fac
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d67e972f-fe95-59be-deb0-720b5043a6ba
---

# Pass custom state in authentication requests (MSAL.js) - Microsoft identity platform | Microsoft Learn

The *state* parameter, as defined by OAuth 2.0, is included in an authentication request and is also returned in the token response to prevent cross-site request forgery attacks. By default, the Microsoft Authentication Library for JavaScript (MSAL.js) passes a randomly generated unique *state* parameter value in the authentication requests.

The state parameter can also be used to encode information of the app's state before redirect. You can pass the user's state in the app, such as the page or view they were on, as input to this parameter. The MSAL.js library allows you to pass your custom state as state parameter in the [Request](https://azuread.github.io/microsoft-authentication-library-for-js/ref/modules/_azure_msal_browser.html#redirectrequest) object. For example:

For security and privacy, do not put URLs or other sensitive data directly in the state parameter. Instead, use a key or identifier that corresponds to data stored in browser storage, such as localStorage or sessionStorage. This approach lets your app securely reference the necessary data after authentication.

```javascript
import {PublicClientApplication} from "@azure/msal-browser";

const myMsalObj = new PublicClientApplication({
    clientId: "ENTER_CLIENT_ID_HERE"
});

let loginRequest = {
    scopes: ["user.read"],
    state: "page_url"
}

myMSALObj.loginRedirect(loginRequest);
```

The passed in state is appended to the unique GUID set by MSAL.js when sending the request. When the response is returned, MSAL.js checks for a state match and then returns the custom passed in state in the [Response](https://azuread.github.io/microsoft-authentication-library-for-js/ref/modules/_azure_msal_common.html#authenticationresult) object as `state`.