---
layout: Conceptual
title: 'Quickstart: Sign in users in JavaScript single-page apps (SPA) with auth code - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/spa-quickstart-portal-javascript-auth-code
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, learn how a JavaScript single-page application (SPA) can sign in users of personal accounts, work accounts, and school accounts by using the authorization code flow.
ROBOTS: NOINDEX
manager: dougeby
ms.custom: 
ms.date: 2022-08-16T00:00:00.0000000Z
ms.topic: quickstart
locale: en-us
document_id: 9dcd699c-5b5a-6006-e6e2-199cd6e90b35
document_version_independent_id: 1a77e28f-0296-9b3d-fc92-3d19c0b594ef
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/spa-quickstart-portal-javascript-auth-code.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/spa-quickstart-portal-javascript-auth-code
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/spa-quickstart-portal-javascript-auth-code.md
platformId: 7332f13e-0d8e-14c5-a179-199bc9f618aa
---

# Quickstart: Sign in users in JavaScript single-page apps (SPA) with auth code - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Sign in users in single-page apps (SPA) via the authorization code flow with Proof Key for Code Exchange (PKCE) using JavaScript](quickstart-single-page-app-sign-in)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

# Quickstart: Sign in users and get an access token in a JavaScript SPA using the auth code flow with PKCE

In this quickstart, you download and run a code sample that demonstrates how a JavaScript single-page application (SPA) can sign in users and call Microsoft Graph using the authorization code flow with Proof Key for Code Exchange (PKCE). The code sample demonstrates how to get an access token to call the Microsoft Graph API or any web API.

See How the sample works for an illustration.

## Prerequisites

- Azure subscription - [Create an Azure subscription for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)
- [Node.js](https://nodejs.org/en/download/)
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor

### Step 1: Configure your application in the Azure portal

For the code sample in this quickstart to work, add a **Redirect URI** of `http://localhost:3000/`.

![Already configured](media/quickstart-v2-javascript/green-check.png) Your application is configured with these attributes.

### Step 2: Download the project

Run the project with a web server by using Node.js

Note

`Enter_the_Supported_Account_Info_Here`

#### Step 3: Your app is configured and ready to run

We have configured your project with values of your app's properties.

Run the project with a web server by using Node.js.

1. To start the server, run the following commands from within the project directory:

    ```console
    npm install
    npm start
    ```
2. Go to `http://localhost:3000/`.
3. Select **Sign In** to start the sign-in process and then call the Microsoft Graph API.

    The first time you sign in, you're prompted to provide your consent to allow the application to access your profile and sign you in. After you're signed in successfully, your user profile information is displayed on the page.

## More information

### How the sample works

![Diagram showing the authorization code flow for a single-page application.](media/quickstart-v2-javascript-auth-code/diagram-01-auth-code-flow.png)

### MSAL.js

The MSAL.js library signs in users and requests the tokens that are used to access an API that's protected by Microsoft &gt; identity platform. The sample's *index.html* file contains a reference to the library:

```html
<script type="text/javascript" src="https://alcdn.msauth.net/browser/2.0.0-beta.0/js/msal-browser.js" integrity=
"sha384-r7Qxfs6PYHyfoBR6zG62DGzptfLBxnREThAlcJyEfzJ4dq5rqExc1Xj3TPFE/9TH" crossorigin="anonymous"></script>
```

If you have Node.js installed, you can download the latest version by using the Node.js Package Manager (npm):

```console
npm install @azure/msal-browser
```