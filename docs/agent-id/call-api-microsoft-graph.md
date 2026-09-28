---
layout: Conceptual
title: Call Microsoft Graph API from an agent using .NET - Microsoft Entra Agent ID | Microsoft Learn
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
description: Learn how to call Microsoft Graph API from an agent using agent identities or agents' user accounts, including authentication configuration and implementation steps.
ms.topic: how-to
ms.date: 2025-11-04T00:00:00.0000000Z
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
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
platformId: 0c5388c7-4acb-7659-ab1a-f4e7a48f750a
---

# Call Microsoft Graph API from an agent using .NET - Microsoft Entra Agent ID | Microsoft Learn

This article explains how to call a Microsoft Graph API from an agent using agent identities or an agent's user account.

To call an API from an agent, you need to obtain an access token that the agent can use to authenticate itself to the API. We recommend using the *Microsoft.Identity.Web* SDK for .NET to call your web APIs. This SDK simplifies the process of acquiring and validating tokens. For other languages, use the [Microsoft Entra ID Auth SDK (sidecar)](/en-us/entra/msidweb/agent-id-sdk/overview).

## Prerequisites

- An agent identity with appropriate permissions to call the target API. You need a user for the on-behalf-of flow.
- An agent's user account with appropriate permissions to call the target API.

## Call a Microsoft Graph API

1. Install the *Microsoft.Identity.Web.GraphServiceClient* that handles authentication for the Graph SDK and the *Microsoft.Identity.Web.AgentIdentities* package to add support for agent identities.

    ```bash
    dotnet add package Microsoft.Identity.Web.GraphServiceClient
    dotnet add package Microsoft.Identity.Web.AgentIdentities
    ```
2. Add the support for Microsoft Graph and agent identities in your service collection.

    ```csharp
    using Microsoft.AspNetCore.Authentication.OpenIdConnect;
    using Microsoft.Identity.Web;
    
    var builder = WebApplication.CreateBuilder(args);
    
    // Add authentication (web app or web API)
    builder.Services.AddAuthentication(OpenIdConnectDefaults.AuthenticationScheme)
        .AddMicrosoftIdentityWebApp(builder.Configuration.GetSection("AzureAd"))
        .EnableTokenAcquisitionToCallDownstreamApi()
        .AddInMemoryTokenCaches();
    
    // Add Microsoft Graph support
    builder.Services.AddMicrosoftGraph();
    
    // Add Agent Identities support
    builder.Services.AddAgentIdentities();
    
    var app = builder.Build();
    app.UseAuthentication();
    app.UseAuthorization();
    app.Run();
    ```
3. Configure Graph and agent identity options in *appsettings.json*.

    Warning

    Client secrets shouldn't be used as client credentials in production environments for agent identity blueprints due to security risks. Instead, use more secure authentication methods such as [federated identity credentials (FIC) with managed identities](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity) or client certificates. These methods provide enhanced security by eliminating the need to store sensitive secrets directly within your application configuration.

    ```json
    {
      "AzureAd": {
        "Instance": "https://login.microsoftonline.com/",
        "TenantId": "<your-tenant-id>",
        "ClientId": "<agent-blueprint-client-id>",
        "ClientCredentials": [
          {
            "SourceType": "ClientSecret",
            "ClientSecret": "your-client-secret"
          }
        ]
      },
      "DownstreamApis": {
        "MicrosoftGraph": {
          "BaseUrl": "https://graph.microsoft.com/v1.0",
          "Scopes": ["User.Read", "User.ReadBasic.All"]
        }
      }
    }
    ```

    Note

    Configure only the Microsoft Graph permissions your agent needs, and make sure the `Scopes` you set match the Graph resources your code calls. These examples use `User.Read` and `User.ReadBasic.All`; calling other resources requires their corresponding permissions.
4. You can now get the `GraphServiceClient` injecting it in your service or from the service provider and call Microsoft Graph.

- For agent identities, you can acquire either an app only token (autonomous agents) or an on-behalf of user token (interactive agents) by using the `WithAgentIdentity` method. For app only tokens, set the `RequestAppToken` property to `true`. For delegated on-behalf of user tokens, don't set the `RequestAppToken` property or explicitly set it to `false`.

    ```csharp
    using Microsoft.Graph;
    using Microsoft.Identity.Web;
    
    // Get the GraphServiceClient
    GraphServiceClient graphServiceClient = serviceProvider.GetRequiredService<GraphServiceClient>();
    
    string agentIdentity = "agent-identity-guid";
    
    // Call Microsoft Graph APIs with the agent identity for app only scenario
    var usersAppOnly = await graphServiceClient.Users
        .GetAsync(r => r.Options.WithAuthenticationOptions(options =>
        {
            options.WithAgentIdentity(agentIdentity);
            options.RequestAppToken = true; // Set to true for app only
        }));
    
    // Call Microsoft Graph APIs with the agent identity for on-behalf of user scenario
    var usersOnBehalfOfUser = await graphServiceClient.Users
        .GetAsync(r => r.Options.WithAuthenticationOptions(options =>
        {
            options.WithAgentIdentity(agentIdentity);
            options.RequestAppToken = false; // False to show it's on-behalf of user
        }));
    ```

    - For agent's user account identities, you can specify either User Principal Name (UPN) or Object Identity (OID) to identify the agent's user account by using the `WithAgentUserIdentity` method.

        ```csharp
        using Microsoft.Graph;
        using Microsoft.Identity.Web;
        
        // Get the GraphServiceClient
        GraphServiceClient graphServiceClient = serviceProvider.GetRequiredService<GraphServiceClient>();
        
        string agentIdentity = "agent-identity-guid";
        
        // Call Microsoft Graph APIs with the agent's user account identity using UPN
        string userUpn = "user-upn";
        var me = await graphServiceClient.Me
            .GetAsync(r => r.Options.WithAuthenticationOptions(options =>
                options.WithAgentUserIdentity(agentIdentity, userUpn)));
        
        // Or using OID
        string userOid = "user-object-id";
        var meByOid = await graphServiceClient.Me
            .GetAsync(r => r.Options.WithAuthenticationOptions(options =>
                options.WithAgentUserIdentity(agentIdentity, userOid)));
        ```