---
layout: Conceptual
title: Agent's user account impersonation protocol - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-user-oauth-flow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how agent identities operate with user context through an agent's user account using the agent's user account impersonation protocol with OAuth 2.0 token exchange.
ms.topic: concept-article
ms.date: 2025-10-30T00:00:00.0000000Z
ms.reviewer: jmprieur
locale: en-us
document_id: 15a5b681-46b6-1ebe-bd8b-d955f24df821
document_version_independent_id: 15a5b681-46b6-1ebe-bd8b-d955f24df821
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-user-oauth-flow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-user-oauth-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-user-oauth-flow.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 8f4e6e50-bee6-5481-fe5f-25f6ff598753
---

# Agent's user account impersonation protocol - Microsoft Entra Agent ID | Microsoft Learn

Agent's user account impersonation enables agent identities to operate with user context through an agent's user account, combining user permissions with autonomous operation. In this scenario, an agent identity blueprint (actor 1) impersonates an agent identity (actor 2) that impersonates an agent's user account (subject) using FIC. Access is scoped to delegations assigned to the agent identity. The agent's user account can be impersonated only by a single agent identity.

Warning

Microsoft recommends using the approved SDKs like Microsoft.Identity.Web and Microsoft Entra ID Auth SDK (sidecar) libraries to implement these protocols. Manual implementation of these protocols is complex and error-prone, and using the SDKs helps ensure security and compliance with best practices.

## Managed identities integration

Managed identities are the preferred credential type. In this configuration, the managed identity token serves as the credential for the parent agent identity blueprint, while standard MSI protocols apply for credential acquisition. This integration allows the agent ID to receive the full benefits of MSI security and management, including automatic credential rotation and secure storage.

## Protocol steps

Then following are the protocol steps.

![Diagram showing the illustration of agent's user account token acquisition flow for agents.](media/agent-user-oauth-flow/agent-user-flow.png)

1. The agent identity blueprint requests an exchange token (T1) that it uses for agent identity impersonation. The agent identity blueprint presents client credentials that could be a secret, a certificate, or a managed identity token used as an FIC.

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

    Where TUAMI is the MSI token for user assigned managed identity (UAMI). This returns token T1.
2. The agent identity requests a token (T2) that it uses for agent's user account impersonation. The agent identity presents T1 as its client assertion. Microsoft Entra ID returns T2 to the agent identity after validating that T1 (aud) == Agent identity parent app == Agent identity blueprint.​

    ```
    POST /oauth2/v2.0/token
    Content-Type: application/x-www-form-urlencoded
    
    client_id=AgentIdentity
    &scope=api://AzureADTokenExchange/.default
    &client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer
    &client_assertion={T1}
    &grant_type=client_credentials
    ```

    This returns token T2.
3. The agent identity then sends an OBO token exchange request to Microsoft Entra ID, including both T1 and T2. Microsoft Entra ID validates that T2 (aud) == agent identity.

    ```
    POST /oauth2/v2.0/token
    Content-Type: application/x-www-form-urlencoded
    
    client_id=AgentIdentity
    &scope=https://resource.example.com/scope1
    &client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer
    &client_assertion={T1}
    &user_federated_identity_credential={T2}
    &username=agentuser@contoso.com
    &grant_type=user_fic
    &requested_token_use=on_behalf_of
    ```
4. Microsoft Entra ID then issues the resource token.

### Sequence diagram

The following sequence diagram shows the agent's user account impersonation flow

![Diagram showing the token sequence of agent's user account token acquisition flow for agents.](media/agent-user-oauth-flow/agent-user-flow-token-sequence.png)

Agent's user account impersonation requires credential chaining that follows the pattern agent identity blueprint → Agent identity → Agent's user account. Each step in this chain uses the token from the previous step as a credential, creating a secure delegation pathway. The same client ID must be used for both phases to prevent privilege escalation attacks.