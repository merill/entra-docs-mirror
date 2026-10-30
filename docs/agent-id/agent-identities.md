---
layout: Conceptual
title: Overview of agent identities in Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-identities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn about agent identities in Microsoft Entra ID, specialized identity constructs that enable secure authentication and authorization for AI agents in enterprise environments.
ms.topic: concept-article
ms.date: 2026-03-30T00:00:00.0000000Z
ms.reviewer: dastrock
locale: en-us
document_id: d61ee70d-a218-658e-3116-6cf632812e52
document_version_independent_id: d61ee70d-a218-658e-3116-6cf632812e52
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-identities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-identities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: faf87e31-fbe7-c9e4-2854-088559f2e8be
---

# Overview of agent identities in Microsoft Entra | Microsoft Learn

An agent identity is a special service principal in Microsoft Entra ID. It represents an identity that the agent identity blueprint created and is authorized to impersonate. It doesn't have credentials on its own. The agent identity blueprint can acquire tokens on behalf of the agent identity provided the user or tenant admin consented for the agent identity to the corresponding scopes. Autonomous agents acquire app tokens on behalf of the agent identity. Interactive agents called with a user token acquire user tokens on behalf of the agent identity.

Agent identities can be used to:

- Request agent tokens from Microsoft Entra ID. The subject of the access token is the agent identity.
- Receive incoming access tokens issued by Microsoft Entra ID. The audience of the access token is the agent identity.
- Request user tokens from Microsoft Entra ID for an authenticated user. The subject of the token is a user, while the actor is the agent identity.

## Anatomy of an agent identity

An account used by an AI agent is referred to as an **agent identity**. Much like your typical user account, an agent identity has a few key components:

![Diagram showing an agent identity illustration.](media/agent-identities/agent-identity.png)

- **Identifier**. Each agent identity has an `id` (also known as object ID), such as `aaaaaaaa-1111-2222-3333-bbbbbbbbbb`. Microsoft Entra generates the `id` and uniquely identifies the account within a Microsoft Entra tenant.
- **Credentials**. Agent identities don't have credentials of their own. They rely on the agent identity blueprint to acquire tokens on their behalf.
- **Display name**. An agent identity's display name is surfaced in many experiences such as the Microsoft Entra admin center, Azure portal, Teams, Outlook, and more. It's the human-friendly name of an agent and can be changed.
- **Sponsor**. Agent identities can have a sponsor, which records the human user or group that's accountable for an agent. This sponsor is used for various purposes, such as contacting a human in case a security incident happens.
- **Blueprint**. All agent identities are created from a reusable template called an agent identity blueprint. The agent identity blueprint establishes the kind of agent and records metadata shared across all agent identities of a common kind.
- **Agent's user account (optional)**. Some agents need access to systems that strictly require a Microsoft Entra user account be used for authentication. In these cases, an agent can be given a second account, called an **agent's user account**. This second account is a user account in the Microsoft Entra tenant that is decorated as an AI agent. It has a different `id` than the agent identity, but a 1:1 relationship is always established between an agent identity and its agent's user account.

These are the basic components of an agent identity that enable secure authentication and authorization. The full object schema of an agent identity is available in Microsoft Graph reference documentation.

## Authorizing agent identities

Agent identity is the primary account used by an AI agent to authenticate to various systems. It has unique identifiers such as the object ID and the app ID, which always have the same value and can be reliably used for authentication and authorization decisions.

Unlike human users, AI agents don't use passwords, Short Message Service (SMS), passkeys, or authenticator apps for authentication. Agent identities don't have credentials of their own. They only *authenticate* using [federated identity credentials (FIC)](/en-us/graph/api/resources/federatedidentitycredentials-overview) issued by the agent identity blueprint. *The blueprint holds credentials* that it uses to acquire tokens on behalf of agent identities. Credentials do *not* reside on the agent identity. These credential types on the blueprint include:

- Federated identity credentials
- Certificates / cryptographic keys
- Client secrets

Agent identities can only be issued tokens in the Microsoft Entra tenant where they're created. They can't access resources or APIs in other tenants.

Note

While agent identities are single-tenant, agent identity blueprints can be configured as multitenant. A multitenant blueprint can be published and added to other tenants, where it creates tenant-local agent identities. The agent identities themselves always remain single-tenant.

## Blueprints: Consistent security for agent identities

A key characteristic of agent identities is that all agent identities are created from a reusable template called an agent identity blueprint. The blueprint establishes the "kind" of agent and records metadata shared across all agent identities of a common kind.

![Diagram showing relationship between agent identity and agent identity blueprint.](media/agent-identities/agent-blueprint.png)

Imagine that an organization uses an AI agent called a "Sales Assistant Agent." Whether the agent is purchased or built in-house, an agent identity blueprint would be added to the organization's Microsoft Entra tenant. The blueprint captures the following information:

- The name of the blueprint, such as "Sales Assistant Agent"
- The organization who published the blueprint, such as "Contoso"
- Any roles the agent might offer, such as "sales manager" or "sales rep"
- Any Microsoft Graph permissions that its agents are granted, such as "read the signed in user's calendar"

Many sales teams within the organization deploy the AI agent. An agent is deployed for North America sales. Another is deployed for South America sales. One for enterprise sales, one for small/medium businesses, and another for startups. Upon creation, each of these agents is given an agent identity. Each agent begins running and performing tasks using its agent identity for authentication.

Because each agent identity is created using the same agent identity blueprint, all agents appear as "Sales Assistant Agents" in the Microsoft Entra admin center. This feature allows the Microsoft Entra administrator to take actions like:

- Apply a conditional access policy to all Sales Assistant Agents.
- Disable all Sales Assistant agents.
- Revoke a permission grant for all Sales Assistant agents.

Agent identity blueprints give the Microsoft Entra administrator the ability to secure agent identities at scale by setting rules and performing operations based on the kind of agent. This feature ensures consistent security for each AI agent that is deployed in the organization.