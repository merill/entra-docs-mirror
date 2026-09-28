---
layout: Conceptual
title: 'Quickstart: Call Microsoft Graph from a Node.js desktop app - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-v2-nodejs-desktop
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
ms.date: 2022-01-14T00:00:00.0000000Z
ms.topic: quickstart
locale: en-us
document_id: 1e30401b-2ee1-f260-b27f-c80a02d66d56
document_version_independent_id: 7bc02233-3538-8f3a-5bcd-6dea0f021fd1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-v2-nodejs-desktop.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-v2-nodejs-desktop
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-v2-nodejs-desktop.md
platformId: eab1ff54-8173-2d35-3176-b1e20344e7d3
---

# Quickstart: Call Microsoft Graph from a Node.js desktop app - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Sign in users and call Microsoft Graph from a Node.js desktop app](quickstart-desktop-app-nodejs-electron-sign-in)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

In this quickstart, you download and run a code sample that demonstrates how an Electron desktop application can sign in users and acquire access tokens to call the Microsoft Graph API.

This quickstart uses the [Microsoft Authentication Library for Node.js (MSAL Node)](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) with the [authorization code flow with PKCE](v2-oauth2-auth-code-flow).

## Prerequisites

- [Node.js](https://nodejs.org/en/download/)
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor

#### Step 1: Configure the application in Azure portal

For the code sample for this quickstart to work, you need to add a reply URL as **msal://redirect**.

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

You can use MSAL Node's acquireTokenInteractive public API to acquire tokens via an external user-agent such as the default system browser.

```javascript
const { shell } = require('electron');

try {
   const openBrowser = async (url) => {
       await shell.openExternal(url);
   };

   const authResponse = await pca.acquireTokenInteractive({
       scopes: ["User.Read"],
       openBrowser,
       successTemplate: '<h1>Successfully signed in!</h1> <p>You can close this window now.</p>',
       failureTemplate: '<h1>Oops! Something went wrong</h1> <p>Check the console for more information.</p>',
   });

   return authResponse;
} catch (error) {
   throw error;
}
```