---
layout: Conceptual
title: Secure a web API with Microsoft Entra ID - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/how-to-validate-agent-tokens-downstream-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Configure a web API to validate Agent ID access tokens and authorize requests from agents and users.
ms.topic: how-to
ms.date: 2026-11-05T00:00:00.0000000Z
ai-usage: ai-assisted
ms.reviewer: dastrock
locale: en-us
document_id: 079c1e26-95fd-ebda-f4d9-a7c2ba0d9858
document_version_independent_id: 079c1e26-95fd-ebda-f4d9-a7c2ba0d9858
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/how-to-validate-agent-tokens-downstream-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/how-to-validate-agent-tokens-downstream-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/how-to-validate-agent-tokens-downstream-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/d452572f-6212-498f-9050-ca4a9e50a425
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/a12e40b7-59a2-4437-96e2-166ce622b864
platformId: 85c48139-649b-f3b2-5910-89c47000e685
---

# Secure a web API with Microsoft Entra ID - Microsoft Entra Agent ID | Microsoft Learn

A downstream API must validate every access token before it trusts the Agent ID, user, or permissions represented by the token. Use a supported authentication middleware or token-validation library instead of parsing tokens in application code.

This article covers Microsoft identity platform v2.0 access tokens.

The API registration must expose the delegated scope or application role that each endpoint requires, and the calling client or agent must have the corresponding grant. For an assembled local delegated test, follow [Call a custom API as a user](aspnet-core-call-custom-api-as-user). For app-only caller setup and consent, follow [Call a custom API as an agent](call-api-custom).

## Configure token validation

Configure the API with:

- The Microsoft Entra tenant or accepted issuer set.
- The API's Application ID URI or client ID as the expected audience.
- Microsoft identity platform signing-key discovery.
- The delegated scopes or application roles required by each operation.

For ASP.NET Core, use Microsoft.Identity.Web. For other frameworks, use a Microsoft-supported JWT validation library.

For complete registration and framework guidance, see [Configure protected web API apps](/en-us/entra/identity-platform/scenario-protected-web-api-app-configuration).

## Configure an ASP.NET Core API

Install Microsoft.Identity.Web:

```dotnetcli
dotnet add package Microsoft.Identity.Web
```

Configure the tenant and API registration:

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "TenantId": "<tenant-id>",
    "ClientId": "<downstream-api-client-id>"
  }
}
```

Register token validation and protect delegated and app-only endpoints:

```csharp
using Microsoft.Identity.Web;
using Microsoft.Identity.Web.Resource;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddMicrosoftIdentityWebApiAuthentication(
    builder.Configuration);

builder.Services.AddAuthorization(options =>
{
    options.AddPolicy(
        "AgentApplication",
        policy => policy.RequireRole("Agent.Access"));
});

var app = builder.Build();

app.UseAuthentication();
app.UseAuthorization();

app.MapGet("/data-for-user", (HttpContext context) =>
{
    context.VerifyUserHasAnyAcceptedScope("access_as_user");
    return Results.Ok();
})
.RequireAuthorization();

app.MapGet("/data-for-agent", () => Results.Ok())
    .RequireAuthorization("AgentApplication");

app.Run();
```

Replace `access_as_user` with the delegated scope exposed by the API. Replace `Agent.Access` with the application role assigned to the Agent ID.

`AddMicrosoftIdentityWebApiAuthentication` validates the token signature, issuer, audience, and lifetime. `VerifyUserHasAnyAcceptedScope` enforces the delegated `scp` claim. `RequireRole` enforces the application permission in the `roles` claim.

For more complete authorization patterns, see [Verify scopes and app roles in a protected web API](/en-us/entra/identity-platform/scenario-protected-web-api-verification-scope-app-roles).

Test each endpoint with a token issued for **this downstream API**, not the agent's inbound token. With the required scope or role, the sample returns `200 OK`. Without a token or with the wrong audience, expect `401`. With an otherwise valid token for this API that lacks the required scope or role, expect rejection. Use the linked walkthroughs for token acquisition; don't return or log tokens to inspect them.

## Validate the token

Reject the request unless all of these checks succeed:

1. **Signature:** The token is signed by a trusted Microsoft Entra signing key.
2. **Issuer:** The `iss` claim matches an issuer accepted by the API.
3. **Audience:** The `aud` claim identifies this API.
4. **Lifetime:** The token is within its valid time window.
5. **Tenant:** The `tid` claim is allowed by the API's tenant policy.
6. **Client:** The authorized-party claim identifies an allowed client or blueprint where the API restricts callers.
7. **Agent identity:** Agent-specific claims, including the Agent ID relationship claims expected by the scenario, are present and valid.
8. **Permission:** Delegated requests contain the required `scp` value; app-only requests contain the required `roles` value.

Don't authorize a request based only on the presence of an Agent ID claim. Apply the same issuer, audience, lifetime, and permission checks used for other Microsoft Entra access tokens.

## Distinguish access types

| Access type | User context | Permission claim | API authorization |
| --- | --- | --- | --- |
| Agent acting as itself | None | `roles` | Verify the required application role and Agent ID. |
| Agent acting for a signed-in user | Signed-in user | `scp` | Verify the scope, user authorization, and Agent ID. |
| Agent acting as its user account | Agent's user account | `scp` | Verify the scope, account authorization, and Agent ID relationship. |

## Return authorization errors

- Return `401 Unauthorized` when the token is missing or invalid.
- Return `403 Forbidden` when the token is valid but lacks the required permission or resource access.

Don't include tokens or sensitive claim values in logs.