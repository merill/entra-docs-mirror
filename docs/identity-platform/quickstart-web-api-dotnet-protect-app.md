---
layout: Conceptual
title: 'Quickstart: Call a web API that is protected by the Microsoft identity platform - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-web-api-dotnet-protect-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you download and modify a code sample that demonstrates how to protect an ASP.NET web API by using the Microsoft identity platform for authorization.
manager: pmwongera
ms.custom: 
ms.date: 2025-04-03T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: quickstart
locale: en-us
document_id: 6ec021c2-ee04-6c54-f7b9-399dd0344b9a
document_version_independent_id: 6ec021c2-ee04-6c54-f7b9-399dd0344b9a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-web-api-dotnet-protect-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-web-api-dotnet-protect-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-web-api-dotnet-protect-app.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/43ab1a66-ffe1-45dd-a4cb-6580218ef802
- https://authoring-docs-microsoft.poolparty.biz/devrel/d452572f-6212-498f-9050-ca4a9e50a425
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bbc4fbf6-70c4-4d12-b47f-9360080c4977
- https://authoring-docs-microsoft.poolparty.biz/devrel/a12e40b7-59a2-4437-96e2-166ce622b864
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 68f1ad1c-927b-0b9f-fb55-c14716ad3964
---

# Quickstart: Call a web API that is protected by the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this quickstart, you use a sample web app to show you how to protect an ASP.NET web API by using the Microsoft identity platform. The sample uses the [Microsoft Authentication Library (MSAL)](msal-overview) to handle authentication and authorization.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com) and record its identifiers from the app **Overview** page. For more information, see [Register an application](quickstart-register-app).
    - **Name**: *NewWebAPI1*
    - **Supported account types**: *Accounts in this organizational directory only (Single tenant)*

# [ASP.NET](#tab/aspnet)
- Visual Studio 2022. Download [Visual Studio for free](https://www.visualstudio.com/downloads/).

# [ASP.NET Core](#tab/aspnet-core)
- [Visual Studio Code](https://code.visualstudio.com/download)

---

## Expose the API

Once the API is registered, you can configure its permission by defining the scopes that the API exposes to client applications. Client applications request permission to perform operations by passing an access token along with its requests to the protected web API. The web API then performs the requested operation only if the access token it receives contains the required scopes.

# [ASP.NET](#tab/aspnet)
1. Under **Manage**, select **Expose an API** &gt; **Add a scope**. Accept the proposed Application ID URI (`api://{clientId}`) by selecting **Save and continue**, and then enter the following information:

    1. For **Scope name**, enter `access_as_user`.
    2. For **Who can consent**, ensure that the **Admins and users** option is selected.
    3. In the **Admin consent display name** box, enter `Access TodoListService as a user`.
    4. In the **Admin consent description** box, enter `Accesses the TodoListService web API as a user`.
    5. In the **User consent display name** box, enter `Access TodoListService as a user`.
    6. In the **User consent description** box, enter `Accesses the TodoListService web API as a user`.
    7. For **State**, keep **Enabled**.
2. Select **Add scope**.

# [ASP.NET Core](#tab/aspnet-core)
### Add delegated permissions (scopes)

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

### Add application permissions (app roles)

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

[![Screenshot that shows the field values when adding the scope to an API.](media/web-api-tutorial-01-register-app/add-a-scope.png)](media/web-api-tutorial-01-register-app/add-a-scope.png#lightbox)

---

## Clone or download the sample application

To obtain the sample application, you can either clone it from GitHub or download it as a *.zip* file.

# [ASP.NET](#tab/aspnet)
```console
git clone https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git
```

- [Download it as a ZIP file](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip).

Tip

To avoid errors caused by path length limitations in Windows, we recommend extracting the archive or cloning the repository into a directory near the root of your drive.

# [ASP.NET Core](#tab/aspnet-core)
```console
git clone https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial.git
```

- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

---

## Configure the sample application

Configure the code sample to match the registered web API.

# [ASP.NET](#tab/aspnet)
1. Open the solution in Visual Studio, and then open the *appsettings.json* file under the root of the TodoListService project.
2. Replace the value of the `Enter_the_Application_Id_here` by the Client ID (Application ID) value from the application you registered in the **App registrations** portal both in the `ClientID` and the `Audience` properties.

### Add the new scope to the app.config file

To add the new scope to the TodoListClient *app.config* file, follow these steps:

1. In the TodoListClient project root folder, open the *app.config* file.
2. Paste the Application ID from the application that you registered for your TodoListService project in the `TodoListServiceScope` parameter, replacing the `{Enter the Application ID of your TodoListService from the app registration portal}` string.

Note

Make sure that the Application ID uses the following format: `api://{TodoListService-Application-ID}/access_as_user` (where `{TodoListService-Application-ID}` is the GUID representing the Application ID for your TodoListService app).

## Register the web app (TodoListClient)

Register your TodoListClient app in **App registrations** in the Microsoft Entra admin center, and then configure the code in the TodoListClient project. If the client and server are considered the same application, you can reuse the application registered in step 2. Use the same application if you want users to sign in with a personal Microsoft account.

### Register the app

To register the TodoListClient app, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **App registrations** and select **New registration**.
3. Select **New registration**.
4. When the **Register an application page** opens, enter your application's registration information:

    1. In the **Name** section, enter a meaningful application name that will be displayed to users of the app (for example, **NativeClient-DotNet-TodoListClient**).
    2. For **Supported account types**, select **Accounts in any organizational directory**.
    3. Select **Register** to create the application.

    Note

    In the TodoListClient project *app.config* file, the default value of `ida:Tenant` is set to `common`. The possible values are:

    - `common`: You can sign in by using a work or school account or a personal Microsoft account (because you selected **Accounts in any organizational directory** in a previous step).
    - `organizations`: You can sign in by using a work or school account.
    - `consumers`: You can sign in only by using a Microsoft personal account.
5. On the app **Overview** page, select **Authentication**, and then complete these steps to add a platform:

    1. Under **Platform configurations**, select the **Add a platform** button.
    2. For **Mobile and desktop applications**, select **Mobile and desktop applications**.
    3. For **Redirect URIs**, select the `https://login.microsoftonline.com/common/oauth2/nativeclient` check box.
    4. Select **Configure**.
6. Select **API permissions**, and then complete these steps to add permissions:

    1. Select the **Add a permission** button.
    2. Select the **My APIs** tab.
    3. In the list of APIs, select **AppModelv2-NativeClient-DotNet-TodoListService API** or the name you entered for the web API.
    4. Select the **access\_as\_user** permission check box if it's not already selected. Use the Search box if necessary.
    5. Select the **Add permissions** button.

### Configure your project

Configure your TodoListClient project by adding the Application ID to the *app.config* file.

1. In the **App registrations** portal, on the **Overview** page, copy the value of the **Application (client) ID**.
2. From the TodoListClient project root folder, open the *app.config* file, and then paste the Application ID value in the `ida:ClientId` parameter.

# [ASP.NET Core](#tab/aspnet-core)
1. In your IDE, open the project folder, *ms-identity-ciam-dotnet-tutorial/2-Authorization/3-call-own-api-dotnet-core-daemon/ToDoListAPI*, containing the sample.
2. Open `appsettings.json` file, which contains the following code snippet:

    ```json
    {
      "AzureAd": {
        "Instance": "Enter_the_Authority_URL_Here", //For external tenants, use instance in the form of "https://Enter_the_Tenant_Subdomain_Here.ciamlogin.com/"
        "TenantId": "Enter_the_Tenant_Id_Here",
        "ClientId": "Enter_the_Application_Id_Here",
        "Scopes": {
          "Read": ["ToDoList.Read", "ToDoList.ReadWrite"],
          "Write": ["ToDoList.ReadWrite"]
        },
        "AppPermissions": {
          "Read": ["ToDoList.Read.All", "ToDoList.ReadWrite.All"],
          "Write": ["ToDoList.ReadWrite.All"]
        }
      },
      "Logging": {...},
      "AllowedHosts": "*"
    }
    ```

    Find the following values:

    - `ClientId` - The identifier of the application, also referred to as the client. Replace the `value` text in quotes with **Application (client) ID** that was recorded earlier from the **Overview** page of the registered application.
    - `TenantId` - The identifier of the tenant where the application is registered. Replace the `value` text in quotes with **Directory (tenant) ID** value that was recorded earlier from the **Overview** page of the registered application.
    - `Instance` - It specifies the directory from which the Microsoft Authentication Library (MSAL) can request tokens from. Replace `Enter_the_Authority_URL_Here`with either of the following values depending on your scenario:
        - For workforce tenants, use `https://login.microsoftonline.com/` as the instance.
        - For external tenants, add an authority URL in the form of `https://<Enter_the_Tenant_Subdomain_Here>.ciamlogin.com/`

---

## Run the sample application

# [ASP.NET](#tab/aspnet)
Start both projects. For Visual Studio users;

1. Right click on the Visual Studio solution and select **Properties**
2. In the **Common Properties**, select **Startup Project** and then **Multiple startup projects**.
3. For both projects choose **Start** as the action
4. Ensure the TodoListService service starts first by moving it to the first position in the list, using the up arrow.

Sign in to run your TodoListClient project.

1. Press F5 to start the projects. The service page opens, as well as the desktop application.
2. In the TodoListClient, at the upper right, select **Sign in**, and then sign in with the same credentials you used to register your application, or sign in as a user in the same directory.

    If you're signing in for the first time, you might be prompted to consent to the TodoListService web API.

    To help you access the TodoListService web API and manipulate the *To-Do* list, the sign-in also requests an access token to the *access\_as\_user* scope.

## Pre-authorize your client application

You can allow users from other directories to access your web API by pre-authorizing the client application to access your web API. You do this by adding the Application ID from the client app to the list of preauthorized applications for your web API. By adding a preauthorized client, you're allowing users to access your web API without having to provide consent.

1. In the **App registrations** portal, open the properties of your TodoListService app.
2. In the **Expose an API** section, under **Authorized client applications**, select **Add a client application**.
3. In the **Client ID** box, paste the Application ID of the TodoListClient app.
4. In the **Authorized scopes** section, select the scope for the `api://<Application ID>/access_as_user` web API.
5. Select **Add application**.

### Run your project

1. Press F5 to run your project. Your TodoListClient app opens.
2. At the upper right, select **Sign in**, and then sign in by using a personal Microsoft account, such as a *live.com* or *hotmail.com* account, or a work or school account.

## Optional: Limit sign-in access to certain users

By default, any personal accounts, such as *outlook.com* or *live.com* accounts, or work or school accounts from organizations that are integrated with Microsoft Entra ID can request tokens and access your web API.

To specify who can sign in to your application, by changing the `TenantId` property in the *appsettings.json* file.

# [ASP.NET Core](#tab/aspnet-core)
1. Run the following command from the root of your web API project directory to start the app:

    ```bash
    dotnet run
    ```
2. If everything worked correctly, your terminal displays an output similar to the following:

    ```bash
     Building...
         info: Microsoft.Hosting.Lifetime[14]
               Now listening on: https://localhost:{port}
         info: Microsoft.Hosting.Lifetime[0]
               Application started. Press Ctrl+C to shut down.
         info: Microsoft.Hosting.Lifetime[0]
               Hosting environment: Development
    ...
    ```

    Record the port number in the `https://localhost:{port}` URL.
3. To verify the endpoint is protected, update the base URL in the following cURL command to match the one you received in the previous step, and then run the command:

    ```bash
    curl -k -X GET https://localhost:<your-api-port>/api/todolist -w "%{http_code}\n"
    ```

    The expected response is 401 Unauthorized.

---