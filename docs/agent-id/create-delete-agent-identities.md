---
layout: Conceptual
title: Create agent identities in Microsoft agent identity platform - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/create-delete-agent-identities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to create agent identities that represent AI agents in your tenant using Microsoft Graph APIs and various authentication libraries.
ms.topic: how-to
ms.date: 2026-04-28T00:00:00.0000000Z
ms.reviewer: dastrock
locale: en-us
document_id: 6f2b9af0-c29f-68d9-f598-c459f8419033
document_version_independent_id: 6f2b9af0-c29f-68d9-f598-c459f8419033
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/create-delete-agent-identities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/create-delete-agent-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/create-delete-agent-identities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 8519594b-3213-d794-9fb0-0a30049c9084
---

# Create agent identities in Microsoft agent identity platform - Microsoft Entra Agent ID | Microsoft Learn

After you create an agent identity blueprint, the next step is to create one or more [agent identities](agent-identities) that represent AI agents in your tenant. Agent identity creation is typically performed when provisioning a new AI agent.

You can create agent identities in two ways:

- **Microsoft Entra admin center** — Use the admin center wizard for quick, individual identity creation.
- **Microsoft Graph API** — Build a web service that creates agent identities programmatically, which is useful for automated provisioning at scale.

If you want to quickly create agent identities for testing purposes, consider using [this Microsoft Entra PowerShell module for creating and using agent identities](https://aka.ms/agentidpowershell).

## Prerequisites

To create agent identities, you need:

- An [agent identity blueprint](create-blueprint). Record the agent identity blueprint app ID from the creation process.
- A web service or application (running locally or deployed to Azure) that hosts the agent identity creation logic. This prerequisite applies only if you're creating agent identities programmatically.

## Use the Microsoft Entra admin center

You can create an agent identity directly in the Microsoft Entra admin center by selecting an existing blueprint and assigning owners and sponsors.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Agents** &gt; **Agent identities**.
3. Select **New agent identity (Preview)**.
4. On the **Basics** tab:

    - Under **Agent blueprint**, select a blueprint to create your agent identity from.
    - Enter a name in the **Agent identity name** field and select **Next**.

        [![Screenshot of the create agent identity wizard showing the Basics tab with blueprint selection and name fields.](media/create-delete-agent-identities/create-agent-identity-wizard.png)](media/create-delete-agent-identities/create-agent-identity-wizard.png#lightbox)
5. On the **Owners & Sponsors** tab, optionally add owners and sponsors for the identity:

    - Select the pencil icon next to the **Owners** field to change or add users who can manage this agent identity.
    - Select the pencil icon next to the **Sponsors** field to change or add users who can sponsor this agent identity.

    Note

    Sponsors can be users, dynamic membership groups, or Microsoft 365 groups. Security groups and role-assignable groups are not supported as sponsors.
6. Select **Next**.
7. Review your settings, and then select **Create**.
8. Select **Done** to exit the wizard or **Go to agent identity** to view the identity's detail page or configure more settings.

In the following steps, you'll learn how to create agent identities programmatically using Microsoft Graph API and Microsoft.Identity.Web. Get an access token first, then call the creation API.

# [Microsoft Graph API](#tab/microsoft-graph-api)
### Get an access token using agent identity blueprint

You use the agent identity blueprint to create each agent identity. Request an access token from Microsoft Entra using your agent identity blueprint:

When using a managed identity as a credential, you must first obtain an access token using your managed identity. Managed identity tokens can be requested from an IP address locally exposed in the compute environment. Refer to the [managed identity documentation for details](/en-us/entra/identity/managed-identities-azure-resources/).

```
GET http://169.254.169.254/metadata/identity/oauth2/token?api-version=2019-08-01&resource=api://AzureADTokenExchange/.default
Metadata: True
```

After you obtain a token for the managed identity, request a token for the agent identity blueprint:

```
POST https://login.microsoftonline.com/<your-tenant-id>/oauth2/v2.0/token
Content-Type: application/x-www-form-urlencoded

client_id=<agent-blueprint-id>
scope=https://graph.microsoft.com/.default
client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer
client_assertion=<msi-token>
grant_type=client_credentials
```

A `client_secret` parameter can also be used instead of `client_assertion` and `client_assertion_type`, when a client secret is being used in local development.

# [Microsoft.Identity.Web](#tab/microsoft-identity-web)
To install Microsoft.Identity.Web:

```ps
dotnet add package Microsoft.Identity.Web
```

*Microsoft.Identity.Web* includes an interface that automatically requests an access token and attaches it to outbound HTTP requests. When using *Microsoft.Identity.Web*, you can skip to the next step.

---

## Create an agent identity

Using the access token acquired in the previous step, you can now create agent identities in your tenant. Agent identity creation might occur in response to many different events or triggers, such as a user selecting a button to create a new agent. We recommend you create one agent identity for each agent, but you might choose a different approach based on your needs.

# [Microsoft Graph API](#tab/microsoft-graph-api)
Always include the OData-Version header when using @odata.type.

```
POST https://graph.microsoft.com/beta/serviceprincipals/Microsoft.Graph.AgentIdentity
OData-Version: 4.0
Content-Type: application/json
Authorization: Bearer <token>
{"displayName": "My Agent Identity","agentIdentityBlueprintId": "<my-agent-blueprint-id>","sponsors@odata.bind": [	"https://graph.microsoft.com/v1.0/users/<id>",	"https://graph.microsoft.com/v1.0/groups/<group-id>"]
}
```

Note

When assigning a group as sponsor, only [supported group types](agent-owners-sponsors-managers#sponsors) are accepted. Groups aren't supported as owners.

# [Microsoft.Identity.Web](#tab/microsoft-identity-web)
To use *Microsoft.Identity.Web* to execute the Microsoft Graph API request to create an agent identity, add the following MISE configuration file:

Warning

Client secrets shouldn't be used as client credentials in production environments for agent identity blueprints due to security risks. Instead, use more secure authentication methods such as [federated identity credentials (FIC) with managed identities](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity) or client certificates. These methods provide enhanced security by eliminating the need to store sensitive secrets directly within your application configuration.

```json
{
  "AzureAd": {"Instance": "https://login.microsoftonline.com/","TenantId": "<your-tenant-id>","ClientId": "<my-agent-blueprint-id>","Scopes": "access_agent","ClientCredentials": [	{		"SourceType": "ClientSecret",		"ClientSecret": "your-client-secret"	}]
  },

  "DownstreamApis": {"agent-identity": {  "BaseUrl": "https://graph.microsoft.com",  "RelativePath": "/beta/serviceprincipals/Microsoft.Graph.AgentIdentity",  "Scopes": ["00000003-0000-0000-c000-000000000000/.default"],  "RequestAppToken": true}
  }
}
```

The code for the ASP.NET Core app (*Program.cs*) is the following example:

```csharp
using System.Text.Json.Serialization;
using Microsoft.Identity.Abstractions;
using Microsoft.Identity.Web;
using Microsoft.Identity.Web.Resource;
using Microsoft.IdentityModel.S2S.Extensions.AspNetCore;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddMicrosoftIdentityWebApiAuthentication(builder.Configuration)
    .EnableTokenAcquisitionToCallDownstreamApi();
builder.Services.AddInMemoryTokenCaches();
var app = builder.Build();

app.UseHttpsRedirection();
app.UseAuthentication();
app.UseAuthorization();

// Create an Agent identity
app.MapGet("/create-agent-identity", async (HttpContext httpContext) =>
{
    try
    {
        // Get the service to call the downstream API (preconfigured in the appsettings.json file)
        IDownstreamApi downstreamApi = httpContext.RequestServices.GetRequiredService<IDownstreamApi>();

        // Call the downstream API with a POST request to create an Agent Identity
        var jsonResult = await downstreamApi.PostForAppAsync<AgentIdentity, AgentIdentity>(
            "agent-identity",
            new AgentIdentity
            {
                displayName = "My agent identity",
                agentIdentityBlueprintId = "<my-agent-blueprint-id>",
                sponsorsOdataBind = new[] { "https://graph.microsoft.com/v1.0/users/<id>" }
            });
        return jsonResult?.id;
    }
    catch (Exception ex)
    {
        return ex.Message;
    }
});

app.Run();

// Type declarations must follow the top-level statements.
public class AgentIdentity
{
    [JsonPropertyName("@odata.type")]
    public string @odata_type { get; set; } = "#Microsoft.Graph.AgentIdentity";

    [JsonPropertyName("displayName")]
    public string? displayName { get; set; }

    [JsonPropertyName("agentIdentityBlueprintId")]
    public string? agentIdentityBlueprintId { get; set; }

    [JsonPropertyName("id")]
    public string? id { get; set; }

    [JsonPropertyName("sponsors@odata.bind")]
    public string[]? sponsorsOdataBind { get; set; }

    [JsonPropertyName("owners@odata.bind")]
    public string[]? ownersOdataBind { get; set; }
}
```

---

## Delete an agent identity

When an agent is deallocated or destroyed, your service should also delete the associated agent identity:

# [Microsoft Graph API](#tab/microsoft-graph-api)
```http
DELETE https://graph.microsoft.com/beta/serviceprincipals/<agent-identity-id>
OData-Version: 4.0
Content-Type: application/json
Authorization: Bearer <token>
```

# [Microsoft.Identity.Web](#tab/microsoft-identity-web)
```csharp
// Delete an Agent identity
app.MapGet("/delete-agent-identity", async (HttpContext httpContext, string id) =>
{// Get the service to call the downstream API (preconfigured in the appsettings.json file)IDownstreamApi downstreamApi = httpContext.RequestServices.GetRequiredService<IDownstreamApi>();
// Call the downstream API with a DELETE request to remove an Agent Identityvar jsonResult = await downstreamApi.DeleteForAppAsync<string, string>(	"agent-identity",	null!,	options =>	{		options.RelativePath += $"/{id}"; // Specify the ID of the agent identity to delete	});return jsonResult;
});
```

---