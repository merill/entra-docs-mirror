---
layout: Conceptual
title: Authenticate users and acquire tokens for interactive agents - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/interactive-agent-authentication-authorization-flow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to authenticate users, configure authorization, and implement the On-Behalf-Of flow for interactive agents to access resources on behalf of users.
ms.topic: how-to
ms.date: 2026-06-15T00:00:00.0000000Z
ms.reviewer: dastrock, jomondi
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: f579f3e2-87b8-a047-3a8b-3a6e99a5f914
document_version_independent_id: f579f3e2-87b8-a047-3a8b-3a6e99a5f914
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/interactive-agent-authentication-authorization-flow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/interactive-agent-authentication-authorization-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/interactive-agent-authentication-authorization-flow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 9e2fe391-5ad9-2d0c-f049-b0f6dc419484
---

# Authenticate users and acquire tokens for interactive agents - Microsoft Entra Agent ID | Microsoft Learn

Interactive agents take actions on behalf of users. To act on behalf of users securely, the agent authenticates the user, gets consent for required permissions, and acquires access tokens for downstream APIs. This article walks you through the end-to-end authentication and token acquisition flow for your interactive agent:

1. Grant permissions through inheritable permissions or consent.
2. Authenticate the user and obtain an access token.
3. Validate the token and extract user claims.
4. Acquire tokens for downstream APIs using the On-Behalf-Of (OBO) flow.

Note

This article covers interactive agents that act **on behalf of** signed-in users using the OBO flow. If your agent needs its own user-like identity (a digital worker scenario), see [Agent's user accounts](agent-users) and [Agent's user account OAuth flow](agent-user-oauth-flow).

## Prerequisites

Before you begin, ensure you have:

- An [agent identity blueprint](agent-blueprint). Record the agent identity blueprint app ID (client ID).
- An [agent identity](create-delete-agent-identities).
- A client application registered in Microsoft Entra to handle user authentication.
- Familiarity with the [OAuth 2.0 authorization code flow](/en-us/entra/identity-platform/v2-oauth2-auth-code-flow).
- The ability to run an ASP.NET Core web API if you plan to use the token validation and OBO samples in this article.

For admin authorization, you also need:

- [Administrator access to grant consent](grant-agent-access-microsoft-365) for application permissions.

## Permissions and consent

Before the agent can act on behalf of a user, the user or an administrator must consent to the required permissions. There are two approaches to granting permissions:

- **Inheritable permissions**: Preauthorize permissions on the blueprint so agent identities inherit them automatically.
- **Request consent**: Register a redirect URI and prompt users or administrators to grant consent through an OAuth request or use the admin consent endpoint.

### Use inheritable permissions

Configure inheritable permissions on the agent identity blueprint to preauthorize a base set of delegated scopes and application roles. Agent identities created from the blueprint automatically inherit those permissions without interactive consent prompts. For more information, see [Configure inheritable permissions for agent identity blueprints](configure-inheritable-permissions-blueprints).

### Request consent

To request consent through an OAuth flow, your agent identity blueprint must first be configured with a redirect URI. For blueprints, the redirect URI must be a **web application** type. Unlike redirect URIs on app registrations, a redirect URI on a blueprint can't be used to obtain delegated permission tokens. Only `response_type=none` is supported in the OAuth2 request, which means the request records consent only and no tokens are returned.

#### Register a redirect URI

# [Microsoft Graph API](#tab/microsoft-graph-api)
To update the redirect URI on the agent identity blueprint, you first need to obtain an access token with the delegated permission `AgentIdentityBlueprint.ReadWrite.All`. Then send a PATCH request to the application object for the agent identity blueprint:

```http
PATCH https://graph.microsoft.com/beta/applications/<agent-blueprint-id>
OData-Version: 4.0
Content-Type: application/json
Authorization: Bearer <token>

{
  "web": {
    "redirectUris": [
      "https://myagentapp.com/authorize"
    ]
  }
}
```

# [Microsoft Graph PowerShell](#tab/microsoft-graph-powershell)
Use Microsoft Graph PowerShell to update the agent identity blueprint with the redirect URI.

```powershell
Connect-MgGraph -Scopes "AgentIdentityBlueprint.ReadWrite.All" -TenantId <your-tenant-id>

$applicationId = "<agent-blueprint-id>"
$web = @{
    redirectUris= @(
        "https://myagentapp.com/authorize"
    )
}

$body = @{
    web   =  $web
}

Invoke-MgGraphRequest -Method PATCH `
        -Uri "https://graph.microsoft.com/beta/applications/$applicationId" `
        -Headers @{ "OData-Version" = "4.0" } `
        -Body ($body | ConvertTo-Json)
```

---

#### Request user consent

Before the agent can act on behalf of a user, the user must consent to the required permissions. The user consent request doesn't return a token. Instead, it records that the user granted the agent permission to act on their behalf. Token acquisition happens in Authenticate the user and request a token.

Important

Use the **agent identity** client ID in the `client_id` parameter, not the agent identity blueprint ID.

To prompt a user for consent, construct an authorization URL and redirect the user to it. The agent can present this URL in different ways, for example, as a link in a chat message.

```text
https://login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/v2.0/authorize?
  client_id=<agent-identity-id>
  &response_type=none
  &redirect_uri=https%3A%2F%2Fmyagentapp.com%2Fauthorize
  &response_mode=query
  &scope=User.Read
  &state=xyz123
```

When the user opens this URL, Microsoft Entra ID prompts them to sign in and grant consent. After consent, the user is sent back to the redirect URI.

The key parameters in the user consent authorization URL are:

- `client_id`: The agent identity client ID (not the agent identity blueprint client ID).
- `response_type`: Set to `none` because this request records consent only. Token acquisition uses `response_type=code` in Authenticate the user and request a token.
- `redirect_uri`: Must match exactly the redirect URI configured on the agent identity blueprint.
- `scope`: Specify the delegated permissions you need (for example, `User.Read`).
- `state`: Optional parameter for maintaining state between the request and callback.

For more information on OAuth authorization concepts, see [Permissions and consent in the Microsoft identity platform](/en-us/entra/identity-platform/permissions-consent-overview).

#### Request admin consent for all users

Agents can also request authorization from a Microsoft Entra ID administrator, who can grant consent to the agent for all users in their tenant. Admin consent might be required depending on the consent settings configured in the tenant.

To grant tenant-wide admin consent, direct an administrator to the following URL. Use the agent identity ID in the `client_id` parameter.

```text
https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0/adminconsent
?client_id=<agent-identity-id>
&scope=User.Read
&redirect_uri=<redirect-uri>
&state=xyz123
```

After the administrator grants consent, the permissions apply to the whole tenant. Users don't need to consent again.

Note

Configure a redirect URI on your blueprint and include a `state` parameter in the consent request. When consent is granted, the user is sent to the redirect URI where you can display confirmation. Your endpoint can use the `state` parameter to track that permission was granted. For single-tenant agents, you can alternatively retry token requests until consent is granted because the tenant ID is already known.

## Authenticate the user and request a token

After consent is granted, the client app (such as a frontend or mobile app) initiates an OAuth 2.0 authorization code request to obtain a token where the audience is the agent identity blueprint. In this step, `client_id` refers to the client app's own registered application ID, not the agent identity or agent identity blueprint.

Note

The `redirect_uri` in this request belongs to the **client app's** registration, not the blueprint's redirect URI configured in the previous consent step.

1. Redirect the user to the Microsoft Entra ID authorization endpoint with the following parameters:

    ```http
    GET https://login.microsoftonline.com/<your-tenant-id>/oauth2/v2.0/authorize?client_id=<client-app-id>
    &response_type=code
    &redirect_uri=<redirect_uri>
    &response_mode=query
    &scope=api://<agent-blueprint-id>/access_agent
    &state=abc123
    ```
2. After the user signs in, your app receives an authorization code at the redirect URI. Exchange the authorization code for an access token:

    ```http
    POST https://login.microsoftonline.com/<your-tenant-id>/oauth2/v2.0/token
    Content-Type: application/x-www-form-urlencoded
    
    client_id=<client-app-id>
    &grant_type=authorization_code
    &code=<authorization_code>
    &redirect_uri=<redirect_uri>
    &scope=api://<agent-blueprint-id>/access_agent
    &client_secret=<client-secret>
    ```

    Include the `client_secret` parameter only if using a confidential client.

    The JSON response contains an access token that can be used to access the agent's API.

## Validate the access token

The web API must validate the incoming access token before the agent can act. Always use an approved library to validate tokens. Don't write your own token validation code.

1. Install the `Microsoft.Identity.Web` NuGet package:

    ```bash
    dotnet add package Microsoft.Identity.Web
    ```
2. In your ASP.NET Core web API project, implement Microsoft Entra ID authentication:

    ```csharp
    // Program.cs
    using Microsoft.AspNetCore.Authentication.JwtBearer;
    using Microsoft.Identity.Web;
    
    var builder = WebApplication.CreateBuilder(args);
    
    builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
        .AddMicrosoftIdentityWebApi(builder.Configuration.GetSection("AzureAd"));
    
    var app = builder.Build();
    
    app.UseAuthentication();
    app.UseAuthorization();
    ```
3. Configure authentication credentials in the `appsettings.json` file:

    Warning

    Client secrets shouldn't be used as client credentials in production environments for agent identity blueprints due to security risks. Instead, use more secure authentication methods such as [federated identity credentials (FIC) with managed identities](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity) or client certificates. These methods provide enhanced security by eliminating the need to store sensitive secrets directly within your application configuration.

    ```json
    "AzureAd": {
        "Instance": "https://login.microsoftonline.com/",
        "TenantId": "<your-tenant-id>",
        "ClientId": "<agent-blueprint-id>",
        "Audience": "<agent-blueprint-id>",
        "ClientCredentials": [
            {
                "SourceType": "ClientSecret",
                "ClientSecret": "your-client-secret"
            }
        ]
    }
    ```

For more information about Microsoft.Identity.Web, see [Microsoft.Identity.Web documentation](/en-us/entra/msal/dotnet/microsoft-identity-web/).

## Validate user claims

After access token validation, the agent can identify the user and perform authorization checks. The following example API route extracts user claims from the access token and returns them in the API response:

```csharp
app.MapGet("/hello-agent", (HttpContext httpContext) =>
{   
    var claims = httpContext.User.Claims.Select(c => new
    {
        Type = c.Type,
        Value = c.Value
    });

    return Results.Ok(claims);
})
.RequireAuthorization();
```

## Acquire tokens for downstream APIs

After an interactive agent validates the user's token, it can request access tokens to call downstream APIs on behalf of the user. The On-Behalf-Of (OBO) flow allows the agent to:

- Receive an access token from a client.
- Exchange it for a new access token for a downstream API like Microsoft Graph.
- Use that new token to access protected resources on behalf of the original user.

# [Use Microsoft Identity Web](#tab/identity-web-tokens)
The `Microsoft.Identity.Web` library simplifies the OBO implementation by handling token exchange automatically, so you don't have to manually implement the flow by following the protocol.

1. Install the required NuGet packages:

    ```bash
    dotnet add package Microsoft.Identity.Web
    dotnet add package Microsoft.Identity.Web.AgentIdentities
    ```
2. In your ASP.NET Core web API project, update the Microsoft Entra ID authentication implementation:

    ```csharp
    // Program.cs
    using Microsoft.AspNetCore.Authorization;
    using Microsoft.Identity.Abstractions;
    using Microsoft.Identity.Web;
    using Microsoft.Identity.Web.Resource;
    using Microsoft.Identity.Web.TokenCacheProviders.InMemory;
    
    var builder = WebApplication.CreateBuilder(args);
    
    builder.Services.AddMicrosoftIdentityWebApiAuthentication(builder.Configuration)
        .EnableTokenAcquisitionToCallDownstreamApi();
    builder.Services.AddAgentIdentities();
    builder.Services.AddInMemoryTokenCaches();
    
    var app = builder.Build();
    
    app.UseAuthentication();
    app.UseAuthorization();
    
    app.Run();
    ```
3. In the agent API, exchange the incoming user access token for a new access token for the agent identity. `Microsoft.Identity.Web` validates the incoming access token and handles the on-behalf-of token exchange:

    ```csharp
    app.MapGet("/agent-obo-user", async (HttpContext httpContext) =>
    {
        string agentIdentity = "<your-agent-identity>";
        IAuthorizationHeaderProvider authorizationHeaderProvider = httpContext.RequestServices.GetService<IAuthorizationHeaderProvider>()!;
        AuthorizationHeaderProviderOptions options = new AuthorizationHeaderProviderOptions().WithAgentIdentity(agentIdentity);
    
        string authorizationHeaderWithUserToken = await authorizationHeaderProvider.CreateAuthorizationHeaderForUserAsync(["https://graph.microsoft.com/.default"], options);
    
        var response = new { header = authorizationHeaderWithUserToken };
        return Results.Json(response);
    })
    .RequireAuthorization();
    ```

# [Use Microsoft Graph SDK](#tab/graph-sdk-tokens)
If you're using the Microsoft Graph SDK, you can authenticate to Microsoft Graph using the `GraphServiceClient`.

1. Install the required NuGet packages:

    ```bash
    dotnet add package Microsoft.Identity.Web
    dotnet add package Microsoft.Identity.Web.AgentIdentities
    dotnet add package Microsoft.Identity.Web.GraphServiceClient
    ```
2. In your ASP.NET Core web API project, configure authentication and add support for Microsoft Graph:

    ```csharp
    // Program.cs
    using Microsoft.AspNetCore.Authorization;
    using Microsoft.Identity.Web;
    using Microsoft.Identity.Web.TokenCacheProviders.InMemory;
    
    var builder = WebApplication.CreateBuilder(args);
    
    builder.Services.AddMicrosoftIdentityWebApiAuthentication(builder.Configuration)
        .EnableTokenAcquisitionToCallDownstreamApi();
    builder.Services.AddAgentIdentities();
    builder.Services.AddInMemoryTokenCaches();
    builder.Services.AddMicrosoftGraph();
    
    var app = builder.Build();
    
    app.UseAuthentication();
    app.UseAuthorization();
    
    app.Run();
    ```
3. Get a `GraphServiceClient` from the service provider and call Microsoft Graph APIs with the agent identity:

    ```csharp
    app.MapGet("/agent-obo-user", async (HttpContext httpContext) =>
    {
        string agentIdentity = "<your-agent-identity>";
    
        GraphServiceClient graphServiceClient = httpContext.RequestServices.GetService<GraphServiceClient>()!;
        var me = await graphServiceClient.Me.GetAsync(r => r.Options.WithAuthenticationOptions(
            o =>
            {
                o.WithAgentIdentity(agentIdentity);
            }));
        return me.UserPrincipalName;
    })
    .RequireAuthorization();
    ```

---

Under the hood, the OBO flow involves two token exchanges: first, the agent identity blueprint obtains an exchange token using its client credential, and then the agent identity exchanges that token along with the user's access token for a downstream API token. For the full protocol walkthrough, including HTTP request formats and token validation details, see [On-behalf-of flow in agents](agent-on-behalf-of-oauth-flow).