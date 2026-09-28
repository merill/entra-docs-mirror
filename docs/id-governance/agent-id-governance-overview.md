---
layout: Conceptual
title: Governing Agent Identities - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/agent-id-governance-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article describes governing agent identities.
ms.topic: concept-article
ms.date: 2026-06-05T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: ed193cb7-7f23-723e-a597-712ddd774728
document_version_independent_id: ed193cb7-7f23-723e-a597-712ddd774728
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/agent-id-governance-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/agent-id-governance-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/agent-id-governance-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/302444b9-4a43-4841-8014-3d9e4251ff15
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/bebd8809-dac1-4c22-83e2-66d98af8a94d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 164bf6d7-81ac-6dea-8405-e32ca38f6971
---

# Governing Agent Identities - Microsoft Entra ID Governance | Microsoft Learn

Microsoft Entra allows you to ensure that the right people have the right access to the right apps and services at the right time. With the addition of the Microsoft agent identity platform, managing the access rights of agents in the same way is just as important in the governance lifecycle of your organization's identities. The Microsoft agent identity platform introduces the concept of Agent Identities (IDs). Agent identities are accounts within Microsoft Entra ID that provide unique identification and authentication capabilities for AI agents.

This allows agent identities to be governed with Microsoft Entra features in the same style as you would govern human identities. With Agent identities, you can govern and manage the identity and access lifecycle of agents, ensuring the agents have a responsible person providing oversight throughout the agent lifecycle and agent's access does not persist longer than it is needed. This article provides an overview of how Microsoft Entra can be utilized to govern agent identities.

## License requirements

Using [Microsoft Entra ID Governance](licensing-fundamentals) for agent identities requires one of the following license plans:

- **Microsoft 365 E7**, which includes Agent 365 and Microsoft Entra Suite, to provide governance of user and agent identities.
- **Microsoft Agent 365** license paired with at least Microsoft Entra P1 or Microsoft 365 E3.

For more information, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing). For the full list of agent-specific capabilities, refer to the **Microsoft Agent 365** column in the [Microsoft Entra ID Governance licensing table](licensing-fundamentals).

## Agent identities basics

Historically, AI agents would rely upon tools to interact with various applications and systems, and each of those tools would have their own identities in those applications and systems. Some of those tools would use service principals to authenticate to Microsoft services via Microsoft Graph or Microsoft Azure APIs. [Microsoft Entra Agent ID](../agent-id/what-are-agent-identities) introduces support for identities for the agents themselves, with four new types of object: agent identity blueprint, agent identity blueprint principal, agent identity, and agent user. Through the [agent identity blueprint](../agent-id/agent-blueprint), the agent can create one or more agent identities, and optionally an agent user for each agent identity. Each agent identity and agent user can have distinct access rights.

![Diagram of the relationship of Microsoft Entra Agent ID objects in a single tenant.](media/agent-id-governance-overview/agent-identity-objects-single-tenant.png)

For a multitenant-capable agent, an agent identity blueprint principal can be brought into the tenant with resources so it can create agent identities in that tenant, similar to how a multitenant application can have a service principal in each tenant.

![Diagram of the relationship of Microsoft Entra Agent ID objects in multiple tenants.](media/agent-id-governance-overview/agent-identity-objects-multiple-tenant.png)

The agent identity and the agent user allow AI agents to take on digital identities within Microsoft Entra. Once agent identities are created, these agent identities are able to be governed using lifecycle and access features. Sponsors can be assigned to agent identities after creation. Sponsors of agent identities are human users accountable for making decisions about its lifecycle and access. For more information about the role of a sponsor of agent identities, see: [Administrative relationships for agent IDs](../agent-id/agent-owners-sponsors-managers).

### Agent identities in other Microsoft products and portals

- **Microsoft Foundry** automatically provisions and manages agent identities throughout the agent lifecycle. When the first agent in a Foundry project is created, Microsoft Foundry provisions a default agent identity blueprint and a default agent identity for the project, and agents in the project authenticate by using the shared project's agent identity. Publishing an agent automatically creates a dedicated agent identity blueprint and agent identity, and the agent will authenticate by using the unique agent identity. Foundry supports use of the agent identity for authentication in Model Context Protocol (MCP) and Agent-to-Agent (A2A) tools. For more information, see [Agent identity concepts in Microsoft Foundry](/en-us/azure/ai-foundry/agents/concepts/agent-identity).
- You can configure an **Azure App Service or Azure Functions app** to use the Microsoft Entra agent identity platform to securely connect to resources as an agent. For more information, see [How to use an agent identity in App Service and Azure Functions](/en-us/azure/app-service/overview-agent-identity).
- Agents created in **Microsoft Copilot Studio** can be configured to automatically be assigned to an agent identity. When an agent identity is first created in a Power Platform environment after enabling this setting, a Microsoft Copilot Studio agent identity blueprint, and an agent identity blueprint principal, are automatically created. For more information, see [Automatically create Entra agent identities for Copilot Studio agents (preview)](/en-us/microsoft-copilot-studio/admin-use-entra-agent-identities).
- For agents in the **Microsoft Teams** platform, a developer can create and manage agent identity blueprints in the Developer Portal for Teams. For more information, see [Manage your apps in Developer Portal](/en-us/microsoftteams/platform/concepts/build-and-test/manage-your-apps-in-developer-portal).
- **Microsoft Agent 365** gives each AI agent its own Microsoft Entra Agent ID, for identity, lifecycle, and access management. For more information, see [Agent identity platform capabilities for Agent 365](/en-us/microsoft-agent-365/admin/capabilities-entra).

## Assigning access to agent identities

When created, agent identities have limited permissions, such as OAuth 2 delegated permission scopes [inherited from their parent agent identity blueprint](../agent-id/configure-inheritable-permissions-blueprints). In addition, agent identities can have resource access assigned to them directly via access packages. Agents can request an access package for own agent IDs, or have their owner or sponsor request one on their behalf. With access packages, you're able to assign agent identities access to the following resources:

- Security Group memberships
- [Application OAuth API permissions](../identity/enterprise-apps/assign-agent-identities-to-applications), including Graph application permissions
- [Microsoft Entra roles](../agent-id/authorization-agent-id#microsoft-entra-role-assignments-for-agent-identities)

To use access packages for agent identities, configure an access package with the required policy settings. When creating an access package assignment policy, in the **Who can get access** section, select **For users, service principals, and agent identities in your directory**, and then select the option of **All agents**.

Note

If your agents aren't using Microsoft Entra agent IDs, then also create an access package assignment policy with the option **All Service principals** to allow service principals in your directory to be able to request this access package.

Agents can then be assigned access packages through three different request pathways.

- The agent identity itself can programmatically request an access package when needed for its operations, by creating an [accessPackageAssignmentRequest](/en-us/graph/api/entitlementmanagement-post-assignmentrequests?tabs=http).
- The agent's sponsor can request access on behalf of the agent ID, providing human oversight in the access request process. For more information, see [Request an access package on behalf of an agent identity](entitlement-management-request-behalf#request-an-access-package-on-behalf-of-an-agent-identity).
- An administrator can [directly assign the agent identity or agent user to the access package](entitlement-management-access-package-assignments#directly-assign-an-identity).

After submission, the access request is routed to designated approvers based on the access package configuration.

When the agent identity has received an access package assignment with an expiry date, and if a sponsor is set on the agent identity, as the expiry date approaches, the sponsor receives notifications about the pending expiration. The sponsor then has two options: they can request an extension of the access package (if permitted by policy), or they can allow the access package assignment to expire. If the sponsor requests an extension, this request can trigger a new approval cycle, where approvers again confirm whether continued access is appropriate. If the sponsor takes no action, the access package assignment automatically expires on its end date, and the agent identity loses access to the target resources.

For a guide on creating an access package for agents, see: [access packages for agent identities in Microsoft Entra Agent ID](../agent-id/agent-access-packages). For a guide on assigning identities to an existing access package, see: [View, add, and remove assignments for an access package in entitlement management](entitlement-management-access-package-assignments).

## Conditional Access for agent identities

Entitlement management controls which resources an agent identity can be assigned. To also control the conditions under which an agent identity can access those resources, you can apply Conditional Access to agent identities. Conditional Access policies evaluate agent context and risk—including agent identity risk from Microsoft Entra ID Protection—before granting access. You can apply these policies at the agent identity blueprint level so that all agent identities created from a blueprint inherit them.

For more information, see [Conditional Access for agents](../identity/conditional-access/agent-id) and [Identity Protection for agents](../id-protection/concept-risky-agents).

## Management of agents

When agent identities are created, owners and sponsors of the agent can manually make decisions for the agent identity via both the My Account portal, and the My Access Portal.

From the [My Account portal](https://myaccount.microsoft.com/), Sponsors and Owners are able to manage the identity lifecycle of agents such as enabling and disabling the agent. You are also able to see information about its access, activity, and lifecycle. For more information about Managing agents, see: [Manage Agents in Microsoft Entra ID](../agent-id/manage-agent).

From the [My Access portal](https://myaccess.microsoft.com/), Sponsors and Owners of agent identities are able to request access packages on behalf of their agent identities. For a guide on requesting access packages, see: [Request an access package on behalf of an agent identity](entitlement-management-request-behalf#request-an-access-package-on-behalf-of-an-agent-identity).

## Agent identities sponsor administration

One of the most important parts of governing agent identities is making sure that a delegated human user is always assigned to make sure the agent identity's access to resources are current. If the sponsor is leaving the organization, sponsorship of the agent identities is automatically transferred to their manager. With sponsorship transferred, there's always a human user accountable for managing the access and lifecycle of the agent identities. Microsoft Entra ID Governance features can help streamline this process within your organization. Lifecycle workflows include multiple tasks around notifying cosponsors, and managers of sponsors, of impending sponsorship changes. For a guide on setting up a workflow for agent identities sponsors, see: [Agent identity sponsor tasks in Lifecycle Workflows](agent-sponsor-tasks).