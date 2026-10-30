---
layout: Conceptual
title: Acquire tokens and call downstream APIs with Microsoft Entra ID Auth SDK (sidecar) - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/microsoft-entra-sdk-for-agent-identities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how autonomous agents acquire tokens using the Microsoft Entra ID Auth SDK (sidecar) to call downstream APIs independently.
ms.topic: how-to
ms.date: 2025-11-05T00:00:00.0000000Z
ms.reviewer: jmprieur
locale: en-us
document_id: f26885e2-42ea-4668-587e-ba90740b85cc
document_version_independent_id: f26885e2-42ea-4668-587e-ba90740b85cc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/microsoft-entra-sdk-for-agent-identities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/microsoft-entra-sdk-for-agent-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/microsoft-entra-sdk-for-agent-identities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 885345cf-96d7-da29-abbc-6dcf19c2bbd7
---

# Acquire tokens and call downstream APIs with Microsoft Entra ID Auth SDK (sidecar) - Microsoft Entra Agent ID | Microsoft Learn

The Microsoft Entra ID Auth SDK (sidecar) is a containerized web service that handles token acquisition, validation, and downstream API calls for agents. This SDK communicates with your application through HTTP APIs, providing consistent integration patterns regardless of your technology stack. Instead of embedding identity logic directly in your application code, the Microsoft Entra ID Auth SDK (sidecar) manages token acquisition, validation, and API calls through standard HTTP requests.

## Prerequisites

Before you begin, ensure you have:

- [Set up the Microsoft Entra ID Auth SDK (sidecar)](/en-us/entra/msidweb/agent-id-sdk/installation)
- [An agent identity](create-delete-agent-identities). Record the agent identity client ID.
- [An agent identity blueprint](create-blueprint). Record the agent identity blueprint client ID.
- Necessary [permissions configured in Microsoft Entra ID](grant-agent-access-microsoft-365)

## Deploy your containerized service

Deploy the Microsoft Entra ID Auth SDK (sidecar) as a containerized service in your environment. Follow the instructions in the [Set up the Microsoft Entra ID Auth SDK (sidecar)](/en-us/entra/msidweb/agent-id-sdk/installation) guide to configure the service with your agent identity details.

## Configure your Microsoft Entra ID Auth SDK (sidecar) settings

Follow these steps to configure your Microsoft Entra ID Auth SDK (sidecar) settings:

Warning

Client secrets shouldn't be used as client credentials in production environments for agent identity blueprints due to security risks. Instead, use more secure authentication methods such as [federated identity credentials (FIC) with managed identities](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity) or client certificates. These methods provide enhanced security by eliminating the need to store sensitive secrets directly within your application configuration.

1. Set up the necessary components in Microsoft Entra ID. Ensure you register your application in the Microsoft Entra ID tenant.
2. Configure your client credentials. This credential can be a client secret, a certificate, or a managed identity that you're using as a federated identity credential.
3. If you're calling a downstream API, ensure that the necessary permissions are granted. Calling a custom web API requires you to provide the API registration details in the SDK configuration.

For more information, see [Configure your Microsoft Entra ID Auth SDK (sidecar) settings](/en-us/entra/msidweb/agent-id-sdk/configuration).

## Acquire tokens using the Microsoft Entra ID Auth SDK (sidecar)

These are the steps to acquire tokens using the Microsoft Entra ID Auth SDK (sidecar):

1. Acquire token using the Microsoft Entra ID Auth SDK (sidecar). This varies based on whether the agent is operating autonomously or on behalf of a user. There are three scenarios to consider:

    - Autonomous agents: Agents operating on their own behalf using service principals created for agents (autonomous).
    - Autonomous agent's user account: Agents operating on their own behalf using user principals created specifically for agents (for instance agents having their own mailbox).
    - Interactive agents: Agents operating on behalf of human users.

    Specify the downstream API by including its name in the request URL based on your Microsoft Entra ID Auth SDK (sidecar) configuration. The authorization header endpoint takes the format `/AuthorizationHeader/{serviceName}` where `serviceName` is the name of the downstream API configured in the SDK settings.
2. To acquire an app-only (client credentials) token for an autonomous agent, you provide the agent identity client ID in the request.

    ```bash
    GET /AuthorizationHeader/Graph?AgentIdentity=<agent-identity-client-id>
    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGc...
    ```
3. To acquire token for an autonomous agent's user account, provide either the user object ID or User Principal Name but not both. This means providing either `AgentUsername` or `AgentUserId`. Providing both causes a validation error. You must also provide the `AgentIdentity` to specify which agent identity to use for token acquisition. If the agent identity parameter is missing, the request fails with a validation error.

    ```bash
    GET /AuthorizationHeader/Graph?AgentIdentity=<agent-identity-client-id>&AgentUserId=<agent-user-object-id>
    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGc...
    ```

    ```bash
    GET /AuthorizationHeader/Graph?AgentIdentity=<agent-identity-client-id>&AgentUsername=<agent-user-principal-name>
    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGc...
    ```
4. For interactive agents, use the on-behalf-of (OBO) flow. The agent first validates the user token granted to it before acquiring the resource token to call the downstream API.

    Agent web API receives user token from the calling application and validates the token via the Microsoft Entra ID Auth SDK (sidecar) `/Validate` endpoint Acquire token for downstream APIs by calling `/AuthorizationHeader` with only the `AgentIdentity` and the incoming authorization header

    ```bash
    # Step 1: Validate incoming user token
    GET /Validate
    Authorization: Bearer <user-token>
    
    # Step 2: Get authorization header on behalf of the user
    GET /AuthorizationHeader/Graph?AgentIdentity=<agent-identity-client-id>
    Authorization: Bearer <user-token>
    ```

## Call an API

When obtaining the authorization header for calling a downstream API, the Microsoft Entra ID Auth SDK (sidecar) returns the `Authorization` header value that can be used directly in your API calls.

You can use this header to call the downstream API. The web API should validate the token by calling the `/Validate` endpoint of the Microsoft Entra ID Auth SDK (sidecar). This endpoint returns token claims for further authorization decisions.