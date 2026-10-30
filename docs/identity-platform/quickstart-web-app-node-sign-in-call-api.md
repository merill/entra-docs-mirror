---
layout: Conceptual
title: Quickstart - Call a web API from a sample Nodejs web app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-web-app-node-sign-in-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure a Node.js web app code sample to sign in users and call an API in an external tenant.
manager: dougeby
ms.subservice: external
ms.topic: quickstart
ms.date: 2025-03-10T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: e2dbbd2f-437a-2baa-0e00-3d2054d0c8d8
document_version_independent_id: e2dbbd2f-437a-2baa-0e00-3d2054d0c8d8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-web-app-node-sign-in-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-web-app-node-sign-in-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-web-app-node-sign-in-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 30cbf0d7-9724-e0a3-12c9-af520a4e10a6
---

# Quickstart - Call a web API from a sample Nodejs web app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this Quickstart, you learn how to sign in users and call a web API from a Node.js web application in your external tenant. The sample application calls a .NET API. The sample web application uses [Microsoft Authentication Library (MSAL)](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) for Node to handle authentication.

## Prerequisites

- Complete the steps and prerequisites in [Quickstart: Sign in users in a sample web app](quickstart-web-app-sign-in?pivots=external&amp;tabs=node-external) article. This article shows you how to sign in users by using a sample Node.js web app.
- An external tenant. To create one, choose from the following methods:
    - (Recommended) Use the [Microsoft Entra External ID extension](https://aka.ms/ciamvscode/samples/marketplace) to set up an external tenant directly in Visual Studio Code.
    - [Create a new external tenant](../external-id/customers/how-to-create-external-tenant-portal) in the Microsoft Entra admin center.
- Register a new app for your web API in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor.
- [Node.js](https://nodejs.org).
- [.NET 7.0](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/install) or later.

## Configure API scopes and roles

By registering the web API, you must configure API scopes to define the permissions that a client application can request to access the web API. Additionally, you need to set up app roles to specify the roles available for users or applications, and grant the necessary API permissions to the web app to enable it to call the web API.

### Configure API scopes

An API needs to publish a minimum of one scope, also called [Delegated Permission](permissions-consent-overview), for the client apps to obtain an access token for a user successfully. To publish a scope, follow these steps:

1. From the **App registrations** page, select the API application that you created (*ciam-ToDoList-api*) to open its **Overview** page.
2. Under **Manage**, select **Expose an API**.
3. At the top of the page, next to **Application ID URI**, select the **Add** link to generate a URI that is unique for this app.
4. Accept the proposed Application ID URI such as `api://{clientId}`, and select **Save**. When your web application requests an access token for the web API, it adds the URI as the prefix for each scope that you define for the API.
5. Under **Scopes defined by this API**, select **Add a scope**.
6. Enter the following values that define a read access to the API, then select **Add scope** to save your changes:

    | Property | Value |
    | --- | --- |
    | Scope name | *ToDoList.Read* |
    | Who can consent | **Admins only** |
    | Admin consent display name | *Read users ToDo list using the 'TodoListApi'* |
    | Admin consent description | *Allow the app to read the user's ToDo list using the 'TodoListApi'*. |
    | State | **Enabled** |
7. Select **Add a scope** again, and enter the following values that define a read and write access scope to the API. Select **Add scope** to save your changes:

    | Property | Value |
    | --- | --- |
    | Scope name | *ToDoList.ReadWrite* |
    | Who can consent | **Admins only** |
    | Admin consent display name | *Read and write users ToDo list using the 'ToDoListApi'* |
    | Admin consent description | *Allow the app to read and write the user's ToDo list using the 'ToDoListApi'* |
    | State | **Enabled** |

Learn more about [the principle of least privilege when publishing permissions](/en-us/security/zero-trust/develop/protected-api-example) for a web API.

### Configure app roles

An API needs to publish a minimum of one app role for applications, also called [Application permission](permissions-consent-overview), for the client apps to obtain an access token as themselves. Application permissions are the type of permissions that APIs should publish when they want to enable client applications to successfully authenticate as themselves and not need to sign-in users. To publish an application permission, follow these steps:

1. From the **App registrations** page, select the application that you created (such as *ciam-ToDoList-api*) to open its **Overview** page.
2. Under **Manage**, select **App roles**.
3. Select **Create app role**, then enter the following values, then select **Apply** to save your changes:

    | Property | Value |
    | --- | --- |
    | Display name | *ToDoList.Read.All* |
    | Allowed member types | **Applications** |
    | Value | *ToDoList.Read.All* |
    | Description | *Allow the app to read every user's ToDo list using the 'TodoListApi'* |
    | Do you want to enable this app role? | Keep it checked |
4. Select **Create app role** again, then enter the following values for the second app role, then select **Apply** to save your changes:

    | Property | Value |
    | --- | --- |
    | Display name | *ToDoList.ReadWrite.All* |
    | Allowed member types | **Applications** |
    | Value | *ToDoList.ReadWrite.All* |
    | Description | *Allow the app to read and write every user's ToDo list using the 'ToDoListApi'* |
    | Do you want to enable this app role? | Keep it checked |

### Configure optional claims

You can add the **idtyp** optional claim to help the web API to determine whether a token is an **app** token or an **app + user** token. Although you can use a combination of **scp** and **roles** claims for the same purpose, using the **idtyp** claim is the easiest way to tell an app token and an app + user token apart. For example, the value of this claim is *app* when the token is an app-only token.

Use the steps in [Configure optional claims](optional-claims?tabs=appui) article to add *idtyp* claim to the access token:

- For the **Token type** select **Access**.
- From the optional claims list, select **idtyp**.

### Grant API permissions to the web app

To grant your client app (*ciam-client-app*) API permissions, follow these steps:

1. From the **App registrations** page, select the application that you created (such as *ciam-client-app*) to open its **Overview** page.
2. Under **Manage**, select **API permissions**.
3. Under **Configured permissions**, select **Add a permission**.
4. Select the **APIs my organization uses** tab.
5. In the list of APIs, select the API such as *ciam-ToDoList-api*.
6. Select **Delegated permissions** option.
7. From the permissions list, select **ToDoList.Read, ToDoList.ReadWrite** (use the search box if necessary).
8. Select the **Add permissions** button. At this point, you've assigned the permissions correctly. However, since the tenant is a customer's tenant, the consumer users themselves can't consent to these permissions. To address this problem, you as the admin must consent to these permissions on behalf of all the users in the tenant:

    1. Select **Grant admin consent for &lt;your tenant name&gt;**, then select **Yes**.
    2. Select **Refresh**, then verify that **Granted for &lt;your tenant name&gt;** appears under **Status** for both scopes.
9. From the **Configured permissions** list, select the **ToDoList.Read** and **ToDoList.ReadWrite** permissions, one at a time, and then copy the permission's full URI for later use. The full permission URI looks something similar to `api://{clientId}/{ToDoList.Read}` or `api://{clientId}/{ToDoList.ReadWrite}`.

## Clone or download sample web application and web API

To obtain the sample application, you can either clone it from GitHub or download it as a .zip file.

- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial.git
    ```
- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

## Install project dependencies

1. Open a console window, and change to the directory that contains the Node.js/Express sample app:

    ```console
    cd 2-Authorization\4-call-api-express\App
    ```
2. Run the following commands to install web app dependencies:

    ```console
    npm install && npm update
    ```

## Configure the sample web app and API

To use your app registration in the client web app sample:

1. In your code editor, open `App\authConfig.js` file.
2. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the client app you registered earlier. The client app is one that you registered in the prerequisites.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
    - `Enter_the_Client_Secret_Here` and replace it with the app secret value you copied earlier.
    - `Enter_the_Web_Api_Application_Id_Here` and replace it with the Application (client) ID of the web API you copied earlier as part of the prerequisites.

To use your app registration in the web API sample:

1. In your code editor, open `API\ToDoListAPI\appsettings.json` file.
2. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the web API you copied. The web API app is one that you registered earlier sa part of the prerequisites.
    - `Enter_the_Tenant_Id_Here` and replace it with the Directory (tenant) ID you copied earlier.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).

## Run and test sample web app and API

1. Open a console window, then run the web API by using the following commands:

    ```console
    cd 2-Authorization\4-call-api-express\API\ToDoListAPI
    dotnet run
    ```
2. Run the web app client by using the following commands:

    ```console
    cd 2-Authorization\4-call-api-express\App
    npm install
    npm start
    ```
3. Open your browser, then go to http://localhost:3000.
4. Select the **Sign In** button. You're prompted to sign in.

    ![Screenshot of sign in into a node web app.](media/how-to-web-app-node-sample-sign-in-call-api/web-app-node-sign-in.png)
5. On the sign-in page, type your **Email address**, select **Next**, type your **Password**, then select **Sign in**. If you don't have an account, select **No account? Create one** link, which starts the sign-up flow.
6. If you choose the sign-up option, after filling in your email, one-time passcode, new password and more account details, you complete the whole sign-up flow. You see a page similar to the following screenshot. You see a similar page if you choose the sign-in option.

    ![Screenshot of sign in into a node web app and call an API.](media/how-to-web-app-node-sample-sign-in-call-api/sign-in-call-api-view-to-do.png)

### Call API

1. To call the API, select the **View your todolist** link. You see a page similar to the following screenshot.

    ![Screenshot of manipulate API to do list.](media/how-to-web-app-node-sample-sign-in-call-api/sign-in-call-api-manipulate-to-do.png)
2. Manipulate the to-do list by creating and removing items.

### How it works

You trigger an API call each time you view, add, or remove a task. Each time you trigger an API call, the client web app acquires an access token with the required permissions (scopes) to call an API endpoint. For example, to read a task, the client web app must acquire an access token with `ToDoList.Read` permission/scope.

The web API endpoint needs to check if the permissions or scopes in the access token, provided by the client app, are valid. If the access token is valid, the endpoint responds to the HTTP request, otherwise, it responds with a `401 Unauthorized` HTTP error.