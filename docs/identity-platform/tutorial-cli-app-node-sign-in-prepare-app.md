---
layout: Conceptual
title: 'Tutorial: Create a Node.js CLI app for authentication - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-cli-app-node-sign-in-prepare-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a Node.js CLI app that signs in users in an external tenant
manager: dougeby
ms.topic: tutorial
ms.date: 2025-04-16T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 9de13761-ad00-1ad4-188f-d101f1efbb38
document_version_independent_id: 9de13761-ad00-1ad4-188f-d101f1efbb38
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-cli-app-node-sign-in-prepare-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-cli-app-node-sign-in-prepare-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-cli-app-node-sign-in-prepare-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 7fbad776-68df-1fc4-4747-5121698f5d1f
---

# Tutorial: Create a Node.js CLI app for authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial is part 1 of a series that demonstrates building a Node.js command line interface (CLI) app and preparing it for authentication using the Microsoft Entra admin center. The client application you build uses the [OAuth 2.0 Authorization Code Flow](v2-oauth2-auth-code-flow) with Proof Key for Code Exchange (PKCE) for secure user authentication.

In this tutorial, you:

- Create a new Node.js application project
- Install app dependencies
- Create the MSAL configuration object

## Prerequisites

- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Mobile and desktop applications** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `http://localhost`
- Associate your app with a user flow in the Microsoft Entra admin center. This user flow can be used across multiple applications. For more information, see [Create self-service sign-up user flows for apps in external tenants](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers) and [Add your application to the user flow](../external-id/customers/how-to-user-flow-add-application).
- Although any integrated development environment (IDE) that supports React applications can be used, this tutorial uses [Visual Studio Code](https://visualstudio.microsoft.com/downloads/).
- [Node.js](https://nodejs.org).

## Enable public client flow

To identify your app as a public client, follow these steps:

1. Under **Manage**, select **Authentication**.
2. Under **Advanced settings**, for **Allow public client flows**, select **Yes**.
3. Select **Save** to save your changes.

## Create a new Node.js application project

Here, you build a new Node.js CLI app from scratch. If you prefer using a completed code sample for learning, download the [sample Node.js CLI application](https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial/archive/refs/heads/main.zip) from GitHub.

To build the Node.js CLI application from scratch, follow these steps:

1. Create a folder to host your application and give it a name, such as *ciam-sign-in-node-cli-app*.
2. In your terminal, navigate to your project directory, such as `cd ciam-sign-in-node-cli-app` and initialize your project using `npm init`. This creates a *package.json* file in your project folder, which contains references to all npm packages.
3. In your project root directory, create two files, then name them *authConfig.js* and *index.js*. The *authConfig.js* file contains the authentication configuration parameters while *index.js* holds the app's authentication logic.

After you create the files, you should achieve the following project structure:

```
ciam-sign-in-node-cli-app/
   ├── authConfig.js
   └── index.js
   └── package.json
```

## Install app dependencies

The application you build uses MSAL Node to sign in users. To install the MSAL Node package as a dependency in your project, open the terminal in your project directory and run the following command.

```powershell
npm install @azure/msal-node   
```

You'll also install the `open` package that allows your Node.js app to open URLs in the web browser.

```powershell
npm install open
```

## Create the MSAL configuration object

In your code editor, open *authConfig.js*, which holds the MSAL object configuration parameters, and add the following code:

```javascript

const { LogLevel } = require('@azure/msal-node');

const msalConfig = {
    auth: {
        clientId: 'Enter_the_Application_Id_Here', 
        authority: `https://Enter_the_Tenant_Subdomain_Here.ciamlogin.com/`, 
    },
    system: {
        loggerOptions: {
            loggerCallback(loglevel, message, containsPii) {
                // console.log(message);
            },
            piiLoggingEnabled: false,
            logLevel: LogLevel.Verbose,
        },
    },
};
```

The `msalConfig` object contains a set of configuration options that can be used to customize the behavior of your authentication flows. This configuration object is passed into the instance of our public client application upon creation. In your *authConfig.js* file, find the placeholders:

- `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the app you registered earlier.
- `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For instance, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant domain name, [learn how to read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).

In the configuration object, you also add `LoggerOptions`, which contains two options:

- `loggerCallback` - A callback function that handles the logging of MSAL statements
- `piiLoggingEnabled` - A config option that when set to true, enables logging of personally identifiable information (PII). For our app, we set this option to false.

After creating the `msalConfig` object, add a `loginRequest` object that contains the scopes our application requires. Scopes define the level of access that the application has to user resources. Although the scopes array in the example snippet has no values, MSAL by default adds the OIDC scopes (openid, profile, email) to any login request. Users are asked to consent to these scopes during sign in. To create the `loginRequest` object, add the following code in *authConfig.js*.

```javascript
const loginRequest = {
    scopes: [],
};
```

In *authcConfig.js*, export the `msalConfig` and `loginRequest` objects to make them accessible when required by adding the following code:

```javascript
module.exports = {
    msalConfig: msalConfig,
    loginRequest: loginRequest,
};
```

Use a custom domain to fully brand the authentication URL. From a user perspective, users remain on your domain during the authentication process, rather than being redirected to *ciamlogin.com* domain name.

Use the following steps to use a custom domain:

1. Use the steps in [Enable custom URL domains for apps in external tenants](../external-id/customers/how-to-custom-url-domain) to enable custom URL domain for your external tenant.
2. In your *authConfig.js* file, locate then `auth` object, then:

    1. Update the value of the `authority` property to *https://Enter\_the\_Custom\_Domain\_Here/Enter\_the\_Tenant\_ID\_Here*. Replace `Enter_the_Custom_Domain_Here` with your custom URL domain and `Enter_the_Tenant_ID_Here` with your tenant ID. If you don't have your tenant ID, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
    2. Add `knownAuthorities` property with a value *[Enter\_the\_Custom\_Domain\_Here]*.

After you make the changes to your *authConfig.js* file, if your custom URL domain is *login.contoso.com*, and your tenant ID is *aaaabbbb-0000-cccc-1111-dddd2222eeee*, then your file should look similar to the following snippet:

```JavaScript
//...
const msalConfig = {
    auth: {
        authority: process.env.AUTHORITY || 'https://login.contoso.com/aaaabbbb-0000-cccc-1111-dddd2222eeee', 
        knownAuthorities: ["login.contoso.com"],
        //Other properties
    },
    //...
};
```