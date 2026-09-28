---
layout: Conceptual
title: Quickstart - Sign in users and call a web API in sample app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-mobile-app-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Quickstart for configuring a sample mobile app to sign in users and call web API with Microsoft identity platform.
manager: pmwongera
ms.topic: quickstart
ms.date: 2024-10-30T00:00:00.0000000Z
locale: en-us
document_id: fc8aae2c-1f64-968c-09cb-5ea910373103
document_version_independent_id: fc8aae2c-1f64-968c-09cb-5ea910373103
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-mobile-app-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-mobile-app-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-mobile-app-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c16911e9-0d7c-2543-8809-f1ea9153438d
---

# Quickstart - Sign in users and call a web API in sample app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Before you begin, use the **Choose a tenant type** selector at the top of this page to select tenant type. Microsoft Entra ID provides two tenant configurations, [workforce](../external-id/tenant-configurations#workforce-tenants) and [external](../external-id/tenant-configurations#external-tenants). A workforce tenant configuration is for your employees, internal apps, and other organizational resources. An external tenant is for your customer-facing apps.

This guide demonstrates how to configure a sample mobile application to sign in users, and call an ASP.NET Core web API.

# [Android](#tab/android-external)
In this article, you do the following tasks:

- Add a platform redirect URL to a web application.
- Enable public client flows.
- Update the Android configuration code sample file to use your own Microsoft Entra External ID for customer tenant details.
- Run and test the sample Android mobile application.
- Call a protected web API.

# [iOS/macOS](#tab/ios-macos-external)
In this article, you do the following tasks:

- Add a platform redirect URL to a web application.
- Enable public client flows to an application.
- Update the iOS configuration code sample file to use your own Microsoft Entra External ID for customer tenant details.
- Run and test the sample iOS mobile application.

---

## Prerequisites

# [Android](#tab/android-external)
- [Android Studio](https://developer.android.com/studio).
- An external tenant. If you don't already have one, [sign up for a free trial](https://aka.ms/ciam-free-trial?wt.mc_id=ciamcustomertenantfreetrial_linkclick_content_cnl).
- Register a new client web app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in any organizational directory and personal Microsoft accounts*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview** page for later use:

    - Application (client) ID
    - Directory (tenant) ID
- A web API registration that exposes at least one scope (delegated permissions) and one app role (application permission) such as *ToDoList.Read*. If you haven't already, follow the instructions for [call an API in a sample Android mobile app](../external-id/customers/sample-native-authentication-android-sample-app-call-web-api) to have a functional protected ASP.NET Core web API. Make sure you complete the following steps:

    - Configure API scopes
    - Configure app roles
    - Configure optional claims
    - Clone or download sample web API
    - Configure and run sample web API

# [iOS/macOS](#tab/ios-macos-external)
- [Xcode](https://developer.apple.com/xcode/resources/).
- An external tenant. If you don't already have one, [sign up for a free trial](https://aka.ms/ciam-free-trial?wt.mc_id=ciamcustomertenantfreetrial_linkclick_content_cnl).
- Register a new client web app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in any organizational directory and personal Microsoft accounts*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview** page for later use:

    - Application (client) ID
    - Directory (tenant) ID\*
- An API registration that exposes at least one scope (delegated permissions) and one app role (application permission) such as *ToDoList.Read*. If you haven't already, follow the instructions for [call an API in a sample iOS mobile app](../external-id/customers/sample-native-authentication-ios-sample-app-call-web-api) to have a functional protected ASP.NET Core web API. Make sure you complete the following steps:

    - Configure API scopes.
    - Configure app roles.
    - Configure optional claims.
    - Clone or download sample web API.
    - Configure and run sample web API.

---

## Add a platform redirect URL

# [Android](#tab/android-external)
To specify your app type to your app registration, follow these steps:

1. Under **Manage**, select **Authentication**.
2. On the **Platform configurations** page, select **Add a platform**, and then select **Android** option.
3. Enter your project's Package Name. If you downloaded the [sample code](https://github.com/Azure-Samples/ms-identity-ciam-browser-delegated-android-sample), this value is `com.azuresamples.msaldelegatedandroidkotlinsampleapp`.
4. In the **Signature hash** section of the **Configure your Android app** pane, select **Generating a development Signature Hash. This will change for each development environment.** Copy and run the KeyTool command for your operating system in your Terminal.
5. Enter the **Signature hash** generated by KeyTool.
6. Select **Configure**.
7. Copy the **MSAL Configuration** from the **Android configuration** pane and save it for later app configuration.
8. Select **Done**.

# [iOS/macOS](#tab/ios-macos-external)
To specify your app type to your app registration, follow these steps:

1. Under **Manage**, select **Authentication**.
2. On the **Platform configurations** page, select **Add a platform**, and then select **iOS / macOS** option.
3. Enter your project's Bundle ID. If you downloaded the [sample code](https://github.com/Azure-Samples/ms-identity-ciam-browser-delegated-ios-sample.git), this value is `com.microsoft.identitysample.ciam.MSALiOS`.
4. Select **Configure** and save the **MSAL Configuration** that appears in the **iOS / macOS configuration** pane so you can enter it when you configure your app later.
5. Select **Done**.

---

## Enable public client flow

To identify your app as a public client, follow these steps:

1. Under **Manage**, select **Authentication**.
2. Under **Advanced settings**, for **Allow public client flows**, select **Yes**.
3. Select **Save** to save your changes.

## Grant web API permissions to the sample app

Once you've registered both your client app, web API, and you've exposed the API by creating scopes, you can configure the client's permissions to the API by following these steps:

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

## Clone sample mobile application

# [Android](#tab/android-external)
To obtain the sample application, you can either clone it from GitHub or download it as a .zip file.

- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-browser-delegated-android-sample
    ```

# [iOS/macOS](#tab/ios-macos-external)
To obtain the sample application, you can either clone it from GitHub or download it as a .zip file.

- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-browser-delegated-ios-sample.git
    ```

---

## Configure the sample Android mobile application

# [Android](#tab/android-external)
To enable authentication and access to web API resources, configure the sample by following these steps:

1. In Android Studio, open the project that you cloned.
2. Open */app/src/main/res/raw/auth\_config\_ciam.json* file.
3. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the **Application (client) ID** of the app you registered earlier.
    - `Enter_the_Redirect_Uri_Here` and replace it with the value of *redirect\_uri* in the Microsoft Authentication Library (MSAL) configuration file you downloaded earlier when you added the platform redirect URL.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't know your tenant subdomain, learn how to [read your tenant details](../external-id/customers/how-to-create-customer-tenant-portal#get-the-customer-tenant-details).
4. Open */app/src/main/AndroidManifest.xml* file.
5. Find the placeholder:

    - `ENTER_YOUR_SIGNATURE_HASH_HERE` and replace it with the **Signature Hash** that you generated earlier when you added the platform redirect URL.
6. Open */app/src/main/java/com/azuresamples/msaldelegatedandroidkotlinsampleapp/MainActivity.kt* file.
7. Find property named `WEB_API_BASE_URL` and set the URL to your web API.
8. Find property named `scopes` and set the scopes recorded in Grant web API permissions to the Android sample app.

    ```kotlin
    private const val scopes = "" // Developers should set the respective scopes of their web API here. For example, private const val scopes = "api://{clientId}/{ToDoList.Read} api://{clientId}/{ToDoList.ReadWrite}"
    ```

You've configured the app and it's ready to run.

# [iOS/macOS](#tab/ios-macos-external)
To enable authentication and access to web API resources, configure the sample by following these steps:

1. In Xcode, open the project that you cloned.
2. Open */MSALiOS/Configuration.swift* file.
3. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the **Application (client) ID** of the app you registered earlier.
    - `Enter_the_Redirect_URI_Here` and replace it with the value of *kRedirectUri* in the Microsoft Authentication Library (MSAL) configuration file you downloaded earlier when you added the platform redirect URL.
    - `Enter_the_Protected_API_Full_URL_Here` and replace it with the URL to your web API. The *Enter\_the\_Protected\_API\_Full\_URL\_Here* should include the base URL (the deployed web API URL) and the endpoint (/api/todolist) for our ASP.NET web API.
    - `Enter_the_Protected_API_Scopes_Here` and replace it with the scopes recorded in Grant web API permissions to the iOS sample app.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't know your tenant subdomain, learn how to [read your tenant details](../external-id/customers/how-to-create-customer-tenant-portal#get-the-customer-tenant-details).

You've configured the app and it's ready to run.

---

## Run sample app and call web API

# [Android](#tab/android-external)
To build and run your app, follow these steps:

1. In the toolbar, select your app from the run configurations menu.
2. In the target device menu, select the device that you want to run your app on.

    If you don't have any devices configured, you need to either create an Android Virtual Device to use the Android Emulator or connect a physical Android device.
3. Select the **Run** button.
4. Select **Acquire Token Interactively** to request an access token.
5. Select **API - Perform GET** to call the previously set up ASP.NET Core web API. A successful call to the web API returns HTTP 200, while HTTP 403 signifies unauthorized access.

# [iOS/macOS](#tab/ios-macos-external)
To build and run your app, follow these steps:

1. To build and run your code, select **Run** from the **Product** menu in Xcode. After a successful build, Xcode will launch the sample app in the Simulator.
2. Select **Acquire Token Interactively** to request an access token.
3. Select **API - Perform GET** to call the previously set up ASP.NET Core web API. A successful call to the web API returns HTTP `200`, while HTTP `403` signifies unauthorized access.

---