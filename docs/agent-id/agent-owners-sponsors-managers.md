---
layout: Conceptual
title: Administrative relationships in Microsoft Entra Agent ID (Owners, sponsors, and managers) - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-owners-sponsors-managers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn about the administrative model for agents in Microsoft Entra, including the roles of owners, sponsors, and managers in maintaining secure operations, business accountability, and compliance oversight.
ms.topic: concept-article
ms.date: 2026-04-16T00:00:00.0000000Z
ms.reviewer: jawoods
locale: en-us
document_id: c77e3e41-d203-4200-cedb-bb7d092a7501
document_version_independent_id: c77e3e41-d203-4200-cedb-bb7d092a7501
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-owners-sponsors-managers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-owners-sponsors-managers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-owners-sponsors-managers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 476bd2d5-b669-31ae-6d4a-18455f2a9ab6
---

# Administrative relationships in Microsoft Entra Agent ID (Owners, sponsors, and managers) - Microsoft Entra Agent ID | Microsoft Learn

Microsoft Entra Agent ID introduces an administrative model that separates technical administration from business accountability, ensuring operational control and oversight without excessive permissions. This document explains the administrative relationships for Microsoft Entra Agent ID identity types. This guidance applies to [agent identities](/en-us/graph/api/resources/agentidentity?view=graph-rest-beta&amp;preserve-view=true), [agent identity blueprints](/en-us/graph/api/resources/agentidentityblueprint?view=graph-rest-beta&amp;preserve-view=true), [agent identity blueprint principals](/en-us/graph/api/resources/agentidentityblueprintprincipal?view=graph-rest-beta&amp;preserve-view=true), and [agents' user accounts](/en-us/graph/api/resources/agentuser?view=graph-rest-beta&amp;preserve-view=true). The article covers owners, sponsors, and managers and their importance in maintaining secure operations.

The administrative relationships available in Agent ID include:

- **Owners**: Technical administrators responsible for operational management of agent identity blueprints and agent identities, including setup, configuration, and credential management.
- **Sponsors**: Business representatives accountable for the agent's purpose and lifecycle decisions, including access reviews and agent retention, without technical administrative access. At least one sponsor is required for each agent identity and agent identity blueprint.
- **Managers**: User responsible for the agent within the organization's hierarchy, able to request access packages for their reporting agents.

These administrative relationships must be configured for each Agent ID object and are separate from the administrative rights granted by Microsoft Entra Role Based Access Control (RBAC) roles, like Agent ID Administrator.

## Owners

Owners usually serve as technical administrators for agents, handling operational and configuration aspects. Individual users (including guest users) and service principals can be assigned as owners. Groups aren't supported as owners. Service principals as owners enable automated management of agent identities. Owners are optional for all agent identity objects.

### Owner responsibilities

Owners can modify properties that the sponsor can't, like authentication properties. Owners can also add or update other owners and sponsors for the agent identities. Like sponsors, they can disable and delete agent identities that are no longer needed. Unlike sponsors, owners can re-enable an agent identity that is disabled, restore soft-deleted identities, or hard-delete identities.

### Owner access and permissions

Owners have administrative privileges scoped to their assigned agent identity blueprint or agent identity. They can edit settings, manage credentials, change configurations, and assign more owners.

Owners of an agent identity blueprint or agent identity blueprint principal can also create agent identities from that blueprint using delegated permissions, without needing an Agent ID Administrator or Agent ID Developer role. The calling application must be granted one of the following delegated permissions: `AgentIdentity.Create.All`, `AgentIdentity.ReadWrite.All`, or `AgentIdentity.ReadWrite.ManagedBy`.

### Owner typical personas

Owners are typically developers or IT professionals with technical knowledge to manage application identities. They might be agent creators, technical application owners, or IT administrators for critical agents. Multiple owners can be assigned for backup coverage.

Service principals can also be set as owners when some other managing service needs the ability to modify or delete specific agent identities without user intervention.

## Sponsors

Sponsors provide business accountability for agents, making lifecycle decisions without technical administrative access. They understand the business purpose of the agent, and they can determine whether an agent is still needed or requires access. Sponsors are required for agent identity blueprints and agent identities, ensuring every agent has a designated business owner.

Sponsorship should be maintained to ensure succession when an employee who's a sponsor moves or leaves. Users (including guest users) and groups can be assigned as sponsors. When a group is assigned, all members of the group have sponsor rights over the Agent ID object. Not all group types are supported as sponsors. The following group types are allowed:

- Dynamic membership groups (security or Microsoft 365)
- Assigned membership groups (Microsoft 365)

The following group types aren't allowed as sponsors:

- Role-assignable groups (security or Microsoft 365)
- Assigned membership groups (security)

### Sponsor responsibilities

Sponsors make decisions about the agent lifecycle, including renewal, extension, or removal based on business need. They request access packages on behalf of agents, and they provide business justification for access requests. During security incidents, sponsors might determine whether agent behavior is expected and authorize appropriate responses including suspension or permission adjustments.

### Sponsor access and permissions

Sponsors operate under least-privilege with limited administrative permissions. They can't modify application settings on agent blueprints or agent identities. Access is limited to nondestructive lifecycle operations: disabling agent identities, modifying the identity's sponsors, or soft-deleting.

Sponsors can't re-enable or restore agent blueprints or identities. If a sponsor disables or deletes a resource by mistake, they should contact a resource owner or an admin to recover it.

### Sponsor typical personas

Sponsors are usually business owners, product managers, team leads, or stakeholders who understand the agent's purpose. For unpublished agents, creators often serve as sponsors. For published agents, sponsors typically come from teams using the agent.

### Agent identity sponsors vs. agent's user account sponsors

In Microsoft Agent ID, the agent's identity, blueprint, and blueprint principal may all have sponsors associated with them. In addition, agents can have an [agent's user account](agent-users) created in order to access user-oriented services. While the Entra user has a sponsor relationship, there are differences between the user account sponsors and sponsors of the agent identity, blueprint, or blueprint principal.

The sponsor relationship on a user is primarily intended for the [sponsors of B2B guests](../external-id/b2b-sponsors). They are not authorized to make any changes to their sponsored users, but they can request access on the user's behalf and may be involved in approval flows. In contrast, sponsors of agent identities, blueprints, and blueprint principals have limited access to manage those identities directly and can also request access or give approvals in lifecycle workflows.

When an agent is represented by both an agent identity object and an agent user account, we recommend maintaining the agent identity sponsor as the primary user or group responsible for the agent.

If you require different access or authorization for an associated user account than from its agent identity, then sponsors for each object can [request access packages](../id-governance/entitlement-management-request-access) on behalf of the identity they sponsor. If you need to set a sponsor on an agent's user account, then the same user or group should be set as the sponsor on both objects to ensure they can request the appropriate access for both the agent identity and the agent's user account as needed.

| - | Agent user account sponsors | Agent identity, blueprint, blueprint principal sponsors |
| --- | --- | --- |
| **Allowed types** | Users (including guests), groups (any) | Users (including guests), select groups (dynamic membership, Microsoft 365). Role-assignable groups not supported. |
| **Limits** | Maximum 5 sponsors | Maximum 100 sponsors, with no more than 5 groups |
| **Authorization** | No direct authorization to modify sponsored users | Delete or disable the agent identity and modify its sponsors |
| **Required** | Not required | Required on create for agent identities and agent blueprints |

## Managers

Managers are individual users responsible for an agent identity within the organizational hierarchy. For agents that are active in user scenarios, consider setting a manager on the agent's user account. Managers can request access packages for their agents' user accounts, and will see agents designated as reporting to them in the Microsoft Entra admin center. Managers don't have authorization to modify or delete agents; owners, sponsors, or administrators are required to take those actions.

## Requirements and constraints

The administrative model enforces specific requirements and constraints to ensure effective oversight and accountability.

### Creation requirements

A sponsor is required when creating an agent identity or agent blueprint. Agent identity blueprint principals are exempt from the sponsor requirement during creation. Owners and managers are always optional.

### Assignment policies

For delegated creation requests where both an application and user context exist, the calling user automatically becomes the sponsor if no sponsors are explicitly specified. However, if one or more other sponsors are designated during creation, the calling user isn't automatically added. Users with Agent ID admin roles aren't made sponsor automatically during creation. This avoids unintentionally overburdening admins with direct responsibility for individual agents.

For app-only create requests, the creating service must set one or more users or supported groups as the sponsor.