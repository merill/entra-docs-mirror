---
layout: Conceptual
title: 'Quickstart: Call an ASP.NET web API that is protected by the Microsoft identity platform - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-v2-dotnet-native-aspnet
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, learn how to call an ASP.NET web API that's protected by the Microsoft identity platform from a Windows Desktop (WPF) application.
ROBOTS: NOINDEX
manager: pmwongera
ms.custom: 
ms.date: 2022-01-11T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: quickstart
locale: en-us
document_id: 3f20598f-7093-dc72-a96d-858547b176e1
document_version_independent_id: b4433406-2a42-72ec-7d6b-2b20f9b14ce9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-v2-dotnet-native-aspnet.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-v2-dotnet-native-aspnet
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-v2-dotnet-native-aspnet.md
platformId: fa949706-398c-8151-2022-0aaaa92716c9
---

# Quickstart: Call an ASP.NET web API that is protected by the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Call a protected ASP.NET web API](quickstart-web-api-aspnet-protect-api)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

In this quickstart, you download and run a code sample that demonstrates how to protect an ASP.NET web API by restricting access to its resources to authorized accounts only. The sample supports authorization of personal Microsoft accounts and accounts in any Microsoft Entra organization.

The article also uses a Windows Presentation Foundation (WPF) app to demonstrate how you can request an access token to access a web API.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Visual Studio 2017 or 2019. Download [Visual Studio for free](https://www.visualstudio.com/downloads/).

## Clone or download the sample

You can obtain the sample in either of two ways:

- Clone it from your shell or command line:

    ```console
    git clone https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git
    ```
- [Download it as a ZIP file](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip).

Tip

To avoid errors caused by path length limitations in Windows, we recommend extracting the archive or cloning the repository into a directory near the root of your drive.

## Register the web API (TodoListService)

Register your web API in **App registrations** in the Azure portal.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select **New registration**.
4. Enter a **Name** for your application, for example `AppModelv2-NativeClient-DotNet-TodoListService`. Users of your app might see this name, and you can change it later.
5. For **Supported account types**, select **Accounts in any organizational directory**.
6. Select **Register** to create the application.
7. On the app **Overview** page, look for the **Application (client) ID** value, and then record it for later use. You'll need it to configure the Visual Studio configuration file for this project (that is, `ClientId` in the *TodoListService\Web.config* file).
8. Under **Manage**, select **Expose an API** &gt; **Add a scope**. Accept the proposed Application ID URI (`api://{clientId}>`) by selecting **Save and continue**, and then enter the following information:

    1. For **Scope name**, enter `access_as_user`.
    2. For **Who can consent**, ensure that the **Admins and users** option is selected.
    3. In the **Admin consent display name** box, enter `Access TodoListService as a user`.
    4. In the **Admin consent description** box, enter `Accesses the TodoListService web API as a user`.
    5. In the **User consent display name** box, enter `Access TodoListService as a user`.
    6. In the **User consent description** box, enter `Accesses the TodoListService web API as a user`.
    7. For **State**, keep **Enabled**.
9. Select **Add scope**.

### Configure the service project

Configure the service project to match the registered web API.

1. Open the solution in Visual Studio, and then open the *Web.config* file under the root of the TodoListService project.
2. Replace the value of the `ida:ClientId` parameter with the Client ID (Application ID) value from the application you registered in the **App registrations** portal.

### Add the new scope to the app.config file

To add the new scope to the TodoListClient *app.config* file, follow these steps:

1. In the TodoListClient project root folder, open the *app.config* file.
2. Paste the Application ID from the application that you registered for your TodoListService project in the `TodoListServiceScope` parameter, replacing the `{Enter the Application ID of your TodoListService from the app registration portal}` string.

Note

Make sure that the Application ID uses the following format: `api://{TodoListService-Application-ID}/access_as_user` (where `{TodoListService-Application-ID}` is the GUID representing the Application ID for your TodoListService app).

## Register the web app (TodoListClient)

Register your TodoListClient app in **App registrations** in the Azure portal, and then configure the code in the TodoListClient project. If the client and server are considered the same application, you can reuse the application that's registered in step 2. Use the same application if you want users to sign in with a personal Microsoft account.

### Register the app

To register the TodoListClient app, follow these steps:

1. Go to the Microsoft identity platform for developers [App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.
2. Select **New registration**.
3. When the **Register an application page** opens, enter your application's registration information:

    1. In the **Name** section, enter a meaningful application name that will be displayed to users of the app (for example, **NativeClient-DotNet-TodoListClient**).
    2. For **Supported account types**, select **Accounts in any organizational directory**.
    3. Select **Register** to create the application.

    Note

    In the TodoListClient project *app.config* file, the default value of `ida:Tenant` is set to `common`. The possible values are:

    - `common`: You can sign in by using a work or school account or a personal Microsoft account (because you selected **Accounts in any organizational directory** in a previous step).
    - `organizations`: You can sign in by using a work or school account.
    - `consumers`: You can sign in only by using a Microsoft personal account.
4. On the app **Overview** page, select **Authentication**, and then complete these steps to add a platform:

    1. Under **Platform configurations**, select the **Add a platform** button.
    2. For **Mobile and desktop applications**, select **Mobile and desktop applications**.
    3. For **Redirect URIs**, select the `https://login.microsoftonline.com/common/oauth2/nativeclient` check box.
    4. Select **Configure**.
5. Select **API permissions**, and then complete these steps to add permissions:

    1. Select the **Add a permission** button.
    2. Select the **My APIs** tab.
    3. In the list of APIs, select **AppModelv2-NativeClient-DotNet-TodoListService API** or the name you entered for the web API.
    4. Select the **access\_as\_user** permission check box if it's not already selected. Use the Search box if necessary.
    5. Select the **Add permissions** button.

### Configure your project

Configure your TodoListClient project by adding the Application ID to the *app.config* file.

1. In the **App registrations** portal, on the **Overview** page, copy the value of the **Application (client) ID**.
2. From the TodoListClient project root folder, open the *app.config* file, and then paste the Application ID value in the `ida:ClientId` parameter.

## Run your projects

Start both projects. If you are using Visual Studio:

1. Right click on the Visual Studio solution and select **Properties**
2. In the **Common Properties** select **Startup Project** and then **Multiple startup projects**.
3. For both projects choose **Start** as the action
4. Ensure the TodoListService service starts first by moving it to the first position in the list, using the up arrow.

Sign in to run your TodoListClient project.

1. Press F5 to start the projects. The service page opens, as well as the desktop application.
2. In the TodoListClient, at the upper right, select **Sign in**, and then sign in with the same credentials you used to register your application, or sign in as a user in the same directory.

    If you're signing in for the first time, you might be prompted to consent to the TodoListService web API.

    To help you access the TodoListService web API and manipulate the *To-Do* list, the sign-in also requests an access token to the *access\_as\_user* scope.

## Pre-authorize your client application

You can allow users from other directories to access your web API by pre-authorizing the client application to access your web API. You do this by adding the Application ID from the client app to the list of pre-authorized applications for your web API. By adding a pre-authorized client, you're allowing users to access your web API without having to provide consent.

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

To specify who can sign in to your application, use one of the following options:

### Option 1: Limit access to a single organization (single tenant)

You can limit sign-in access to your application to user accounts that are in a single Microsoft Entra tenant, including guest accounts of that tenant. This scenario is common for line-of-business applications.

1. Open the *App\_Start\Startup.Auth* file, and then change the value of the metadata endpoint that's passed into the `OpenIdConnectSecurityTokenProvider` to `https://login.microsoftonline.com/{Tenant ID}/v2.0/.well-known/openid-configuration`. You can also use the tenant name, such as `contoso.onmicrosoft.com`.
2. In the same file, set the `ValidIssuer` property on the `TokenValidationParameters` to `https://sts.windows.net/{Tenant ID}/`, and set the `ValidateIssuer` argument to `true`.

### Option 2: Use a custom method to validate issuers

You can implement a custom method to validate issuers by using the `IssuerValidator` parameter. For more information about this parameter, see [TokenValidationParameters class](/en-us/dotnet/api/microsoft.identitymodel.tokens.tokenvalidationparameters).

## Help and support

If you need help, want to report an issue, or want to learn about your support options, see [Help and support for developers](developer-support-help-options).