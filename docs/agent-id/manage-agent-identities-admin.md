---
layout: Conceptual
title: Manage agent identities in your organization - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/manage-agent-identities-admin
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to manage agent identities across your organization. View, disable, govern, and monitor agents using the Microsoft Entra admin center and Conditional Access.
ms.topic: how-to
ms.date: 2026-05-01T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-108
locale: en-us
document_id: 146fd252-2c0e-a85e-8ffd-cb4bfb776cb4
document_version_independent_id: 146fd252-2c0e-a85e-8ffd-cb4bfb776cb4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/manage-agent-identities-admin.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/manage-agent-identities-admin
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/manage-agent-identities-admin.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 54c3c724-cf4e-b2b9-de7b-08be321b5c4a
---

# Manage agent identities in your organization - Microsoft Entra Agent ID | Microsoft Learn

Microsoft Entra Agent ID provides a centralized set of tools for managing agent identities across your organization. Agent identities are a distinct identity type in Microsoft Entra ID, designed for AI agents with classification, metadata, and security controls tailored to agentic workloads.

This article covers key agent management tasks: from viewing and disabling agents, to governing access, monitoring activity, and responding to security risks. Whether you're an administrator responsible for tenant-wide agent oversight or a sponsor managing specific agents, this guide provides the information you need to effectively manage agent identities in your organization.

## Prerequisites

Different management tasks require different roles and licenses. The following table summarizes the roles you need for each area of agent identity management.

| Task | Required role | Notes |
| --- | --- | --- |
| View agent identities | Microsoft Entra user account | No admin role needed for viewing. |
| Manage agent identities | Agent ID Administrator or Cloud Application Administrator | Agent identity owners can manage their own agents without these roles. |
| Create agent blueprints | Agent ID Developer | User is added as owner of the blueprint and its service principal. |
| Configure Conditional Access policies | Conditional Access Administrator | Requires Microsoft Entra ID P1 license. |
| View ID Protection risk reports | Security Administrator, Security Operator, or Security Reader | Requires Microsoft Entra ID P2 license during preview. |
| Configure Lifecycle Workflows | Lifecycle Workflows Administrator |  |

## View agent identities

The Microsoft Entra admin center provides a centralized interface to view all agent identities in your tenant. You can search, filter, sort, and customize columns to find specific agents.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Agents** &gt; **Agent identities**.
3. Select any agent identity to view its details, including name, description, status, owners, sponsors, granted permissions, and sign-in logs.

To search for a specific agent, enter the **name** or **object ID** in the search box, or add the **Blueprint App ID** filter. You can customize which columns are shown by selecting the **Choose columns** button. Available columns include **Name**, **Created On**, **Status**, **Object ID**, **View Access**, **Blueprint App ID**, **Owners and Sponsors**, and **Uses agent identity**.

For detailed instructions on filtering, column customization, and viewing agents from this view, see [View and filter agent identities in your tenant](agent-lists).

## Manage agent identity blueprints

Agent identity blueprints are the parent definitions from which individual agent identities are created. The admin center lets you view all blueprint principals, manage their permissions, and monitor their activity.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Agents** &gt; **Agent blueprints**.
3. Select any agent identity blueprint principal to manage it.

From a blueprint's management page, you can:

- **View linked agent identities**: See all child agent identities created from this blueprint.
- **Manage blueprint access**: View, manage, and revoke permissions assigned to the blueprint.
- **Manage owners and sponsors**: Owners handle technical administration, while sponsors are accountable for the agent's purpose and lifecycle decisions.
- **View audit logs**: Track administrative changes for security and compliance.
- **View sign-in logs**: Monitor authentication events.
- **Disable the blueprint**: Select **Disable** in the command bar.

For detailed instructions, see [View and manage agent identity blueprints in your tenant](manage-agent-blueprint).

## Configure inheritable permissions for blueprints

Inheritable permissions let agent identities automatically inherit OAuth 2.0 delegated permission scopes from their parent blueprint. When you configure inheritable permissions on a blueprint, newly created agent identities receive a base set of scopes without requiring interactive user or admin consent prompts.

Two inheritance patterns are supported per resource app:

| Pattern | Description |
| --- | --- |
| **Enumerated scopes** | Inherit only explicitly listed scopes. Use for fine-grained control. |
| **All allowed scopes** | Inherit all available delegated scopes for the resource app. Newly granted scopes on the blueprint are automatically included. |

Start with enumerated scopes using only essential permissions, then expand as needed. This approach follows the principle of least privilege and makes it easier to audit which permissions agents actually use.

Key limits:

- Maximum of 10 resource apps per blueprint.
- For enumerated scopes, maximum of 40 scopes per resource app.
- Some high-privilege scopes are blocked by platform policy and can't be inherited.

Inheritable permissions are configured via the `inheritablePermissions` navigation property on the `agentIdentityBlueprint` application resource using Microsoft Graph. For step-by-step API examples (add, update, delete), see [Configure inheritable permissions for agent identity blueprints](configure-inheritable-permissions-blueprints).

## Control agent access to resources

Conditional Access policies provide tenant-wide controls for agent identity authentication. You can use these policies to block all agent identities, allow only specific agents, or block risky agents based on ID Protection signals.

Key points about Conditional Access for agent identities:

- Policies can scope to **All agent identities** or **All agent users** with a **Block** grant control.
- Policies can target **All resources** to prevent agent access across your organization.
- **Agent risk conditions** (high, medium, low) allow you to block agents based on risk signals from ID Protection.
- Policies support **Report-only mode** for safe evaluation before enforcement.

Important

Conditional Access enforcement applies when an agent identity or agent's user account requests a token for any resource. It does **not** apply when an agent identity blueprint acquires a token to create agent identities or agent's user accounts.

For detailed policy configuration, step-by-step walkthroughs, and business scenario examples, see [Conditional Access for Agent ID](/en-us/entra/identity/conditional-access/agent-id).

## Monitor agent activity

### Sign-in and audit logs

Agent identity activities are captured in Microsoft Entra audit and sign-in logs:

- **Audit logs** record agent-related events under the base identity type from which they originate. For example, creating an agent identity user appears as a "Create user" audit activity, and creating an agent identity appears as a "Create service principal."
- **Sign-in logs** include the `agentSignIn` resource type, which provides properties about the agent and its sign-in behavior.

To view agent sign-in logs:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
3. Use the following filters:
    - **Agent type**: Choose from **Agent ID user**, **Agent Identity**, **Agent Identity Blueprint**, or **Not Agentic**.
    - **Is Agent**: Choose from **No** or **Yes**.

You can also retrieve agent sign-in events using Microsoft Graph:

```http
GET https://graph.microsoft.com/beta/auditLogs/signIns?$filter=signInEventTypes/any(t: t eq 'servicePrincipal') and agent/agentType eq 'AgentIdentity'
```

For full details on log types and access methods, see [Microsoft Entra Agent ID logs](sign-in-audit-logs-agents).

## Detect and remediate agent risk

### Identity Protection for agents

Microsoft Entra ID Protection monitors agent identities for anomalous behavior. It detects six offline risk types, including unfamiliar resource access, sign-in spikes, and failed access attempts. Administrators can review the **Risky Agents report** and take response actions: confirm compromise, confirm safe, dismiss risk, or disable the agent.

Note

ID Protection for agents requires a Microsoft Entra ID P2 license during preview.

When you confirm an agent as compromised, the risk level is set to **High**. If you have a Conditional Access policy configured to block on High Agent Risk, the agent is automatically blocked from accessing resources.

For the full risk detection table, response actions, Graph API details, and report walkthrough, see [Identity Protection for agents](/en-us/entra/id-protection/concept-risky-agents).

### Respond to agent security incidents

When agent activity triggers a risk detection or security concern, follow this sequence:

1. **Detect**: Review the **Risky Agents report** in the Microsoft Entra admin center. Risk detections are viewable for up to 90 days. Details include the agent's display name, risk state, risk level, agent type, and sponsors.
2. **Respond**: Take an immediate action:
    - **Confirm compromise**: Sets the risk level to High and triggers risk-based Conditional Access policies configured to block on High Agent Risk.
    - **Disable**: Prevents all sign-ins across Microsoft Entra ID and connected apps.
3. **Investigate**: Review risk detection details, sign-in logs, and audit logs to understand the scope and impact.
4. **Recover**: Based on your investigation:
    - If false positive: dismiss the risk and re-enable the agent.
    - If true compromise: rotate credentials before re-enabling, or retire the agent identity.

For detailed information on risk types, detection mechanisms, and response actions, see [Identity Protection for agents](/en-us/entra/id-protection/concept-risky-agents).

## Govern agent identities and sponsor oversight

### Sponsor responsibilities

Each agent identity should have an accountable human sponsor responsible for lifecycle and access decisions. Key governance behaviors include:

- **Automatic sponsor transfer**: If a sponsor leaves the organization, Microsoft Entra ID automatically reassigns sponsorship to the sponsor's manager.
- **Expiration notifications**: Sponsors receive notifications when access package assignments approach expiration. Sponsors can request an extension (which triggers a new approval cycle) or let assignments expire.
- **Access request pathways**: Access packages can be requested through three pathways: the agent's own programmatic request, a sponsor on behalf of the agent, or an admin direct assignment.

Access packages can grant Security Group memberships, Application OAuth API permissions (including Microsoft Graph application permissions), and Microsoft Entra roles.

For the full governance overview including access package configuration and sponsor policies, see [Governing Agent Identities](/en-us/entra/id-governance/agent-id-governance-overview).

### Automate sponsor notifications with Lifecycle Workflows

Lifecycle Workflows provides two automated tasks for agent identity sponsorship:

- Send email to manager about sponsorship changes
- Send email to cosponsors about sponsor changes

Both tasks are **mover and leaver** category tasks: they trigger only under mover or leaver workflow templates, not joiner templates. This ensures continuity of sponsorship when an agent's sponsor changes roles or leaves the organization.

For step-by-step workflow configuration, see [Agent identity sponsor tasks in Lifecycle Workflows](/en-us/entra/id-governance/agent-sponsor-tasks).

## Automate agent management at scale

For organizations managing large numbers of agent identities, the following options are available:

- **Multi-select disable**: The admin center supports selecting multiple agent identities at once and disabling them in batch from the **All agent identities** page.
- **Microsoft Graph API**: Agent identity endpoints support programmatic management. For example, ID Protection exposes `riskyAgents` and `agentRiskDetections` collections for programmatic risk monitoring.

## Disable or restrict agent identities

Organizations can control agent identity usage at three levels, depending on the scope needed:

| Scope | What it does | Details |
| --- | --- | --- |
| **Individual agent** | Disable a specific agent identity to block its access and token issuance. Administrators use the admin center; owners and sponsors use the My Account portal. | [View and filter agent identities in your tenant](agent-lists) · [Manage agents in end user experience](manage-agent-identities-end-user) |
| **Blueprint-level** | Disable an agent identity blueprint from its management page. This prevents new agent identities from being created from that blueprint and blocks existing ones. | [View and manage agent identity blueprints in your tenant](manage-agent-blueprint) |
| **Tenant-wide** | Block all agent identity authentication using Conditional Access policies, and optionally block creation of new agent identities through product-specific controls (Microsoft Entra ID, Security Copilot, Copilot Studio, Azure AI Foundry, Microsoft Teams). | [Disable agent identities in your tenant](disable-agent-identities) |

Re-enabling a disabled agent identity at any scope restores access and token issuance.

Caution

Globally disabling agent identities can cause existing agents to fail, degrade Microsoft product experiences, and push teams to use less transparent application or service principal identities. Evaluate the impact before enforcing. For a partial approach, use Conditional Access policies to block specific agents rather than all agent identities.