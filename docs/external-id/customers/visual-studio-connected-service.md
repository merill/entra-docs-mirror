---
layout: Conceptual
title: Get Started with the Microsoft identity platform Visual Studio's Connected Services - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/visual-studio-connected-service
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to use Visual Studio Connected Services to integrate Microsoft Entra ID into your applications right from your development environment.
ms.topic: quickstart
ms.date: 2024-12-23T00:00:00.0000000Z
locale: en-us
document_id: 86cfd3c9-9209-f8b9-07b6-0f0dbc284afb
document_version_independent_id: 86cfd3c9-9209-f8b9-07b6-0f0dbc284afb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/visual-studio-connected-service.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/visual-studio-connected-service
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/visual-studio-connected-service.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/4628cbd9-6f47-4ae1-b371-d34636609eaf
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/43ab1a66-ffe1-45dd-a4cb-6580218ef802
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/be21deb8-8c64-44b0-b71f-2dc56ca7364f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/bbc4fbf6-70c4-4d12-b47f-9360080c4977
platformId: 6657a037-dd0e-b09c-18da-913f9e4fb6ee
---

# Get Started with the Microsoft identity platform Visual Studio's Connected Services - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Integrating identity management solutions into your organizational and customer-facing applications is essential for securing resources and customer data. Visual Studio's Connected Services allow you to quickly integrate the Microsoft identity platform into your ASP.NET web apps and configure sign-in experiences, all within Visual Studio. This article provides details of using Visual Studio's Connected Services feature for Microsoft Entra ID.

## Prerequisites

- [**Visual Studio 2022**](https://visualstudio.microsoft.com/downloads/) with the ASP.NET and web development workload installed.
- A **Microsoft Entra tenant**(workforce or external). If you don’t have one, choose from the following methods:
    - [Create a new tenant](how-to-create-external-tenant-portal) in the Microsoft Entra admin center.
    - Use an Azure account with an active subscription. If you don't have one, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- The account you use must have permissions to manage applications in your tenant. Any of the following Microsoft Entra roles have the required permissions:
    - Application Administrator
    - Application Developer
    - Cloud Application Administrator

## Create your project and connect it to the Microsoft identity platform

1. In Visual Studio, create or open an ASP.NET Model–view–controller (MVC) project, or an ASP.NET Web API project. For this quickstart, you use the ‘ASP.NET Core Web App (Razor Pages) template.
2. Enter **Project Name**, for example,‘sample-asp-dotnet-webapp’ and the **Location** where you’d like to create the project then select **Next**.
3. In the **Framework** selection, select .NET 8.0 (Long Term Support).
4. Under **Authentication Type**, select Microsoft identity platform.

If you’re creating your app from an empty project template in Visual Studio or already have an existing ASP.NET web app and would like to add Microsoft Entra ID authentication, follow these steps:

1. Open the solutions explorer and select **Connected Services**.
2. When the Connected Services pane opens on Visual Studio, select **Add a service dependency** or use the + icon.

    ![Screenshot showing the Connected Services pane on Visual Studio.](media/visual-studio-connected-service/add-service-dependency.png)
3. From the dropdown list, select **Microsoft identity platform**. You can use the search tab if needed.

    ![Screenshot showing Microsoft identity platform and other service dependencies on Visual Studio.](media/visual-studio-connected-service/microsoft-identity-platform-service-dependency.png)
4. Microsoft identity platform shows under service dependencies in the Connected Services pane, as shown:

    ![Screenshot showing Microsoft identity platform successfully connected as a service dependency on Visual Studio.](media/visual-studio-connected-service/microsoft-identity-platform-connected.png)

## Install required components

To use Microsoft identity platform in your project, you need to install the **dotnet msidentity tool**. This command line tool enables you to create Microsoft Entra app registrations. It also updates your app to use Microsoft identity platform by modifying the configuration files of your ASP.NET Core applications (MVC, Razor Pages, Blazor WebAssembly (WASM), Blazor WASM Hosted, Blazor Server).

If you don't have the dotnet msidentity tool installed on your device, Visual Studio prompts you to install it, as shown:

![Screenshot showing a Visual Studio prompt to install the dotnet msidentity tool](media/visual-studio-connected-service/dotnet-msidentity-tool-installation-prompt.png)

You can install the dotnet msidentity tool from your command line by running:

```sh
dotnet tool install --global Microsoft.dotnet-msidentity --version 2.0.8
```

Once you complete installing the dotnet msidentity tool, select **Next** to proceed to configuration.

## Configure application to use Microsoft identity platform

The Microsoft identity platform connected service allows you to configure applications in either workforce or external tenants. To complete configuration, follow these steps:

1. In the top right section, sign in to your Microsoft account. If you have multiple accounts, select the account with the tenant where you’d like to register your application.

    ![Screenshot showing the Visual Studio window where you configure the application to use Microsoft identity platform.](media/visual-studio-connected-service/configure-application-to-use-microsoft-identity-platform.png)
2. Once you're signed in, you see a list of applications registered in your tenant; with the application’s display name, client ID, and date created.
3. If you're yet to create an app registration in the Microsoft Entra admin center, select **Create new**. Choose the tenant where you’d like to create the application and provide a display name, such as sample-web-app and Select **Register**. You can change the application's display name later.

    ![Screenshot showing the Visual Studio window where you register a new application.](media/visual-studio-connected-service/register-new-application.png)
4. The application you created now shows in the list. Select it and choose **Next.**

    ![Screenshot showing a list of app registrations in your tenant.](media/visual-studio-connected-service/app-registrations-list.png)
5. On the next screen, you can configure your app's permissions to access Microsoft Graph or other APIs. Select **Next** to complete the configuration later if you don't have the information yet.
6. A screen with the summary of the changes being made to your project appears. Select **Finish** to complete the process.

    ![Screenshot showing a list of the changes being made to your project.](media/visual-studio-connected-service/summary-of-changes-to-the-project.png)
7. A Dependency configuration progress screen showing the actual changes being in your project appears, as shown. Once successful, select **Close**.

    ![Screenshot showing the dependency configuration progress.](media/visual-studio-connected-service/dependency-configuration-progress.png)

## [Optional]: Configure permissions to access a web API

The Microsoft identity platform connected service allows you to optionally add permissions to access Microsoft Graph or any other web API. You can add support for your own API or third-party APIs registered with the Microsoft identity platform.

If you want to modify it, such as to add support for an API such as Microsoft Graph, select the three dots on the Microsoft identity platform service dependency, and then choose **Edit dependency**. You can repeat the steps and add the APIs that you want to grant access to.

![Screenshot showing the window that allows you to add permissions to access Microsoft Graph or any other web API.](media/visual-studio-connected-service/configure-additional-api-permissions.png)

## Run and test the app

To run the sample application, follow these steps:

1. Navigate to Visual Studio’s top navigation bar and select **Debug &gt; Start Without Debugging** to start building your application, as shown:

    ![Screenshot showing a sample application building on Visual Studio.](media/visual-studio-connected-service/build-sample-application.png)
2. Once your build is complete, a new browser window opens at https://localhost:7142.
3. Depending on what your application does, Microsoft Entra ID will redirect you to perform the required action. For our sample application, the app prompts you to complete the sign-up and sign-in process as shown:

    ![Screenshot showing a sample application integrated with Microsoft identity platform running on Visual Studio.](media/visual-studio-connected-service/sample-app-running.png)

### Related content

- [Add sign-in with Microsoft to an ASP.NET web app](../../identity-platform/quickstart-v2-aspnet-webapp)
- [Visual Studio Code extension for Microsoft Entra External ID](visual-studio-code-extension)