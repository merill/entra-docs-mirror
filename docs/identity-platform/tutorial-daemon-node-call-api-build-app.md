---
layout: Conceptual
title: 'Tutorial: Call a web API from your Node.js daemon application - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-daemon-node-call-api-build-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about how to prepare your Node.js client daemon app, then configure it to acquire an access token for calling a web API.
manager: dougeby
ms.topic: tutorial
ms.date: 2024-08-27T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 12431b2a-f904-de3f-8f77-70ac16e02444
document_version_independent_id: 12431b2a-f904-de3f-8f77-70ac16e02444
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-daemon-node-call-api-build-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-daemon-node-call-api-build-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-daemon-node-call-api-build-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d51e6acd-af0d-90d0-f39b-91363ad30360
---

# Tutorial: Call a web API from your Node.js daemon application - Microsoft identity platform | Microsoft Learn

This tutorial demonstrates how to prepare your Node.js daemon client app using the [Open Authorization (OAuth) 2.0 client credentials grant flow](v2-oauth2-client-creds-grant-flow), then configure it to acquire an access token for calling a web API. You'll build a Node.js application using [Microsoft Authentication Library (MSAL) for Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) to simplify adding authorization to your app.

In this tutorial;

- Configure app roles for the web API
- Grant permissions to the daemon app
- Create a Node.js app in Visual Studio Code, then install dependencies.
- Enable the Node.js app to acquire an access token for calling a web API.

## Prerequisites

- Register a new client app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in any organizational directory and personal Microsoft accounts*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
    - Directory (tenant) domain name (for example, *contoso.onmicrosoft.com* or *contoso.com*).
- Add a client secret to your client app registration. **Do not** use client secrets in production apps. Use certificates or federated credentials instead. For more information, see [add credentials to your application](how-to-add-credentials?tabs=client-secret).
- A protected web API that is running and ready to accept requests. Make sure your web API exposes the following endpoints via HTTPS:
    - `GET /api/todolist` to get all todos.
    - `POST /api/todolist` to add a TODO.
- [Node.js](https://nodejs.org).
- Although any integrated development environment (IDE) that supports React applications can be used, this tutorial uses [Visual Studio Code](https://visualstudio.microsoft.com/downloads/).

## Configure app roles

An API needs to publish a minimum of one app role for applications, also called [Application permission](permissions-consent-overview), for the client apps to obtain an access token as themselves. Application permissions are the type of permissions that APIs should publish when they want to enable client applications to successfully authenticate as themselves and not need to sign-in users. To publish an application permission, follow these steps:

1. From the **App registrations** page, select the application that you created (such as *ciam-ToDoList-api*) to open its **Overview** page.
2. Under **Manage**, select **App roles**.
3. Select **Create app role**, then enter the following values, then select **Apply** to save your changes:

    | Property | Value |
    | --- | --- |
    | Display name | *ToDoList.Read.All* |
    | Allowed member types | **Applications** |
    | Value | *ToDoList.Read.All* |
    | Description | *Allow the app to read every user's ToDo list using the 'TodoListApi'* |
    | Do you want to enable this app role? | Keep it checked |
4. Select **Create app role** again, then enter the following values for the second app role, then select **Apply** to save your changes:

    | Property | Value |
    | --- | --- |
    | Display name | *ToDoList.ReadWrite.All* |
    | Allowed member types | **Applications** |
    | Value | *ToDoList.ReadWrite.All* |
    | Description | *Allow the app to read and write every user's ToDo list using the 'ToDoListApi'* |
    | Do you want to enable this app role? | Keep it checked |

## Configure idtyp token claim

You can add the **idtyp** optional claim to help the web API to determine whether a token is an **app** token or an **app + user** token. Although you can use a combination of **scp** and **roles** claims for the same purpose, using the **idtyp** claim is the easiest way to tell an app token and an app + user token apart. For example, the value of this claim is *app* when the token is an app-only token.

## Grant API permissions to the daemon app

1. From the **App registrations** page, select the application that you created, such as *ciam-client-app*.
2. Under **Manage**, select **API permissions**.
3. Under **Configured permissions**, select **Add a permission**.
4. Select the **APIs my organization uses** tab.
5. In the list of APIs, select the API such as *ciam-ToDoList-api*.
6. Select **Application permissions** option. We select this option as the app signs in as itself, but not on behalf of a user.
7. From the permissions list, select **TodoList.Read.All, ToDoList.ReadWrite.All** (use the search box if necessary).
8. Select the **Add permissions** button.
9. At this point, you've assigned the permissions correctly. However, since the daemon app doesn't allow users to interact with it, the users themselves can't consent to these permissions. To address this problem, you as the admin must consent to these permissions on behalf of all the users in the tenant:

    1. Select **Grant admin consent for &lt;your tenant name&gt;**, then select **Yes**.
    2. Select **Refresh**, then verify that **Granted for &lt;your tenant name&gt;** appears under **Status** for both permissions.

## Create the Node.js daemon project

Create a folder to host your Node.js daemon application, such as `ciam-call-api-node-daemon`:

1. In your terminal, change directory into your Node daemon app folder, such as `cd ciam-call-api-node-daemon`, then run `npm init -y`. This command creates a default package.json file for your Node.js project. This command creates a default `package.json` file for your Node.js project.
2. Create additional folders and files to achieve the following project structure:

    ```text
        ciam-call-api-node-daemon/
        ├── auth.js
        └── authConfig.js
        └── fetch.js
        └── index.js 
        └── package.json
    ```

## Install app dependencies

In your terminal, install `axios`, `yargs` and `@azure/msal-node` packages by running the following command:

```console
npm install axios yargs @azure/msal-node   
```

## Create MSAL configuration object

In your code editor, open *authConfig.js* file, then add the following code:

```javascript
require('dotenv').config();

/**
 * Configuration object to be passed to MSAL instance on creation.
 * For a full list of MSAL Node configuration parameters, visit:
 * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/configuration.md
 */    
const msalConfig = {
    auth: {
        clientId: process.env.CLIENT_ID || 'Enter_the_Application_Id_Here', // 'Application (client) ID' of app registration in Azure portal - this value is a GUID
        authority: process.env.AUTHORITY || 'https://Enter_the_Tenant_Subdomain_Here.ciamlogin.com/', // Replace "Enter_the_Tenant_Subdomain_Here" with your tenant subdomain
        clientSecret: process.env.CLIENT_SECRET || 'Enter_the_Client_Secret_Here', // Client secret generated from the app 
    },
    system: {
        loggerOptions: {
            loggerCallback(loglevel, message, containsPii) {
                console.log(message);
            },
            piiLoggingEnabled: false,
            logLevel: 'Info',
        },
    },
};    
const protectedResources = {
    apiToDoList: {
        endpoint: process.env.API_ENDPOINT || 'https://localhost:44351/api/todolist',
        scopes: [process.env.SCOPES || 'api://Enter_the_Web_Api_Application_Id_Here'],
    },
};

module.exports = {
    msalConfig,
    protectedResources,
};
```

The `msalConfig` object contains a set of configuration options that you use to customize the behavior of your authorization flow.

In your *authConfig.js* file, replace:

- `Enter_the_Application_Id_Here` with the Application (client) ID of the client daemon app that you registered earlier.
- `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
- `Enter_the_Client_Secret_Here` with the client daemon app secret value that you copied earlier.
- `Enter_the_Web_Api_Application_Id_Here` with the Application (client) ID of the web API app that you copied earlier.

Notice that the `scopes` property in the `protectedResources` variable is the resource identifier (application ID URI) of the web API that you registered as part of the prerequisites. The complete scope URI looks similar to `api://Enter_the_Web_Api_Application_Id_Here/.default`.

## Acquire an access token

In your code editor, open *auth.js* file, then add the following code:

```javascript
const msal = require('@azure/msal-node');
const { msalConfig, protectedResources } = require('./authConfig');
/**
 * With client credentials flows permissions need to be granted in the portal by a tenant administrator.
 * The scope is always in the format '<resource-appId-uri>/.default'. For more, visit:
 * https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-client-creds-grant-flow
 */
const tokenRequest = {
    scopes: [`${protectedResources.apiToDoList.scopes}/.default`],
};

const apiConfig = {
    uri: protectedResources.apiToDoList.endpoint,
};

/**
 * Initialize a confidential client application. For more info, visit:
 * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md
 */
const cca = new msal.ConfidentialClientApplication(msalConfig);
/**
 * Acquires token with client credentials.
 * @param {object} tokenRequest
 */
async function getToken(tokenRequest) {
    return await cca.acquireTokenByClientCredential(tokenRequest);
}

module.exports = {
    apiConfig: apiConfig,
    tokenRequest: tokenRequest,
    getToken: getToken,
};
```

In the code:

- Prepare the `tokenRequest` and `apiConfig` object. The `tokenRequest` contains the scope for which you request an access token. The scope looks something like `api://Enter_the_Web_Api_Application_Id_Here/.default`. The `apiConfig` object contains the endpoint to your web API. Learn more about [OAuth 2.0 client credentials flow](v2-oauth2-client-creds-grant-flow).
- You create a confidential client instance by passing the `msalConfig` object to the [ConfidentialClientApplication](/en-us/javascript/api/%40azure/msal-node/confidentialclientapplication#constructors) class' constructor.

    ```javascript
    const cca = new msal.ConfidentialClientApplication(msalConfig);
    ```
- You then use the [acquireTokenByClientCredential](/en-us/javascript/api/%40azure/msal-node/confidentialclientapplication#@azure-msal-node-confidentialclientapplication-acquiretokenbyclientcredential) function to acquire an access token. You implement this logic in the `getToken` function:

    ```javascript
    cca.acquireTokenByClientCredential(tokenRequest);
    ```

Once you acquire an access token, you can proceed to call an API.

## Call an API

In your code editor, open *fetch.js* file, then add the following code:

```javascript
const axios = require('axios');

/**
 * Calls the endpoint with authorization bearer token.
 * @param {string} endpoint
 * @param {string} accessToken 
 */
async function callApi(endpoint, accessToken) {

    const options = {
        headers: {
            Authorization: `Bearer ${accessToken}`
        }
    };

    console.log('request made to web API at: ' + new Date().toString());

    try {
        const response = await axios.get(endpoint, options);
        return response.data;
    } catch (error) {
        console.log(error)
        return error;
    }
};

module.exports = {
    callApi: callApi
};
```

In this code, you make a call to the web API, by passing the access token as a bearer token in the request `Authorization` header:

```javascript
 Authorization: `Bearer ${accessToken}`
```

You use the access token that you acquired earlier in Acquire an access token.

Once the web API receives the request, it evaluates it then determines that it's an application request. If the access token is valid, the web API returns requested data. Otherwise, the API returns a `401 Unauthorized` HTTP error.

## Finalize your daemon app

In your code editor, open *index.js* file, then add the following code:

```javascript
#!/usr/bin/env node

// read in env settings

require('dotenv').config();

const yargs = require('yargs');
const fetch = require('./fetch');
const auth = require('./auth');

const options = yargs
    .usage('Usage: --op <operation_name>')
    .option('op', { alias: 'operation', describe: 'operation name', type: 'string', demandOption: true })
    .argv;

async function main() {
    console.log(`You have selected: ${options.op}`);

    switch (yargs.argv['op']) {
        case 'getToDos':
            try {
                const authResponse = await auth.getToken(auth.tokenRequest);
                const todos = await fetch.callApi(auth.apiConfig.uri, authResponse.accessToken);                
            } catch (error) {
                console.log(error);
            }

            break;
        default:
            console.log('Select an operation first');
            break;
    }
};

main();
```

This code is the entry point to your app. You use the [yargs JavaScript](https://www.npmjs.com/package/yargs) command-line argument parsing library for Node.js apps to interactively fetch an access token, then call API. You use the `getToken` and `callApi` functions you defined earlier:

```javascript
const authResponse = await auth.getToken(auth.tokenRequest);
const todos = await fetch.callApi(auth.apiConfig.uri, authResponse.accessToken);                
```

## Run and test daemon app and API

At this point, you're ready to test your client daemon app and web API:

1. Use the steps you learned in the [Secure an ASP.NET web API](tutorial-web-api-dotnet-core-build-app) tutorial to start your web API. Your web API is now ready to serve client requests. If you don't run your web API on port `44351` as specified in the *authConfig.js* file, make sure you update the *authConfig.js* file to use the correct web API's port number.
2. In your terminal, make sure you're in the project folder that contains your daemon Node.js app such as `ciam-call-api-node-daemon`, then run the following command:

    ```console
    node . --op getToDos
    ```

If your daemon app and web API run successfully, you should find the data returned by the web API endpoint `todos` variable, similar to the following JSON array, in your console window:

```json
{
    id: 1,
    owner: '3e8....-db63-43a2-a767-5d7db...',
    description: 'Pick up grocery'
},
{
    id: 2,
    owner: 'c3cc....-c4ec-4531-a197-cb919ed.....',
    description: 'Finish invoice report'
},
{
    id: 3,
    owner: 'a35e....-3b8a-4632-8c4f-ffb840d.....',
    description: 'Water plants'
}
```