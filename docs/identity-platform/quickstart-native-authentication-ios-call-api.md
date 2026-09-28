---
layout: Conceptual
title: Sign in users and call an API in sample iOS mobile app by using native authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-native-authentication-ios-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how sign in users and call an API in sample iOS (Swift) mobile app by using native authentication
manager: pmwongera
ms.subservice: external
ms.topic: quickstart
ms.date: 2024-08-21T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: f7a013f5-0cd0-e3b4-3f1f-b5c6c059107d
document_version_independent_id: f7a013f5-0cd0-e3b4-3f1f-b5c6c059107d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-native-authentication-ios-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-native-authentication-ios-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-native-authentication-ios-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 54aafa0e-5f62-43fa-44c0-86cdb27e9e73
---

# Sign in users and call an API in sample iOS mobile app by using native authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this quickstart you learn how to configure iOS sample application to call an ASP.NET Core web API.

## Prerequisites

- [Sign in users in sample iOS (Swift) mobile app by using native authentication](quickstart-native-authentication-ios-sign-in).
- Register a new application in the [Microsoft Entra admin center](https://entra.microsoft.com) for your web API, configured for *Accounts in any organizational directory and personal Microsoft accounts*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID

### Register a web API application

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Developer](../identity/role-based-access-control/permissions-reference#application-developer).
2. If you have access to multiple tenants, use the **Settings** icon ![](../external-id/customers/media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **App registrations**.
4. Select **+ New registration**.
5. In the **Register an application** page that appears, enter your application's registration information:

    1. In the Name section, enter a meaningful application name that will be displayed to users of the app, for example *ciam-ToDoList-api*.
    2. Under **Supported account types**, select **Accounts in this organizational directory only**.
6. Select **Register** to create the application.
7. The application's **Overview pane** is displayed when registration is complete. Record the **Directory (tenant) ID** and the **Application (client) ID** to be used in your application source code.

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

## Grant API permissions to the iOS sample app

Once you've registered both your client app and web API and you've exposed the API by creating scopes, you can configure the client's permissions to the API by following these steps:

1. From the **App registrations** page, select the application that you created (such as *ciam-client-app*) to open its **Overview** page.
2. Under **Manage**, select **API permissions**.
3. Under **Configured permissions**, select **Add a permission**.
4. Select the **APIs my organization uses** tab.
5. In the list of APIs, select the API such as *ciam-ToDoList-api*.
6. Select **Delegated permissions** option.
7. From the permissions list, select **ToDoList.Read, ToDoList.ReadWrite** (use the search box if necessary).
8. Select the **Add permissions** button.
9. At this point, you've assigned the permissions correctly. However, since the tenant is a customer's tenant, the consumer users themselves can't consent to these permissions. To address this, you as the admin must consent to these permissions on behalf of all the users in the tenant:

    1. Select **Grant admin consent for &lt;your tenant name&gt;**, then select **Yes**.
    2. Select **Refresh**, then verify that **Granted for &lt;your tenant name&gt;** appears under **Status** for both permissions.
10. From the **Configured permissions** list, select the **ToDoList.Read** and **ToDoList.ReadWrite** permissions, one at a time, and then copy the permission's full URI for later use. The full permission URI looks something similar to `api://{clientId}/{ToDoList.Read}` or `api://{clientId}/{ToDoList.ReadWrite}`.

## Clone or download sample web API

To obtain the sample application, you can either clone it from GitHub or download it as a .zip file.

- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial.git
    ```
- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

## Configure and run sample web API

1. In your code editor, open `2-Authorization/1-call-own-api-aspnet-core-mvc/ToDoListAPI/appsettings.json` file.
2. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the **Application (client) ID** of the web API you copied earlier.
    - `Enter_the_Tenant_Id_Here` and replace it with the **Directory (tenant) ID** you copied earlier.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).

You need to host your web API for the iOS sample app to call it. Follow [Quickstart: Deploy an ASP.NET web app](/en-us/azure/app-service/quickstart-dotnetcore) to deploy your web API.

## Configure sample iOS mobile app to call web API

The sample allows you to configure multiple Web API URL endpoints and sets of scopes. In this case, you configure only one Web API URL endpoint and its associated scopes.

1. In your Xcode, open `/NativeAuthSampleApp/ProtectedAPIViewController.swift` file. If you're using macOS, here's a sample [ProtectedAPIViewController.swift](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-ios-sample/blob/main/NativeAuthSampleApp/ProtectedAPIViewController.swift) code file.
2. Find `protectedAPIUrl1` and enter your web API URL as its value.

    ```swift
    let protectedAPIUrl1: String? = nil // Developers should set the respective URL of their web API here. For example let protectedAPIUrl1: String? = "https://api.example.com/v1/resource"
    ```
3. Find `protectedAPIScopes1` and set the scopes recorded in Grant API permissions to the iOS sample app.

    ```swift
    let protectedAPIScopes1: [String] = [] // Developers should set the respective scopes of their web API here.For example, let protectedAPIScopes = ["api://{clientId}/{ToDoList.Read}","api://{clientId}/{ToDoList.ReadWrite}"]
    ```

## Run iOS sample app and call web API

To build and run your app, follow these steps:

1. To build and run your code, select **Run** from the **Product** menu in Xcode. After a successful build, Xcode will launch the sample app in the Simulator.
2. Select the API tab to test the API call. A successful call to the web API returns HTTP `200`, while HTTP `403` signifies unauthorized access.