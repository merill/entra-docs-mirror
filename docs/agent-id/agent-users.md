---
layout: Conceptual
title: Learn about the agent's user account in Microsoft Entra Agent ID - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: This article explains the concept of the agent's user account, how it functions within Microsoft Entra ID, and its relationship with agent identities.
ms.date: 2025-11-04T00:00:00.0000000Z
ms.topic: concept-article
ms.reviewer: yukarppa
locale: en-us
document_id: 9be4db6d-b056-61c8-2c2d-627f4616d1e8
document_version_independent_id: 9be4db6d-b056-61c8-2c2d-627f4616d1e8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 08ac836b-0804-f6ed-cad5-5d379348b4de
---

# Learn about the agent's user account in Microsoft Entra Agent ID - Microsoft Entra Agent ID | Microsoft Learn

The agent's user account is a specialized identity type designed to bridge the gap between agents and human user capabilities. The agent's user account enables AI-powered applications to interact with systems and services that require user identities, while maintaining appropriate security boundaries and management controls. It allows organizations to manage the agent's access using similar capabilities as they do for human users.

## Example of agent's user account scenarios

Sometimes it's not enough for an agent to perform tasks on behalf of a user or operate as an autonomous application. In certain scenarios, an agent needs to act as a user, functioning essentially as a digital worker. The following are example scenarios where the agent's user account would be applicable:

- The organization needs long-term digital employees that function as team members with mailboxes, chat access, and inclusion in HR systems.
- The agent needs to access APIs or resources that are only available to user identities
- The agent needs to participate in collaborative workflows as a team member

For these reasons, the agent's user account is created. The agent's user account is optional and should only be created for interactions where the agent needs to act as a user or access resources restricted to user accounts.

## The agent's user account

The agent's user account represents a subtype of user identity within Microsoft Entra. These identities are designed to enable agent applications to perform actions in contexts where a user identity is required. Unlike nonagentic service principals or application identities, the agent's user account receives tokens with claim `idtyp=user`, allowing it to access APIs and services that specifically require user identities. It also maintains security constraints necessary for nonhuman identities.

An agent's user account isn't created automatically. It requires an explicit creation process that connects it to its parent agent identity. This parent-child relationship is fundamental to understanding how the agent's user account functions and is secured in Microsoft Entra. Once established, this relationship is immutable and serves as a cornerstone of the security model for the agent's user account. The relationship is a one-to-one (1:1) mapping. Each agent identity can have at most one associated agent's user account, and each agent's user account is linked to exactly one parent agent identity, itself linked to exactly one agent identity blueprint application.

The agent's user account:

- Is also created using an agent identity blueprint.
- Is always associated to a specific agent identity, specified upon creation.
- Has distinct unique identifiers, separate from the agent identity.
- Can only authenticate by presenting a token issued to the associated agent identity.

![Diagram showing the relationship between an agent's user account and agent identity.](media/agent-users/agent-user.png)

## Agent's user account and agent identity relationship

The agent identity blueprint doesn't have the permission by default to create the agent's user account because this capability is optional and not always needed. It's a permission that must be explicitly granted to the agent identity blueprint.

The agent's user account is created using the agent identity blueprint. When granted proper permissions, the agent identity blueprint can create an agent's user account and establish a parent relationship with a specific agent identity. The agent identity is considered the parent of the agent's user account.

Admins manage the lifecycle of an agent's user account. An admin user can delete the agent's user account once its functionalities aren't needed anymore.

## Authentication and security model

The authentication model for the agent's user account differs significantly from human-user accounts:

- **Federated identity credentials**: Authentication happens through credentials assigned to the agent's user account. In production systems, use Federated Identity Credentials (FIC). These credentials are used for authenticating both the agent identity blueprint and the agent identity. The credential assigned to the user is used for authenticating across the agent ecosystem.
- **Restricted credential model**: The agent's user account doesn't have regular credentials like passwords. Instead, it's restricted to using the credentials provided through its parent relationship. This restriction on credentials, along with restrictions on interactive sign-in, ensures that the agent's user account can't be used like a standard user account.
- **Impersonation mechanism**: The associated agent identity can impersonate its child agent's user account. It allows the parent's business logic to obtain tokens and act as the agent's user account when needed.

## Capabilities of the agent's user account

The agent's user account possesses capabilities that allow it to function effectively within Microsoft 365 and other environments:

- An agent's user account can be added to Microsoft Entra groups, including dynamic groups, enabling it to inherit permissions granted to those groups. It can't, however, be added to role-assignable groups.
- The agent's user account can access resources and utilize other collaborative features typically reserved for human users.
- The agent's user account can be added to administrative units, similar to human users.
- The agent's user account can be assigned licenses, which is often necessary for provisioning Microsoft 365 resources.

## Security constraints

The agent's user account operates under specific security constraints to ensure appropriate use:

- Credential limitations: The agent's user account can't have credentials like passwords or passkeys. The only credential type it supports is the agent identity reference to its parent. So even if the agent's user account behaves as a user, its credentials are confidential client credentials.
- Administrative role restrictions: The agent's user account can't be assigned privileged administrator roles. This limitation provides an important security boundary, preventing potential elevation of privileges. The agent's user account can be assigned with custom roles.
- Permission model: The agent's user account typically has permissions similar to guest users, with more capabilities for enumerating users and groups.

## Provisioning agent user accounts for Microsoft 365

To fully provision an agent's user account with digital worker capabilities such as a mailbox, Teams presence, or HR system integration, create the agent through Microsoft Teams. Agent 365 and the Agent 365 SDK provide the foundation for agent user accounts to fully participate in Microsoft 365.

Note

Creating an agent's user account directly through the Microsoft Graph API establishes the identity in Microsoft Entra but doesn't provision Microsoft 365 capabilities. Use the Graph API approach only for scenarios that don't require Microsoft 365 participation.

For more information, see the [Microsoft 365 Agents SDK documentation](/en-us/microsoft-365/agents-sdk/).