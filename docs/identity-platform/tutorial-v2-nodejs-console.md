---
layout: Conceptual
title: 'Tutorial: Call Microsoft Graph in a Node.js console daemon app - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-v2-nodejs-console
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this tutorial, you build a console daemon app for calling Microsoft Graph.
manager: pmwongera
ms.date: 2024-04-09T00:00:00.0000000Z
ms.subservice: workforce
ms.topic: tutorial
ms.custom: sfi-image-nochange
locale: en-us
document_id: df0c6e78-4a24-6600-2512-478d2629f2a1
document_version_independent_id: 2853475e-ae28-6c1a-0249-0ff59757f0fe
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-v2-nodejs-console.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-v2-nodejs-console
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-v2-nodejs-console.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 1095a4fc-f738-2a8b-78ce-05713d157dfc
---

# Tutorial: Call Microsoft Graph in a Node.js console daemon app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you build a console daemon app that calls Microsoft Graph API using its own identity. The daemon app you build uses the [Microsoft Authentication Library (MSAL) for Node.js](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node).

Follow the steps in this tutorial to:

- Register the application in the Azure portal
- Create a Node.js console daemon app project
- Add authentication logic to your app
- Add app registration details
- Add a method to call a web API
- Test the app

## Prerequisites

- [Node.js](https://nodejs.org/en/download/)
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor

## Register the application

First, complete the steps in [Register an application with the Microsoft identity platform](quickstart-register-app) to register your app.

Use the following settings for your app registration:

- Name: `NodeDaemonApp` (suggested)
- Supported account types: **Accounts in this organizational directory only**
- API permissions: **Microsoft APIs** &gt; **Microsoft Graph** &gt; **Application Permissions** &gt; `User.Read.All`
- Client secret: `*********` (record this value for use in a later step - it's shown only once)

## Create the project

1. Start by creating a directory for this Node.js tutorial project. For example, *NodeDaemonApp*.
2. In your terminal, change into the directory you created (the project root), and then run the following commands:

    ```console
    npm init -y
    npm install --save dotenv yargs axios @azure/msal-node
    ```
3. Next, edit the *package.json* file in the project root and prefix the value of `main` with `bin/`, like this:

    ```json
    "main": "bin/index.js",
    ```
4. Now create the *bin* directory, and inside *bin*, add the following code to a new file named *index.js*:

    ```JavaScript
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
            case 'getUsers':
    
                try {
                    // here we get an access token
                    const authResponse = await auth.getToken(auth.tokenRequest);
    
                    // call the web API with the access token
                    const users = await fetch.callApi(auth.apiConfig.uri, authResponse.accessToken);
    
                    // display result
                    console.log(users);
                } catch (error) {
                    console.log(error);
                }
    
                break;
            default:
                console.log('Select a Graph operation first');
                break;
        }
    };
    
    main();
    ```

The *index.js* file you just created references two other node modules that you'll create next:

- *auth.js* - Uses MSAL Node for acquiring access tokens from the Microsoft identity platform.
- *fetch.js* - Requests data from the Microsoft Graph API by including access tokens (acquired in *auth.js*) in HTTP requests to the API.

At the end of the tutorial, your project's file and directory structure should look similar to this:

```
NodeDaemonApp/
├── bin
│   ├── auth.js
│   ├── fetch.js
│   ├── index.js
├── package.json
└── .env
```

## Add authentication logic

Inside the *bin* directory, add the following code to a new file named *auth.js*. The code in *auth.js* acquires an access token from the Microsoft identity platform for including in Microsoft Graph API requests.

```JavaScript
const msal = require('@azure/msal-node');

/**
 * Configuration object to be passed to MSAL instance on creation.
 * For a full list of MSAL Node configuration parameters, visit:
 * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/configuration.md
 */
const msalConfig = {
    auth: {
        clientId: process.env.CLIENT_ID,
        authority: process.env.AAD_ENDPOINT + '/' + process.env.TENANT_ID,
        clientSecret: process.env.CLIENT_SECRET,
    }
};

/**
 * With client credentials flows permissions need to be granted in the portal by a tenant administrator.
 * The scope is always in the format '<resource>/.default'. For more, visit:
 * https://learn.microsoft.com/azure/active-directory/develop/v2-oauth2-client-creds-grant-flow
 */
const tokenRequest = {
    scopes: [process.env.GRAPH_ENDPOINT + '/.default'],
};

const apiConfig = {
    uri: process.env.GRAPH_ENDPOINT + '/v1.0/users',
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
    getToken: getToken
};
```

In the code snippet above, we first create a configuration object (*msalConfig*) and pass it to initialize an MSAL [ConfidentialClientApplication](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md). Then we create a method for acquiring tokens via **client credentials** and finally expose this module to be accessed by *main.js*. The configuration parameters in this module are drawn from an environment file, which we will create in the next step.

## Add app registration details

Create an environment file to store the app registration details that will be used when acquiring tokens. To do so, create a file named *.env* inside the root folder of the sample (*NodeDaemonApp*), and add the following code:

```
# Credentials
TENANT_ID=Enter_the_Tenant_Id_Here
CLIENT_ID=Enter_the_Application_Id_Here
CLIENT_SECRET=Enter_the_Client_Secret_Here

# Endpoints
AAD_ENDPOINT=Enter_the_Cloud_Instance_Id_Here/
GRAPH_ENDPOINT=Enter_the_Graph_Endpoint_Here/
```

Fill in these details with the values you obtain from Azure app registration portal:

- `Enter_the_Tenant_Id_here`should be one of the following:
    - If your application supports *accounts in this organizational directory*, replace this value with the **Tenant ID** or **Tenant name**. For example, `contoso.microsoft.com`.
    - If your application supports *accounts in any organizational directory*, replace this value with `organizations`.
    - If your application supports *accounts in any organizational directory and personal Microsoft accounts*, replace this value with `common`.
    - To restrict support to *personal Microsoft accounts only*, replace this value with `consumers`.
- `Enter_the_Application_Id_Here`: The **Application (client) ID** of the application you registered.
- `Enter_the_Cloud_Instance_Id_Here`: The Azure cloud instance in which your application is registered.
    - For the main (or *global*) Azure cloud, enter `https://login.microsoftonline.com`.
    - For **national** clouds (for example, China), you can find appropriate values in [National clouds](authentication-national-cloud).
- `Enter_the_Graph_Endpoint_Here`is the instance of the Microsoft Graph API the application should communicate with.
    - For the **global** Microsoft Graph API endpoint, replace both instances of this string with `https://graph.microsoft.com`.
    - For endpoints in **national** cloud deployments, see [National cloud deployments](/en-us/graph/deployments) in the Microsoft Graph documentation.

## Add a method to call a web API

Inside the *bin* folder, create another file named *fetch.js* and add the following code for making REST calls to the Microsoft Graph API:

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

Here, the `callApi` method is used to make an HTTP `GET` request against a protected resource that requires an access token. The request then returns the content to the caller. This method adds the acquired token in the *HTTP Authorization header*. The protected resource here is the Microsoft Graph API [users endpoint](/en-us/graph/api/user-list) which displays the users in the tenant where this app is registered.

## Test the app

You've completed creation of the application and are now ready to test the app's functionality.

Start the Node.js console daemon app by running the following command from within the root of your project folder:

```console
node . --op getUsers
```

This should result in some JSON response from Microsoft Graph API and you should see an array of user objects in the console:

```console
You have selected: getUsers
request made to web API at: Fri Jan 22 2021 09:31:52 GMT-0800 (Pacific Standard Time)
{
    '@odata.context': 'https://graph.microsoft.com/v1.0/$metadata#users',
    value: [
        {
            displayName: 'Adele Vance'
            givenName: 'Adele',
            jobTitle: 'Retail Manager',
            mail: 'AdeleV@msaltestingjs.onmicrosoft.com',
            mobilePhone: null,
            officeLocation: '18/2111',
            preferredLanguage: 'en-US',
            surname: 'Vance',
            userPrincipalName: 'AdeleV@msaltestingjs.onmicrosoft.com',
            id: '00aa00aa-bb11-cc22-dd33-44ee44ee44ee'
        }
    ]
}
```

![Command-line interface displaying Graph response](media/tutorial-v2-nodejs-console/screenshot.png)

## How the application works

This application uses [OAuth 2.0 client credentials grant](v2-oauth2-client-creds-grant-flow). This type of grant is commonly used for server-to-server interactions that must run in the background, without immediate interaction with a user. The credentials grant flow permits a web service (confidential client) to use its own credentials, instead of impersonating a user, to authenticate when calling another web service. The type of applications supported with this authentication model are usually **daemons** or **service accounts**.

The scope to request for a client credential flow is the name of the resource followed by `/.default`. This notation tells Microsoft Entra ID to use the application-level permissions declared statically during application registration. Also, these API permissions must be granted by a **tenant administrator**.