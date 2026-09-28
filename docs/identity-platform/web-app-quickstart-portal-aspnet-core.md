---
layout: Conceptual
title: 'Quickstart: Add sign-in with Microsoft Identity to an ASP.NET Core web app - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/web-app-quickstart-portal-aspnet-core
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you learn how an app implements Microsoft sign-in on an ASP.NET Core web app by using OpenID Connect
ROBOTS: NOINDEX
manager: dougeby
ms.custom: 
ms.date: 2022-08-16T00:00:00.0000000Z
ms.topic: quickstart
locale: en-us
document_id: 7662e9f6-c318-20f5-0576-2a43010f853b
document_version_independent_id: 00dddb88-1660-409e-03cf-9ed8406143a1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/web-app-quickstart-portal-aspnet-core.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/web-app-quickstart-portal-aspnet-core
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/web-app-quickstart-portal-aspnet-core.md
platformId: b4a155a0-95c3-ad1f-a352-dede40d44f86
---

# Quickstart: Add sign-in with Microsoft Identity to an ASP.NET Core web app - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Add sign-in with Microsoft to an ASP.NET Core web app](quickstart-web-app-dotnet-core-sign-in)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

# Quickstart: Add sign-in with Microsoft to an ASP.NET Core web app

In this quickstart, you download and run a code sample that demonstrates how an ASP.NET Core web app can sign in users from any Microsoft Entra organization.

### Step 1: Configure your application in the Microsoft Entra admin center

For the code sample in this quickstart to work:

- For **Redirect URI**, enter **https://localhost:44321/** and **https://localhost:44321/signin-oidc**.
- For **Front-channel logout URL**, enter **https://localhost:44321/signout-oidc**.

The authorization endpoint will issue request ID tokens.

![Already configured](media/quickstart-v2-aspnet-webapp/green-check.png) Your application is configured with these attributes.

### Step 2: Download the ASP.NET Core project

Run the project.

Tip

To avoid errors caused by path length limitations in Windows, we recommend extracting the archive or cloning the repository into a directory near the root of your drive.

#### Step 3: Your app is configured and ready to run

We've configured your project with values of your app's properties, and it's ready to run.

Note

`Enter_the_Supported_Account_Info_Here`

## More information

This section gives an overview of the code required to sign in users. This overview can be useful to understand how the code works, what the main arguments are, and how to add sign-in to an existing ASP.NET Core application.

### How the sample works

![Diagram of the interaction between the web browser, the web app, and the Microsoft identity platform in the sample app.](media/quickstart-v2-aspnet-core-webapp/aspnetcorewebapp-intro.svg)

### Startup class

The *Microsoft.AspNetCore.Authentication* middleware uses a `Startup` class that's run when the hosting process starts:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddAuthentication(OpenIdConnectDefaults.AuthenticationScheme)
        .AddMicrosoftIdentityWebApp(Configuration.GetSection("AzureAd"));

    services.AddControllersWithViews(options =>
    {
        var policy = new AuthorizationPolicyBuilder()
            .RequireAuthenticatedUser()
            .Build();
        options.Filters.Add(new AuthorizeFilter(policy));
    });
   services.AddRazorPages()
        .AddMicrosoftIdentityUI();
}
```

The `AddAuthentication()` method configures the service to add cookie-based authentication. This authentication is used in browser scenarios and to set the challenge to OpenID Connect.

The line that contains `.AddMicrosoftIdentityWebApp` adds Microsoft identity platform authentication to your application. The application is then configured to sign in users based on the following information in the `AzureAD` section of the *appsettings.json* configuration file:

| *appsettings.json*key | Description |
| --- | --- |
| `ClientId` | Application (client) ID of the application registered in the Microsoft Entra admin center. |
| `Instance` | Security token service (STS) endpoint for the user to authenticate. This value is typically `https://login.microsoftonline.com/`, indicating the Azure public cloud. |
| `TenantId` | Name of your tenant or the tenant ID (a GUID), or `common` to sign in users with work or school accounts or Microsoft personal accounts. |

The `Configure()` method contains two important methods, `app.UseAuthentication()` and `app.UseAuthorization()`, that enable their named functionality. Also in the `Configure()` method, you must register Microsoft Identity Web routes with at least one call to `endpoints.MapControllerRoute()` or a call to `endpoints.MapControllers()`:

```csharp
app.UseAuthentication();
app.UseAuthorization();

app.UseEndpoints(endpoints =>
{
    endpoints.MapControllerRoute(
        name: "default",
        pattern: "{controller=Home}/{action=Index}/{id?}");
    endpoints.MapRazorPages();
});
```

### Attribute for protecting a controller or methods

You can protect a controller or controller methods by using the `[Authorize]` attribute. This attribute restricts access to the controller or methods by allowing only authenticated users. An authentication challenge can then be started to access the controller if the user isn't authenticated.

## Help and support

If you need help, want to report an issue, or want to learn about your support options, see [Help and support for developers](developer-support-help-options).