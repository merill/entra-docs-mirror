---
layout: Conceptual
title: Configure a web API that calls web APIs - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-web-api-call-api-app-configuration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a web API that calls web APIs (app's code configuration)
manager: pmwongera
ms.custom: 
ms.date: 2024-07-19T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: 2fc5b4a3-0d85-102b-8b4c-8dfdd664b2d8
document_version_independent_id: 13086ddd-1cf0-a8ca-46f2-588e59734122
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-web-api-call-api-app-configuration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-web-api-call-api-app-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-web-api-call-api-app-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/d452572f-6212-498f-9050-ca4a9e50a425
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/a12e40b7-59a2-4437-96e2-166ce622b864
platformId: dec98fc3-d649-9c7f-9af0-a6bf7bcea763
---

# Configure a web API that calls web APIs - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This article describes how to configure code for a Web API app using the [OAuth 2.0 authorization code flow](v2-oauth2-auth-code-flow).

Microsoft recommends that you use the [Microsoft.Identity.Web](https://www.nuget.org/packages/Microsoft.Identity.Web) NuGet package when developing an ASP.NET Core protected API calling downstream web APIs. See [Protected web API: Code configuration | Microsoft.Identity.Web](scenario-protected-web-api-app-configuration#microsoftidentityweb) for a quick presentation of that library in the context of a web API.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). This account must have permissions to manage applications. Use any of the following roles needed to register the application:
    - Application Administrator
    - Application Developer
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add a client certificate to the app registration. For more information, see [Add and manage application credentials in Microsoft Entra ID](how-to-add-credentials).

## Configure the app

Choose a language for your web API.

# [ASP.NET Core](#tab/aspnetcore)
## Client secrets or client certificates

Given that your web app now calls a downstream web API, provide a client secret or client certificate in the *appsettings.json* file. You can also add a section that specifies:

- The URL of the downstream web API
- The scopes required for calling the API

In the following example, the `GraphBeta` section specifies these settings.

```JSON
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "ClientId": "[Enter_the_Application_Id_Here]",
    "TenantId": "common",

   // To call an API
   "ClientCredentials": [
    {
      "SourceType": "ClientSecret",
      "ClientSecret":"[Enter_the_Client_Secret_Here]"
    }
  ]
 },
 "GraphBeta": {
    "BaseUrl": "https://graph.microsoft.com/beta",
    "Scopes": ["user.read"]
    }
}
```

Note

You can propose a collection of client credentials, including a credential-less solution like workload identity federation for Azure Kubernetes. Previous versions of Microsoft.Identity.Web expressed the client secret in a single property "ClientSecret" instead of "ClientCredentials". This is still supported for backwards compatibility but you cannot use both the "ClientSecret" property, and the "ClientCredentials" collection.

Instead of a client secret, you can provide a client certificate. The following code snippet shows using a certificate stored in Azure Key Vault.

```JSON
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "ClientId": "[Enter_the_Application_Id_Here]",
    "TenantId": "common",

   // To call an API
   "ClientCredentials": [
      {
        "SourceType": "KeyVault",
        "KeyVaultUrl": "https://msidentitywebsamples.vault.azure.net",
        "KeyVaultCertificateName": "MicrosoftIdentitySamplesCert"
      }
   ]
  },
  "GraphBeta": {
    "BaseUrl": "https://graph.microsoft.com/beta",
    "Scopes": ["user.read"]
  }
}
```

Warning

If you forget to change the `Scopes` to an array, when you try to use the `IDownstreamApi` the scopes will appear null, and `IDownstreamApi` will attempt an anonymous (unauthenticated) call to the downstream API, which will result in a `401/unauthenticated`.

*Microsoft.Identity.Web* provides several ways to describe certificates, both by configuration or by code. For details, see [Microsoft.Identity.Web - Using certificates](https://github.com/AzureAD/microsoft-identity-web/wiki/Using-certificates) on GitHub.

## Program.cs

```csharp
using Microsoft.Identity.Web;

// ...
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddMicrosoftIdentityWebApi(Configuration, Configuration.GetSection("AzureAd"))
    .EnableTokenAcquisitionToCallDownstreamApi()
    .AddInMemoryTokenCaches();
// ...
```

A web API needs to acquire a token for the downstream API. Specify it by adding the `.EnableTokenAcquisitionToCallDownstreamApi()` line after `.AddMicrosoftIdentityWebApi(Configuration)`. This line exposes the `ITokenAcquisition` service that can be used in the controller/pages actions.

However, an alternative method is to implement a token cache. For example, adding `.AddInMemoryTokenCaches()`, to *Program.cs* allows the token to be cached in memory.

```csharp
using Microsoft.Identity.Web;

// ...
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddMicrosoftIdentityWebApi(Configuration, Configuration.GetSection("AzureAd"))
    .EnableTokenAcquisitionToCallDownstreamApi()
    .AddInMemoryTokenCaches();
// ...
```

*Microsoft.Identity.Web* provides two mechanisms for calling a downstream web API from another API. The option you choose depends on whether you want to call Microsoft Graph or another API.

### Option 1: Call Microsoft Graph

To call Microsoft Graph, *Microsoft.Identity.Web* enables you to directly use the `GraphServiceClient` (exposed by the Microsoft Graph SDK) in the API actions.

Note

There is an ongoing issue for Microsoft Graph SDK v5+. For more information, refer to the [GitHub issue](https://github.com/AzureAD/microsoft-identity-web/issues/2097).

To expose Microsoft Graph:

1. Add the [Microsoft.Identity.Web.GraphServiceClient](https://www.nuget.org/packages/Microsoft.Identity.Web.GraphServiceClient) NuGet package to the project.
2. Add `.AddMicrosoftGraph()` after `.EnableTokenAcquisitionToCallDownstreamApi()` in *Program.cs*. `.AddMicrosoftGraph()` has several overrides. Using the override that takes a configuration section as a parameter, the code becomes:

```csharp
using Microsoft.Identity.Web;

// ...
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddMicrosoftIdentityWebApi(Configuration, Configuration.GetSection("AzureAd"))
    .EnableTokenAcquisitionToCallDownstreamApi()
    .AddMicrosoftGraph(Configuration.GetSection("GraphBeta"))
    .AddInMemoryTokenCaches();
// ...
```

### Option 2: Call a downstream web API other than Microsoft Graph

1. Add the [Microsoft.Identity.Web.DownstreamApi](https://www.nuget.org/packages/Microsoft.Identity.Web.DownstreamApi) NuGet package to the project.
2. Add `.AddDownstreamApi()` after `.EnableTokenAcquisitionToCallDownstreamApi()` in *Program.cs*. The code becomes:

```csharp
using Microsoft.Identity.Web;

// ...
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddMicrosoftIdentityWebApi(Configuration, "AzureAd")
    .EnableTokenAcquisitionToCallDownstreamApi()
    .AddDownstreamApi("MyApi", Configuration.GetSection("MyApiScope"))
    .AddInMemoryTokenCaches();
// ...
```

where;

- `MyApi` denotes the name of the downstream web API that your web API intends to call
- `MyApiScope` is the scope necessary for your web API to request in order to interact with the downstream web API

These values will be represented in your JSON that will be similar to the following snippet.

```json
"DownstreamAPI": {
      "BaseUrl": "https://downstreamapi.contoso.com/",
      "Scopes": "user.read"
    },
```

If the web app needs to call another API resource, repeat the `.AddDownstreamApi()` method with the relevant scope as shown in the following snippet:

```csharp
using Microsoft.Identity.Web;

// ...
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddMicrosoftIdentityWebApi(Configuration, "AzureAd")
    .EnableTokenAcquisitionToCallDownstreamApi()
    .AddDownstreamApi("MyApi", Configuration.GetSection("MyApiScope"))
    .AddDownstreamApi("MyApi2", Configuration.GetSection("MyApi2Scope"))
    .AddInMemoryTokenCaches();
// ...
```

Note that `.EnableTokenAcquisitionToCallDownstreamApi` is called without any parameter, which means that the access token is acquired just in time as the controller requests the token by specifying the scope.

The scope can also be passed in when calling `.EnableTokenAcquisitionToCallDownstreamApi`, which would make the web app acquire the token during the initial user login itself. The token will then be pulled from the cache when controller requests it.

Similar to web apps, various token cache implementations can be chosen. For details, see [Microsoft identity web - Token cache serialization](https://aka.ms/ms-id-web/token-cache-serialization) on GitHub.

The following image shows the possibilities of *Microsoft.Identity.Web* and the impact on *Program.cs*:

![Block diagram showing service configuration options in startup dot C S for calling a web API and specifying a token cache implementation](media/scenarios/microsoft-identity-web-startup-cs.svg)

Note

To fully understand the code examples here, be familiar with [ASP.NET Core fundamentals](/en-us/aspnet/core/fundamentals/), and in particular with [dependency injection](/en-us/aspnet/core/fundamentals/dependency-injection) and [options](/en-us/aspnet/core/fundamentals/configuration/options).

# [ASP.NET](#tab/aspnet)
## Client secrets or client certificates

Given that your web app now calls a downstream web API, provide a client secret or client certificate in the *appsettings.json* file. You can also add a section that specifies:

- The URL of the downstream web API
- The scopes required for calling the API

In the following example, the `GraphBeta` section specifies these settings.

```JSON
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "ClientId": "[Enter_the_Application_Id_Here]",
    "TenantId": "common",

   // To call an API
   "ClientCredentials": [
    {
      "SourceType": "ClientSecret",
      "ClientSecret":"[Enter_the_Client_Secret_Here]"
    }
  ]
 },
 "GraphBeta": {
    "BaseUrl": "https://graph.microsoft.com/beta",
    "Scopes": ["user.read"]
    }
}
```

Note

You can propose a collection of client credentials, including a credential-less solution like workload identity federation for Azure Kubernetes. Previous versions of Microsoft.Identity.Web expressed the client secret in a single property "ClientSecret" instead of "ClientCredentials". This is still supported for backwards compatibility but you cannot use both the "ClientSecret" property, and the "ClientCredentials" collection.

Instead of a client secret, you can provide a client certificate. The following code snippet shows using a certificate stored in Azure Key Vault.

```JSON
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "ClientId": "[Enter_the_Application_Id_Here]",
    "TenantId": "common",

   // To call an API
   "ClientCredentials": [
      {
        "SourceType": "KeyVault",
        "KeyVaultUrl": "https://msidentitywebsamples.vault.azure.net",
        "KeyVaultCertificateName": "MicrosoftIdentitySamplesCert"
      }
   ]
  },
  "GraphBeta": {
    "BaseUrl": "https://graph.microsoft.com/beta",
    "Scopes": ["user.read"]
  }
}
```

Warning

If you forget to change the `Scopes` to an array, when you try to use the `IDownstreamApi` the scopes will appear null, and `IDownstreamApi` will attempt an anonymous (unauthenticated) call to the downstream API, which will result in a `401/unauthenticated`.

*Microsoft.Identity.Web* provides several ways to describe certificates, both by configuration or by code. For details, see [Microsoft.Identity.Web - Using certificates](https://github.com/AzureAD/microsoft-identity-web/wiki/Using-certificates) on GitHub.

## Modify *Startup.Auth.cs*

Your web app needs to acquire a token for the downstream API, *Microsoft.Identity.Web* provides two mechanisms for calling a downstream API from a web API. The option you choose depends on whether you want to call Microsoft Graph or another API.

### Option 1: Call Microsoft Graph

If you want to call Microsoft Graph, *Microsoft.Identity.Web* enables you to directly use the `GraphServiceClient` (exposed by the Microsoft Graph SDK) in your API actions. To expose Microsoft Graph:

1. Add the [Microsoft.Identity.Web.GraphServiceClient](https://www.nuget.org/packages/Microsoft.Identity.Web.GraphServiceClient) NuGet package to your project.
2. Add `.AddMicrosoftGraph()` to the service collection in the *Startup.Auth.cs* file. `.AddMicrosoftGraph()` has several overrides. Using the override that takes a configuration section as a parameter, the code becomes:

    ```csharp
    using Microsoft.Extensions.DependencyInjection;
    using Microsoft.Identity.Client;
    using Microsoft.Identity.Web;
    using Microsoft.Identity.Web.OWIN;
    using Microsoft.Identity.Web.TokenCacheProviders.InMemory;
    using Microsoft.IdentityModel.Validators;
    using Microsoft.Owin.Security;
    using Microsoft.Owin.Security.Cookies;
    using Owin;
    
    namespace WebApp
    {
       public partial class Startup
       {
           public void ConfigureAuth(IAppBuilder app)
           {
               app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
    
               app.UseCookieAuthentication(new CookieAuthenticationOptions());
    
               // Get an TokenAcquirerFactory specialized for OWIN
               OwinTokenAcquirerFactory owinTokenAcquirerFactory = TokenAcquirerFactory.GetDefaultInstance<OwinTokenAcquirerFactory>();
    
               // Configure the web app.
               app.AddMicrosoftIdentityWebApi(owinTokenAcquirerFactory);
    
               // Add the services you need.
               owinTokenAcquirerFactory.Services
                   .AddMicrosoftGraph()
                   .AddInMemoryTokenCaches();
               owinTokenAcquirerFactory.Build();
           }
       }
    }
    ```

### Option 2: Call a downstream web API other than Microsoft Graph

If you want to call an API other than Microsoft Graph, *Microsoft.Identity.Web* enables you to use the `IDownstreamApi` interface in your API actions. To use this interface:

1. Add the [Microsoft.Identity.Web.DownstreamApi](https://www.nuget.org/packages/Microsoft.Identity.Web.DownstreamApi) NuGet package to your project.
2. Add `.AddDownstreamApi()` after `.EnableTokenAcquisitionToCallDownstreamApi()` in the *Startup.cs* file. `.AddDownstreamApi()`has two arguments:
    - The name of a service (API): you use this name in your controller actions to reference the corresponding configuration
    - a configuration section representing the parameters used to call the downstream web API.

Here's the code:

```csharp
  using Microsoft.Extensions.DependencyInjection;
  using Microsoft.Identity.Client;
  using Microsoft.Identity.Web;
  using Microsoft.Identity.Web.OWIN;
  using Microsoft.Identity.Web.TokenCacheProviders.InMemory;
  using Microsoft.IdentityModel.Validators;
  using Microsoft.Owin.Security;
  using Microsoft.Owin.Security.Cookies;
  using Owin;

  namespace WebApp
  {
      public partial class Startup
      {
          public void ConfigureAuth(IAppBuilder app)
          {
              app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

              app.UseCookieAuthentication(new CookieAuthenticationOptions());

              // Get a TokenAcquirerFactory specialized for OWIN.
              OwinTokenAcquirerFactory owinTokenAcquirerFactory = TokenAcquirerFactory.GetDefaultInstance<OwinTokenAcquirerFactory>();

              // Configure the web app.
              app.AddMicrosoftIdentityWebApi(owinTokenAcquirerFactory);

              // Add the services you need.
              owinTokenAcquirerFactory.Services
                  .AddDownstreamApi("Graph", owinTokenAcquirerFactory.Configuration.GetSection("GraphBeta"))
                  .AddInMemoryTokenCaches();
              owinTokenAcquirerFactory.Build();
          }
      }
  }
```

# [Java](#tab/java)
## Using on-behalf-of (OBO) flow

The on-behalf-of (OBO) flow is used to obtain a token to call the downstream web API. In this flow, your web API receives a bearer token with user delegated permissions from the client application and then exchanges this token for another access token to call the downstream web API.

The code below uses Spring Security framework's `SecurityContextHolder` in the web API to get the validated bearer token. It then uses the MSAL Java library to obtain a token for downstream API using the `acquireToken` call with `OnBehalfOfParameters`. MSAL caches the token so that subsequent calls to the API can use `acquireTokenSilently` to get the cached token.

```java
@Component
class MsalAuthHelper {

    @Value("${security.oauth2.client.authority}")
    private String authority;

    @Value("${security.oauth2.client.client-id}")
    private String clientId;

    @Value("${security.oauth2.client.client-secret}")
    private String secret;

    @Autowired
    CacheManager cacheManager;

    private String getAuthToken(){
        String res = null;
        Authentication authentication = SecurityContextHolder.getContext().getAuthentication();

        if(authentication != null){
            res = ((OAuth2AuthenticationDetails) authentication.getDetails()).getTokenValue();
        }
        return res;
    }

    String getOboToken(String scope) throws MalformedURLException {
        String authToken = getAuthToken();

        ConfidentialClientApplication application =
                ConfidentialClientApplication.builder(clientId, ClientCredentialFactory.create(secret))
                        .authority(authority).build();

        String cacheKey = Hashing.sha256()
                .hashString(authToken, StandardCharsets.UTF_8).toString();

        String cachedTokens = cacheManager.getCache("tokens").get(cacheKey, String.class);
        if(cachedTokens != null){
            application.tokenCache().deserialize(cachedTokens);
        }

        IAuthenticationResult auth;
        SilentParameters silentParameters =
                SilentParameters.builder(Collections.singleton(scope))
                        .build();
        auth = application.acquireTokenSilently(silentParameters).join();

        if (auth == null){
            OnBehalfOfParameters parameters =
                    OnBehalfOfParameters.builder(Collections.singleton(scope),
                            new UserAssertion(authToken))
                            .build();

            auth = application.acquireToken(parameters).join();
        }

        cacheManager.getCache("tokens").put(cacheKey, application.tokenCache().serialize());

        return auth.accessToken();
    }
}
```

# [Python](#tab/python)
## Using on-behalf-of (OBO) flow

The on-behalf-of (OBO) flow is used to obtain a token to call the downstream web API. In this flow, your web API receives a bearer token with user delegated permissions from the client application and then exchanges this token for another access token to call the downstream web API.

A Python web API needs to use some middleware to validate the bearer token received from the client. The web API can then obtain the access token for downstream API using MSAL Python library by calling the [`acquire_token_on_behalf_of`](https://msal-python.readthedocs.io/en/latest/?badge=latest#msal.ConfidentialClientApplication.acquire_token_on_behalf_of) method. For an example of using this API, see the [test code for the microsoft-authentication-library-for-python on GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-python/blob/1.2.0/tests/test_e2e.py#L429-L472). Also see the discussion of [issue 53](https://github.com/AzureAD/microsoft-authentication-library-for-python/issues/53) in that same repository for an approach that bypasses the need for a middle-tier application.

You can also see an example of the OBO flow implementation in the [ms-identity-python-on-behalf-of](https://github.com/Azure-Samples/ms-identity-python-on-behalf-of) sample.

---

You can also see an example of OBO flow implementation in [Node.js and Azure Functions](https://github.com/Azure-Samples/ms-identity-nodejs-webapi-onbehalfof-azurefunctions/blob/master/Function/MyHttpTrigger/index.js#L61).

## Protocol

For more information about the OBO protocol, see the [Microsoft identity platform and OAuth 2.0 On-Behalf-Of flow](v2-oauth2-on-behalf-of-flow).