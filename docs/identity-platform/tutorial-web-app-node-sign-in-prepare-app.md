---
layout: Conceptual
title: Sign in users in a Node.js/Express web app by using Microsoft identity platform - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-web-app-node-sign-in-prepare-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Set up node web app project that signs in users into customer facing app by in an external tenant or employees in a workforce tenant
manager: dougeby
ms.topic: tutorial
ms.date: 2025-02-25T00:00:00.0000000Z
locale: en-us
document_id: 9e68af09-d9ca-b2f2-46e6-962881805518
document_version_independent_id: 9e68af09-d9ca-b2f2-46e6-962881805518
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-web-app-node-sign-in-prepare-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-web-app-node-sign-in-prepare-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-web-app-node-sign-in-prepare-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/2624a017-7337-44fa-9494-a407bb0e59fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/a438284e-c3c3-4c36-ab0b-aa7c244b912c
platformId: b47fc234-e269-0cb8-31d0-eaf5965087cd
---

# Sign in users in a Node.js/Express web app by using Microsoft identity platform - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to build a Node/Express.js web app that signs in users into customer facing app in an external tenant or employees in a workforce tenant. The tutorial also demonstrates how to acquire an access token for calling Microsoft Graph API.

This tutorial is part 1 of a 3-part series.

In this tutorial you'll;

- Set up a Node.js project
- Install dependencies
- Add app views and UI components

## Prerequisites

# [Workforce tenant](#tab/workforce-tenant)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Web** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `http://localhost:3000/auth/redirect`
    - **Front-channel logout URL**: `https://localhost:5001/signout-callback-oidc`
- Add a client secret to your app registration. **Do not** use client secrets in production apps. Use certificates or federated credentials instead. For more information, see [add credentials to your application](how-to-add-credentials?tabs=client-secret).

# [External tenant](#tab/external-tenant)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Web** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `http://localhost:3000/auth/redirect`
    - **Front-channel logout URL**: `https://localhost:5001/signout-callback-oidc`
- Add a client secret to your app registration. **Do not** use client secrets in production apps. Use certificates or federated credentials instead. For more information, see [add credentials to your application](how-to-add-credentials?tabs=client-secret).
- Associate your app with a user flow in the Microsoft Entra admin center. This user flow can be used across multiple applications. For more information, see [Create self-service sign-up user flows for apps in external tenants](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers) and [Add your application to the user flow](../external-id/customers/how-to-user-flow-add-application).

---

- [Node.js](https://nodejs.org).
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor.

## Create the Node.js project

1. In a location of choice in your computer, create a folder to host your node application, such as *ciam-sign-in-node-express-web-app*.
2. In your terminal, change directory into your Node web app folder, such as `cd ciam-sign-in-node-express-web-app`, then run the following command to create a new Node.js project:

    ```powershell
    npm init -y
    ```

    The `init -y` command creates a default *package.json* file for your Node.js project.
3. Create additional folders and files to achieve the following project structure:

    ```text
        ciam-sign-in-node-express-web-app/
        ├── server.js
        └── app.js
        └── authConfig.js
        └── package.json
        └── .env
        └── auth/
            └── AuthProvider.js
        └── controller/
            └── authController.js
        └── routes/
            └── auth.js
            └── index.js
            └── users.js
        └── views/
            └── layouts.hbs
            └── error.hbs
            └── id.hbs
            └── index.hbs   
        └── public/stylesheets/
            └── style.css
    ```

## Install app dependencies

To install required identity and Node.js related npm packages, run the following command in your terminal

```powershell
npm install express dotenv hbs express-session axios cookie-parser http-errors morgan @azure/msal-node   
```

## Build app UI components

1. In your code editor, open *views/index.hbs* file, then add the following code:

    ```html
        <h1>{{title}}</h1>
        {{#if isAuthenticated }}
        <p>Hi {{username}}!</p>
        <a href="/users/id">View ID token claims</a>
        <br>
        <a href="/auth/signout">Sign out</a>
        {{else}}
        <p>Welcome to {{title}}</p>
        <a href="/auth/signin">Sign in</a>
        {{/if}}
    ```

    In this view, if the user is authenticated, we show their username and links to visit `/auth/signout` and `/users/id` endpoints, otherwise, user needs to visit the `/auth/signin` endpoint to sign in. We define the express routes for these endpoints later in this article.
2. In your code editor, open *views/id.hbs* file, then add the following code:

    ```html
        <h1>Azure AD for customers</h1>
        <h3>ID Token</h3>
        <table>
            <tbody>
                {{#each idTokenClaims}}
                <tr>
                    <td>{{@key}}</td>
                    <td>{{this}}</td>
                </tr>
                {{/each}}
            </tbody>
        </table>
        <a href="/">Go back</a>
    ```

    We use this view to display ID token claims that Microsoft Entra External ID returns to this app after a user successfully signs in.
3. In your code editor, open *views/error.hbs* file, then add the following code:

    ```html
        <h1>{{message}}</h1>
        <h2>{{error.status}}</h2>
        <pre>{{error.stack}}</pre>
    ```

    We use this view to display any errors that occur when the app runs.
4. In your code editor, open *views/layout.hbs* file, then add the following code:

    ```html
        <!DOCTYPE html>
        <html>        
            <head>
                <title>{{title}}</title>
                <link rel='stylesheet' href='/stylesheets/style.css' />
            </head>            
            <body>
                {{{body}}}
            </body>        
        </html>
    ```

    The `layout.hbs` file is in the layout file. It contains the HTML code that we require throughout the application view.
5. In your code editor, open *public/stylesheets/style.css*, file, then add the following code:

    ```css
        body {
          padding: 50px;
          font: 14px "Lucida Grande", Helvetica, Arial, sans-serif;
        }
    
        a {
          color: #00B7FF;
        }
    ```