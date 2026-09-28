---
layout: Conceptual
title: 'Quickstart: Sign in users in JavaScript Angular single-page apps (SPA) with auth code and call Microsoft Graph - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-v2-javascript-auth-code-angular
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, learn how a JavaScript Angular single-page application (SPA) can sign in users of personal accounts, work accounts, and school accounts by using the authorization code flow and call Microsoft Graph.
ROBOTS: NOINDEX
manager: pmwongera
ms.custom: 
ms.date: 2024-02-27T00:00:00.0000000Z
ms.reviewer: 
ms.topic: quickstart
locale: en-us
document_id: f8b05193-2138-2983-2901-e6768ffb0d06
document_version_independent_id: da8e4407-bdfe-ea36-abfd-af94a1b6eaea
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-v2-javascript-auth-code-angular.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-v2-javascript-auth-code-angular
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-v2-javascript-auth-code-angular.md
platformId: 7453b9bd-ea66-ff6f-e670-10e4addde28f
---

# Quickstart: Sign in users in JavaScript Angular single-page apps (SPA) with auth code and call Microsoft Graph - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Sign in users in single-page apps (SPA) via the authorization code flow with Proof Key for Code Exchange (PKCE) using Angular](quickstart-single-page-app-angular-sign-in)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

In this quickstart, you download and run a code sample that demonstrates how a JavaScript Angular single-page application (SPA) can sign in users and call Microsoft Graph using the authorization code flow. The code sample demonstrates how to get an access token to call the Microsoft Graph API or any web API.

See How the sample works for an illustration.

This quickstart uses MSAL Angular v2 with the authorization code flow.

## Prerequisites

- Azure subscription - [Create an Azure subscription for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)
- [Node.js](https://nodejs.org/en/download/)
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor

#### Step 1: Configure your application in the Azure portal

For the code sample in this quickstart to work, add a **Redirect URI** of `http://localhost:4200/`.

![Already configured](media/quickstart-v2-javascript/green-check.png) Your application is configured with these &gt; attributes.

#### Step 2: Download the project

Run the project with a web server by using Node.js

Note

`Enter_the_Supported_Account_Info_Here`

#### Step 3: Your app is configured and ready to run

We have configured your project with values of your app's properties.

#### Step 4: Run the project

Run the project with a web server by using Node.js:

1. To start the server, run the following commands from within the project directory:

    ```console
    npm install
    npm start
    ```
2. Browse to `http://localhost:4200/`.
3. Select **Login** to start the sign-in process and then call the Microsoft Graph API.

    The first time you sign in, you're prompted to provide your consent to allow the application to access your profile and sign you in. After you're signed in successfully, click the **Profile** button to display your user information on the page.

## More information

### How the sample works

![Diagram showing the authorization code flow for a single-page application.](media/quickstart-v2-javascript-auth-code/diagram-01-auth-code-flow.png)

### msal.js

The MSAL.js library signs in users and requests the tokens that are used to access an API that's protected by the Microsoft identity platform.

If you have Node.js installed, you can download the latest version by using the Node.js Package Manager (npm):

```console
npm install @azure/msal-browser @azure/msal-angular@2
```