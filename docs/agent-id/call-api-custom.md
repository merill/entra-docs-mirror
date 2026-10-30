---
layout: Conceptual
title: Call custom APIs from an agent using .NET - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/call-api-custom
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to call custom protected APIs from an agent using different approaches including IDownstreamApi, MicrosoftIdentityMessageHandler, and IAuthorizationHeaderProvider.
ms.topic: how-to
ms.date: 2025-11-04T00:00:00.0000000Z
ms.reviewer: jmprieur
locale: en-us
document_id: 26836eea-e08d-d045-56b6-b5686ce65cf0
document_version_independent_id: 26836eea-e08d-d045-56b6-b5686ce65cf0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/call-api-custom.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/call-api-custom
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/call-api-custom.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 7294d6a1-4b4c-88b0-54d4-fc172fb5f035
---

# Call custom APIs from an agent using .NET - Microsoft Entra Agent ID | Microsoft Learn

There are multiple ways to call custom APIs from an agent. Depending on your scenario, you can use either `IDownstreamApi`, `MicrosoftIdentityMessageHandler`, or `IAuthorizationHeaderProvider`. This guide explains the different approaches for calling your own protected APIs all the three ways.

To call an API from an agent, you need to obtain an access token that the agent can use to authenticate itself to the API. We recommend using the *Microsoft.Identity.Web* SDK for .NET to call your web APIs. This SDK simplifies the process of acquiring and validating tokens. For other languages, use the [Microsoft Entra ID Auth SDK (sidecar)](/en-us/entra/msidweb/agent-id-sdk/overview).

## Prerequisites

- An agent identity with appropriate permissions to call the target API. You need a user for the on-behalf-of flow.
- An agent's user account with appropriate permissions to call the target API.

## Decide which approach to use based on your scenario

The following table helps you decide which approach to use. For most scenarios, we recommend using `IDownstreamApi`.

| Approach | Complexity | Flexibility | Use Case |
| --- | --- | --- | --- |
| `IDownstreamApi` | Low | Medium | Standard REST APIs with configuration |
| `MicrosoftIdentityMessageHandler` | Medium | High | HttpClient with Direct Injection (DI) and composable pipeline |
| `IAuthorizationHeaderProvider` | High | Very High | Complete control over HTTP requests |

# [Use IDownstreamApi](#tab/idownstream)
`IDownstreamApi` is the preferred way to call a protected API among the three options. It's highly configurable and requires minimal code changes. It also offers automatic token acquisition.

Use `IDownstreamApi` when you need the following listed items:

- You're calling standard REST APIs
- You want a configuration-driven approach
- You need automatic serialization/deserialization
- You want to write minimal code

# [Use MicrosoftIdentityMessageHandler](#tab/messagehandler)
`MicrosoftIdentityMessageHandler` from the *Microsoft.Identity.Web.TokenAcquisition* package is a delegating handler that adds authentication to HttpClient requests. Use this when you need full HttpClient functionality with automatic token acquisition.

The *Microsoft.Identity.Web.TokenAcquisition* package is already referenced by *Microsoft.Identity.Web.AgentIdentities*.

Use `MicrosoftIdentityMessageHandler` when you need the following listed items:

- You need fine-grained control over HTTP requests
- You want to compose multiple message handlers
- You're integrating with existing HttpClient-based code
- You need access to raw HttpResponseMessage

# [Use IAuthorizationHeaderProvider](#tab/authheaderprovider)
`IAuthorizationHeaderProvider` from *Microsoft.Identity.Web* gives you direct access to authorization headers for complete control over HTTP requests. This means you can customize the authentication process to fit your needs, including adding or modifying headers as necessary. This method also allows you to use custom HTTP libraries to make API calls.

Use `IAuthorizationHeaderProvider` when you need the following listed items:

- You need complete control over HTTP request construction
- You're integrating with nonstandard HTTP APIs
- You need to use HttpClient without DI
- You're building custom HTTP abstractions

---

## Call your API

After determining what works for you, proceed to call your custom web API.

Warning

Client secrets shouldn't be used as client credentials in production environments for agent identity blueprints due to security risks. Instead, use more secure authentication methods such as [federated identity credentials (FIC) with managed identities](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity) or client certificates. These methods provide enhanced security by eliminating the need to store sensitive secrets directly within your application configuration.

# [Use IDownstreamApi](#tab/idownstream)
1. Install the required NuGet package:

    ```bash
    dotnet add package Microsoft.Identity.Web.DownstreamApi
    dotnet add package Microsoft.Identity.Web.AgentIdentities
    ```
2. Configure token credential options and your APIs in *appsettings.json*.

    ```json
    {
      "AzureAd": {
        "Instance": "https://login.microsoftonline.com/",
        "TenantId": "your-tenant-id",
        "ClientId": "your-blueprint-id",
        "ClientCredentials": [
          {
            "SourceType": "ClientSecret",
            "ClientSecret": "your-client-secret"
          }
        ]
      },
      "DownstreamApis": {
        "MyApi": {
          "BaseUrl": "https://api.example.com",
          "Scopes": ["api://my-api-client-id/read", "api://my-api-client-id/write"],
          "RelativePath": "/api/v1",
          "RequestAppToken": false
        }
      }
    }
    ```
3. Configure your services to add downstream API support:

    ```csharp
    using Microsoft.AspNetCore.Authentication.OpenIdConnect;
    using Microsoft.Identity.Web;
    
    var builder = WebApplication.CreateBuilder(args);
    
    // Add authentication
    builder.Services.AddAuthentication(OpenIdConnectDefaults.AuthenticationScheme)
        .AddMicrosoftIdentityWebApp(builder.Configuration.GetSection("AzureAd"))
        .EnableTokenAcquisitionToCallDownstreamApi()
        .AddInMemoryTokenCaches();
    
    // Register downstream APIs
    builder.Services.AddDownstreamApis(
        builder.Configuration.GetSection("DownstreamApis"));
    
    // Add Agent Identities support
    builder.Services.AddAgentIdentities();
    
    builder.Services.AddControllersWithViews();
    
    var app = builder.Build();
    app.UseAuthentication();
    app.UseAuthorization();
    app.MapControllers();
    app.Run();
    ```
4. Call your protected API using `IDownstreamApi`. When calling the API, you can specify the agent identity or agent's user account identity using the `WithAgentIdentity` or `WithAgentUserIdentity` methods. `IDownstreamApi` automatically handles token acquisition and attaches the access token to the request.

    - For `WithAgentIdentity`, you either call the API using an app only token (autonomous agent) or on-behalf of a user (interactive agent).

        ```csharp
        using Microsoft.Identity.Abstractions;
        using Microsoft.AspNetCore.Authorization;
        using Microsoft.AspNetCore.Mvc;
        
        [Authorize]
        public class ProductsController : Controller
        {
            private readonly IDownstreamApi _api;
        
            public ProductsController(IDownstreamApi api)
            {
                _api = api;
            }
        
            // GET request for app only token scenario for agent identity
            public async Task<IActionResult> Index()
            {
        
                string agentIdentity = "<your-agent-identity>";
                var products = await _api.GetForAppAsync<List<Product>>(
                    "MyApi",
                    "products",
                    options => options.WithAgentIdentity(agentIdentity));
        
                return View(products);
            }
        
            // GET request for on-behalf of user token scenario for agent identity
            public async Task<IActionResult> UserProducts()
            {
        
                string agentIdentity = "<your-agent-identity>";
                var products = await _api.GetForUserAsync<List<Product>>(
                    "MyApi",
                    "products",
                    options => options.WithAgentIdentity(agentIdentity));
        
                return View(products);
            }
        }
        ```
    - For `WithAgentUserIdentity`, you can specify either User Principal Name (UPN) or Object Identity (OID) to identify the agent's user account.

        ```csharp
        using Microsoft.Identity.Abstractions;
        using Microsoft.AspNetCore.Authorization;
        using Microsoft.AspNetCore.Mvc;
        
        [Authorize]
        public class ProductsController : Controller
        {
            private readonly IDownstreamApi _api;
        
            public ProductsController(IDownstreamApi api)
            {
                _api = api;
            }
        
            // GET request for agent's user account identity using UPN
            public async Task<IActionResult> Index()
            {
        
                string agentIdentity = "<your-agent-identity>";
                string userUpn = "user@contoso.com";
        
                var products = await _api.GetForUserAsync<List<Product>>(
                    "MyApi",
                    "products",
                    options => options.WithAgentUserIdentity(agentIdentity, userUpn));
                return View(products);
            }
        
            // GET request for agent's user account identity using OID
            public async Task<IActionResult> UserProducts()
            {
        
                string agentIdentity = "<your-agent-identity>";
                string userOid = "user-object-id";
        
                var products = await _api.GetForUserAsync<List<Product>>(
                    "MyApi",
                    "products",
                    options => options.WithAgentUserIdentity(agentIdentity, userOid));
        
                return View(products);
            }
        
        }
        ```

# [Use MicrosoftIdentityMessageHandler](#tab/messagehandler)
1. Install the required NuGet package:

    ```bash
    dotnet add package Microsoft.Identity.Web.AgentIdentities
    ```
2. Configure your services to add authentication with agent identities and register HttpClient with `MicrosoftIdentityMessageHandler`:

    ```csharp
    using Microsoft.AspNetCore.Authentication.OpenIdConnect;
    using Microsoft.Identity.Web;
    using Microsoft.Identity.Abstractions;
    
    var builder = WebApplication.CreateBuilder(args);
    
    builder.Services.AddAuthentication(OpenIdConnectDefaults.AuthenticationScheme)
        .AddMicrosoftIdentityWebApp(builder.Configuration.GetSection("AzureAd"))
        .EnableTokenAcquisitionToCallDownstreamApi()
        .AddInMemoryTokenCaches();
    
    // Configure named HttpClient with authentication
    builder.Services.AddHttpClient("MyApiClient", client =>
    {
        client.BaseAddress = new Uri("https://api.example.com");
        client.DefaultRequestHeaders.Add("Accept", "application/json");
        client.Timeout = TimeSpan.FromSeconds(30);
    })
    .AddHttpMessageHandler(sp =>
    {
        var authProvider = sp.GetRequiredService<IAuthorizationHeaderProvider>();
        return new MicrosoftIdentityMessageHandler(
            authProvider,
            new MicrosoftIdentityMessageHandlerOptions
            {
                Scopes = new[] { "api://my-api-client-id/read" },
            });
    });
    
    builder.Services.AddControllersWithViews();
    
    // Add Agent Identities support
    builder.Services.AddAgentIdentities();

    var app = builder.Build();
    app.UseAuthentication();
    app.UseAuthorization();
    app.MapControllers();
    app.Run();
    ```
3. Acquire token and call your protected API using the configured HttpClient. You can specify the agent identity or agent's user account using the `WithAgentIdentity` or `WithAgentUserIdentity` methods.

    - For `WithAgentIdentity`, you either call the API using an app only token (autonomous agent) or on-behalf of a user (interactive agent).

        To call the API using an app only token for the agent identity, set `RequestAppToken` to `true`.

        ```csharp
        public class MyService
        {
            private readonly HttpClient _httpClient;
        
            public MyService(IHttpClientFactory httpClientFactory)
            {
                _httpClient = httpClientFactory.CreateClient("MyApiClient");
            }
        
            public async Task<string> CallApiWithAgentIdentity(string agentIdentity)
            {
                // Create request with agent identity authentication
                var request = new HttpRequestMessage(HttpMethod.Get, "/api/data")
                    .WithAuthenticationOptions(options => 
                    {
                        options.WithAgentIdentity(agentIdentity);
                        options.RequestAppToken = true;
                    });
        
                var response = await _httpClient.SendAsync(request);
                response.EnsureSuccessStatusCode();
                return await response.Content.ReadAsStringAsync();
            }
        }
        ```

        To call the API on-behalf of a user for the agent identity, don't set `RequestAppToken` or explicitly set it to `false`.

        ```csharp
        public class MyService
        {
            private readonly HttpClient _httpClient;
        
            public MyService(IHttpClientFactory httpClientFactory)
            {
                _httpClient = httpClientFactory.CreateClient("MyApiClient");
            }
        
            public async Task<string> CallApiWithAgentIdentity(string agentIdentity)
            {
                // Create request with agent identity authentication
                var request = new HttpRequestMessage(HttpMethod.Get, "/api/data")
                    .WithAuthenticationOptions(options =>
                    {
                        options.WithAgentIdentity(agentIdentity);
                        options.RequestAppToken = false;
                    });
        
                var response = await _httpClient.SendAsync(request);
                response.EnsureSuccessStatusCode();
                return await response.Content.ReadAsStringAsync();
            }
        }
        ```
    - To use `WithAgentUserIdentity`, you can specify either UPN or OID to identify the agent's user account.

        ```csharp
        // Create request with agent's user account identity authentication with UPN
        public async Task<string> CallApiWithAgentUserIdentityByUpn(string agentIdentity, string userUpn)
        {
        
            var request = new HttpRequestMessage(HttpMethod.Get, "/api/userdata")
                .WithAuthenticationOptions(options => 
                {
                    options.WithAgentUserIdentity(agentIdentity, userUpn);
                    options.Scopes.Add("https://myapi.domain.com/user.read");
                });
        
            var response = await _httpClient.SendAsync(request);
            response.EnsureSuccessStatusCode();
            return await response.Content.ReadAsStringAsync();
        }
        
        // Create request with agent's user account identity authentication with OID
        public async Task<string> CallApiWithAgentUserIdentityByOid(string agentIdentity, string userOid)
        {
        
            var request = new HttpRequestMessage(HttpMethod.Get, "/api/userdata")
                .WithAuthenticationOptions(options => 
                {
                    options.WithAgentUserIdentity(agentIdentity, userOid);
                    options.Scopes.Add("https://myapi.domain.com/user.read");
                });
        
            var response = await _httpClient.SendAsync(request);
            response.EnsureSuccessStatusCode();
            return await response.Content.ReadAsStringAsync();
        }
        ```

# [Use IAuthorizationHeaderProvider](#tab/authheaderprovider)
1. Install the required NuGet package:

    ```bash
    dotnet add package Microsoft.Identity.Web.AgentIdentities
    ```
2. Configure your services to add authentication with agent identities:

    ```csharp
    using Microsoft.AspNetCore.Authorization;
    using Microsoft.Identity.Abstractions;
    using Microsoft.Identity.Web;
    
    var builder = WebApplication.CreateBuilder(args);
    
    // With Microsoft.Identity.Web
    builder.Services.AddMicrosoftIdentityWebApiAuthentication(builder.Configuration)
        .EnableTokenAcquisitionToCallDownstreamApi();
    
    builder.Services.AddAgentIdentities();
    
    var app = builder.Build();
    
    app.UseAuthentication();
    app.UseAuthorization();
    
    app.Run();
    ```

    - Configure auth credentials in *appsettings.json*

    ```json
    {
      "AzureAd": {
        "Instance": "https://login.microsoftonline.com/",
        "TenantId": "your-tenant-id",
        "ClientId": "your-blueprint-id",
        "ClientCredentials": [
          {
            "SourceType": "ClientSecret",
            "ClientSecret": "your-client-secret"
          }
        ]
      }
    }
    ```
3. Acquire and extract access token then call the web API.

    - For `WithAgentIdentity`, you either call the API using an app only token (autonomous agent) or on-behalf of a user (interactive agent).

        - For app only token scenario, use `CreateAuthorizationHeaderForAppAsync` method.
        - For the on-behalf-of (OBO) token scenario, use `CreateAuthorizationHeaderForUserAsync` method

        ```csharp
        using Microsoft.Identity.Abstractions;
        
        [Authorize]
        public class CustomApiController : Controller
        {
            private readonly IAuthorizationHeaderProvider _headerProvider;
        
            public CustomApiController(IAuthorizationHeaderProvider headerProvider)
            {
                _headerProvider = headerProvider;
            }
        
            // App only token scenario for agent identity
            public async Task<IActionResult> GetBackgroundData()
            {
                // Configure options for the agent identity
                string agentIdentity = "agent-identity-guid";
                var options = new AuthorizationHeaderProviderOptions()
                    .WithAgentIdentity(agentIdentity);
        
                // Acquire an access token for the agent identity
                var authHeader = await _headerProvider.CreateAuthorizationHeaderForAppAsync(
                    scopes: new[] { "api://my-api/.default" }, options: options);
        
                // Call the protected API
                using var client = new HttpClient();
                client.DefaultRequestHeaders.Add("Authorization", authHeader);
        
                var response = await client.GetAsync("https://api.example.com/background");
                var data = await response.Content.ReadFromJsonAsync<BackgroundData>();
        
                return Ok(data);
            }
        
            // On-behalf of user token scenario for agent identity
            public async Task<IActionResult> GetUserData()
            {
                // Configure options for the agent identity
                string agentIdentity = "agent-identity-guid";
                var options = new AuthorizationHeaderProviderOptions()
                    .WithAgentIdentity(agentIdentity);
        
                // Acquire an access token for the agent identity
                var authHeader = await _headerProvider.CreateAuthorizationHeaderForUserAsync(
                    scopes: new[] { "api://my-api/.default" }, options: options);
        
                // Call the protected API
                using var client = new HttpClient();
                client.DefaultRequestHeaders.Add("Authorization", authHeader);
        
                var response = await client.GetAsync("https://api.example.com/background");
                var data = await response.Content.ReadFromJsonAsync<BackgroundData>();
        
                return Ok(data);
            }
        }
        ```
    - For `WithAgentUserIdentity`, you call the API on behalf of a user using their UPN or OID.

        ```csharp
        using Microsoft.Identity.Abstractions;
        
        [Authorize]
        public class CustomApiController : Controller
        {
            private readonly IAuthorizationHeaderProvider _headerProvider;
        
            public CustomApiController(IAuthorizationHeaderProvider headerProvider)
            {
                _headerProvider = headerProvider;
            }
        
            // App only token scenario for agent identity
            public async Task<IActionResult> GetBackgroundData()
            {
                // Configure options for the agent identity
                string agentIdentity = "agent-identity-guid";
                string userUpn = "user@contoso.com";
        
                var options = new AuthorizationHeaderProviderOptions()
                    .WithAgentUserIdentity(agentIdentity, userUpn);
        
                // Create a ClaimsPrincipal to enable token caching
                ClaimsPrincipal user = new ClaimsPrincipal();
        
                // Acquire an access token for the agent identity
                var authHeader = await _headerProvider.CreateAuthorizationHeaderForAppAsync(
                    scopes: new[] { "api://my-api/.default" }, options: options, user: user);
        
                // Call the protected API
                using var client = new HttpClient();
                client.DefaultRequestHeaders.Add("Authorization", authHeader);
        
                var response = await client.GetAsync("https://api.example.com/background");
                var data = await response.Content.ReadFromJsonAsync<BackgroundData>();
        
                return Ok(data);
            }
        
            // On-behalf of user token scenario for agent identity
            public async Task<IActionResult> GetUserData()
            {
                // Configure options for the agent identity
                string agentIdentity = "agent-identity-guid";
                string userUpn = "user@contoso.com";
        
                var options = new AuthorizationHeaderProviderOptions()
                    .WithAgentUserIdentity(agentIdentity, userUpn);
        
                // Create a ClaimsPrincipal to enable token caching
                ClaimsPrincipal user = new ClaimsPrincipal();
        
                // Acquire an access token for the agent identity
                var authHeader = await _headerProvider.CreateAuthorizationHeaderForAppAsync(
                    scopes: new[] { "api://my-api/.default" }, options: options, user: user);
        
                // Call the protected API
                using var client = new HttpClient();
                client.DefaultRequestHeaders.Add("Authorization", authHeader);
        
                var response = await client.GetAsync("https://api.example.com/background");
                var data = await response.Content.ReadFromJsonAsync<BackgroundData>();
        
                return Ok(data);
            }
        }       
        ```

---