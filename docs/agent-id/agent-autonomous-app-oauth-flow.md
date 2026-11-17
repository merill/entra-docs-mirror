---
layout: Conceptual
title: Agent autonomous app OAuth flow - App-only protocol - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-autonomous-app-oauth-flow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how agent identities operate autonomously without user context using app-only protocol with OAuth 2.0 client credentials flows.
ms.topic: concept-article
ms.date: 2026-11-03T00:00:00.0000000Z
ms.reviewer: jmprieur
ai-usage: ai-assisted
locale: en-us
document_id: 3c747d17-e9ff-66e9-f382-8bcf278d875c
document_version_independent_id: 3c747d17-e9ff-66e9-f382-8bcf278d875c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-autonomous-app-oauth-flow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-autonomous-app-oauth-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-autonomous-app-oauth-flow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ffc5e0b3-f86d-e384-09ec-bc2781c9cdd5
---

# Agent autonomous app OAuth flow - App-only protocol - Microsoft Entra Agent ID | Microsoft Learn

App-only operations enable agent identities to act autonomously without user context, using client credentials flows. The agent identity is both the actor and subject. An administrator grants the application permissions required for the operation.

The protocol below describes **multi-instance** Agent IDs, where the blueprint impersonates a child identity. A single-instance Agent ID instead requests a token directly with the shared client ID and a credential configured on the blueprint. It doesn't use the intermediate T1 token or `fmi_path`. For that request, see [Request an app-only token for a single-instance Agent ID](authenticate-single-instance-agent#request-an-app-only-token).

Agent identity blueprints can only impersonate their child agent identities. Only a single agent identity blueprint can impersonate an agent identity. An agent identity blueprint can impersonate many agent identities, but no agent identity can be owned by multiple blueprints. Agent identities are always single-tenant regardless of their parent Agent identity blueprint's tenancy model. Each agent identity operates within one tenant's security and policy boundaries.

Warning

Microsoft recommends using the approved SDKs like Microsoft.Identity.Web and Microsoft Entra ID Auth SDK (sidecar) libraries to implement these protocols. Manual implementation of these protocols is complex and error-prone, and using the SDKs helps ensure security and compliance with best practices.

## Managed identities integration

For Azure-hosted agents, prefer a managed identity when the hosting service provides one. Its token authenticates the parent blueprint through a configured federated identity credential; configuring the managed identity alone doesn't grant API access to the agent. A local developer's Azure CLI sign-in isn't a managed identity. For hosting requirements and local credential alternatives, see [Configure blueprint credentials](create-blueprint#configure-credentials-for-the-agent-identity-blueprint).

## Protocol steps

The following are the protocol steps.

![Diagram showing the illustration of autonomous app token acquisition flow for agents.](media/agent-autonomous-app-oauth-flow/autonomous-app-flow.png)

1. Agent identity blueprint requests an exchange token T1. The agent identity blueprint presents its credentials that could be a secret, a certificate, or a managed identity token. Microsoft Entra ID returns the T1 to the agent identity blueprint. In this example we use a managed identity as Federated Identity Credential (FIC).

    Warning

    Client secrets shouldn't be used as client credentials in production environments for agent identity blueprints due to security risks. Instead, use more secure authentication methods such as [federated identity credentials (FIC) with managed identities](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity) or client certificates. These methods provide enhanced security by eliminating the need to store sensitive secrets directly within your application configuration.

    ```
    POST /oauth2/v2.0/token
    Content-Type: application/x-www-form-urlencoded
    
    client_id=AgentBlueprint
    &scope=api://AzureADTokenExchange/.default
    &fmi_path=AgentIdentity
    &client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer
    &client_assertion=TUAMI
    &grant_type=client_credentials
    ```

    - `fmi_path`: The client ID (app ID) of the agent identity. This parameter tells Microsoft Entra ID which child agent identity the blueprint is impersonating during the token exchange.

    Where TUAMI is the managed identity token for user assigned managed identity (UAMI). This step returns T1. Where T1 is the token-exchange token for FIC.
2. Agent identity sends a token exchange request to Microsoft Entra ID. The request includes the token T1.

    ```
    POST /oauth2/v2.0/token
    Content-Type: application/x-www-form-urlencoded
    
    client_id=AgentIdentity
    &scope=https://resource.example.com/.default
    &client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer
    &client_assertion={T1}
    &grant_type=client_credentials
    ```
3. Microsoft Entra ID issues an app-only resource access token (TR) to the agent identity after validating T1. T1's audience is the token-exchange resource requested in step 1, not the blueprint. Microsoft Entra ID validates that T1 is bound to the blueprint and that its subject resolves to the child agent identity performing the exchange. The resource token represents the agent identity, not the blueprint.

## Sequence diagram

The following is a sequence diagram for the app-only flow:

![Diagram showing the token sequence of autonomous app token acquisition flow for agents.](media/agent-autonomous-app-oauth-flow/autonomous-app-flow-token-sequence.png)