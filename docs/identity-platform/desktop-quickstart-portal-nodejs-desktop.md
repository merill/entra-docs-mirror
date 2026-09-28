---
layout: Conceptual
title: 'Quickstart: Call Microsoft Graph from a Node.js desktop app - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/desktop-quickstart-portal-nodejs-desktop
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you learn how a Node.js Electron desktop application can sign-in users and get an access token to call an API protected by a Microsoft identity platform endpoint
ROBOTS: NOINDEX
manager: pmwongera
ms.custom: 
ms.date: 2022-08-18T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: 1941e6f9-3d5d-de12-846b-3e8a6d6e2a62
document_version_independent_id: 0c6d83c1-deb8-8464-51c8-39e9a1372883
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/desktop-quickstart-portal-nodejs-desktop.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/desktop-quickstart-portal-nodejs-desktop
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/desktop-quickstart-portal-nodejs-desktop.md
platformId: fa544639-5a11-1243-98c3-e3ba99061f52
---

# Quickstart: Call Microsoft Graph from a Node.js desktop app - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Sign in users and call Microsoft Graph from a Node.js desktop app](quickstart-desktop-app-nodejs-electron-sign-in)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

# Quickstart: Acquire an access token and call the Microsoft Graph API from an Electron desktop app

In this quickstart, you download and run a code sample that demonstrates how an Electron desktop application can sign in users and acquire access tokens to call the Microsoft Graph API.

This quickstart uses the [Microsoft Authentication Library for Node.js (MSAL Node)](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) with the [authorization code flow with PKCE](v2-oauth2-auth-code-flow).

## Prerequisites

- [Node.js](https://nodejs.org/en/download/)
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor

#### Step 1: Configure the application in Azure portal

For the code sample for this quickstart to work, you need to add a reply URL as `msal://redirect`.

![Already configured](media/quickstart-v2-windows-desktop/green-check.png) Your application is configured with these attributes.

#### Step 2: Download the Electron sample project

Note

`Enter_the_Supported_Account_Info_Here`

#### Step 4: Run the application

You'll need to install the dependencies of this sample once:

```console
npm install
```

Then, run the application via command prompt or console:

```console
npm start
```

You should see application's UI with a **Sign in** button.

## About the code

Below, some of the important aspects of the sample application are discussed.

### MSAL Node

[MSAL Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) is the library used to sign in users and request tokens used to access an API protected by Microsoft identity platform. For more information on how to use MSAL Node with desktop apps, see [this article](scenario-desktop-app-configuration).

You can install MSAL Node by running the following npm command.

```console
npm install @azure/msal-node --save
```

### MSAL initialization

You can add the reference for MSAL Node by adding the following code:

```javascript
const { PublicClientApplication } = require('@azure/msal-node');
```

Then, initialize MSAL using the following code:

```javascript
const MSAL_CONFIG = {
    auth: {
        clientId: "Enter_the_Application_Id_Here",
        authority: "https://login.microsoftonline.com/Enter_the_Tenant_Id_Here",
    },
};

const pca = new PublicClientApplication(MSAL_CONFIG);
```

> 
> 
> | Where: | Description |
> | --- | --- |
> | `clientId` | Is the **Application (client) ID** for the application registered in the Azure portal. You can find this value in the app's **Overview** page in the Azure portal. |
> | `authority` | The STS endpoint for user to authenticate. Usually `https://login.microsoftonline.com/{tenant}` for public cloud, where {tenant} is the name of your tenant or your tenant Id. |
> 

### Requesting tokens

In the first leg of authorization code flow with PKCE, prepare and send an authorization code request with the appropriate parameters. Then, in the second leg of the flow, listen for the authorization code response. Once the code is obtained, exchange it to obtain a token.

```javascript
// The redirect URI you setup during app registration with a custom file protocol "msal"
const redirectUri = "msal://redirect";

const cryptoProvider = new CryptoProvider();

const pkceCodes = {
    challengeMethod: "S256", // Use SHA256 Algorithm
    verifier: "", // Generate a code verifier for the Auth Code Request first
    challenge: "" // Generate a code challenge from the previously generated code verifier
};

/**
 * Starts an interactive token request
 * @param {object} authWindow: Electron window object
 * @param {object} tokenRequest: token request object with scopes
 */
async function getTokenInteractive(authWindow, tokenRequest) {

    /**
     * Proof Key for Code Exchange (PKCE) Setup
     *
     * MSAL enables PKCE in the Authorization Code Grant Flow by including the codeChallenge and codeChallengeMethod
     * parameters in the request passed into getAuthCodeUrl() API, as well as the codeVerifier parameter in the
     * second leg (acquireTokenByCode() API).
     */

    const {verifier, challenge} = await cryptoProvider.generatePkceCodes();

    pkceCodes.verifier = verifier;
    pkceCodes.challenge = challenge;

    const authCodeUrlParams = {
        redirectUri: redirectUri
        scopes: tokenRequest.scopes,
        codeChallenge: pkceCodes.challenge, // PKCE Code Challenge
        codeChallengeMethod: pkceCodes.challengeMethod // PKCE Code Challenge Method
    };

    const authCodeUrl = await pca.getAuthCodeUrl(authCodeUrlParams);

    // register the custom file protocol in redirect URI
    protocol.registerFileProtocol(redirectUri.split(":")[0], (req, callback) => {
        const requestUrl = url.parse(req.url, true);
        callback(path.normalize(`${__dirname}/${requestUrl.path}`));
    });

    const authCode = await listenForAuthCode(authCodeUrl, authWindow); // see below

    const authResponse = await pca.acquireTokenByCode({
        redirectUri: redirectUri,
        scopes: tokenRequest.scopes,
        code: authCode,
        codeVerifier: pkceCodes.verifier // PKCE Code Verifier
    });

    return authResponse;
}

/**
 * Listens for auth code response from Azure AD
 * @param {string} navigateUrl: URL where auth code response is parsed
 * @param {object} authWindow: Electron window object
 */
async function listenForAuthCode(navigateUrl, authWindow) {

    authWindow.loadURL(navigateUrl);

    return new Promise((resolve, reject) => {
        authWindow.webContents.on('will-redirect', (event, responseUrl) => {
            try {
                const parsedUrl = new URL(responseUrl);
                const authCode = parsedUrl.searchParams.get('code');
                resolve(authCode);
            } catch (err) {
                reject(err);
            }
        });
    });
}
```

> 
> 
> | Where: | Description |
> | --- | --- |
> | `authWindow` | Current Electron window in process. |
> | `tokenRequest` | Contains the scopes being requested, such as `"User.Read"` for Microsoft Graph or `"api://<Application ID>/access_as_user"` for custom web APIs. |
>