---
layout: Conceptual
title: Call a custom API as an agent with ASP.NET Core - Microsoft Entra Agent ID | Microsoft Learn
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
description: Configure an ASP.NET Core agent to get an app-only token and call a custom API.
ms.topic: how-to
ms.date: 2026-11-06T00:00:00.0000000Z
ms.reviewer: jmprieur, jomondi, dastrock
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
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
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/64b65f6c-101f-411a-9b83-9f577fab52d0
- https://authoring-docs-microsoft.poolparty.biz/devrel/d452572f-6212-498f-9050-ca4a9e50a425
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/1a667fd1-8145-4b11-af0f-9f5de205a6e5
- https://authoring-docs-microsoft.poolparty.biz/devrel/a12e40b7-59a2-4437-96e2-166ce622b864
platformId: 7294d6a1-4b4c-88b0-54d4-fc172fb5f035
---

# Call a custom API as an agent with ASP.NET Core - Microsoft Entra Agent ID | Microsoft Learn

Use app-only access when your cloud agent calls a custom API with its own permissions, not the signed-in user's access. In this walkthrough, an authorized user triggers the agent, and Microsoft.Identity.Web gets an app-only token for the downstream call.

You'll configure the credential, grant access, and verify a protected API response. The user's permission to invoke the agent and the agent's permission to call the downstream API are separate checks.

## Prerequisites

- An existing ASP.NET Core web API project and the .NET SDK for its target framework. The examples were tested with .NET 10 and Microsoft.Identity.Web 4.17.0; these are tested versions, not minimum supported versions.
- Completion of [Create an identity for your agent](create-single-instance-agent), including tenant enablement, administrator approvals, and the recorded client and object IDs.
- A credential registered on the blueprint: a certificate for local testing, or a managed identity federated credential for an Azure host.
- A custom API that exposes an application permission (app role), plus its application ID URI and HTTPS endpoint. The API must validate access tokens and enforce that role.
- An administrator to grant the downstream application permission. For standard tenant-wide consent to a custom API, **Cloud Application Administrator**, **Application Administrator**, or **AI Administrator** can grant consent. Microsoft Graph application permissions instead require **Privileged Role Administrator**. Confirm the applicable role for this preview with your Microsoft representative. See [Grant tenant-wide admin consent](../identity/enterprise-apps/grant-admin-consent).
- An authorized Microsoft Graph management client with `Application.Read.All` to verify the assignment. For delegated access, the signed-in user also needs a supported role, such as **Directory Readers**. This read permission doesn't grant runtime access.
- A caller configured through [Authenticate users to the agent API](aspnet-core-authenticate-users), with `Agent.User` configured, verified, and assigned through [Control access to agents](control-user-access-agents#define-app-roles). Complete both role-definition steps in that procedure. The sample retains `RequireRole("Agent.User")`; downstream consent doesn't authorize the caller.

## Install the packages

If you don't have an existing project, create one with `dotnet new webapi --framework net10.0 --name AgentApi`, then run `cd AgentApi`. Keep your existing target framework when adding this guidance to an existing project.

Run the following command from the directory containing your web API's project file:

```dotnetcli
dotnet add package Microsoft.Identity.Web --version 4.17.0
```

## Configure the blueprint credential

Use the configuration for where you run the API. Configure one credential source, not both.

# [Local workstation](#tab/local)
### Configure a local development credential

In the agent project's `appsettings.json`, set `AzureAd:Instance` to `https://login.microsoftonline.com/`, `AzureAd:TenantId` to your tenant ID, and `AzureAd:ClientId` to the client ID recorded during setup.

Use the [certificate registered during setup](create-single-instance-agent#add-a-certificate-for-confidential-clients). You need the corresponding PFX containing the private key, not just the public certificate uploaded to Microsoft Graph.

In `appsettings.Development.json`, use this `ClientCredentials` array. Don't append a managed identity credential or commit the PFX file.

```json
{
  "AzureAd": {
    "ClientCredentials": [
      {
        "SourceType": "Path",
        "CertificateDiskPath": "<absolute-path-to-local-pfx>"
      }
    ]
  }
}
```

In the PowerShell terminal that starts the app, set `$env:ASPNETCORE_ENVIRONMENT = "Development"` and set `$env:AzureAd__ClientCredentials__0__CertificatePassword = Read-Host "PFX password" -MaskInput`. Use PowerShell 7 for `-MaskInput`. The environment variable supplies the password without placing it in the JSON file or shell history. Clear it with `Remove-Item Env:\AzureAd__ClientCredentials__0__CertificatePassword` after stopping the app. Don't use this local file configuration in production.

# [Azure host](#tab/azure)
Use this configuration on an Azure host with the specified user-assigned managed identity assigned and its federated credential configured on the blueprint. It doesn't provide a workstation credential.

Set `ClientId` to the client ID recorded during setup in `appsettings.json`:

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "TenantId": "<tenant-id>",
    "ClientId": "<agent-client-id>",
    "ClientCredentials": [
      {
        "SourceType": "SignedAssertionFromManagedIdentity",
        "ManagedIdentityClientId": "<managed-identity-client-id>"
      }
    ]
  }
}
```

---

Warning

Client secrets shouldn't be used as client credentials in production environments for agent identity blueprints due to security risks. Instead, use more secure authentication methods such as [federated identity credentials (FIC) with managed identities](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity) or client certificates. These methods provide enhanced security by eliminating the need to store sensitive secrets directly within your application configuration.

## Grant application permissions

Declare the API's app role in the blueprint's `requiredResourceAccess`, as described in the creation procedure. Declaring a permission doesn't grant it.

Use the custom API's configured application ID URI followed by `/.default` in both the consent request and the token request. The default URI format is `api://<custom-api-client-id>`, but a custom URI must be used instead if the API defines one.

1. Have the administrator open the following URL in a browser, sign in, and review the requested permissions. Replace the placeholders, URL-encode the query parameter values, and join the lines into one URL. Use a `web` redirect URI registered on the blueprint, even when the agent only runs unattended. Generate a unique `state` value and retain it to validate the callback.

    ```http
    GET https://login.microsoftonline.com/<tenant-id>/v2.0/adminconsent
        ?client_id=<agent-client-id>
        &scope=<custom-api-application-id-uri>/.default
        &redirect_uri=<registered-web-redirect-uri>
        &state=<state>
    ```
2. Match the returned `state` to the value you sent. Confirm that `admin_consent=True` is present and no `error` parameter is returned. Error callbacks also include `admin_consent=True`. Check the expected tenant, but don't use the callback's tenant value to authenticate or authorize a caller. For the response formats, see [Admin consent on the Microsoft identity platform](../identity-platform/v2-admin-consent).
3. Open [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) and sign in to the same tenant with the authorized management account. Use **Modify permissions** to request `Application.Read.All`, and have an authorized administrator grant consent if required. Select **GET** and **v1.0**, then run the following request. Graph Explorer supplies its management access token; don't use the agent's downstream token.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals/<agent-identity-object-id>/appRoleAssignments
    ```

    Use the agent identity's `id` recorded during creation for `<agent-identity-object-id>`, not its shared OAuth client ID or the blueprint's object ID. Follow any `@odata.nextLink` values. Confirm that `principalId` is the agent identity's object ID, `resourceId` is the custom API's service principal object ID, and `appRoleId` is the intended role. For the required read permissions and delegated-user roles, see [List appRoleAssignments](/en-us/graph/api/serviceprincipal-list-approleassignments).

Allow time for a new assignment to become visible. If it remains missing, confirm the approved permission and tenant before requesting a token.

## Configure ASP.NET Core

In `Program.cs`, register Microsoft.Identity.Web, an HTTP client, and the inbound `AgentUser` authorization policy. This path uses ordinary confidential-client token acquisition, without `AddAgentIdentities` or `WithAgentIdentity`. The incoming caller's token is for the agent API; the downstream app-only token is for the custom API.

```csharp
using System.Net.Http.Headers;
using Microsoft.Identity.Abstractions;
using Microsoft.Identity.Web;

var builder = WebApplication.CreateBuilder(args);

builder.Services
    .AddMicrosoftIdentityWebApiAuthentication(builder.Configuration)
    .EnableTokenAcquisitionToCallDownstreamApi()
    .AddInMemoryTokenCaches();

builder.Services.AddHttpClient();
builder.Services.AddAuthorization(options =>
{
    options.AddPolicy(
        "AgentUser",
        policy => policy.RequireRole("Agent.User"));
});

var app = builder.Build();

app.UseAuthentication();
app.UseAuthorization();

// Map the custom API endpoint before app.Run().
app.Run();
```

## Call the API

Use `IAuthorizationHeaderProvider.CreateAuthorizationHeaderForAppAsync`. Pass the custom API's `.default` scope as a string. Replace `<custom-api-application-id-uri>` with the same URI you used for consent, and replace `https://api.contoso.com/data` with the API endpoint. The provider uses the configured client ID and credential directly.

Insert the following endpoint at the comment in `Program.cs`, before `app.Run()`. The required `using` directives are already at the top of the file. The endpoint gets an app-only authorization header and sends it to the custom API:

```csharp
app.MapGet("/custom-api", async (
    IAuthorizationHeaderProvider authorizationHeaderProvider,
    IHttpClientFactory httpClientFactory) =>
{
    string authorizationHeader = await authorizationHeaderProvider
        .CreateAuthorizationHeaderForAppAsync(
            "<custom-api-application-id-uri>/.default");

    HttpClient client = httpClientFactory.CreateClient();
    client.DefaultRequestHeaders.Authorization =
        AuthenticationHeaderValue.Parse(authorizationHeader);

    using HttpResponseMessage response =
        await client.GetAsync("https://api.contoso.com/data");
    response.EnsureSuccessStatusCode();

    return Results.Content(
        await response.Content.ReadAsStringAsync(),
        response.Content.Headers.ContentType?.ToString());
})
.RequireAuthorization("AgentUser");
```

The returned authorization header includes the `Bearer` scheme. Don't return tokens or authorization headers from a production endpoint.

The sample requires an authenticated caller with the `Agent.User` role. Configure that assignment through the [agent's inbound access policy](control-user-access-agents) before allowing the caller to trigger an app-only operation.

Request only the application permissions required by the endpoint. For guidance on defining and granting app roles, see [application roles](/en-us/entra/identity-platform/howto-add-app-roles-in-apps).

## Verify API access

A successful token response doesn't establish authorization at the API.

1. Run the project from its project directory in an environment where the configured blueprint credential is available. The managed identity configuration requires an Azure host with the specified managed identity and federation configured; it doesn't provide a local workstation credential.

    ```dotnetcli
    dotnet run --urls https://localhost:5001
    ```

    For a workstation, complete Configure a local development credential first. Trust the ASP.NET Core development certificate if necessary with `dotnet dev-certs https --trust`; this can require interactive confirmation. Don't disable certificate validation. For an unattended local smoke test of the unauthenticated `401` response only, you can instead start with `dotnet run --urls http://localhost:5001` and call that HTTP URL without a token. Don't send access tokens over HTTP.
2. Use the upstream client from [Authenticate users to the agent API](aspnet-core-authenticate-users) to obtain an access token **for the agent API**, with the required delegated scope and `Agent.User` role. Request a new token after changing assignments. Make it available as the `AGENT_API_ACCESS_TOKEN` environment variable in your test shell without recording it in source control or shell history. Don't substitute an ID token, Graph management token, or downstream custom API token.
3. In a separate PowerShell terminal, call the agent endpoint:

    ```powershell
    $response = Invoke-WebRequest `
        -Uri "https://localhost:5001/custom-api" `
        -Headers @{ Authorization = "Bearer $env:AGENT_API_ACCESS_TOKEN" }
    $response.StatusCode
    $response.Content
    ```

    For an API endpoint that returns `200 OK`, expect `200` and its response body. The agent calls the custom API as itself, not as the inbound user. A downstream non-success status causes `EnsureSuccessStatusCode` to fail; this sample doesn't translate downstream errors into matching inbound status codes.
4. Repeat the request without an authorization header: expect `401 Unauthorized` from the agent. With an otherwise valid agent API token that lacks `Agent.User`, expect `403 Forbidden` if the tenant issues that token. When assignment is required, the tenant might reject token issuance first.
5. At the downstream API, confirm signature, issuer, audience, lifetime, and the required app role are validated. Compare the validated token's `oid` with the agent identity object ID, not the blueprint object ID, and check its `roles` claim. See [Validate Agent ID tokens in a downstream API](how-to-validate-agent-tokens-downstream-api). A successful token response alone doesn't prove these checks.
6. Test the downstream API's rejection of a token without its required role, using a separate test identity or fixture rather than removing production grants. Expect rejection at that API; don't infer its status from the agent's exception response.

Don't log access tokens, certificate assertions, or private keys. Record correlation IDs and request times when troubleshooting.