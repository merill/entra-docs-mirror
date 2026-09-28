---
layout: Conceptual
title: Prompt behavior with MSAL.js - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-js-prompt-behavior
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn to customize prompt behavior using the Microsoft Authentication Library for JavaScript (MSAL.js).
manager: pmwongera
ms.custom: 
ms.date: 2019-04-24T00:00:00.0000000Z
ms.reviewer: 
ms.topic: how-to
locale: en-us
document_id: c6def816-86a6-e3ed-79e1-d7c9c747c205
document_version_independent_id: 22553a1d-ec26-52c3-1e88-3e5648fef2a7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-js-prompt-behavior.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-js-prompt-behavior
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-js-prompt-behavior.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/fe39cd45-39de-4047-953d-db268d7c71d9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ca56ff04-5597-4109-9f5d-17812bae2fac
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 63c05bb7-ac38-3e4a-880a-6459c94c1739
---

# Prompt behavior with MSAL.js - Microsoft identity platform | Microsoft Learn

MSAL.js allows passing a prompt value as part of its login or token request methods. Based on your application scenario, you can customize the Microsoft Entra prompt behavior for a request by setting the **prompt** parameter in the [request object](https://azuread.github.io/microsoft-authentication-library-for-js/ref/modules/_azure_msal_common.html#commonauthorizationurlrequest):

```javascript
import { PublicClientApplication } from "@azure/msal-browser";

const pca = new PublicClientApplication({
    auth: {
        clientId: "YOUR_CLIENT_ID"
    }
});

const loginRequest = {
    scopes: ["user.read"],
    prompt: 'select_account',
}

pca.loginPopup(loginRequest)
    .then(response => {
        // do something with the response
    })
    .catch(error => {
        // handle errors
    });
```

## Supported prompt values

The following prompt values can be used when authenticating with the Microsoft identity platform:

| Parameter | Behavior |
| --- | --- |
| `login` | Forces the user to enter their credentials on that request, negating single-sign on. |
| `none` | Ensures that the user isn't presented with any interactive prompt. If the request can't be completed silently by using single-sign on, the Microsoft identity platform returns a *login\_required* or *interaction\_required* error. |
| `consent` | Triggers the OAuth consent dialog after the user signs in, asking the user to grant permissions to the app. |
| `select_account` | Interrupts single sign-on by providing an account selection experience listing all the accounts in session or an option to choose a different account altogether. |
| `create` | Triggers a sign-up dialog allowing external users to create an account. For more information, see: [Self-service sign-up](../external-id/self-service-sign-up-overview) |

MSAL.js will throw an `invalid_prompt` error for any unsupported prompt values:

```console
invalid_prompt_value: Supported prompt values are 'login', 'select_account', 'consent', 'create' and 'none'. Please see here for valid configuration options: https://azuread.github.io/microsoft-authentication-library-for-js/ref/modules/_azure_msal_common.html#commonauthorizationurlrequest Given value: my_custom_prompt
```

## Default prompt values

The following shows default prompt values that MSAL.js uses:

| MSAL.js method | Default prompt | Allowed prompts |
| --- | --- | --- |
| `loginPopup` | N/A | Any |
| `loginRedirect` | N/A | Any |
| `ssoSilent` | `none` | N/A (ignored) |
| `acquireTokenPopup` | N/A | Any |
| `acquireTokenRedirect` | N/A | Any |
| `acquireTokenSilent` | `none` | N/A (ignored) |

Note

Note that **prompt** is a protocol-level parameter and signals the desired authentication behavior to the identity provider. It does not affect MSAL.js behavior and MSAL.js does not have control over how the service will ultimately handle the request. In most circumstances, Microsoft Entra ID will try to honor the request. If this is not possible, it may return an error response, or completely ignore the given prompt value.

## Interactive requests with prompt=none

Generally, when you need to make a silent request, use a silent MSAL.js method (`ssoSilent`, `acquireTokenSilent`), and handle any *login\_required* or *interaction\_required* errors with an interactive method (`loginPopup`, `loginRedirect`, `acquireTokenPopup`, `acquireTokenRedirect`).

In some cases however, the prompt value `none` can be used together with an interactive MSAL.js method to achieve silent authentication. For instance, due to the third-party cookie restrictions in some browsers, `ssoSilent` requests will fail despite an active user session with Microsoft Entra ID. As a remedy, you can pass the prompt value `none` to an interactive request such as `loginPopup`. MSAL.js will then open a popup window to Microsoft Entra ID and Microsoft Entra ID will honor the prompt value by utilizing the existing session cookie. In this case, the user will see a brief popup window but will not be prompted for a credential entry.