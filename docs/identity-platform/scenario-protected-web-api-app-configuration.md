---
layout: Conceptual
title: Configure protected web API apps - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-protected-web-api-app-configuration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a protected web API and configure your application's code.
manager: pmwongera
ms.date: 2025-04-14T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: 906f1086-776e-9abe-b6cc-bf93e84dc238
document_version_independent_id: 50b27c9e-8f8a-3425-a1bb-b5d30e9d95e4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-protected-web-api-app-configuration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-protected-web-api-app-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-protected-web-api-app-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d452572f-6212-498f-9050-ca4a9e50a425
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/43ab1a66-ffe1-45dd-a4cb-6580218ef802
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a12e40b7-59a2-4437-96e2-166ce622b864
- https://authoring-docs-microsoft.poolparty.biz/devrel/bbc4fbf6-70c4-4d12-b47f-9360080c4977
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 492ebf04-3c87-cf42-8cc4-b00c7b07ec98
---

# Configure protected web API apps - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

To configure the code for your protected web API, understand:

- What defines APIs as protected.
- How to configure a bearer token.
- How to validate the token.

## Accepted token version

The Microsoft identity platform can issue v1.0 tokens and v2.0 tokens. For more information about these tokens, refer to [Access tokens](/en-us/entra/identity-platform/access-tokens).

The token version your API may accept depends on your **Supported account types** selection when you create your web API application registration in the Azure portal.

- If the value of **Supported account types** is **Accounts in any organizational directory and personal Microsoft accounts (such as Skype, Xbox, Outlook.com)**, the accepted token version must be v2.0.
- Otherwise, the accepted token version can be v1.0.

After you create the application, you can determine or change the accepted token version by following these steps:

1. In the Microsoft Entra admin center, select your app and then select **Manifest**.
2. Find the property **accessTokenAcceptedVersion** in the manifest.
3. The value specifies to Microsoft Entra which token version the web API accepts.
    - If the value is 2, the web API accepts v2.0 tokens.
    - If the value is **null**, the web API accepts v1.0 tokens.
4. If you changed the token version, select **Save**.

The web API specifies which token version it accepts. When a client requests a token for your web API from the Microsoft identity platform, the client gets a token that indicates which token version the web API accepts.

## What defines ASP.NET and ASP.NET Core APIs as protected?

Like web apps, ASP.NET and ASP.NET Core web APIs are protected because their controller actions are prefixed with the **[Authorize]** attribute. The controller actions can be called only if the API is called with an authorized identity.

Consider the following questions:

- Only an app can call a web API. How does the API know the identity of the app that calls it?
- If the app calls the API on behalf of a user, what's the user's identity?

## Bearer token

The bearer token that's set in the header when the app is called holds information about the app identity. It also holds information about the user unless the web app accepts service-to-service calls from a daemon app.

Here's a C# code example that shows a client calling the API after it acquires a token with the Microsoft Authentication Library for .NET (MSAL.NET):

```csharp
var scopes = new[] {$"api://.../access_as_user"};
var result = await app.AcquireToken(scopes)
                      .ExecuteAsync();

httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

// Call the web API.
HttpResponseMessage response = await _httpClient.GetAsync(apiUri);
```

Important

A client application requests the bearer token to the Microsoft identity platform *for the web API*. The API is the only application that should verify the token and view the claims it contains. Client apps should never try to inspect the claims in tokens.

In the future, the web API might require that the token be encrypted. This requirement would prevent access for client apps that can view access tokens.

## JwtBearer configuration

This section describes how to configure a bearer token.

### Config file

You need to specify the `TenantId` only if you want to accept access tokens from a single tenant (line-of-business app). Otherwise, it can be left as `common`. The different values can be:

- A GUID (Tenant ID = Directory ID)
- `common` can be any organization and personal accounts
- `organizations` can be any organization
- `consumers` are Microsoft personal accounts

```Json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "ClientId": "Enter_the_Application_(client)_ID_here",
    "TenantId": "common"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

#### Using a custom App ID URI for a web API

If you've accepted the default App ID URI proposed by the Azure portal, you don't need to specify the audience. Otherwise, add an `Audience` property whose value is the App ID URI for your web API. This typically starts with `api://`.

```Json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "ClientId": "Enter_the_Application_(client)_ID_here",
    "TenantId": "common",
    "Audience": "Enter_the_Application_ID_URI_here"
  },
}
```

### Code initialization

When an app is called on a controller action that holds an **[Authorize]** attribute, ASP.NET and ASP.NET Core extract the access token from the Authorization header's bearer token. The access token is then forwarded to the JwtBearer middleware, which calls Microsoft IdentityModel Extensions for .NET.

#### Microsoft.Identity.Web

# [ASP.NET Core](#tab/aspnetcore)
Microsoft recommends you use the [Microsoft.Identity.Web](https://www.nuget.org/packages/Microsoft.Identity.Web) NuGet package when developing a web API with ASP.NET Core.

*Microsoft.Identity.Web* provides the glue between ASP.NET Core, the authentication middleware, and the [Microsoft Authentication Library (MSAL)](msal-overview) for .NET. It allows for a clearer, more robust developer experience and leverages the power of the Microsoft identity platform and Azure AD B2C.

#### ASP.NET for .NET 6.0

To create a new web API project that uses Microsoft.Identity.Web, use a project template in the .NET 6.0 CLI or Visual Studio.

**Dotnet core CLI**

```dotnetcli
# Create new web API that uses Microsoft.Identity.Web
dotnet new webapi --auth SingleOrg
```

**Visual Studio** - To create a web API project in Visual Studio, select **File** &gt; **New** &gt; **Project** &gt; **ASP.NET Core Web API**.

Both the .NET CLI and Visual Studio project templates create a *Program.cs* file that looks similar to this code snippet. Notice `Microsoft.Identity.Web` using directive and the lines containing authentication and authorization.

```csharp
using Microsoft.AspNetCore.Authentication;
using Microsoft.AspNetCore.Authentication.JwtBearer;
using Microsoft.Identity.Web;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddMicrosoftIdentityWebApi(builder.Configuration.GetSection("AzureAd"));

builder.Services.AddControllers();
// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();

app.UseAuthentication();
app.UseAuthorization();

app.MapControllers();

app.Run();
```

# [ASP.NET](#tab/aspnet)
Microsoft recommends you use the [Microsoft.Identity.Web.OWIN](https://www.nuget.org/packages/Microsoft.Identity.Web.OWIN) NuGet package when developing a web API with ASP.NET.

*Microsoft.Identity.Web.OWIN* provides the glue between ASP.NET, the ASP.NET authentication middleware, and the [Microsoft Authentication Library (MSAL)](msal-overview) for .NET. It allows for a clearer, more robust developer experience and leverages the power of the Microsoft identity platform and Azure AD B2C.

It uses the same configuration file as ASP.NET Core (appsettings.json) and you need to make sure that this file is copied with the output of your project (property copy always in the file properties in Visual Studio or in the .csproj)

*Microsoft.Identity.Web.OWIN* adds an extension methods to IAppBuilder named `AddMicrosoftIdentityWebApi`. These method takes as a parameter an instance of `OwinTokenAcquirerFactory` that you get calling `OwinTokenAcquirerFactory.GetDefaultInstance<OwinTokenAcquirerFactory>()` and that surfaces an instance of `IServiceCollection` to which you can add many services to call downstream APIs or configure the token cache.

Here is some sample code for [Startup.Auth.cs](https://github.com/AzureAD/microsoft-identity-web/blob/master/tests/DevApps/aspnet-mvc/OwinWebApp/App_Start/Startup.Auth.cs). The full code is available from [tests/DevApps/aspnet-mvc/OwinWebApp](https://github.com/AzureAD/microsoft-identity-web/tree/master/tests/DevApps/aspnet-mvc/OwinWebApp)

```CSharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Owin;
using Microsoft.Identity.Web;
using Microsoft.Identity.Web.TokenCacheProviders.InMemory;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Identity.Client;
using Microsoft.Identity.Abstractions;
using Microsoft.Identity.Web.OWIN;
using System.Web.Services.Description;

namespace OwinWebApp
{
    public partial class Startup
    {
        public void ConfigureAuth(IAppBuilder app)
        {
            app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
            app.UseCookieAuthentication(new CookieAuthenticationOptions());

            OwinTokenAcquirerFactory factory = TokenAcquirerFactory.GetDefaultInstance<OwinTokenAcquirerFactory>();

            app.AddMicrosoftIdentityWebApp(factory);
            factory.Services
                .Configure<ConfidentialClientApplicationOptions>(options => { options.RedirectUri = "https://localhost:44386/"; })
                .AddMicrosoftGraph()
                .AddDownstreamApi("DownstreamAPI1", factory.Configuration.GetSection("DownstreamAPI"))
                .AddInMemoryTokenCaches();
            factory.Build();
        }
    }
}
```

--

## Token validation

In the preceding snippet, the JwtBearer middleware, like the OpenID Connect middleware in web apps, validates the token based on the value of `TokenValidationParameters`. The token is decrypted as needed, the claims are extracted, and the signature is verified. The middleware then validates the token by checking for this data:

- Audience: The token is targeted for the web API.
- Sub: It was issued for an app that's allowed to call the web API.
- Issuer: It was issued by a trusted security token service (STS).
- Expiry: Its lifetime is in range.
- Signature: It wasn't tampered with.

There can also be special validations. For example, it's possible to validate that signing keys, when embedded in a token, are trusted and that the token isn't being replayed. Finally, some protocols require specific validations.

### Validators

The validation steps are captured in validators, which are provided by the [Microsoft IdentityModel Extensions for .NET](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) open-source library. The validators are defined in the library source file [Microsoft.IdentityModel.Tokens/Validators.cs](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet/blob/master/src/Microsoft.IdentityModel.Tokens/Validators.cs).

This table describes the validators:

| Validator | Description |
| --- | --- |
| **ValidateAudience** | Ensures the token is for the application that validates the token for you. |
| **ValidateIssuer** | Ensures the token was issued by a trusted STS, meaning it's from someone you trust. |
| **ValidateIssuerSigningKey** | Ensures the application validating the token trusts the key that was used to sign the token. There's a special case where the key is embedded in the token. But this case doesn't usually arise. |
| **ValidateLifetime** | Ensures the token is still or already valid. The validator checks if the lifetime of the token is in the range specified by the **notbefore** and **expires** claims. |
| **ValidateSignature** | Ensures the token hasn't been tampered with. |
| **ValidateTokenReplay** | Ensures the token isn't replayed. There's a special case for some onetime-use protocols. |

#### Customizing token validation

The validators are associated with properties of the *TokenValidationParameters* class. The properties are initialized from the ASP.NET and ASP.NET Core configuration.

In most cases, you don't need to change the parameters. Apps that aren't single tenants are exceptions. These web apps accept users from any organization or from personal Microsoft accounts. Issuers in this case must be validated. Microsoft.Identity.Web takes care of the issuer validation as well.

In ASP.NET Core, if you want to customize the token validation parameters, use the following snippet in your *Startup.cs*:

```c
services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
        .AddMicrosoftIdentityWebApi(Configuration);
services.Configure<JwtBearerOptions>(JwtBearerDefaults.AuthenticationScheme, options =>
{
  options.TokenValidationParameters.ValidAudiences = new[] { /* list of valid audiences */};
});
```

For ASP.NET MVC, the following code sample shows how to do custom token validation:

https://github.com/azure-samples/active-directory-dotnet-webapi-manual-jwt-validation

## Token validation in Azure Functions

You can also validate incoming access tokens in Azure Functions. You can find examples of such validation in the following code samples on GitHub:

- .NET: [Azure-Samples/ms-identity-dotnet-webapi-azurefunctions](https://github.com/Azure-Samples/ms-identity-dotnet-webapi-azurefunctions)
- Node.js: [Azure-Samples/ms-identity-nodejs-webapi-azurefunctions](https://github.com/Azure-Samples/ms-identity-nodejs-webapi-azurefunctions)
- Python: [Azure-Samples/ms-identity-python-webapi-azurefunctions)](https://github.com/Azure-Samples/ms-identity-python-webapi-azurefunctions)

---