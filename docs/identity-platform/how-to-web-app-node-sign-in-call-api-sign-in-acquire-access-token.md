---
layout: Conceptual
title: Acquire an access token in your Node.js web app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-web-app-node-sign-in-call-api-sign-in-acquire-access-token
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to acquire an access token for calling an API in your own Node.js web application.
manager: dougeby
ms.topic: how-to
ms.date: 2025-03-16T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 81b41699-a377-b3ff-da43-53aac14fb824
document_version_independent_id: 81b41699-a377-b3ff-da43-53aac14fb824
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-web-app-node-sign-in-call-api-sign-in-acquire-access-token.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-web-app-node-sign-in-call-api-sign-in-acquire-access-token
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-web-app-node-sign-in-call-api-sign-in-acquire-access-token.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 618b4a9a-2dc8-73aa-687d-0fb732f17e68
---

# Acquire an access token in your Node.js web app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this article, you update your code, to enable your web app to acquire an access token. You use [Microsoft Authentication Library (MSAL) for Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) to simplify adding authentication and authorization to your node web application. This article is the third part of a four-part guide series.

## Prerequisites

- Complete the steps in the first part of this guide series, [Prepare external tenant to call an API in a Node.js web application](how-to-web-app-node-sign-in-call-api-prepare-tenant).
- Complete the steps in the second part of this guide series, [Prepare app to call an API in a Node.js web application](how-to-web-app-node-sign-in-call-api-prepare-app).

## Update MSAL configuration object

In your code editor, open *authConfig.js* file, then update the code by adding the `protectedResources` object:

```javascript
    //..   
    const toDoListReadScope = process.env.TODOLIST_READ || 'api://Enter_the_Web_Api_Application_Id_Here/ToDoList.Read';
    const toDoListReadWriteScope = process.env.TODOLIST_READWRITE || 'api://Enter_the_Web_Api_Application_Id_Here/ToDoList.ReadWrite';
    
    const protectedResources = {
        toDoListAPI: {
            endpoint: 'https://localhost:44351/api/todolist',
            scopes: {
                read: [toDoListReadScope],
                write: [toDoListReadWriteScope],
            },
        },
    };    
    module.exports = {
        //..
        protectedResources,
        //..
    };
```

In your *authConfig.js* file, replace `Enter_the_Web_Api_Application_Id_Here` with the Application (client) ID of the web API app that you registered in your customer's tenant.

The `todolistReadScope` and `todolistReadWriteScope` variables hold the web API full scope URLs that you set in your external tenant. Make sure you export the `protectedResources` object.

## Acquire access token

In your code editor, open *auth/AuthProvider.js* file, then update the `getToken` method in the `AuthProvider` class:

```javascript
    const axios = require('axios');
    class AuthProvider {
    //...
        getToken(scopes) {
            return  async function (req, res, next) {
                const msalInstance = authProvider.getMsalInstance(authProvider.config.msalConfig);
                try {
                    msalInstance.getTokenCache().deserialize(req.session.tokenCache);
    
                    const silentRequest = {
                        account: req.session.account,
                        scopes: scopes,
                    };
    
                    const tokenResponse = await msalInstance.acquireTokenSilent(silentRequest);
    
                    req.session.tokenCache = msalInstance.getTokenCache().serialize();
                    req.session.accessToken = tokenResponse.accessToken;
                    next();
                } catch (error) {
                    if (error instanceof msal.InteractionRequiredAuthError) {
                        req.session.csrfToken = authProvider.cryptoProvider.createNewGuid();
    
                        const state = authProvider.cryptoProvider.base64Encode(
                            JSON.stringify({
                                redirectTo: 'http://localhost:3000/todos',
                                csrfToken: req.session.csrfToken,
                            })
                        );
                        
                        const authCodeUrlRequestParams = {
                            state: state,
                            scopes: scopes,
                        };
    
                        const authCodeRequestParams = {
                            state: state,
                            scopes: scopes,
                        };
    
                        authProvider.redirectToAuthCodeUrl(
                            req,
                            res,
                            next,
                            authCodeUrlRequestParams,
                            authCodeRequestParams,
                            msalInstance
                        );
                    }
    
                    next(error);
                }
            };
        }
    //...
    }
```

- First, the function attempts to acquire an access token silently (without prompting the user for credentials):

    ```javascript
    const silentRequest = {
        account: req.session.account,
        scopes: scopes,
    };
    
    const tokenResponse = await msalInstance.acquireTokenSilent(silentRequest);
    ```
- If you successfully acquire a token silently, store it in a session. You retrieve the token from the session when you call an API.

    ```javascript
    req.session.accessToken = tokenResponse.accessToken;
    ```
- If you fail to acquire the token silently (such as with `InteractionRequiredAuthError` exception), request an access token afresh.

Note

Once your client application receives an access token, it should treat it as an opaque string. The access token is intended for the API, not for the client application. Therefore, the client application should not attempt to read or process the access token. Instead, it should include the access token as-is in the *Authorization* header of its requests to the API. The API is responsible for interpreting the access token and using it to authenticate and authorize the client application’s requests.