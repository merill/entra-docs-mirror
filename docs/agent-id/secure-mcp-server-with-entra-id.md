---
layout: Conceptual
title: Secure an MCP server with Microsoft Entra ID - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/secure-mcp-server-with-entra-id
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to protect an MCP server and check client access tokens.
ms.topic: how-to
ms.date: 2026-11-05T00:00:00.0000000Z
ms.reviewer: dastrock
ai-usage: ai-assisted
locale: en-us
document_id: 3dae09c9-a5ff-1449-f5b2-a72bc8b8b16c
document_version_independent_id: 3dae09c9-a5ff-1449-f5b2-a72bc8b8b16c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/secure-mcp-server-with-entra-id.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/secure-mcp-server-with-entra-id
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/secure-mcp-server-with-entra-id.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a700c79c-2a4b-e611-3a61-741effb2dc7b
---

# Secure an MCP server with Microsoft Entra ID - Microsoft Entra Agent ID | Microsoft Learn

An MCP server is an OAuth 2.0 protected resource. Register the server as an API in Microsoft Entra ID, publish protected-resource metadata, and validate each access token before processing an MCP request.

This guidance supports Microsoft identity platform v2.0 access tokens only.

## Prerequisites

- A Microsoft Entra tenant.
- An HTTPS endpoint for the MCP server.
- Permission to create an app registration and grant consent.
- An MCP client that supports OAuth protected-resource metadata.

## Register the MCP server

1. Register an application for the MCP server.
2. Set an Application ID URI that uniquely identifies the server.
3. Expose the delegated scopes required by MCP clients.
4. Define application roles only if the server supports app-only access.
5. Record the tenant ID, application client ID, and Application ID URI.

Grant only the permissions required by the tools and resources that the server exposes.

## Publish protected-resource metadata

Publish a metadata document at `<server-url>/.well-known/oauth-protected-resource`. MCP clients that support OAuth protected-resource discovery fetch this document to find the authorization server and supported scopes before requesting a token.

The following example shows a minimal document for a Microsoft Entra-backed MCP server:

```json
{
  "resource": "https://mcp.contoso.com",
  "authorization_servers": [
    "https://login.microsoftonline.com/<tenant-id>/oauth21/2026-08"
  ],
  "scopes_supported": [
    "mcp.access"
  ],
  "bearer_methods_supported": [
    "header"
  ]
}
```

- **`resource`** — The Application ID URI registered for the MCP server. This value must match the `aud` claim the server expects in incoming tokens.
- **`authorization_servers`** — The Microsoft Entra authorization server URL, `https://login.microsoftonline.com/<tenant>/oauth21/2026-08`. Use your tenant ID for a server that accepts users from a single tenant, or `common` for a server that accepts users from any organization. Clients append `/.well-known/openid-configuration` to this URL to discover the authorization and token endpoints.
- **`scopes_supported`** — The delegated scopes exposed by the MCP server. List only the scopes clients need to call the server.
- **`bearer_methods_supported`** — Set to `["header"]` to indicate that clients must send the token in the `Authorization` request header.

For the full metadata format and discovery behavior, see the [MCP authorization specification](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization).

## Validate access tokens

Require an access token on protected MCP requests. Validate the token's signature, issuer, audience, lifetime, tenant, client, and permissions.

Use the MCP server's Application ID URI or client ID as the expected audience, according to its registration. Enforce delegated scopes from `scp` and application permissions from `roles`.

For the complete validation checklist, see [Validate Agent ID tokens in a downstream API](how-to-validate-agent-tokens-downstream-api).

## Configure token validation in ASP.NET Core

Install Microsoft.Identity.Web:

```dotnetcli
dotnet add package Microsoft.Identity.Web
```

Configure the tenant and MCP server registration:

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "TenantId": "<tenant-id>",
    "ClientId": "<mcp-server-client-id>"
  }
}
```

Register token validation and define a policy for the MCP delegated scope or application role:

```csharp
using Microsoft.Identity.Web;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddMicrosoftIdentityWebApiAuthentication(
    builder.Configuration);

builder.Services.AddAuthorization(options =>
{
    options.AddPolicy("McpAccess", policy =>
    {
        policy.RequireAuthenticatedUser();
        policy.RequireAssertion(context =>
            context.User.IsInRole("Mcp.Access")
            || context.User.FindAll("scp").Any(claim =>
                claim.Value
                    .Split(' ', StringSplitOptions.RemoveEmptyEntries)
                    .Contains("mcp.access", StringComparer.Ordinal)));
    });
});

var app = builder.Build();

app.UseAuthentication();
app.UseAuthorization();

app.MapPost("/mcp", () => Results.Ok())
    .RequireAuthorization("McpAccess");

app.Run();
```

Replace `mcp.access` with the delegated scope exposed by the MCP server. Replace `Mcp.Access` with its application role. Apply the `McpAccess` policy to the endpoint mapped by the MCP server framework rather than adding a second `/mcp` route.

The `Results.Ok()` handler is an authorization placeholder, not an MCP implementation. After applying the policy to your framework's endpoint, verify that an authorized client can perform the intended MCP tool or resource operation. Also test a missing token and a valid token without the required permission; an HTTP success from the placeholder alone doesn't verify MCP interoperability.

The authentication middleware returns `401 Unauthorized` for a missing or invalid token. The authorization policy returns `403 Forbidden` when a valid token lacks both the required delegated scope and application role.

For complete framework and authorization guidance, see [Configure protected web API apps](/en-us/entra/identity-platform/scenario-protected-web-api-app-configuration) and [Verify scopes and app roles in a protected web API](/en-us/entra/identity-platform/scenario-protected-web-api-verification-scope-app-roles).

## Connect a client

The client discovers the protected-resource metadata, signs in or authenticates through Microsoft Entra ID, requests a token for the MCP server, and sends the token in the request's `Authorization` header.

Use one of these client identity models:

- A registered Agent ID.
- A local public-client Agent ID using authorization code flow with PKCE.
- A [Client ID Metadata Document](client-id-metadata-documents) URL when preregistration isn't practical.

The MCP server doesn't need different token-validation logic for CIMD clients. Microsoft Entra ID still issues the access token, and the server validates it against the same issuer and audience policy.