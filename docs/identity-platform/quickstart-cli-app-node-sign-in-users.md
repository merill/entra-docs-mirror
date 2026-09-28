---
layout: Conceptual
title: Quickstart - Sign in users in a sample Node.js CLI app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-cli-app-node-sign-in-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to authenticate users in a sample Node.js Command Line Interface (CLI) application in your external tenant
manager: dougeby
ms.topic: quickstart
ms.date: 2024-11-20T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 15aec209-d83f-4144-ff94-2bb659b84a62
document_version_independent_id: 15aec209-d83f-4144-ff94-2bb659b84a62
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-cli-app-node-sign-in-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-cli-app-node-sign-in-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-cli-app-node-sign-in-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 4cfb78a2-65ff-e780-0f20-23fc389d5503
---

# Quickstart - Sign in users in a sample Node.js CLI app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this quickstart, you use a sample Node Command Line Interface (CLI) application to sign in users in your external tenant. The sample application uses the [Microsoft Authentication Library for Node](/en-us/javascript/api/%40azure/msal-node/) (MSAL Node) to handle authentication.

## Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor.
- [Node.js](https://nodejs.org).
- An external tenant. To create one, choose from the following methods:
    - (Recommended) Use the [Microsoft Entra External ID extension](https://aka.ms/ciamvscode/samples/marketplace) to set up an external tenant directly in Visual Studio Code.
    - [Create a new external tenant](../external-id/customers/how-to-create-external-tenant-portal) in the Microsoft Entra admin center.
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Mobile and desktop applications** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Custom redirect URIs**: `http://localhost`
- Associate your app with a user flow in the Microsoft Entra admin center. This user flow can be used across multiple applications. For more information, see [Create self-service sign-up user flows for apps in external tenants](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers) and [Add your application to the user flow](../external-id/customers/how-to-user-flow-add-application).

## Enable public client flows

To identify your app as a public client, follow these steps:

1. Under **Manage**, select **Authentication**.
2. Under **Advanced settings**, for **Allow public client flows**, select **Yes**.
3. Select **Save** to save your changes.

## Clone or download the sample Node.js CLI application

To obtain the sample application, you can either clone it from GitHub or download it as a .zip file.

- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial.git
    ```
- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

## Configure the sample Node.js CLI application

To configure the client application (Node.js CLI app) to use your Microsoft Entra app registration details, open the project in your IDE and follow these steps:

1. Open the *App\authConfig.js* file.
2. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace the existing value with the application ID (clientId) of `node-cli-app` application copied from the Microsoft Entra admin center.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details)

## Run and test the sample Node.js CLI application

You can now test the sample Node.js CLI application.

1. In your terminal, run the following command:

    ```console
    cd 1-Authentication\6-sign-in-node-cli-app\App
    npm start
    ```
2. The browser opens up automatically and you should see a page similar to the following:

    ![Screenshot of the sign in page in a node CLI application.](media/tutorial-node-cli-app-sign-in/node-cli-app-sign-in-page.png)
3. On the sign-in page, type your **Email address**. If you don't have an account, select **No account? Create one**, which starts the sign-up flow.
4. If you choose the sign-up option, after filling in your email, one-time passcode, new password, and more account details, you complete the whole sign-up flow. After completing the sign up flow and signing in, you see a page similar to the following screenshot:

    ![Screenshot showing a signed-in user in a node CLI application.](media/tutorial-node-cli-app-sign-in/node-cli-app-signed-in-user.png)
5. Go back to the terminal and see your authentication information including the ID token claims.