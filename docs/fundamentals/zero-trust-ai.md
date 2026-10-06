---
layout: Conceptual
title: Configure Microsoft Entra agent identities for increased security - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/zero-trust-ai
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Improve your security posture with the Microsoft Entra Zero Trust assessment to secure AI agents and workloads.
ms.topic: concept-article
ms.date: 2026-05-18T00:00:00.0000000Z
ms.reviewer: ramical
ai-usage: ai-assisted
locale: en-us
document_id: 48e09a3f-0701-df0f-295c-d33e76e791c8
document_version_independent_id: 48e09a3f-0701-df0f-295c-d33e76e791c8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/zero-trust-ai.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/zero-trust-ai
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/zero-trust-ai.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b4b35fcf-0e64-7bc6-8972-d734113af0be
---

# Configure Microsoft Entra agent identities for increased security - Microsoft Entra | Microsoft Learn

AI agents acquire access tokens for organizational resources on every interaction, including mail, files, line-of-business APIs, and downstream agents. Unlike interactive users, agents usually don't present the same sign-in signals, such as user MFA, managed device state, or location context. Securing the AI control plane is therefore essential to your Zero Trust journey.

Agent issues commonly appear in three areas:

- **Authentication and policy mismatch**: Policies designed for users can miss agent-specific token patterns and execution models.
- **Overpermissioned access**: Agents often accumulate broad API permissions across Microsoft Graph and custom APIs, increasing blast radius.
- **Lifecycle and accountability gaps**: Orphaned agent identities, missing owners or sponsors, and stale credentials create persistent risk.

The recommendations and Zero Trust checks that are part of this pillar help reduce the risk of unauthorized AI access. Themes include enforcing Entra authentication on agent endpoints, applying Conditional Access policies to agent identities, assigning lifecycle governance controls, and ensuring AI administrative roles have accountable principals.

## Zero Trust security recommendations for AI

### Require Microsoft Entra ID authentication to interact with agents

An agent endpoint that does not require Microsoft Entra user authentication is an unauthenticated but reachable surface inside the tenant's AI estate. A threat actor might find this endpoint by discovering public agent URLs, using leaked Copilot Studio links, or enumerating Foundry project endpoints. The actor can then interact with the agent without presenting an identity and use the agent’s existing grants to access grounding data, connected tools, and downstream APIs.

Calls that don't reach Microsoft Entra can't be evaluated by Conditional Access policies, have no sign-in risk to calculate, and can't tie audit records to a specific user. The lack of this information makes it difficult to investigate and remediate. The runtime behavior that enforces Microsoft Entra user authentication lives inside each agent's host (Copilot Studio, Microsoft Copilot, Microsoft Foundry, custom code, or non-Microsoft platforms) and is therefore not directly observable from the directory. What *is* observable is the trail left in the Microsoft Entra sign-in logs whenever an agent and its callers do go through Microsoft Entra.

This check inspects the last 30 days of sign-in activity for each agent identity and classifies the agent by the strongest evidence found: a non-interactive agent sign-in where the subject is a real user is the strongest positive signal. An interactive user sign-in to the agent's blueprint is also positive evidence that users reach the agent through Microsoft Entra. Absence of either signal across the observation period means the platform can't confirm the agent enforces Microsoft Entra user authentication, and an accountable owner must verify the agent's host configuration directly.

**Remediation action**

- [Authenticate users in interactive agents](/en-us/entra/agent-id/interactive-agent-authentication-authorization-flow)
- [Request delegated user authorization for interactive agents](/en-us/entra/agent-id/grant-agent-access-microsoft-365)
- [Agent users in Microsoft Entra Agent ID](/en-us/entra/agent-id/agent-users)
- [Microsoft Entra Agent ID overview](/en-us/entra/agent-id/what-is-microsoft-entra-agent-id)
- [Sign-in logs in Microsoft Entra ID](/en-us/entra/identity/monitoring-health/concept-sign-ins)

### Conditional Access policies cover both agent identities and agents' user accounts

When an organization deploys AI agents, those agents acquire access tokens to access organizational resources on every interaction, but without an interactive user session and device, location, or MFA signals that classic Conditional Access uses to make trust decisions for human users. Microsoft Entra Agent ID introduces two distinct identity types:

- An [agent identity](/en-us/entra/agent-id/agent-identities): An identity account within Microsoft Entra ID that provides unique identification and authentication capabilities for AI agents.
- An [agent's user account](/en-us/entra/agent-id/agent-users): An optional account that pairs 1:1 with an agent identity when the agent must access systems that require a user object.

Conditional Access treats both agent identity objects as separate principal types. So a policy that targets agent identities can't target an agent's user account, and vice versa. A tenant that enables agent workloads without at least one Conditional Access policy enforcing block-unless-approved has no enforcement boundary on autonomous AI access. Every token request from an agent identity or agent's user account is allowed by default. Threat actors seek to exploit this type of failure mode when they compromise a single agent identity or its backing agent's user account and pivot through the resources that identity can reach.

**Remediation action**

- [Conditional Access for Agent ID (Preview)](/en-us/entra/identity/conditional-access/agent-id)
- [Identity Protection signals for agents](/en-us/entra/id-protection/concept-risky-agents)
- [Filter for applications in Conditional Access](/en-us/entra/identity/conditional-access/concept-filter-for-applications)
- [Custom security attributes in Microsoft Entra ID](/en-us/entra/fundamentals/custom-security-attributes-add)

### Risk-based Conditional Access blocks risky agent identities

When an organization enables AI agents in Microsoft Entra, [agent identities](/en-us/entra/agent-id/agent-identities) can access tokens to access organizational resources without an interactive user session and device, location, or MFA signals that classic Conditional Access uses to make trust decisions for human users. Microsoft Entra ID Protection for agents continuously evaluates each agent's behavior and emits a risk level that is driven by signals such as:

- Unfamiliar resource access (the agent reaches outside its established patterns)
- Sign-in spikes (token replay or automation abuse)
- Failed-access probing (an attacker enumerating resources with the agent's credentials)
- Sign-ins by risky users during delegated authentication (an attacker leveraging a compromised user account)
- Admin-confirmed compromise (a security admin manually flags the agent as compromised)

Without a Conditional Access policy that consumes the risk level and blocks token issuance, the platform can just record that an agent is high risk while continuing to mint the very tokens the adversary needs. The logs say "compromised" while the resource still says "yes." A risk-based Conditional Access policy that blocks high-risk agent identities is required to close this gap between detection and enforcement.

**Remediation action**

- [ID Protection for agents](/en-us/entra/id-protection/concept-risky-agents)
- [Conditional Access for agent identities](/en-us/entra/identity/conditional-access/agent-id)

### Custom security attributes for agent identities are present

Custom security attributes are the primary mechanism for Conditional Access to distinguish between agent identities at scale. Without them, Conditional Access policies can only target all agent identities, individual agents by object ID, or agents grouped by blueprint. As your agent fleet grows, these mechanisms can't scale. Custom security attributes unlock the ability to filter agents by department, approval status, sensitivity tier, or any organization-defined classification. For example, an attribute set called `AgentAttributes` with an `AgentApprovalStatus` attribute (values such as `New`, `In_Review`, `HR_Approved`, `Finance_Approved`, `IT_Approved`) enables attribute-based Conditional Access policies that match agents to resources based on their classification.

When agent identities lack custom security attributes, the organization can't reliably enforce attribute-based Conditional Access policies. A newly provisioned or unclassified agent identity receives the same access controls as a fully vetted agent identity because there is no metadata to differentiate them. A threat actor who compromises or registers a rogue agent identity gains access without being subject to classification-based policy enforcement. Assigning custom security attributes closes this gap by ensuring every agent identity carries machine-readable classification metadata that Conditional Access and audit queries can consume.

Policies that target all agent identities without attribute filters may still provide baseline protection, but they can't distinguish between approved and unapproved agents. Implementing attribute-based controls requires:

- Defining an attribute taxonomy
- Coordinating with application owners
- Establishing an operational process to tag new agents as they're provisioned

**Remediation action**

- [Conditional Access for agent identities](/en-us/entra/identity/conditional-access/agent-id)
- [Add or deactivate custom security attributes in Microsoft Entra ID](/en-us/entra/fundamentals/custom-security-attributes-add)
- [Assign custom security attributes to an application](/en-us/entra/identity/enterprise-apps/custom-security-attributes-apps)
- [Manage custom security attribute assignments using Microsoft Graph](/en-us/graph/custom-security-attributes-examples)
- [Filter for applications in Conditional Access](/en-us/entra/identity/conditional-access/concept-filter-for-applications)

### Identity governance for agent identity sponsors is configured

Microsoft Entra Agent ID requires every [agent identity](/en-us/entra/agent-id/agent-identities) and [agent identity blueprint](/en-us/entra/agent-id/agent-blueprint) to have at least one sponsor. A sponsor is a human user, or supported group, that holds business accountability for the agent's lifecycle, such as deciding when the agent is no longer needed, approving extensions when access expires, and authorizing suspension during incidents. A sponsor is different from an owner, which designates the human users responsible for technical operations and incident response.

Sponsorship is the entry point for identity governance:

- Lifecycle Workflows can route sponsor-leaving notifications to managers
- Access package expiry escalations are sent to the sponsor
- Entitlement management approvers rely on the sponsor relationship to validate continued access.

Without an assigned sponsor, agent identities can't be properly governed. An agent identity that exists without a sponsor is governance-invisible. Without an access package that targets agent identities, every permission an agent receives must be granted directly, through `appRoleAssignment`, `oauth2PermissionGrant`, group membership, or directory-role assignment, which is outside the entitlement management control loop. Direct grants have no built-in expiration, no approver loops, and no access review schedules. Without a Lifecycle Workflow containing agent sponsor tasks, the sponsor relationship is a static directory record with no automation when a sponsor moves or leaves. A threat actor who compromises an ungoverned agent — through credential theft, blueprint compromise, or a malicious access-package request that no governance pipeline existed to intercept — operates against an identity whose permissions were never reviewed. This check also verifies that at least one access package assignment policy targets all directory agent identities.

**Remediation action**

- [Administrative relationships in Microsoft Entra Agent ID](/en-us/entra/agent-id/agent-owners-sponsors-managers)
- [Governing agent identities](/en-us/entra/id-governance/agent-id-governance-overview)
- [Agent identity sponsor tasks in Lifecycle Workflows](/en-us/entra/id-governance/agent-sponsor-tasks)
- [Access packages for agent identities](/en-us/entra/agent-id/agent-access-packages)
- [Create an access package in entitlement management](/en-us/entra/id-governance/entitlement-management-access-package-create)

### Agent identities and blueprint principals have assigned technical owners and no disabled agents remain in the directory

Microsoft Entra Agent ID introduced two identity types: [agent identities](/en-us/entra/agent-id/agent-identities) and [agent identity blueprint principals](/en-us/entra/agent-id/agent-blueprint). These identity objects derive from service principals, and so carry the same requirements and best practices for ownership, lifecycle management, and cleanup as any service principal. Blueprint principals are the provisioning surface from which agent identities are created and can hold grants that propagate to child agents. Having a designated owner for these objects helps in two important areas of agent identity management:

- Risks are contained and investigated by a responsible party
- Disabled objects don't introduce dormant privileges

The owners relationship on each agent identity object designates the human users responsible for technical operations and incident response, distinct from the sponsors relationship that carries business accountability for lifecycle and access decisions. So when ID Protection flags an agent identity as risk or anomalous resource access patterns emerge, the security operations team can route to a responsible party for containment and investigation. If there's no owner designated, a threat actor who compromises an ownerless agent or blueprint principal (through credential theft, blueprint exploitation, or malicious delegated consent) operates against a principal with no designated human for immediate containment. This issue can extend dwell time from minutes to the next manual directory audit cycle.

When an agent identity or agent identity blueprint is disabled, it can't acquire new tokens so it can't access resources. The object still exists in the directory, so its app role assignments, group memberships, and OAuth2 permission grants persist. If an administrative error or a threat actor with directory write access re-enables the object, every permission snaps back without reapproval. If a disabled blueprint principal is re-enabled, it also restores the provisioning surface for all child agent identities. The combination of ownerless objects and stale disabled objects creates a standing-privilege accumulation pattern that proper ownership and cleanup are designed to prevent.

**Remediation action**

- [Administrative relationships in Microsoft Entra Agent ID](/en-us/entra/agent-id/agent-owners-sponsors-managers)
- [Manage agent identities in your organization](/en-us/entra/agent-id/manage-agent-identities-admin)
- [Governing agent identities](/en-us/entra/id-governance/agent-id-governance-overview)
- [Manage agents in end-user experience](/en-us/entra/agent-id/manage-agent-identities-end-user)

### AI administrative roles have assigned principals

The AI control plane surface includes Microsoft 365, Microsoft Power Platform, Microsoft SharePoint, and every layer of the Microsoft Security stack. Microsoft Entra ID is the identity control plane for this entire surface, and its administrative scopes manage agent identities, Microsoft Copilot admin settings, Conditional Access for AI, Copilot Studio environments, AI grounding sources, AI posture signals, and AI detection and response. If there's no human assigned to an administrative role that manages these AI capabilities, then there's no accountable operator for that slice of the AI surface. This gap could mean:

- Agent identities aren't monitored or reviewed
- Admin settings drift
- AI-specific detections have no owner to investigate or adjust
- Network control policies for AI aren't adjusted as the AI estate evolves
- AI-related escalations have no designated responder

Threat actors exploit this gap by targeting the AI control plane directly. They rely on the gap between a role existing in the directory and someone actually monitoring it. Confirming that every AI admin role has at least one assigned principal is the minimum organizational posture for AI administration. This check evaluates Microsoft Entra directory role assignments only. A role appearing as unassigned means no Microsoft Entra principal is assigned to the corresponding directory role, so workload-native administrators might still exist outside Microsoft Entra and are outside this assessment. AI administration of other platforms, such as Microsoft Purview role groups or Microsoft Defender custom roles, must be reviewed separately.

**Remediation action**

- [Assign a Microsoft Entra ID role via the admin center](/en-us/entra/identity/role-based-access-control/manage-roles-portal)
- [Create a PIM-eligible assignment for a Microsoft Entra ID role](/en-us/entra/id-governance/privileged-identity-management/pim-how-to-add-role-to-user)