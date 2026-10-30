---
layout: Conceptual
title: Call an API in a Node.js web application - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-web-app-node-sign-in-call-api-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to call a protected API in your Node.js web application using access tokens from Microsoft Entra External ID.
manager: dougeby
ms.topic: how-to
ms.date: 2025-03-16T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 00975c4d-1c7f-edcd-7631-26fecd1da863
document_version_independent_id: 00975c4d-1c7f-edcd-7631-26fecd1da863
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-web-app-node-sign-in-call-api-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-web-app-node-sign-in-call-api-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-web-app-node-sign-in-call-api-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: acbd4ae1-31f0-dcc6-e452-69d3f99bb2f0
---

# Call an API in a Node.js web application - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this article, you learn how to call a web API from your Node.js client web app using the access token you acquire in [Acquire access token](how-to-web-app-node-sign-in-call-api-sign-in-acquire-access-token#acquire-access-token). The web API is protected by Microsoft Entra External ID. This article is the fourth and last part of a four-part guide series.

## Prerequisite

- Complete the steps in the first part of this guide series, [Prepare external tenant to call an API in a Node.js web application](how-to-web-app-node-sign-in-call-api-prepare-tenant).
- Complete the steps in the second part of this guide series, [Prepare app to call an API in a Node.js web application](how-to-web-app-node-sign-in-call-api-prepare-app).
- Complete the steps in third the part of this guide series [Acquire an access token in your Node.js web app](how-to-web-app-node-sign-in-call-api-sign-in-acquire-access-token) article.

## Update code

1. In your code editor, open *routes/todos.js* file, then add the following code:

    ```javascript
        const express = require('express');
        const router = express.Router();
    
        const toDoListController = require('../controller/todolistController');
        const authProvider = require('../auth/AuthProvider');
        const { protectedResources } = require('../authConfig');
    
        // custom middleware to check auth state
        function isAuthenticated(req, res, next) {
            if (!req.session.isAuthenticated) {
                return res.redirect('/auth/signin'); // redirect to sign-in route
            }
    
            next();
        }        
        // isAuthenticated checks if user is authenticated
        router.get('/',isAuthenticated, authProvider.getToken(protectedResources.toDoListAPI.scopes.read),toDoListController.getToDos);
    
        router.delete('/', isAuthenticated,authProvider.getToken(protectedResources.toDoListAPI.scopes.write),toDoListController.deleteToDo);
    
        router.post('/',isAuthenticated,authProvider.getToken(protectedResources.toDoListAPI.scopes.write),toDoListController.postToDo);
    
        module.exports = router;
    ```

    This file contains express routes for create, read and delete resource in the protected API. Each route uses three middleware functions, which execute in that sequence:

    - `isAuthenticated` checks whether the user is authenticated.
    - `getToken` requests an access token. You defined this function earlier in [Acquire access token](how-to-web-app-node-sign-in-call-api-sign-in-acquire-access-token#acquire-access-token). For example, the create resource route (POST request) requests an access token with read and write permissions.
    - Finally, the `postToDo` or `deleteToDo``getToDos` methods handles the actual logic for manipulating the resource. These functions are defined in *controller/todolistController.js* file.
2. In your code editor, open *controller/todolistController.js* file, then add the following code:

    ```javascript
        const { callEndpointWithToken } = require('../fetch');
        const { protectedResources } = require('../authConfig');
    
        exports.getToDos = async (req, res, next) => {
            try {
                const todoResponse = await callEndpointWithToken(
                    protectedResources.toDoListAPI.endpoint,
                    req.session.accessToken,
                    'GET'
                );
                res.render('todos', { isAuthenticated: req.session.isAuthenticated, todos: todoResponse.data });
            } catch (error) {
                next(error);
            }
        };
    
        exports.postToDo = async (req, res, next) => {
            try {
                if (!!req.body.description) {
                    let todoItem = {
                        description: req.body.description,
                    };
    
                    await callEndpointWithToken(
                        protectedResources.toDoListAPI.endpoint,
                        req.session.accessToken,
                        'POST',
                        todoItem
                    );
                    res.redirect('todos');
                } else {
                    throw { error: 'empty request' };
                }
            } catch (error) {
                next(error);
            }
        };
    
        exports.deleteToDo = async (req, res, next) => {
            try {
                await callEndpointWithToken(
                    protectedResources.toDoListAPI.endpoint,
                    req.session.accessToken,
                    'DELETE',
                    req.body._id
                );
                res.redirect('todos');
            } catch (error) {
                next(error);
            }
        };
    ```

    Each of these functions collects all the information required to call an API. It then delegates the work to the `callEndpointWithToken` function and waits for a response. The `callEndpointWithToken` function is defined in the *fetch.js* file. For example, to create a resource in the API, the `postToDo` function passes an endpoint, an access token, an HTTP method and a request body to the `callEndpointWithToken` function and waits for a response. It then redirects the user to the *todo.hbs* view to show all tasks.
3. In your code editor, open *fetch.js* file, then add the following code:

    ```javascript
        const axios = require('axios');
    
        /**
         * Makes an Authorization "Bearer" request with the given accessToken to the given endpoint.
         * @param endpoint
         * @param accessToken
         * @param method
         */
        const callEndpointWithToken = async (endpoint, accessToken, method, data = null) => {
            const options = {
                headers: {
                    Authorization: `Bearer ${accessToken}`,
                },
            };
    
            switch (method) {
                case 'GET':
                    return await axios.get(endpoint, options);
                case 'POST':
                    return await axios.post(endpoint, data, options);
                case 'DELETE':
                    return await axios.delete(endpoint + `/${data}`, options);
                default:
                    return null;
            }
        };
    
        module.exports = {
            callEndpointWithToken,
        };
    ```

    This function makes the actual API call. Notice how you include the access token as the value of bearer token in the HTTP request header:

    ```javascript
        //...        
        headers: {
            Authorization: `Bearer ${accessToken}`,
        }        
        //...
    ```
4. In your code editor, open *.env* file, then add the following configuration:

    ```text
        # Use this variable only in the development environment. 
        # Please remove the variable when you move the app to the production environment.
        NODE_TLS_REJECT_UNAUTHORIZED='0'
    ```

    The `NODE_TLS_REJECT_UNAUTHORIZED='0'` setting in your .env file instructs Node.js to ignore any SSL certificate errors, such as the self-signed certificate error.
5. In your code editor, open the `app.js` file, then:

    1. Add the todo router by using the following code:

        ```javascript
            var todosRouter = require('./routes/todos');
        ```
    2. Use the todo router by using the following code:

        ```javascript
            app.use('/todos', todosRouter); 
        ```

## Run and test web app and API

At this point, you're ready to call the web API from the client web app:

1. Use the steps in [Secure an ASP.NET web API](/en-us/entra/external-id/customers/tutorial-protect-web-api-dotnet-core-build-app) article to start your web API app. Your web API is now ready to serve client requests.
2. In your terminal, make sure you're in the project folder that contains your client web app such as `ciam-sign-in-call-api-node-express-web-app`, then run the following command:

    ```console
    npm start
    ```

    Your client web app starts.
3. Use the steps in [Run and test sample web app and API](quickstart-web-app-node-sign-in-call-api#run-and-test-sample-web-app-and-api) to demonstrate how the client app calls the web API.