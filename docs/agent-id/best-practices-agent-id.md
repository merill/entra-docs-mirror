---
layout: Conceptual
title: Best practices for Microsoft Entra Agent ID - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/best-practices-agent-id
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn operational best practices for designing, securing, and governing AI agent identities with Microsoft Entra Agent ID, including blueprint design, credential management, access controls, and monitoring strategies.
ms.date: 2026-11-06T00:00:00.0000000Z
ms.topic: best-practice
ai-usage: ai-assisted
ms.reviewer: kylemar
locale: en-us
document_id: 6f781d26-886f-5c07-279a-2ac90829032a
document_version_independent_id: 6f781d26-886f-5c07-279a-2ac90829032a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/best-practices-agent-id.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/best-practices-agent-id
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/best-practices-agent-id.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: baabd874-6b44-41e8-e8cc-6cc85e037c56
---

# Best practices for Microsoft Entra Agent ID - Microsoft Entra Agent ID | Microsoft Learn

This article provides operational best practices for designing, securing, and governing AI agent identities with Microsoft Entra Agent ID. These recommendations help you make informed decisions when planning agent deployments, managing credentials, enforcing access policies, and monitoring agent activity.

For foundational concepts, see [What is Microsoft Entra Agent ID?](what-is-microsoft-entra-agent-id) and [Key concepts](key-concepts). To build an agent, start with [Choose an integration path](choose-agent-integration-path); you don't need to complete architecture planning before following a tutorial.

## Design agent identity blueprints

[Agent identity blueprints](agent-blueprint) define authentication settings and the security posture for one or more agents. Thoughtful blueprint design is the foundation of well-governed agent deployments.

- **Plan blueprints before deploying agents.** Define required settings, permissions, and metadata in the blueprint up front rather than creating ad-hoc service principals. This ensures a consistent, governed rollout across all instances. For guidance on structuring your identity model, see [Plan your agent identity architecture](how-to-plan-agent-identity-architecture).
- **Give separately managed agents distinct identities.** Separate identities when agents need independent access, accountability, or lifecycle controls. Multiple replicas, processes, or user sessions of the same logical agent don't by themselves require new identities. For fleet provisioning, see [Create and delete agent identities](create-delete-agent-identities).
- **Assign a sponsor and an owner at creation time.** Every blueprint and agent identity must have a [sponsor](agent-owners-sponsors-managers), the person or supported group accountable for the agent's purpose. Assign an owner (technical admin) as well. Periodically verify that these assignments are current, especially when personnel changes occur.
- **Provide descriptive metadata.** Fill in the description, tags, and verified publisher fields on each blueprint to clearly document the agent's purpose, scope, and owning team. Good metadata improves discovery and helps colleagues understand the agent's role at a glance. For blueprint setup details, see [Create an agent identity blueprint](create-blueprint).
- **Separate policy targeting from permission grants.** Use blueprint-level policy controls where supported. API permissions aren't automatically inherited just because a blueprint declares them: fleet inheritance requires both consent and [configuration of inheritable permissions](concept-inheritable-permissions). A cloud or local single-instance agent receives grants directly, without a blueprint principal. For policy details, see [Conditional Access for agents](../identity/conditional-access/agent-id).
- **Use the Agent ID framework for all agents.** Don't create AI agents as plain app registrations or service principals outside the Agent ID framework. Always use the supported [creation channels](agent-id-creation-channels) so agents are tracked as agent identities with built-in sponsor accountability and lifecycle controls.
- **Create agent's user accounts only when necessary.**[Agent's user accounts](agent-users) should only be created for scenarios that truly require a user object, such as an agent needing a mailbox or Teams presence. If your agent can operate with app credentials alone, avoid agent's user accounts because they add complexity with licenses, group memberships, and user-level policies.

## Guardrails for AI coding assistants

AI coding assistants often default to creating a standard app registration when asked to build an agent, because that's the traditional workload identity pattern. Keep these guardrails visible in your instructions:

- Start with the [scenario tutorial](choose-agent-integration-path), rather than assuming every agent needs a fleet.
- Provision the supported Agent ID object type, not an ordinary app registration labeled as an agent.
- Keep the management client, upstream client, downstream API, and runtime agent identities separate.
- Match the SDK to the scenario: standard Microsoft.Identity.Web APIs for a cloud agent, Microsoft.Identity.Web.AgentIdentities with explicit child selection for a fleet, and MSAL without a client credential for a local public client.
- Distinguish human-user OBO from a dedicated agent-user account.
- Verify tenant enablement, operator authorization, management consent, and target API grants. Record object IDs separately from client IDs.

Copy the following sample into your repository's `.github/copilot-instructions.md` or `AGENTS.md` file:

```markdown
## Microsoft Entra Agent ID
- Start with the scenario tutorial at /entra/agent-id/choose-agent-integration-path. Don't impose a fleet topology on a cloud or local agent.
- Use the tutorial's supported Agent ID provisioning request, including the derived blueprint type where specified. An ordinary app registration doesn't represent an Agent ID.
- Keep management, upstream client, downstream API, and agent identities distinct. Ordinary app registrations can still be required for those non-agent roles.
- For a cloud ASP.NET Core agent, follow Microsoft.Identity.Web's standard client APIs. For a fleet, follow Microsoft.Identity.Web.AgentIdentities and select the child agent explicitly. For a local public client, follow MSAL and don't add a client credential.
- A human user's OBO request and a dedicated agent-user account are different scenarios; don't substitute WithAgentUserIdentity for human-user OBO.
- Verify tenant availability, operator authorization, management-client consent, and target API grants before claiming setup succeeded. Record object IDs separately from client IDs.
```

## Manage credentials securely

Credential management is critical to preventing unauthorized access through agent identities. For detailed steps, see [Create an agent identity blueprint](create-blueprint).

- **Use managed identities or certificates in production.** For production agents, prefer [federated identity credentials](/en-us/entra/identity/managed-identities-azure-resources/overview) (managed identities) or certificates over client secrets. Managed identities eliminate stored secrets entirely. Use client secrets only for initial development or testing, and rotate them out before going live.
- **Isolate credentials per blueprint.** Don't reuse the same credential across unrelated blueprints. If you have separate environments (dev, test, prod), use separate blueprints or environment-specific federated credentials so that a compromise in one environment doesn't affect others. For setup instructions, see [Create an agent identity blueprint](create-blueprint).
- **Store credentials securely.** Store certificate private keys in [Azure Key Vault](/en-us/azure/key-vault/general/overview) or an HSM. If using federated credentials tied to a managed identity, limit the managed identity's scope. Establish a rotation schedule to rotate certificates at least annually even though blueprints allow long-lived credentials.
- **Align OAuth flows with agent scenarios.** Use the appropriate [OAuth flow](agent-oauth-protocols) for your agent's operating model:

    - For autonomous agents with no user context, use the client credentials flow with only the required app permissions.
    - For a cloud agent API receiving a signed-in user's request, use the on-behalf-of (OBO) flow. Local public clients use authorization code flow with PKCE.
    - Avoid granting app permissions when delegated permissions would suffice.
- **Monitor token usage after deployment.** Review [sign-in logs](sign-in-audit-logs-agents) to confirm agents are using the intended authentication method and credential type. Periodically audit the API permissions consented on each blueprint to prevent privilege creep.

## Enforce access controls

Apply the same Zero Trust principles to agent identities as you do to user identities. For detailed configuration, see [Conditional Access for agents](../identity/conditional-access/agent-id) and [Identity Protection for agents](/en-us/entra/id-protection/concept-risky-agents).

- **Segment agents with custom security attributes.** Define organization-wide attributes such as `Environment`, `Department`, or `DataSensitivity` and assign them to agent identities. Use these attributes in Conditional Access policy conditions to apply fine-grained controls at scale, for example, blocking non-production agents from accessing production resources. For details, see [Assign custom security attributes](/en-us/entra/identity/users/users-custom-security-attributes).
- **Block high-risk agents automatically.** Deploy a Conditional Access policy that blocks agent identities flagged with high risk levels by [Identity Protection](/en-us/entra/id-protection/concept-risky-agents). This is analogous to blocking risky users and ensures compromised agents are cut off immediately.
- **Create agent-specific Conditional Access policies.** Don't rely on user-targeted policies for agents. Agents can't satisfy interactive controls like MFA, so create separate policies that use identity filters, risk signals, and named locations as control points. Use report-only mode to test policies before enforcing them. For step-by-step guidance, see [Conditional Access for agents](../identity/conditional-access/agent-id).
- **Review existing policies for agent impact.** Audit broad policies (like "All users must use MFA") to ensure they don't unintentionally block agent flows. Refactor to exclude agent identities and create dedicated agent policies with appropriate controls.
- **Implement least-privilege permissions.** Use the [authorization guidance](authorization-agent-id) to grant only the permissions each agent needs. Don't grant broad permissions as a convenience. Limit permissions to specific scopes, API resources, or sites. Review and right-size permissions periodically.

## Govern the agent lifecycle

Effective governance prevents agent sprawl and ensures agents remain accountable throughout their lifecycle. For governance tools, see [Identity governance for agents](/en-us/entra/id-governance/agent-id-governance-overview) and [Access packages for agent identities](agent-access-packages).

- **Register all agents in Microsoft Entra.** Register every agent, whether built in Copilot Studio, Azure, or external platforms, in Microsoft Entra through the Agent ID framework. Centralized registration eliminates shadow AI and gives IT full visibility. For supported methods, see [Agent creation channels](agent-id-creation-channels).
- **Standardize naming conventions.** Define and enforce a naming convention for agent identities, such as prefixing display names with the department or function (for example, `Agent-HROnboardingBot`). Consistent naming makes agents recognizable in logs and the admin center.
- **Include agents in access reviews.** Configure periodic [access reviews](/en-us/entra/id-governance/access-reviews-overview) that include agent identities. Have sponsors attest every 6-12 months that each agent is still needed and properly configured. If a sponsor doesn't confirm, evaluate the agent for decommissioning.
- **Monitor for orphaned agents.** Develop a quarterly review process to identify agents with missing sponsors, outdated metadata, or no recent activity. Reassign sponsorship or decommission unused agents. For a centralized view, see [View and filter agent identities](agent-lists).
- **Use access packages for standardized access.** For agents with common access patterns (for example, a fleet of customer support agents), use [access packages](agent-access-packages) to grant time-bound, auditable access through approval workflows rather than direct permission assignments.

## Monitor and audit agent activity

Continuous monitoring ensures agents operate within expected boundaries. For log details, see [Sign-in and audit logs for agents](sign-in-audit-logs-agents).

- **Monitor sign-in logs for anomalies.** Set up alerts for unusual patterns such as sudden spikes in token requests, access to unexpected APIs, or sign-ins from unfamiliar IP ranges. Agent sign-in logs show each token acquisition with details about the resource, credential type, and outcome.
- **Track configuration changes in audit logs.** Monitor [audit logs](sign-in-audit-logs-agents) for changes to agent blueprints, credential additions, permission grants, and role assignments. Alert on changes that happen outside your normal deployment pipeline.
- **Include agents in incident response.** When analyzing security incidents, check whether any agents had access to affected resources and review their activity during the incident window. Fold agent identity checks into your existing post-mortem processes.
- **Set up proactive alerts for:**

    - Credential expiration (certificates or secrets approaching their end date)
    - Agent blocked by Conditional Access or Identity Protection
    - Excessive failed token acquisition attempts
    - Unexpected permission or role changes
- **Retain logs for compliance.** Ensure your log retention policy covers agent activity for the duration required by your organization's compliance framework. Export high-volume agent logs to a secure archive if needed. For configuration options, see [Configure diagnostic settings](/en-us/entra/identity/monitoring-health/howto-configure-diagnostic-settings).

## Coordinate development and IT workflows

Smooth agent deployments require alignment between developers building agents and IT administrators governing them.

- **Use the procedure for your creation channel.** A managed platform can provision identities for you. For direct Microsoft Graph provisioning, preserve the tutorial's required object types, properties, and headers, and verify each returned object. Don't assume every [creation channel](agent-id-creation-channels) automates credentials, consent, and runtime setup.
- **Establish a production handshake process.** When a new agent moves to production, have an identity admin verify its Microsoft Entra Agent ID settings: confirm the blueprint and sponsor are correct, required permissions are consented, and Conditional Access policies apply. Verify any group assignments against the [agent identity restrictions](faq); agent identities can't be added to administrative units.
- **Test in nonproduction environments.** Use a separate development tenant or sandbox to validate agent authentication flows, Conditional Access policies, and permission configurations before deploying to production.
- **Treat nonsecret agent configurations as code.** Check blueprint definitions, permission configurations, and setup scripts into source control, but exclude tokens, secrets, private keys, and certificate passwords. This supports peer review and helps prevent configuration drift.