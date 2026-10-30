---
layout: Conceptual
title: 'Tutorial: Create a .NET MAUI shell app, add MSAL, and include an image resource - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-mobile-app-maui-sign-in-prepare-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: This tutorial demonstrates how to create a .NET MAUI shell app, add MSALClient, and include an image resource.
manager: pmwongera
ms.topic: tutorial
ms.custom: 
ms.date: 2025-03-12T00:00:00.0000000Z
locale: en-us
document_id: aa788c5c-43fb-21fe-b3e1-b1e8f35a5bd5
document_version_independent_id: aa788c5c-43fb-21fe-b3e1-b1e8f35a5bd5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-mobile-app-maui-sign-in-prepare-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-mobile-app-maui-sign-in-prepare-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-mobile-app-maui-sign-in-prepare-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
platformId: 5af41cac-359e-2d20-7c6a-28a0decd0a6d
---

# Tutorial: Create a .NET MAUI shell app, add MSAL, and include an image resource - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial is part 1 of a series that demonstrates how to create a .NET Multi-platform App UI (.NET MAUI) shell app and prepare it for authentication using the Microsoft Entra admin center. In this tutorial, you'll add a custom Microsoft Authentication Library (MSAL) client helper to initialize the MSAL SDK, install required libraries and include an image resource.

In this tutorial, you:

- Create a .NET MAUI shell app.
- Add MSAL SDK support using MSAL helper classes.
- Install required packages.
- Add image resource.

## Prerequisites

- Register a new client web app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in any organizational directory and personal Microsoft accounts*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Mobile and Desktop applications** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `msal{client_id}://auth` where `{client_id}` is the Application (client) ID of your app.
- [.NET SDK](https://dotnet.microsoft.com/download/dotnet/latest)
- [Visual Studio 2022](https://aka.ms/vsdownloads)with the MAUI workload installed:
    - [Instructions for Visual Studio Setup](/en-us/dotnet/maui/get-started/installation?tabs=visual-studio)

## Create .NET MAUI shell app

1. In the start window of Visual Studio 2022, select **Create a new project**.
2. In the **Create a new project** window, select **MAUI** in the All project types dropdown list, select the **.NET MAUI App** template, and select **Next**.
3. In the **Configure your new project** window, **Project name** must be set to *SignInMaui*. Update the **Solution name** to *sign-in-maui* and select **Next**.
4. In the **Additional information** window, choose latest **.NET SDK** and select **Create**.

Wait for the project to be created and its dependencies to be restored.

## Add MSAL SDK support using MSAL helper classes

MSAL client enables developers to acquire security tokens from an external tenant to authenticate and access secured web APIs. In this section, you download files that makes up MSALClient.

Download the following files into a folder in your computer:

- [AzureAdConfig.cs](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/blob/main/1-Authentication/2-sign-in-maui/MSALClient/AzureAdConfig.cs) - This file gets and sets the Microsoft Entra app unique identifiers from your app configuration file.
- [DownStreamApiConfig.cs](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/blob/main/1-Authentication/2-sign-in-maui/MSALClient/DownStreamApiConfig.cs) - This file gets and sets the scopes for Microsoft Graph call.
- [DownstreamApiHelper.cs](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/blob/main/1-Authentication/2-sign-in-maui/MSALClient/DownstreamApiHelper.cs) - This file handles the exceptions that occur when calling the downstream API.
- [Exception.cs](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/blob/main/1-Authentication/2-sign-in-maui/MSALClient/Exception.cs) - This file offers a few extension method related to exception throwing and handling.
- [IdentityLogger.cs](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/blob/main/1-Authentication/2-sign-in-maui/MSALClient/IdentityLogger.cs) - This file handles shows how to use MSAL.NET logging.
- [MSALClientHelper.cs](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/blob/main/1-Authentication/2-sign-in-maui/MSALClient/MSALClientHelper.cs) - This file contains methods to initialize MSAL SDK.
- [PlatformConfig.cs](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/blob/main/1-Authentication/2-sign-in-maui/MSALClient/PlatformConfig.cs) - This file contains methods to handle specific platform. For example, Windows.
- [PublicClientSingleton.cs](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/blob/main/1-Authentication/2-sign-in-maui/MSALClient/PublicClientSingleton.cs) - This file contains a singleton implementation to wrap the MSALClient and associated classes to support static initialization model for platforms.
- [WindowsHelper.cs](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/blob/main/1-Authentication/2-sign-in-maui/MSALClient/WindowsHelper.cs) - This file contains methods to retrieve window handle.

Important

Don't skip downloading the MSALClient files, they're required to complete this tutorial.

### Move the MSALClient files with Visual Studio

1. In the **Solution Explorer** pane, right-click on the **SignInMaui** project and select **Add** &gt; **New Folder**. Name the folder *MSALClient*.
2. Right-click on **MSALClient** folder, select **Add** &gt; **Existing Item...**.
3. Navigate to the folder that contains the downloaded MSALClient files that you downloaded earlier.
4. Select all of the MSALClient files you downloaded, then select **Add**

## Install required packages

You need to install the following packages:

- *Microsoft.Identity.Client* - This package contains the binaries of the Microsoft Authentication Library for .NET (MSAL.NET).
- *Microsoft.Extensions.Configuration.Json* - This package contains JSON configuration provider implementation for Microsoft.Extensions.Configuration.
- *Microsoft.Extensions.Configuration.Binder* - This package contains functionality to bind an object to data in configuration providers for Microsoft.Extensions.Configuration.
- *Microsoft.Extensions.Configuration.Abstractions* - This package contains abstractions of key-value pair-based configuration.
- *Microsoft.Identity.Client.Extensions.Msal* - This package contains extensions to Microsoft Authentication Library for .NET (MSAL.NET).

### NuGet Package Manager

To use the **NuGet Package Manager** to install the *Microsoft.Identity.Client* package in Visual Studio, follow these steps:

1. Select **Tools** &gt; **NuGet Package Manager** &gt; **Manage NuGet Packages for Solution...**.
2. From the **Browse** tab, search for *Microsoft.Identity.Client*.
3. Select **Microsoft.Identity.Client** in the list.
4. Select **SignInMaui** in the **Project** list pane.
5. Select **Install**.
6. If you're prompted to verify the installation, select **OK**.

Repeat the process to install the remaining required packages.

## Add image resource

In this section, you download an image that you use in your app to enhance how users interact with it.

Download the following image:

- [Icon: Microsoft Entra ID](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/blob/main/1-Authentication/2-sign-in-maui/Resources/Images/azure_active_directory.png) - This image is used as icon in the main page.

### Move the image with Visual Studio

1. In the **Solution Explorer** pane of Visual Studio, expand the **Resources** folder, which reveals the **Images** folder.
2. Right-click on **Images** and select **Add** &gt; **Existing Item...**.
3. Navigate to the folder that contains the downloaded images.
4. Change the filter to file type filter to **Image Files**.
5. Select the image you downloaded.
6. Select **Add**.