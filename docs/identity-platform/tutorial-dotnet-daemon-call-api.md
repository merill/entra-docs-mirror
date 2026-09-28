---
layout: Conceptual
title: 'Tutorial: Call protected web API from your .NET daemon app - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-dotnet-daemon-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about how to call a protected web API from your .NET client daemon app. In this tutorial, we call Microsoft Graph API.
manager: pmwongera
ms.custom: 
ms.topic: tutorial
ms.date: 2025-02-24T00:00:00.0000000Z
locale: en-us
document_id: 9f39fc33-0593-e1c1-2c1b-8de51c20b2f9
document_version_independent_id: 9f39fc33-0593-e1c1-2c1b-8de51c20b2f9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-dotnet-daemon-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-dotnet-daemon-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-dotnet-daemon-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: eeabbeac-feda-8ece-748a-5e9be37727ad
---

# Tutorial: Call protected web API from your .NET daemon app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to call a protected web API from a .NET daemon app. You enable the client daemon app to acquire an access token using its own identity, then call the web API. In our case, we call a protected Microsoft Graph endpoint.

In this tutorial;

- Configure a daemon app to use it's app registration details. Ensure you grant the app the *User.Read.All* permission on Microsoft Graph API.
- Build a daemon app that acquires a token on its own behalf and calls a protected web API.

## Prerequisites

- [.NET](https://dotnet.microsoft.com/download). In this tutorial, we use .NET 9.0.
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor.
- [An app registration](quickstart-register-app)in your tenant. Make sure you have the following from your app registration details:
    - The *Application (client) ID* of the client web app that you registered.
    - The *Directory (tenant) ID* where you registered your web app.
    - The *Client secret* value for the web app you created.

## Create a .NET daemon app

1. Open your terminal and navigate to the folder where you want your project to live.
2. Initialize a .NET console app and navigate to its root folder.

    ```dotnetcli
    dotnet new console -n DotnetDaemon
    cd DotnetDaemon
    ```

## Install packages

Install `Microsoft.Identity.Web` and `Microsoft.Identity.Web.DownstreamApi` packages:

```dotnetcli
dotnet add package Microsoft.Identity.Web
dotnet add package Microsoft.Identity.Web.DownstreamApi
```

`Microsoft.Identity.Web` provides the glue between ASP.NET Core, the authentication middleware, and the Microsoft Authentication Library (MSAL) for .NET making it easier for you to add authentication and authorization capabilities to your app. `Microsoft.Identity.Web.DownstreamApi` provides an interface used to call a downstream API.

## Create appsettings.json file an add registration configs

1. Create *appsettings.json* file in the root folder of the app.
2. Add app registration details to the *appsettings.json* file.

    ```json
    {
        "AzureAd": {
            // "Authority": "", you can use this for customer tenants in place of Instance and TenantId values
            "Instance": "https://login.microsoftonline.com/",
            "TenantId": "Enter_the_Tenant_ID_Here",
            "ClientId": "Enter_the_Application_ID_Here",
            "ClientCredentials": [
                {
                    "SourceType": "ClientSecret",
                    "ClientSecret": "Enter_the_Client_Secret_Here"
                }
            ]
        },
        "DownstreamApi": {
            "BaseUrl": "https://graph.microsoft.com",
            "RelativePath": "/v1.0/users/",
            "RequestAppToken": true,
            "Scopes": [
                "https://graph.microsoft.com/.default"
            ]
        }
    }
    ```

    Replace the following values with your own:

    | Value | Description |
    | --- | --- |
    | *Enter\_the\_Application\_ID\_Here* | The Application (client) ID of the client daemon app that you registered. |
    | *Enter\_the\_Client\_Secret\_Here* | The daemon app secret value you created. |
    | *Enter\_the\_Tenant\_ID\_Here* | The tenant ID of the directory / tenant where the app is registered. |

    Note

    For apps registered in external tenant, you can use *Authority* and remove both *Instance* and *TenantId*.

    `"Authority": "https://<Enter_the_Tenant_Subdomain_Here>.ciamlogin.com/"`. Where *Enter\_the\_Tenant\_Subdomain\_Here* is the subdomain of the tenant.
3. Add the *appsettings.json* file to the project file. The project file is a *.csproj* file in your project. This is because the file needs to be copied to the output directory.

    ```xml
    <ItemGroup>
        <None Update="appsettings.json">
            <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
        </None>
    </ItemGroup>
    ```

## Acquire access token

1. Open the program.cs file in your code editor and delete its contents.
2. Add your packages to the file.

    ```csharp
    using Microsoft.Extensions.DependencyInjection;
    using Microsoft.Identity.Abstractions;
    using Microsoft.Identity.Web;
    ```
3. Create the token acquisition instance. Use the `GetDefaultInstance` method of the `TokenAcquirerFactory` class of `Microsoft.Identity.Web` package to build the token acquisition instance. By default, the instance reads an *appsettings.json* file if it exists in the same folder as the app. `GetDefaultInstance` also allows us to add services to the service collection.

    Add this line of code to the *program.cs* file:

    ```csharp
    var tokenAcquirerFactory = TokenAcquirerFactory.GetDefaultInstance();
    ```
4. Configure the application options to be read from the configuration and add the `DownstreamApi` service. The `DownstreamApi` service provides an interface used to call a downstream API. We call this service *DownstreamAPI* in the config object. The daemon app reads the downstream API configs from the *DownstreamApi* section of *appsettings.json*. By default, you get an in-memory token cache.

    Add the following code snippet to the *program.cs* file:

    ```csharp
    const string ServiceName = "DownstreamApi";
    
    tokenAcquirerFactory.Services.AddDownstreamApi(ServiceName,
        tokenAcquirerFactory.Configuration.GetSection("DownstreamApi"));
    ```

    The downstream API you call is Microsoft Graph. In this tutorial, we use the `DownstreamApi` service. You can also use Microsoft Graph SDK.
5. Build the token acquirer. This composes all the services you add and returns a service provider. Use this service provider to get access to the API resource you add. In this case, you add only one API resource as a downstream service that you want access to.

    Add the following code snippet to the *program.cs* file:

    ```csharp
    var serviceProvider = tokenAcquirerFactory.Build();
    ```

## Call the web API

1. Add code to call your protected web API using the `IDownstreamApi` interface. In this tutorial, we call a Microsoft Graph API Endpoint.
2. Add this code to the *program.cs* file:

    ```csharp
    try
    {
        IDownstreamApi downstreamApi = serviceProvider.GetRequiredService<IDownstreamApi>();
    
        var response = await downstreamApi.GetForAppAsync<HttpResponseMessage>("DownstreamApi");
        var content = await response.Content.ReadAsStringAsync();
        var statusCode = response.StatusCode;
    
        Console.WriteLine($"Response status code: {statusCode}");
    
        if (!content.Any())
        {
            Console.WriteLine("There are no users to display.");
            return;
        }
    
        Console.WriteLine(content);
    }
    catch (Exception ex) { Console.WriteLine("We could not retrieve the user's list: " + $"{ex}"); }
    ```

    The code calls the endpoint you defined in the *appsettings.json* file. The `GetForAppAsync` method of the `IDownstreamApi` interface is used to call the endpoint. The app makes a call on its own behalf. The method returns an `HttpResponseMessage` object. The response is then read as a string and displayed in the console.

## Run the client daemon app

Navigate to the root folder of the daemon app and run the following command:

```dotnetcli
dotnet run
```

If everything is okay, you should see *Response status code: OK* in your terminal. If there are users, the users are listed in the terminal, otherwise you see the message *There are no users to display*.

If any errors occur, you see an error message in the terminal.

### Troubleshoot

In case you run into errors,

- Confirm the registration details you added to the *appsettings.json* file.
- Confirm that you added the *appsettings.json* file to the project file.
- Confirm that your app permissions are configured correctly.