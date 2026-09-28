---
layout: Conceptual
title: 'Quickstart: Protect an ASP.NET Core web API with the Microsoft identity platform - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/web-api-quickstart-portal-aspnet-core
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you download and modify a code sample that demonstrates how to protect an ASP.NET Core web API by using the Microsoft identity platform for authorization.
ROBOTS: NOINDEX
manager: dougeby
ms.custom: 
ms.date: 2022-08-16T00:00:00.0000000Z
ms.topic: quickstart
locale: en-us
document_id: 882ee932-56af-18be-7808-5140e7c6a349
document_version_independent_id: 8cca1d31-51fa-26f6-8767-67263d880e55
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/web-api-quickstart-portal-aspnet-core.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/web-api-quickstart-portal-aspnet-core
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/web-api-quickstart-portal-aspnet-core.md
platformId: 262ba215-90e8-54fb-31c9-a425189af289
---

# Quickstart: Protect an ASP.NET Core web API with the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart:Protect an ASP.NET Core web API](quickstart-web-api-aspnet-core-protect-api)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

# Quickstart: Protect an ASP.NET Core web API with the Microsoft identity platform

In this quickstart, you download an ASP.NET Core web API code sample and review the way it restricts resource access to authorized accounts only. The sample supports authorization of personal Microsoft accounts and accounts in any Microsoft Entra organization.

## Prerequisites

- Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Microsoft Entra tenant](quickstart-create-new-tenant)
- A minimum requirement of [.NET 6.0 SDK](https://dotnet.microsoft.com/)
- [Visual Studio 2019](https://visualstudio.microsoft.com/vs/) or [Visual Studio Code](https://code.visualstudio.com/)

## Step 1: Register the application

First, register the web API in your Microsoft Entra tenant and add a scope by following these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select **New registration**.
4. For **Name**, enter a name for your application. For example, enter **AspNetCoreWebApi-Quickstart**. Users of your app will see this name, and you can change it later.
5. Select **Register**.
6. Under **Manage**, select **Expose an API** &gt; **Add a scope**. For **Application ID URI**, accept the default by selecting **Save and continue**, and then enter the following details:
    - **Scope name**: `access_as_user`
    - **Who can consent?**: **Admins and users**
    - **Admin consent display name**: `Access AspNetCoreWebApi-Quickstart`
    - **Admin consent description**: `Allows the app to access AspNetCoreWebApi-Quickstart as the signed-in user.`
    - **User consent display name**: `Access AspNetCoreWebApi-Quickstart`
    - **User consent description**: `Allow the application to access AspNetCoreWebApi-Quickstart on your behalf.`
    - **State**: **Enabled**
7. Select **Add scope** to complete the scope addition.

## Step 2: Download the ASP.NET Core project

[Download the ASP.NET Core solution](https://github.com/Azure-Samples/active-directory-dotnet-native-aspnetcore-v2/archive/aspnetcore3-1.zip) from GitHub.

Tip

To avoid errors caused by path length limitations in Windows, we recommend extracting the archive or cloning the repository into a directory near the root of your drive.

## Step 3: Configure the ASP.NET Core project

In this step, configure the sample code to work with the app registration that you created earlier.

1. Extract the .zip archive into a folder near the root of your drive. For example, extract into *C:\Azure-Samples*.

    We recommend extracting the archive into a directory near the root of your drive to avoid errors caused by path length limitations on Windows.
2. Open the solution in the *webapi* folder in your code editor.
3. Open the *appsettings.json* file and modify the following code:

    ```json
    "ClientId": "Enter_the_Application_Id_here",
    "TenantId": "Enter_the_Tenant_Info_Here"
    ```

    - Replace `Enter_the_Application_Id_here` with the application (client) ID of the application that you registered. You can find the application (client) ID on the app's **Overview** page.
    - Replace `Enter_the_Tenant_Info_Here`with one of the following:
        - If your application supports **Accounts in this organizational directory only**, replace this value with the directory (tenant) ID (a GUID) or tenant name (for example, `contoso.onmicrosoft.com`). You can find the directory (tenant) ID on the app's **Overview** page.
        - If your application supports **Accounts in any organizational directory**, replace this value with `organizations`.
        - If your application supports **All Microsoft account users**, leave this value as `common`.

For this quickstart, don't change any other values in the *appsettings.json* file.

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

The line that contains `.AddMicrosoftIdentityWebApi` adds the Microsoft identity platform authorization to your web API. It's then configured to validate access tokens issued by the Microsoft identity platform based on the information in the `AzureAD` section of the *appsettings.json* configuration file:

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

You can protect a controller or controller methods by using the `[Authorize]` attribute. This attribute restricts access to the controller or methods by allowing only authenticated users. An authentication challenge can be started to access the controller if the user isn't authenticated.

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