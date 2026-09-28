---
layout: Conceptual
title: 'Quickstart: Call Microsoft Graph from a Node.js console app - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-v2-nodejs-console
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you download and run a code sample that shows how a Node.js console application can get an access token and call an API protected by a Microsoft identity platform endpoint, using the app's own identity
ROBOTS: NOINDEX
manager: pmwongera
ms.custom: 
ms.date: 2022-01-10T00:00:00.0000000Z
ms.topic: quickstart
locale: en-us
document_id: 542de611-7cdf-b23a-3375-1353676a7e22
document_version_independent_id: 5c0e8f6e-ee12-4a7e-638f-8b46ef8ec8a6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-v2-nodejs-console.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-v2-nodejs-console
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-v2-nodejs-console.md
platformId: d43ae680-17fe-4013-4262-3dfe5d020a1f
---

# Quickstart: Call Microsoft Graph from a Node.js console app - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Acquire a token and call Microsoft Graph from a Node.js console app](quickstart-console-app-nodejs-acquire-token)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

In this quickstart, you download and run a code sample that demonstrates how a Node.js console application can get an access token using the app's identity to call the Microsoft Graph API and display a [list of users](/en-us/graph/api/user-list) in the directory. The code sample demonstrates how an unattended job or Windows service can run with an application identity, instead of a user's identity.

This quickstart uses the [Microsoft Authentication Library for Node.js (MSAL Node)](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) with the [client credentials grant](v2-oauth2-client-creds-grant-flow).

## Prerequisites

- [Node.js](https://nodejs.org/en/download/)
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor

### Download and configure the sample app

#### Step 1: Configure the application in Azure portal

For the code sample for this quickstart to work, you need to create a client secret, and add Graph API's **User.Read.All** application permission.

![Already configured](media/quickstart-v2-netcore-daemon/green-check.png) Your application is configured with these attributes.

#### Step 2: Download the Node.js sample project

[Download the code sample](https://github.com/azure-samples/ms-identity-javascript-nodejs-console/archive/main.zip)

Note

`Enter_the_Supported_Account_Info_Here`

#### Step 3: Admin consent

If you try to run the application at this point, you'll receive *HTTP 403 - Forbidden* error: `Insufficient privileges to complete the operation`. This error happens because any *app-only permission* requires **admin consent**: an Administrator of your directory must give consent to your application. Select one of the options below depending on your role:

##### Tenant administrator

If you are an Administrator, go to **API Permissions** page select **Grant admin consent for &gt; Enter\_the\_Tenant\_Name\_Here**

> 
> Go to the API Permissions page

##### Standard user

If you're a standard user of your tenant, then you need to ask at least a Cloud Application Administrator to grant **admin consent** for your application. To do this, give the following URL to your administrator:

```url
https://login.microsoftonline.com/Enter_the_Tenant_Id_Here/adminconsent?client_id=Enter_the_Application_Id_Here
```

#### Step 4: Run the application

Locate the sample's root folder (where `package.json` resides) in a command prompt or console. You'll need to install the dependencies of this sample once:

```console
npm install
```

Then, run the application via command prompt or console:

```console
node . --op getUsers
```

You should see on the console output some JSON fragment representing a list of users in your Microsoft Entra directory.

## About the code

Below, some of the important aspects of the sample application are discussed.

### MSAL Node

[MSAL Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) is the library used to sign in users and request tokens used to access an API protected by Microsoft identity platform. As described, this quickstart requests tokens by application permissions (using the application's own identity) instead of delegated permissions. The authentication flow used in this case is known as [OAuth 2.0 client credentials flow](v2-oauth2-client-creds-grant-flow). For more information on how to use MSAL Node with daemon apps, see [Scenario: Daemon application](scenario-daemon-app-configuration).

You can install MSAL Node by running the following npm command.

```console
npm install @azure/msal-node --save
```

### MSAL initialization

You can add the reference for MSAL by adding the following code:

```javascript
const msal = require('@azure/msal-node');
```

Then, initialize MSAL using the following code:

```javascript
const msalConfig = {
    auth: {
        clientId: "Enter_the_Application_Id_Here",
        authority: "https://login.microsoftonline.com/Enter_the_Tenant_Id_Here",
        clientSecret: "Enter_the_Client_Secret_Here",
   }
};
const cca = new msal.ConfidentialClientApplication(msalConfig);
```

> 
> 
> | Where: | Description |
> | --- | --- |
> | `clientId` | Is the **Application (client) ID** for the application registered in the Azure portal. You can find this value in the app's **Overview** page in the Azure portal. |
> | `authority` | The STS endpoint for user to authenticate. Usually `https://login.microsoftonline.com/{tenant}` for public cloud, where {tenant} is the name of your tenant or your tenant Id. |
> | `clientSecret` | Is the client secret created for the application in Azure portal. |
> 

For more information, please see the [reference documentation for `ConfidentialClientApplication`](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md)

### Requesting tokens

To request a token using app's identity, use `acquireTokenByClientCredential` method:

```javascript
const tokenRequest = {
    scopes: [ 'https://graph.microsoft.com/.default' ],
};

const tokenResponse = await cca.acquireTokenByClientCredential(tokenRequest);
```

> 
> 
> | Where: | Description |
> | --- | --- |
> | `tokenRequest` | Contains the scopes requested. For confidential clients, this should use the format similar to `{Application ID URI}/.default` to indicate that the scopes being requested are the ones statically defined in the app object set in the Azure portal (for Microsoft Graph, `{Application ID URI}` points to `https://graph.microsoft.com`). For custom web APIs, `{Application ID URI}` is defined under **Expose an API** section in Azure portal's Application Registration. |
> | `tokenResponse` | The response contains an access token for the scopes requested. |
> 

## Help and support

If you need help, want to report an issue, or want to learn about your support options, see [Help and support for developers](developer-support-help-options).