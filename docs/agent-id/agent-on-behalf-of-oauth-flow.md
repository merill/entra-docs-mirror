---
layout: Conceptual
title: Agent OAuth flows - On-behalf-of flow - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-on-behalf-of-oauth-flow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how agent applications operate on behalf of signed-in users using OAuth 2.0 On-Behalf-Of flows with agent identity blueprints and agent identities.
ms.topic: concept-article
ms.date: 2025-11-04T00:00:00.0000000Z
ms.reviewer: jmprieur
locale: en-us
document_id: 2ce787b9-ee65-aeb6-5e31-c3db2b5b7852
document_version_independent_id: 2ce787b9-ee65-aeb6-5e31-c3db2b5b7852
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-on-behalf-of-oauth-flow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-on-behalf-of-oauth-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-on-behalf-of-oauth-flow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: b0496786-2082-d728-532d-c2c882d80440
---

# Agent OAuth flows - On-behalf-of flow - Microsoft Entra Agent ID | Microsoft Learn

Agents (agent identity blueprints) operating on behalf of regular, signed-in users use the standard OAuth 2.0 protocol with all its capabilities. User delegation enables agent identities to operate on behalf of signed-in users using standard OAuth 2.0 On-Behalf-Of flows with agent-specific impersonation. The agent identity is assigned the necessary delegated permissions needed for OBO access. It requires consent from users to access their data.

Agents have the capabilities of Microsoft Entra ID resource (API) applications and support the API attributes required for the (OAuth2Permissions, AppURI). Agent identity blueprints can't initiate interactive authorization (`/authorize`) flows directly. They must receive a user token from a client application and then perform an OBO token exchange. A web redirect URI can be configured on a blueprint for consent flows only (`response_type=none`), but it has limited functionality compared to a redirect URI on an app registration.

Important

Like their parent blueprints, child agent identities can't initiate interactive `/authorize` flows. Consequently, users can't grant them consent interactively (attempting this on the child identity returns the error `AADSTS82014`). Instead, you must preauthorize the required delegated permissions by configuring inheritable permissions on the parent agent identity blueprint. Ensure an administrator has actually granted consent for these permissions on the blueprint. The child agent identities will then inherit these scopes without triggering an interactive consent prompt. For step-by-step guidance, see [Configure inheritable permissions for agent identity blueprints](configure-inheritable-permissions-blueprints).

Warning

Microsoft recommends using the approved SDKs like Microsoft.Identity.Web and Microsoft Entra ID Auth SDK (sidecar) libraries to implement these protocols. Manual implementation of these protocols is complex and error-prone, and using the SDKs helps ensure security and compliance with best practices.

## Managed identities integration

Managed identities are the preferred credential type. In this configuration, the managed identity token serves as the credential for the parent agent identity blueprint, while standard MSI protocols apply for credential acquisition. This integration allows the agent ID to receive the full benefits of MSI security and management, including automatic credential rotation and secure storage.

## Protocol steps

Agents aren't supported for interactive (`/authorize`) flows. Supported grant types are `client_credential`, `jwt-bearer`, and `refresh_token`. The flow involves the agent identity blueprint, agent identity, and a client credential. The client credential can be a client secret, a client certificate, or a Federated Identity Credential (FIC). When possible, use a managed identity to obtain the FIC.

![Diagram showing the illustration of on-behalf-of token acquisition flow for agents.](media/agent-on-behalf-of-oauth-flow/on-behalf-of-flow.png)

1. The user authenticates with the client and obtains a user access token (client token, Tc).
2. Client sends the user access token (Tc) to the agent identity blueprint to act on behalf of the user. It's the token that is used for the OBO exchange for the agent identity blueprint.
3. The agent identity blueprint requests an exchange token by presenting its client credential (secret, certificate, or managed identity token (TUAMI)). In this example, we use a managed identity as FIC. Microsoft Entra ID returns token T1 to the agent.

    Warning

    Client secrets shouldn't be used as client credentials in production environments for agent identity blueprints due to security risks. Instead, use more secure authentication methods such as [federated identity credentials (FIC) with managed identities](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity) or client certificates. These methods provide enhanced security by eliminating the need to store sensitive secrets directly within your application configuration.

    ```
    POST /oauth2/v2.0/token
    Content-Type: application/x-www-form-urlencoded
    
    client_id=AgentBlueprint
    &scope=api://AzureADTokenExchange/.default
    &fmi_path=AgentIdentity
    &client_assertion=TUAMI
    &grant_type=client_credentials
    ```

    - `fmi_path`: The client ID (app ID) of the agent identity. This parameter tells Microsoft Entra ID which child agent identity the blueprint is impersonating during the token exchange.

    Where TUAMI is the managed identity token for user assigned managed identity (UAMI). This step returns T1.
4. The agent identity, a child of the agent identity blueprint, sends an OBO token exchange request. This request includes both T1 and the user access token Tc. Note that `client_id` switches from the blueprint (in the previous step) to the **agent identity** here, because the agent identity is the entity performing the OBO exchange.

    ```
    POST /oauth2/v2.0/token
    Content-Type: application/x-www-form-urlencoded
    
    client_id=AgentIdentity
    &scope=https://resource.example.com/scope1
    &client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer
    &client_assertion={T1}
    &grant_type=urn:ietf:params:oauth:grant-type:jwt-bearer
    &assertion={Tc(aud=AgentIdentity Blueprint, oid=User)}
    &requested_token_use=on_behalf_of
    ```
5. Microsoft Entra ID returns the resource token after validating both T1 and Tc. The following audience and linkage requirements apply:

    - Tc (aud) == agent identity blueprint client ID. The user assertion must be audienced to the blueprint; a token audienced to another resource (for example, Microsoft Graph) is rejected with `AADSTS50013`.
    - T1 is obtained with `scope=api://AzureADTokenExchange/.default`, so its `aud` is the token-exchange resource rather than the blueprint. Microsoft Entra ID validates that T1 is bound to the blueprint (its `azp` is the blueprint) and that T1's `sub` (the FMI path) resolves to the child agent identity performing the exchange.

### Sequence diagram

The following sequence diagram shows the OBO flow

![Diagram showing the token sequence of on-behalf-of token acquisition flow for agents.](media/agent-on-behalf-of-oauth-flow/on-behalf-of-flow-token-sequence.png)

### Refresh token support

Refresh token can be used for asynchronous scenarios and background processes:

```
POST /oauth2/v2.0/token
Content-Type: application/x-www-form-urlencoded

client_id=AgentIdentity
&scope=https://resource.example.com/scope1
&client_assertion_type=urn:ietf:params:oauth:client-assertion-type:jwt-bearer
&client_assertion={T1}
&grant_type=refresh_token
&refresh_token={AgentIdentityRefreshToken}
```

### Permission inheritance

Agent identities can inherit delegated permissions from their parent agent identity blueprint when the `InheritDelegatedPermissions` property is enabled. This inheritance mechanism reduces consent complexity for multi-instance scenarios by allowing agent identities to use permissions already granted to their parent application. The inheritance functionality applies specifically when FIC impersonation is used and enables efficient permission management across multiple instances. However, inheritance works only within tenant boundaries, ensuring that permission scope remains contained within appropriate organizational limits.