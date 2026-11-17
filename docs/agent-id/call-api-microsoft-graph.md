---
layout: Conceptual
title: Call Microsoft Graph as an agent with ASP.NET Core - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/call-api-microsoft-graph
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Configure GraphServiceClient to call Microsoft Graph with an app-only token for an agent identity.
ms.topic: how-to
ms.date: 2026-11-05T00:00:00.0000000Z
ai-usage: ai-assisted
ms.reviewer: jmprieur
locale: en-us
document_id: 80830347-872a-b5f7-134f-c5dc1b0cd84b
document_version_independent_id: 80830347-872a-b5f7-134f-c5dc1b0cd84b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/call-api-microsoft-graph.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/call-api-microsoft-graph
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/call-api-microsoft-graph.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 0c5388c7-4acb-7659-ab1a-f4e7a48f750a
---

# Call Microsoft Graph as an agent with ASP.NET Core - Microsoft Entra Agent ID | Microsoft Learn

List directory users with the agent's application permissions, not the inbound caller's delegated access.

In this article, you configure `GraphServiceClient` to obtain a Microsoft Graph token for the agent while the agent API separately authorizes the caller.

## Prerequisites

- The Microsoft Graph application permissions required by the operation.
- Application permissions granted to the agent identity with admin consent. See [Grant Microsoft Graph application permissions to an agent identity](grant-application-permissions-agent-identity).
- The [blueprint credential and ASP.NET Core services](call-api-custom#configure-the-blueprint-credential), including token acquisition and the `AgentUser` inbound authorization policy. Reuse its local certificate configuration for workstation testing. You don't need that walkthrough's custom API app role or consent grant for this Microsoft Graph example.

## Add Microsoft Graph

Install the integration package:

```dotnetcli
dotnet add package Microsoft.Identity.Web.GraphServiceClient
```

Register `GraphServiceClient` with the services configured in the parent article. For app-only access, call `builder.Services.AddMicrosoftGraph` with `options.BaseUrl` set to `https://graph.microsoft.com/v1.0` and `options.Scopes` set to `["https://graph.microsoft.com/.default"]`. Use the configured client ID directly; don't add `WithAgentIdentity`.

Place this registration before `builder.Build()` in the agent API's `Program.cs`.

```csharp
builder.Services.AddMicrosoftGraph(options =>
{
    options.BaseUrl = "https://graph.microsoft.com/v1.0";
    options.Scopes = ["https://graph.microsoft.com/.default"];
});
```

## Call Microsoft Graph

Set `RequestAppToken` to `true` so `GraphServiceClient` acquires an app-only token for the agent identity:

Merge the following `using` directives with those at the top of `Program.cs`, and insert the endpoint before its single `app.Run()`. You can omit the custom API endpoint.

```csharp
using Microsoft.Graph;
using Microsoft.Identity.Web;

app.MapGet("/graph-users", async (GraphServiceClient graphClient) =>
{
    var users = await graphClient.Users.GetAsync(request =>
        request.Options.WithAuthenticationOptions(options =>
        {
            options.RequestAppToken = true;
        }));

    return Results.Ok(users?.Value);
})
.RequireAuthorization("AgentUser");
```

The client uses the shared client ID and blueprint credential configured in the parent article. Don't add an Agent ID override. The example requires an application permission that can list users, such as `User.Read.All`. Grant only the permissions required by your calls.

## Verify the Graph call

Follow the parent journey's [API access test](call-api-custom#verify-api-access), replacing `/custom-api` with `/graph-users`. Expect `200` and a JSON collection of users when the agent has the required Graph application permission. This endpoint returns the first response page, not necessarily every user in the directory.

Without an inbound token, expect `401`. With an otherwise valid token missing `Agent.User`, expect `403` if the tenant issues that token. A downstream Graph failure causes the sample to throw rather than returning that same status from the agent. Verify Graph consent on the agent identity separately from the caller's role assignment.