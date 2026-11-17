---
layout: Conceptual
title: Call Azure services from an agent using .NET Azure SDK - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/call-api-azure-services
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Call Azure services as an agent by using MicrosoftIdentityTokenCredential and the .NET Azure SDK.
ms.topic: how-to
ms.date: 2026-11-05T00:00:00.0000000Z
ai-usage: ai-assisted
ms.reviewer: jmprieur
locale: en-us
document_id: 9313e37e-fcde-9252-777a-c9e50c614768
document_version_independent_id: 9313e37e-fcde-9252-777a-c9e50c614768
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/call-api-azure-services.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/call-api-azure-services
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/call-api-azure-services.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/fd7d5d12-dbbc-4585-98a0-c6a0a5324f97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/298ced0f-48c4-410b-86eb-c2214b75cbdd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0a420050-40f1-dae3-5dd2-1dda84206ae1
---

# Call Azure services from an agent using .NET Azure SDK - Microsoft Entra Agent ID | Microsoft Learn

Read blob data with the agent's own identity, without a signed-in user's delegated access. Azure services authorize the Agent ID through Azure role-based access control (Azure RBAC).

In this article, you adapt an ASP.NET Core agent's token acquisition to Azure SDK clients. Assign the minimum role at the narrowest resource scope.

## Prerequisites

- The [blueprint credential and ASP.NET Core services](call-api-custom#configure-the-blueprint-credential), including token acquisition. Reuse the local certificate configuration when running on a workstation. This example doesn't require the custom API's app role or consent grant.
- An existing storage account and an `agent-data` blob container. Replace `<storage-account>` in the example with the account name.
- An Azure data-plane role assignment for the **agent identity's object ID** on that container or account, not for the blueprint or its managed identity credential.

Install the integration package and Blob Storage SDK from the agent project's directory:

```dotnetcli
dotnet add package Microsoft.Identity.Web.Azure
dotnet add package Azure.Storage.Blobs
```

## Configure the token credential

Register `MicrosoftIdentityTokenCredential` with dependency injection:

Add the following registration before `builder.Build()` in `Program.cs`, and merge the `using` directive with those at the top of the file.

```csharp
using Microsoft.Identity.Web;

builder.Services.AddMicrosoftIdentityAzureTokenCredential();
```

The credential uses the Microsoft.Identity.Web configuration established in the parent journey. Use a managed identity federated credential in hosted environments.

Warning

Client secrets shouldn't be used as client credentials in production environments for agent identity blueprints due to security risks. Instead, use more secure authentication methods such as [federated identity credentials (FIC) with managed identities](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity) or client certificates. These methods provide enhanced security by eliminating the need to store sensitive secrets directly within your application configuration.

## Call Azure Blob Storage as the agent

Inject `MicrosoftIdentityTokenCredential` and request an app-only token with the shared client ID configured in the parent journey:

The following is a service component, not a complete `Program.cs`. Put the class in `AgentStorageService.cs`, register it with `builder.Services.AddScoped<AgentStorageService>()` before `builder.Build()`, and invoke `ListBlobsAsync()` from an authorized application operation. Preserve the parent journey's `AgentUser` policy on any endpoint that triggers this app-only operation.

```csharp
using Azure.Storage.Blobs;
using Microsoft.Identity.Web;

public sealed class AgentStorageService
{
    private readonly MicrosoftIdentityTokenCredential _credential;

    public AgentStorageService(MicrosoftIdentityTokenCredential credential)
    {
        _credential = credential;
    }

    public async Task<IReadOnlyList<string>> ListBlobsAsync()
    {
        _credential.Options.RequestAppToken = true;

        var serviceClient = new BlobServiceClient(
            new Uri("https://<storage-account>.blob.core.windows.net"),
            _credential);
        var container = serviceClient.GetBlobContainerClient("agent-data");
        var names = new List<string>();

        await foreach (var blob in container.GetBlobsAsync())
        {
            names.Add(blob.Name);
        }

        return names;
    }
}
```

`RequestAppToken = true` selects autonomous, app-only access. For a user-delegated Azure call, use [Call an Azure service as a user](aspnet-core-call-azure-api-as-user).

The Agent ID needs an appropriate data-plane role, such as **Storage Blob Data Reader**. A management-plane role such as **Reader** doesn't grant access to blob data.

Use the same credential with other Azure SDK clients, including Azure Key Vault clients. Replace the endpoint and role with the values required by the target service.

For a container containing test blobs, `ListBlobsAsync()` should return their names; an empty container returns an empty list. A storage `403` requires checking the agent's data-plane role and target resource separately from successful token acquisition. Don't grant a management-plane role to fix missing blob data access.