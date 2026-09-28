---
layout: Conceptual
title: 'Quickstart: Protect an ASP.NET Core web API with the Microsoft identity platform - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-v2-aspnet-core-web-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you download and modify a code sample that demonstrates how to protect an ASP.NET Core web API by using the Microsoft identity platform for authorization.
ROBOTS: NOINDEX
manager: pmwongera
ms.custom: 
ms.date: 2025-04-16T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: quickstart
locale: en-us
document_id: d6102ebf-9a84-413b-81f9-711f7e2ff9e1
document_version_independent_id: 1a6dcb5b-cd4b-a09e-15ea-953cddf109f1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-v2-aspnet-core-web-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-v2-aspnet-core-web-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-v2-aspnet-core-web-api.md
platformId: cd91fec4-611d-6299-d03b-377bc88b8348
---

# Quickstart: Protect an ASP.NET Core web API with the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Call an ASP.NET Core web API that is protected by the Microsoft identity platform](quickstart-web-api-aspnet-protect-api)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

The following quickstart uses a ASP.NET Core web API code sample to demonstrate how to restrict resource access to authorized accounts. The sample supports authorization of personal Microsoft accounts and accounts in any Microsoft Entra organization.

## Prerequisites

- Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Microsoft Entra tenant](quickstart-create-new-tenant)
- A minimum requirement of [.NET 6.0 SDK](https://dotnet.microsoft.com/download/dotnet)
- [Visual Studio 2022](https://visualstudio.microsoft.com/vs/) or [Visual Studio Code](https://code.visualstudio.com/)

## Step 1: Register the application

First, register the web API in your Microsoft Entra tenant and add a scope by following these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select **New registration**.
4. For **Name**, enter a name for the application. For example, enter **AspNetCoreWebApi-Quickstart**. Users of the app will see this name, and can be changed later.
5. Select **Register**.
6. Under **Manage**, select **Expose an API** &gt; **Add a scope**. For **Application ID URI**, accept the default by selecting **Save and continue**, and then enter the following details:

- **Scope name**: `access_as_user`
- **Who can consent?**: **Admins and users**
- **Admin consent display name**: `Access AspNetCoreWebApi-Quickstart`
- **Admin consent description**: `Allows the app to access AspNetCoreWebApi-Quickstart as the signed-in user.`
- **User consent display name**: `Access AspNetCoreWebApi-Quickstart`
- **User consent description**: `Allow the application to access AspNetCoreWebApi-Quickstart on your behalf.`
- **State**: **Enabled**

1. Select **Add scope** to complete the scope addition.

## Step 2: Download the ASP.NET Core project

[Download the ASP.NET Core solution](https://github.com/Azure-Samples/active-directory-dotnet-native-aspnetcore-v2/archive/aspnetcore3-1.zip) from GitHub.

Note

The code sample currently targets ASP.NET Core 3.1. The sample can be updated to use .NET Core 6.0 and is covered in the following steps: Update the sample code to ASP.NET Core 6.0. This quickstart will be deprecated in the near future and will be updated to use .NET 6.0.

## Step 3: Configure the ASP.NET Core project

In this step, the sample code will be configured to work with the app registration that was created earlier.

1. Extract the *.zip* file to a local folder that's close to the root of the disk to avoid errors caused by path length limitations on Windows. For example, extract to *C:\Azure-Samples*.
2. Open the solution in the *webapi* folder in your code editor.
3. In *appsettings.json*, replace the values of `ClientId`, and `TenantId`.

    ```json
    "ClientId": "Enter_the_Application_Id_here",
    "TenantId": "Enter_the_Tenant_Info_Here"
    ```

    - `Enter_the_Application_Id_Here` is the application (client) ID for the registered application.
    - Replace `Enter_the_Tenant_Info_Here`with one of the following:
        - If the application supports **Accounts in this organizational directory only**, replace this value with the directory (tenant) ID (a GUID) or tenant name (for example, `contoso.onmicrosoft.com`). The directory (tenant) ID can be found on the app's **Overview** page.
        - If the application supports **Accounts in any organizational directory**, replace this value with `organizations`.
        - If the application supports **All Microsoft account users**, leave this value as `common`.

For this quickstart, don't change any other values in the *appsettings.json* file.

### Step 4: Update the sample code to ASP.NET Core 6.0

To update this code sample to target ASP.NET Core 6.0, follow these steps:

1. Open webapi.csproj
2. Remove the following line:

```xml
<TargetFramework>netcoreapp3.1</TargetFramework>
```

1. Add the following line in its place:

```xml
<TargetFramework>netcoreapp6.0</TargetFramework>
```

This step will ensure that the sample is targeting the .NET Core 6.0 framework.

### Step 5: Run the sample

1. Open a terminal and change directory to the project folder.

    ```powershell
    cd webapi
    ```
2. Run the following command to build the solution:

```powershell
dotnet run
```

If the build has been successful, the following output is displayed:

```powershell
Building...
info: Microsoft.Hosting.Lifetime[0]
    Now listening on: https://localhost:{port}
info: Microsoft.Hosting.Lifetime[0]
    Now listening on: http://localhost:{port}
info: Microsoft.Hosting.Lifetime[0]
    Application started. Press Ctrl+C to shut down.
...
```

## How the sample works

### Startup class

The *Microsoft.AspNetCore.Authentication* middleware uses a `Startup` class that's executed when the hosting process starts. In its `ConfigureServices` method, the `AddMicrosoftIdentityWebApi` extension method provided by *Microsoft.Identity.Web* is called.

```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
                .AddMicrosoftIdentityWebApi(Configuration, "AzureAd");
    }
```

The `AddAuthentication()` method configures the service to add JwtBearer-based authentication.

The line that contains `.AddMicrosoftIdentityWebApi` adds the Microsoft identity platform authorization to the web API. It's then configured to validate access tokens issued by the Microsoft identity platform based on the information in the `AzureAD` section of the *appsettings.json* configuration file:

| *appsettings.json*key | Description |
| --- | --- |
| `ClientId` | Application (client) ID of the application registered. |
| `Instance` | Security token service (STS) endpoint for the user to authenticate. This value is typically `https://login.microsoftonline.com/`, indicating the Azure public cloud. |
| `TenantId` | Name of your tenant or its tenant ID (a GUID), or `common` to sign in users with work or school accounts or Microsoft personal accounts. |

The `Configure()` method contains two important methods, `app.UseAuthentication()` and `app.UseAuthorization()`, that enable their named functionality:

```csharp
// The runtime calls this method. Use this method to configure the HTTP request pipeline.
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    // more code
    app.UseAuthentication();
    app.UseAuthorization();
    // more code
}
```

### Protecting a controller, a controller's method, or a Razor page

A controller or controller methods can be protected by using the `[Authorize]` attribute. This attribute restricts access to the controller or methods by allowing only authenticated users. An authentication challenge can be started to access the controller if the user isn't authenticated.

```csharp
namespace webapi.Controllers
{
    [Authorize]
    [ApiController]
    [Route("[controller]")]
    public class WeatherForecastController : ControllerBase
```

### Validation of scope in the controller

The code in the API verifies that the required scopes are in the token by using `HttpContext.VerifyUserHasAnyAcceptedScope> (scopeRequiredByApi);`:

```csharp
namespace webapi.Controllers
{
    [Authorize]
    [ApiController]
    [Route("[controller]")]
    public class WeatherForecastController : ControllerBase
    {
        // The web API will only accept tokens 1) for users, and 2) having the "access_as_user" scope for this API
        static readonly string[] scopeRequiredByApi = new string[] { "access_as_user" };

        [HttpGet]
        public IEnumerable<WeatherForecast> Get()
        {
            HttpContext.VerifyUserHasAnyAcceptedScope(scopeRequiredByApi);

            // some code here
        }
    }
}
```

## Help and support

If you need help, want to report an issue, or want to learn about your support options, see [Help and support for developers](developer-support-help-options).