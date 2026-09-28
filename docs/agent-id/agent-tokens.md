---
layout: Conceptual
title: Tokens in Microsoft agent identity platform - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-tokens
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn about tokens in the Microsoft agent identity platform, including token types, claims structure, authentication flows, and how tokens enable secure communication between agent applications and resources.
ms.topic: concept-article
ms.date: 2025-11-10T00:00:00.0000000Z
ms.reviewer: jmprieur
locale: en-us
document_id: 7a4d7949-4818-a3de-b492-3e0f29dbef60
document_version_independent_id: 7a4d7949-4818-a3de-b492-3e0f29dbef60
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-tokens.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-tokens
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-tokens.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/96407ebd-b9e6-40db-9488-063e1af76a01
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8af61fb5-33c5-4523-b00a-7a42d7bbe9cd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7b48e539-e331-0580-1a61-6d6b4643375f
---

# Tokens in Microsoft agent identity platform - Microsoft Entra Agent ID | Microsoft Learn

Tokens are the fundamental security mechanism that enables secure communication and authorization in the Microsoft agent identity platform. This article explains how tokens work in agent app scenarios.

In agent app scenarios, tokens carry enhanced claims to support the unique requirements. Unlike nonagentic application tokens, tokens used by agents include specialized claims that identify entity types, delegation relationships, and authorization contexts specific to agent operations.

These tokens enable secure communication between:

- Agent identity blueprints and their agent identities
- Agent identities and resource APIs
- Agents' user accounts and the services they interact with
- Complex delegation chains involving multiple agent entities

## Token claims entity identifiers

Agent tokens include specialized claims that identify the type and role of entities participating in authentication flows:

- Actor facet claims (`xms_act_fct`): Identify the entity performing actions within the token flow. These claims enable systems to understand who is actually requesting access or performing operations.
- Subject facet claims (`xms_sub_fct`): Identify the ultimate subject for whom operations are being performed. It enables proper attribution even in complex delegation scenarios.
- Identity type claims (`idtyp`): Distinguish between user and application contexts, enabling appropriate policy application and security enforcement.
- Identity relationship claims (`xms_idrel`): Describe the relationship between the token subject and the resource tenant, supporting multi-tenancy and guest access scenarios.

## Token flow patterns

Agents participate in several distinct token flow patterns, each designed for specific operational scenarios. For more information, see [auth protocols in Microsoft agent identity platform](agent-oauth-protocols).

### Tokens in user delegation scenarios

User delegation scenarios enable agent applications to operate on behalf of users. In this scenario, tokens preserve user identity while identifying the agent identity blueprint as the acting entity. The on-behalf-of (OBO) protocol requires token audience to match the client ID. However, for agent identity (agent ID), the incoming token has the audience of the agent identity blueprint. In this scenario, tokens have the following key characteristics:

- Maintain user identity context throughout operations
- Include delegated permissions granted to the agent identity blueprint
- Enable policy evaluation at both user and application levels
- Support both interactive and background operations

The agent identity receives delegated permissions that can be directly assigned or inherited from the parent agent identity blueprint when impersonation is used.

### Tokens in application-only scenarios

Application-only scenarios represent autonomous operations where agent identity blueprints act on their own behalf without user context.

In this scenario, tokens have the following key characteristics:

- Represent the agent identity blueprint's own identity
- Include application-level permissions directly assigned by the tenant administrator
- Enable unscoped access within granted permission boundaries. Delegated permissions aren't applied.
- Support fully autonomous background operations

### Tokens in agent's user account impersonation scenarios

Agent's user account impersonation scenarios enable the agent's user account to operate like a human user. These tokens support scenarios where agents need user-like context but with controlled, predefined identities.

In this scenario, tokens have the following key characteristics:

- Use specialized agent's user account identities
- Maintain user-context behavior patterns
- Include scoped delegated permissions
- Require explicit assignment to agent identities

In this scenario, the agent identity blueprint impersonates the agent identity, which then impersonates the assigned agent's user account. Access is scoped to delegated permissions assigned to the agent identity, ensuring the agent can't exceed its granted permissions even when operating with user context. The agent's user account can only be used when assigned to an agent identity and can't authenticate independently.

## Nonagentic API integration

Both agents and nonagentic OBO clients carry forward subject facets. It enables resource servers to apply appropriate policies and logging for agent subjects. It also enables proper attribution even when tokens pass through nonagentic intermediaries.

## Builder application claims

Platforms that create agents and integrate with Microsoft Entra Agent ID don't receive special token claims. These platforms use standard token claims appropriate for their authentication method and don't participate in the specialized agent claim structure.

## Tenancy models and token behavior

All tokens contain a tenant ID (`tid`) representing the organization's tenant. Tokens are bounded within the tenant of the agent identity. Each agent identity receives tokens scoped to its operational tenant. Agent identities can't access resources outside their assigned customer tenant. Permission inheritance flows directly from parent to child entities.

## Token validation

Clients using agent identities are expected to treat the access tokens issued to them to use at resource servers as opaque, and not try to parse them. However, resource servers that receive access tokens issued to agents need to parse the tokens to validate them and extract claims for authorization purposes.

Resource servers should validate agent tokens by:

- Verifying standard OAuth claims (aud, exp, iss)
- Checking agent facet claims for proper entity identification
- Validating permissions based on token type (delegated vs app-only)
- Ensuring tenant boundary compliance

Token claims enable policy engines to:

- Identify agents vs nonagentic clients
- Distinguish between different agent scenarios
- Apply appropriate conditional access policies
- Generate accurate audit logs

Example of the validation process would be to do the following actions:

- Check if a token was issued for an agent identity and for which agent blueprint.

    ```csharp
    HttpContext.User.GetParentAgentBlueprint()
    ```
- Check if a token was issued for an agent's user account identity.

    ```csharp
    HttpContext.User.IsAgentUserIdentity()
    ```

These two extensions methods, apply to both `ClaimsIdentity` and `ClaimsPrincipal`.

## Audit and logging integration

Token claims provide the foundation for comprehensive audit trails:

- `azp` identifies the requesting agent identity for client attribution
- `oid` identifies the subject for resource access attribution
- `xms_act_fct` and `xms_sub_fct` enable detailed flow analysis
- `tid` ensures proper tenant context in logs