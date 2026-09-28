---
layout: Conceptual
title: 'Quickstart: Add authentication to a Node.js web app with MSAL Node - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/web-app-quickstart-portal-node-js
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you learn how to implement authentication with a Node.js web app and the Microsoft Authentication Library (MSAL) for Node.js.
ROBOTS: NOINDEX
manager: dougeby
ms.custom: 
ms.date: 2022-08-16T00:00:00.0000000Z
ms.topic: quickstart
locale: en-us
document_id: bc1cd9b8-c11e-f472-94e8-e3678b1a93fe
document_version_independent_id: c4af624d-f78d-76cc-a8da-0e32d1d24019
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/web-app-quickstart-portal-node-js.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/web-app-quickstart-portal-node-js
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/web-app-quickstart-portal-node-js.md
platformId: 5c919db7-fdd5-3e31-ca32-95338799910d
---

# Quickstart: Add authentication to a Node.js web app with MSAL Node - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Add authentication to a Node.js web app with MSAL Node](quickstart-web-app-nodejs-sign-in)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

# Quickstart: Sign in users and get an access token in a Node.js web app using the authorization code flow

In this quickstart, you download and run a code sample that demonstrates how a Node.js web app can sign in users by using the authorization code flow. The code sample also demonstrates how to get an access token to call Microsoft Graph API.

See How the sample works for an illustration.

This quickstart uses the Microsoft Authentication Library for Node.js (MSAL Node) with the authorization code flow.

## Prerequisites

- An Azure subscription. [Create an Azure subscription for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Node.js](https://nodejs.org/en/download/)
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor

#### Step 1: Configure the application in the Microsoft Entra admin center

For the code sample for this quickstart to work, you need to create a client secret and add the following reply URL: `http:/> /localhost:3000/redirect`.

![Already configured](media/quickstart-v2-windows-desktop/green-check.png) Your application is configured with these &gt; attributes.

#### Step 2: Download the project

Run the project with a web server by using Node.js.

#### Step 3: Your app is configured and ready to run

Run the project by using Node.js.

1. To start the server, run the following commands from within the project directory:

    ```console
    npm install
    npm start
    ```
2. Go to `http://localhost:3000/`.
3. Select **Sign In** to start the sign-in process.

    The first time you sign in, you're prompted to provide your consent to allow the application to access your profile and sign you in. After you're signed in successfully, you will see a log message in the command line.

## More information

### How the sample works

The sample hosts a web server on localhost, port 3000. When a web browser accesses this site, the sample immediately redirects the user to a Microsoft authentication page. Because of this, the sample does not contain any HTML or display elements. Authentication success displays the message "OK".

### MSAL Node

The MSAL Node library signs in users and requests the tokens that are used to access an API that's protected by Microsoft identity platform. You can download the latest version by using the Node.js Package Manager (npm):

```console
npm install @azure/msal-node
```