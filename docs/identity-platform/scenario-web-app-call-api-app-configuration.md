---
layout: Conceptual
title: Configure a web app that calls web APIs - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-web-app-call-api-app-configuration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure the code of a web app that calls web APIs
manager: pmwongera
ms.date: 2024-07-19T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
ms.custom: sfi-ropc-nochange
locale: en-us
document_id: f81a334a-eccc-b862-1a45-e58d151b8621
document_version_independent_id: cee85377-c930-2e20-715d-004e5431a92f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-web-app-call-api-app-configuration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-web-app-call-api-app-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-web-app-call-api-app-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 59749198-520f-b438-cab1-4da4c2f0a31c
---

# Configure a web app that calls web APIs - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This article will show you how to configure the application code, and modify your web app so that it not only signs users in but also now calls web APIs. The application you create uses the [OAuth 2.0 authorization code flow](v2-oauth2-auth-code-flow) to sign the user in. This flow has two steps:

1. Request an authorization code. This part delegates a private dialogue with the user to the Microsoft identity platform. During that dialogue, the user signs in and consents to the use of web APIs. When the private dialogue ends successfully, the web app receives an authorization code on its redirect URI.
2. Request an access token for the API by redeeming the authorization code.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). This account must have permissions to manage applications. Use any of the following roles needed to register the application:
    - Application Administrator
    - Application Developer
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID

## Microsoft libraries supporting web apps

The following Microsoft libraries support web apps:

| Language / framework | Project onGitHub | Package | Gettingstarted | Sign in users | Access web APIs | Generally available (GA)*or*Public preview^1^ |
| --- | --- | --- | --- | --- | --- | --- |
| .NET | [MSAL.NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client) | — | ![Library cannot request ID tokens for user sign-in.](media/common/no.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| .NET | [Microsoft.IdentityModel](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | [Microsoft.IdentityModel](https://www.nuget.org/packages?q=Microsoft.IdentityModel) | — | ![Library cannot request ID tokens for user sign-in.](media/common/no.png)^2^ | ![Library cannot request access tokens for protected web APIs.](media/common/no.png)^2^ | GA |
| ASP.NET Core | [Microsoft.Identity.Web](https://github.com/AzureAD/microsoft-identity-web) | [Microsoft.Identity.Web](https://www.nuget.org/packages/Microsoft.Identity.Web) | [Quickstart](quickstart-web-app-dotnet-core-sign-in) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Java | [MSAL4J](https://github.com/AzureAD/microsoft-authentication-library-for-java) | [msal4j](https://central.sonatype.com/artifact/com.microsoft.azure/msal4j) | [Quickstart](quickstart-web-app-java-sign-in) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Spring | [spring-cloud-azure-starter-active-directory](https://github.com/Azure/azure-sdk-for-java/tree/spring-cloud-azure-autoconfigure_4.3.0/sdk/spring/spring-cloud-azure-starter-active-directory) | [spring-cloud-azure-starter-active-directory](https://central.sonatype.com/artifact/com.azure.spring/spring-cloud-azure-starter-active-directory) | [Tutorial](/en-us/azure/developer/java/spring-framework/configure-spring-boot-starter-java-app-with-azure-active-directory) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Node.js | [MSAL Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) | [msal-node](https://www.npmjs.com/package/@azure/msal-node) | [Quickstart](quickstart-web-app-nodejs-sign-in) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Python | [MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python) | [msal](https://pypi.org/project/msal) | — | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Python | [identity](https://github.com/rayluo/identity) | [identity](https://pypi.org/project/identity/) | [Quickstart](quickstart-web-app-python-flask) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | -- |

^(1)^[Universal License Terms for Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) apply to libraries in *Public preview*.

^(2)^ The [Microsoft.IdentityModel](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) library only *validates* tokens - it can't request ID or access tokens.

Select the tab for the platform you're interested in:

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

## Modify the *Startup.cs* file

Your web app needs to acquire a token for the downstream API. You specify it by adding the `.EnableTokenAcquisitionToCallDownstreamApi()` line after `.AddMicrosoftIdentityWebApp(Configuration)`. This line exposes the `IAuthorizationHeaderProvider` service that you can use in your controller and page actions. However, as you see in the following two options, it can be done more simply. You also need to choose a token cache implementation, for example `.AddInMemoryTokenCaches()`, in *Startup.cs*:

```csharp
using Microsoft.Identity.Web;

public class Startup
{
  // ...
  public void ConfigureServices(IServiceCollection services)
  {
  // ...
  services.AddAuthentication(OpenIdConnectDefaults.AuthenticationScheme)
          .AddMicrosoftIdentityWebApp(Configuration, "AzureAd")
            .EnableTokenAcquisitionToCallDownstreamApi(new string[]{"user.read" })
            .AddInMemoryTokenCaches();
   // ...
  }
  // ...
}
```

The scopes passed to `EnableTokenAcquisitionToCallDownstreamApi` are optional, and enable your web app to request the scopes and the user's consent to those scopes when they sign in. If you don't specify the scopes, *Microsoft.Identity.Web* enables an incremental consent experience.

*Microsoft.Identity.Web* offers two mechanisms for calling a web API from a web app without you having to acquire a token. The option you choose depends on whether you want to call Microsoft Graph or another API.

### Option 1: Call Microsoft Graph

If you want to call Microsoft Graph, *Microsoft.Identity.Web* enables you to directly use the `GraphServiceClient` (exposed by the Microsoft Graph SDK) in your API actions. To expose Microsoft Graph:

1. Add the [Microsoft.Identity.Web.GraphServiceClient](https://www.nuget.org/packages/Microsoft.Identity.Web.GraphServiceClient) NuGet package to your project.
2. Add `.AddMicrosoftGraph()` after `.EnableTokenAcquisitionToCallDownstreamApi()` in the *Startup.cs* file. `.AddMicrosoftGraph()` has several overrides. Using the override that takes a configuration section as a parameter, the code becomes:

    ```csharp
    using Microsoft.Identity.Web;
    
    public class Startup
    {
      // ...
      public void ConfigureServices(IServiceCollection services)
      {
      // ...
      services.AddAuthentication(OpenIdConnectDefaults.AuthenticationScheme)
              .AddMicrosoftIdentityWebApp(Configuration, "AzureAd")
                .EnableTokenAcquisitionToCallDownstreamApi(new string[]{"user.read" })
                   .AddMicrosoftGraph(Configuration.GetSection("GraphBeta"))
                .AddInMemoryTokenCaches();
       // ...
      }
      // ...
    }
    ```

### Option 2: Call a downstream web API other than Microsoft Graph

If you want to call an API other than Microsoft Graph, *Microsoft.Identity.Web* enables you to use the `IDownstreamApi` interface in your API actions. To use this interface:

1. Add the [Microsoft.Identity.Web.DownstreamApi](https://www.nuget.org/packages/Microsoft.Identity.Web.DownstreamApi) NuGet package to your project.
2. Add `.AddDownstreamApi()` after `.EnableTokenAcquisitionToCallDownstreamApi()` in the *Startup.cs* file. `.AddDownstreamApi()` has two arguments, and is shown in the following snippet:

    - The name of a service (API), which is used in your controller actions to reference the corresponding configuration
    - a configuration section representing the parameters used to call the downstream web API.

    ```csharp
    using Microsoft.Identity.Web;
    
    public class Startup
    {
      // ...
      public void ConfigureServices(IServiceCollection services)
      {
      // ...
      services.AddAuthentication(OpenIdConnectDefaults.AuthenticationScheme)
              .AddMicrosoftIdentityWebApp(Configuration, "AzureAd")
                .EnableTokenAcquisitionToCallDownstreamApi(new string[]{"user.read" })
                   .AddDownstreamApi("MyApi", Configuration.GetSection("GraphBeta"))
                .AddInMemoryTokenCaches();
       // ...
      }
      // ...
    }
    ```

### Summary

As with web APIs, you can choose various token cache implementations. For details, see [Microsoft.Identity.Web - Token cache serialization](https://aka.ms/ms-id-web/token-cache-serialization) on GitHub.

The following image shows the various possibilities of *Microsoft.Identity.Web* and their effect on the *Startup.cs* file:

![Block diagram showing service configuration options in startup dot C S for calling a web API and specifying a token cache implementation](media/scenarios/microsoft-identity-web-startup-cs.svg)

Note

To fully understand the code examples here, be familiar with [ASP.NET Core fundamentals](/en-us/aspnet/core/fundamentals), and in particular with [dependency injection](/en-us/aspnet/core/fundamentals/dependency-injection) and [options](/en-us/aspnet/core/fundamentals/configuration/options).

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

## Startup.Auth.cs

Your web app needs to acquire a token for the downstream API, *Microsoft.Identity.Web* provides two mechanisms for calling a web API from a web app. The option you choose depends on whether you want to call Microsoft Graph or another API.

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
            app.AddMicrosoftIdentityWebApp(owinTokenAcquirerFactory,
                                          updateOptions: options => {});

            // Add the services you need.
            owinTokenAcquirerFactory.Services
                .Configure<ConfidentialClientApplicationOptions>(options => 
                      { options.RedirectUri = "https://localhost:44326/"; })
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
              app.AddMicrosoftIdentityWebApp(owinTokenAcquirerFactory,
                                            updateOptions: options => {});

              // Add the services you need.
              owinTokenAcquirerFactory.Services
                  .Configure<ConfidentialClientApplicationOptions>(options => 
                        { options.RedirectUri = "https://localhost:44326/"; })
                  .AddDownstreamApi("Graph", owinTokenAcquirerFactory.Configuration.GetSection("GraphBeta"))
                  .AddInMemoryTokenCaches();
              owinTokenAcquirerFactory.Build();
          }
      }
  }
```

### Summary

You can choose various token cache implementations. For details, see [Microsoft.Identity.Web - Token cache serialization](https://aka.ms/ms-id-web/token-cache-serialization) on GitHub.

The following image shows the various possibilities of *Microsoft.Identity.Web* and their effect on the *Startup.cs* file:

![Block diagram showing service configuration options in startup dot C S for calling a web API and specifying a token cache implementation](media/scenarios/microsoft-identity-web-startup-cs.svg)

Note

To fully understand the code examples here, be familiar with [ASP.NET Core fundamentals](/en-us/aspnet/core/fundamentals/), and in particular with [dependency injection](/en-us/aspnet/core/fundamentals/dependency-injection) and [options](/en-us/aspnet/core/fundamentals/configuration/options).

Code examples in this article and the following one are extracted from the [ASP.NET Web app sample](https://github.com/Azure-Samples/ms-identity-aspnet-webapp-openidconnect). You might want to refer to that sample for full implementation details.

# [Java](#tab/java)
## Implement the Java code sample

Code examples in this article and the following one are extracted from the [Java web application that calls Microsoft Graph](https://github.com/Azure-Samples/ms-identity-java-webapp), a web-app sample that uses MSAL for Java. The sample currently lets MSAL for Java produce the authorization-code URL and handles the navigation to the authorization endpoint for the Microsoft identity platform. It's also possible to use Sprint security to sign the user in. You might want to refer to the sample for full implementation details.

# [Node.js](#tab/nodejs)
## Implement the Node.js code sample

Code examples in this article and the following one are extracted from the [Node.js & Express.js web application that calls Microsoft Graph](https://github.com/Azure-Samples/ms-identity-node), a web app sample that uses MSAL Node.

The sample currently lets MSAL Node produce the authorization-code URL and handles the navigation to the authorization endpoint for the Microsoft identity platform. This is shown below:

```js
/**
 * Prepares the auth code request parameters and initiates the first leg of auth code flow
 * @param req: Express request object
 * @param res: Express response object
 * @param next: Express next function
 * @param authCodeUrlRequestParams: parameters for requesting an auth code url
 * @param authCodeRequestParams: parameters for requesting tokens using auth code
 */
redirectToAuthCodeUrl(authCodeUrlRequestParams, authCodeRequestParams, msalInstance) {
    return async (req, res, next) => {
        // Generate PKCE Codes before starting the authorization flow
        const { verifier, challenge } = await this.cryptoProvider.generatePkceCodes();

        // Set generated PKCE codes and method as session vars
        req.session.pkceCodes = {
            challengeMethod: 'S256',
            verifier: verifier,
            challenge: challenge,
        };

        /**
         * By manipulating the request objects below before each request, we can obtain
         * auth artifacts with desired claims. For more information, visit:
         * https://azuread.github.io/microsoft-authentication-library-for-js/ref/modules/_azure_msal_node.html#authorizationurlrequest
         * https://azuread.github.io/microsoft-authentication-library-for-js/ref/modules/_azure_msal_node.html#authorizationcoderequest
         **/
        req.session.authCodeUrlRequest = {
            ...authCodeUrlRequestParams,
            responseMode: msal.ResponseMode.FORM_POST, // recommended for confidential clients
            codeChallenge: req.session.pkceCodes.challenge,
            codeChallengeMethod: req.session.pkceCodes.challengeMethod,
        };

        req.session.authCodeRequest = {
            ...authCodeRequestParams,
            code: '',
        };

        try {
            const authCodeUrlResponse = await msalInstance.getAuthCodeUrl(req.session.authCodeUrlRequest);
            res.redirect(authCodeUrlResponse);
        } catch (error) {
            next(error);
        }
    };
}
```

# [Python](#tab/python)
## Implement the Python code sample

Code snippets in this article and the following are extracted from the [Python web application calling Microsoft Graph](https://github.com/Azure-Samples/ms-identity-python-webapp) sample using the [identity package](https://pypi.org/project/identity/) (a wrapper around MSAL Python).

The sample uses the identity package to produce the authorization-code URL and handles the navigation to the authorization endpoint for the Microsoft identity platform. You might want to refer to the sample for full implementation details.

---

## Code that redeems the authorization code

# [ASP.NET Core](#tab/aspnetcore)
Microsoft.Identity.Web simplifies your code by setting the correct OpenID Connect settings, subscribing to the code received event, and redeeming the code. No extra code is required to redeem the authorization code. See [Microsoft.Identity.Web source code](https://github.com/AzureAD/microsoft-identity-web/blob/c29f1a7950b940208440bebf0bcb524a7d6bee22/src/Microsoft.Identity.Web/WebAppExtensions/WebAppCallsWebApiAuthenticationBuilderExtensions.cs#L140) for details on how this works.

# [ASP.NET](#tab/aspnet)
*Microsoft.Identity.Web.OWIN* simplifies your code by setting the correct OpenID Connect settings, subscribing to the code received event, and redeeming the code. No extra code is required to redeem the authorization code. See [Microsoft.Identity.Web source code](https://github.com/AzureAD/microsoft-identity-web/blob/9fdcf15c66819b31b1049955eed5d3e5391656f5/src/Microsoft.Identity.Web.OWIN/AppBuilderExtension.cs#L95) for details on how this works.

# [Node.js](#tab/nodejs)
The *handleRedirect* method in **AuthProvider** class processes the authorization code received from Microsoft Entra ID. This is shown below:

```js
handleRedirect(options = {}) {
    return async (req, res, next) => {
        if (!req.body || !req.body.state) {
            return next(new Error('Error: response not found'));
        }

        const authCodeRequest = {
            ...req.session.authCodeRequest,
            code: req.body.code,
            codeVerifier: req.session.pkceCodes.verifier,
        };

        try {
            const msalInstance = this.getMsalInstance(this.msalConfig);

            if (req.session.tokenCache) {
                msalInstance.getTokenCache().deserialize(req.session.tokenCache);
            }

            const tokenResponse = await msalInstance.acquireTokenByCode(authCodeRequest, req.body);

            req.session.tokenCache = msalInstance.getTokenCache().serialize();
            req.session.idToken = tokenResponse.idToken;
            req.session.account = tokenResponse.account;
            req.session.isAuthenticated = true;

            const state = JSON.parse(this.cryptoProvider.base64Decode(req.body.state));
            res.redirect(state.successRedirect);
        } catch (error) {
            next(error);
        }
    }
}
```

# [Java](#tab/java)
After the app receives the authorization code, the [AuthFilter.java#L51-L56](https://github.com/Azure-Samples/ms-identity-java-webapp/blob/d55ee4ac0ce2c43378f2c99fd6e6856d41bdf144/src/main/java/com/microsoft/azure/msalwebsample/AuthFilter.java#L51-L56):

1. Delegates to the `AuthHelper.processAuthenticationCodeRedirect` method in [AuthHelper.java#L67-L97](https://github.com/Azure-Samples/ms-identity-java-webapp/blob/d55ee4ac0ce2c43378f2c99fd6e6856d41bdf144/src/main/java/com/microsoft/azure/msalwebsample/AuthHelper.java#L67-L97).
2. Calls `getAuthResultByAuthCode`.

```Java
class AuthHelper {
  // Code omitted
  void processAuthenticationCodeRedirect(HttpServletRequest httpRequest, String currentUri, String fullUrl)
            throws Throwable {

  // Code omitted
  AuthenticationResponse authResponse = AuthenticationResponseParser.parse(new URI(fullUrl), params);

  // Code omitted
  IAuthenticationResult result = getAuthResultByAuthCode(
                    httpRequest,
                    oidcResponse.getAuthorizationCode(),
                    currentUri);

// Code omitted
  }
}
```

The `getAuthResultByAuthCode` method is defined in [AuthHelper.java#L176](https://github.com/Azure-Samples/ms-identity-java-webapp/blob/d55ee4ac0ce2c43378f2c99fd6e6856d41bdf144/src/main/java/com/microsoft/azure/msalwebsample/AuthHelper.java#L176). It creates an MSAL `ConfidentialClientApplication`, and then calls `acquireToken()` with `AuthorizationCodeParameters` created from the authorization code.

```Java
   private IAuthenticationResult getAuthResultByAuthCode(
            HttpServletRequest httpServletRequest,
            AuthorizationCode authorizationCode,
            String currentUri) throws Throwable {

        IAuthenticationResult result;
        ConfidentialClientApplication app;
        try {
            app = createClientApplication();

            String authCode = authorizationCode.getValue();
            AuthorizationCodeParameters parameters = AuthorizationCodeParameters.builder(
                    authCode,
                    new URI(currentUri)).
                    build();

            Future<IAuthenticationResult> future = app.acquireToken(parameters);

            result = future.get();
        } catch (ExecutionException e) {
            throw e.getCause();
        }

        if (result == null) {
            throw new ServiceUnavailableException("authentication result was null");
        }

        SessionManagementHelper.storeTokenCacheInSession(httpServletRequest, app.tokenCache().serialize());

        return result;
    }

    private ConfidentialClientApplication createClientApplication() throws MalformedURLException {
        return ConfidentialClientApplication.builder(clientId, ClientCredentialFactory.create(clientSecret)).
                authority(authority).
                build();
    }
```

# [Python](#tab/python)
Refer to [Tutorial: Sign-in users to a Python Flask web app by using Microsoft identity platform](tutorial-web-app-python-flask-sign-in-out)

The Microsoft sign-in screen sends the authorization code to the `/getAToken` URL that was specified in the app registration. The `auth_response` route handles that URL, calling `auth.complete_login` to process the authorization code, and then either returning an error or redirecting to the home page.

```python
@app.route(app_config.REDIRECT_PATH)
def auth_response():
    result = auth.complete_log_in(request.args)
    if "error" in result:
        return render_template("auth_error.html", result=result)
    return redirect(url_for("index"))
```

See *app.py* for the full context of that code.

---

Instead of a client secret, the confidential client application can also prove its identity by using a client certificate or a client assertion. The use of client assertions is an advanced scenario, detailed in [Client assertions](/en-us/entra/msal/dotnet/acquiring-tokens/msal-net-client-assertions).

## Token cache

Important

The token-cache implementation for web apps or web APIs is different from the implementation for desktop applications, which is often [file based](/en-us/entra/msal/dotnet/how-to/token-cache-serialization). For security and performance reasons, it's important to ensure that for web apps and web APIs there is one token cache per user account. You must serialize the token cache for each account.

# [ASP.NET Core](#tab/aspnetcore)
The ASP.NET core tutorial uses dependency injection to let you decide the token cache implementation in the Startup.cs file for your application. Microsoft.Identity.Web comes with prebuilt token-cache serializers described in [Token cache serialization](/en-us/entra/msal/dotnet/how-to/token-cache-serialization). An interesting possibility is to choose ASP.NET Core [distributed memory caches](/en-us/aspnet/core/performance/caching/distributed#distributed-memory-cache):

```csharp
// Use a distributed token cache by adding:
    services.AddMicrosoftIdentityWebAppAuthentication(Configuration, "AzureAd")
            .EnableTokenAcquisitionToCallDownstreamApi(
                initialScopes: new string[] { "user.read" })
            .AddDistributedTokenCaches();

// Then, choose your implementation.
// For instance, the distributed in-memory cache (not cleared when you stop the app):
services.AddDistributedMemoryCache();

// Or a Redis cache:
services.AddStackExchangeRedisCache(options =>
{
 options.Configuration = "localhost";
 options.InstanceName = "SampleInstance";
});

// Or even a SQL Server token cache:
services.AddDistributedSqlServerCache(options =>
{
 options.ConnectionString = _config["DistCache_ConnectionString"];
 options.SchemaName = "dbo";
 options.TableName = "TestCache";
});
```

For details about the token-cache providers, see also Microsoft.Identity.Web's [Token cache serialization](https://aka.ms/ms-id-web/token-cache-serialization) article, and the [ASP.NET Core web app tutorials | Token caches](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/2-WebApp-graph-user/2-2-TokenCache) phase of the web apps tutorial.

# [ASP.NET](#tab/aspnet)
The ASP.NET tutorial uses dependency injection to let you decide the token cache implementation in the *Startup.Auth.cs* file for your application. *Microsoft.Identity.Web* comes with prebuilt token-cache serializers described in [Token cache serialization](/en-us/entra/msal/dotnet/how-to/token-cache-serialization). An interesting possibility is to choose ASP.NET Core [distributed memory caches](/en-us/aspnet/core/performance/caching/distributed#distributed-memory-cache):

```csharp
var services = owinTokenAcquirerFactory.Services;
// Use a distributed token cache by adding:
services.AddDistributedTokenCaches();

// Then, choose your implementation.
// For instance, the distributed in-memory cache (not cleared when you stop the app):
services.AddDistributedMemoryCache();

// Or a Redis cache:
services.AddStackExchangeRedisCache(options =>
{
 options.Configuration = "localhost";
 options.InstanceName = "SampleInstance";
});

// Or even a SQL Server token cache:
services.AddDistributedSqlServerCache(options =>
{
 options.ConnectionString = _config["DistCache_ConnectionString"];
 options.SchemaName = "dbo";
 options.TableName = "TestCache";
});
```

For details about the token-cache providers, see also the *Microsoft.Identity.Web*[Token cache serialization](https://aka.ms/ms-id-web/token-cache-serialization) article, and the [ASP.NET Core web app tutorials | Token caches](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/2-WebApp-graph-user/2-2-TokenCache) phase of the web app's tutorial.

For details see [Token cache serialization for MSAL.NET](/en-us/entra/msal/dotnet/how-to/token-cache-serialization).

# [Java](#tab/java)
MSAL Java provides methods to serialize and deserialize the token cache. The Java sample handles the serialization from the session, as shown in the `getAuthResultBySilentFlow` method in [AuthHelper.java#L99-L122](https://github.com/Azure-Samples/ms-identity-java-webapp/blob/d55ee4ac0ce2c43378f2c99fd6e6856d41bdf144/src/main/java/com/microsoft/azure/msalwebsample/AuthHelper.java#L99-L122):

```Java
IAuthenticationResult getAuthResultBySilentFlow(HttpServletRequest httpRequest, HttpServletResponse httpResponse)
      throws Throwable {

  IAuthenticationResult result =  SessionManagementHelper.getAuthSessionObject(httpRequest);

  IConfidentialClientApplication app = createClientApplication();

  Object tokenCache = httpRequest.getSession().getAttribute("token_cache");
  if (tokenCache != null) {
      app.tokenCache().deserialize(tokenCache.toString());
  }

  SilentParameters parameters = SilentParameters.builder(
          Collections.singleton("User.Read"),
          result.account()).build();

  CompletableFuture<IAuthenticationResult> future = app.acquireTokenSilently(parameters);
  IAuthenticationResult updatedResult = future.get();

  // Update session with latest token cache.
  SessionManagementHelper.storeTokenCacheInSession(httpRequest, app.tokenCache().serialize());

  return updatedResult;
}
```

The detail of the `SessionManagementHelper` class is provided in the [MSAL sample for Java](https://github.com/Azure-Samples/ms-identity-java-webapp/blob/d55ee4ac0ce2c43378f2c99fd6e6856d41bdf144/src/main/java/com/microsoft/azure/msalwebsample/SessionManagementHelper.java).

# [Node.js](#tab/nodejs)
In the Node.js sample, the application session is used to store the token cache. Using MSAL Node cache methods, the token cache in session is read before a token request is made, and then updated once the token request is successfully completed. This is shown below:

```js
acquireToken(options = {}) {
    return async (req, res, next) => {
        try {
            const msalInstance = this.getMsalInstance(this.msalConfig);

            /**
             * If a token cache exists in the session, deserialize it and set it as the 
             * cache for the new MSAL CCA instance. For more, see: 
             * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/caching.md
             */
            if (req.session.tokenCache) {
                msalInstance.getTokenCache().deserialize(req.session.tokenCache);
            }

            const tokenResponse = await msalInstance.acquireTokenSilent({
                account: req.session.account,
                scopes: options.scopes || [],
            });

            /**
             * On successful token acquisition, write the updated token 
             * cache back to the session. For more, see: 
             * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/caching.md
             */
            req.session.tokenCache = msalInstance.getTokenCache().serialize();
            req.session.accessToken = tokenResponse.accessToken;
            req.session.idToken = tokenResponse.idToken;
            req.session.account = tokenResponse.account;

            res.redirect(options.successRedirect);
        } catch (error) {
            if (error instanceof msal.InteractionRequiredAuthError) {
                return this.login({
                    scopes: options.scopes || [],
                    redirectUri: options.redirectUri,
                    successRedirect: options.successRedirect || '/',
                })(req, res, next);
            }

            next(error);
        }
    };
}
```

# [Python](#tab/python)
In the Python sample, the identity package takes care of the token cache, using the global `session` object for storage.

Flask has built-in support for sessions stored in a cookie, but due to the length of the identity cookies, the sample uses the [Flask-session](https://flask-session.readthedocs.io/) package instead. Everything is initialized in *app.py*:

```python
import identity
import identity.web
import requests
from flask import Flask, redirect, render_template, request, session, url_for
from flask_session import Session

import app_config

app = Flask(__name__)
app.config.from_object(app_config)
Session(app)

auth = identity.web.Auth(
    session=session,
    authority=app.config["AUTHORITY"],
    client_id=app.config["CLIENT_ID"],
    client_credential=app.config["CLIENT_SECRET"],
)
```

Due to the `SESSION_TYPE="filesystem"` setting in `app_config.py`, the Flask-session package stores sessions using the local file system.

For production, you should use [a setting](https://flask-session.readthedocs.io/en/latest/#configuration) that persists across multiple instances and deploys of your app, such as "sqlachemy" or "redis".

---