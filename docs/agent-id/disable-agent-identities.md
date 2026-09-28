---
layout: Conceptual
title: Disable agent identities in your tenant - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/disable-agent-identities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to disable agent identities in your Microsoft Entra ID tenant using Conditional Access policies and creation restrictions.
ms.topic: how-to
ms.date: 2026-04-29T00:00:00.0000000Z
ms.reviewer: dastrock
ai-usage: ai-assisted
locale: en-us
document_id: 34d86613-f80c-3cb4-8861-94260f3a6e4c
document_version_independent_id: 34d86613-f80c-3cb4-8861-94260f3a6e4c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/disable-agent-identities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/disable-agent-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/disable-agent-identities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: ba16b950-b950-cfce-6f11-332c53f43262
---

# Disable agent identities in your tenant - Microsoft Entra Agent ID | Microsoft Learn

As an IT administrator overseeing agent identities in your tenant, you might need to temporarily stop agent activity to investigate an issue or review agent usage. You can disable agent identities and agent identity blueprints in your tenant depending on your need. Both actions have implications that you should understand before proceeding.

You can also configure Conditional Access policies and remove agent creation permissions, if your organization needs to restrict agent identities from being created or used in your tenant. These processes can serve as a different approach to disabling agent identities. This article covers scenarios related to disabling agent identities.

## Types of identities used by AI agents

Your Microsoft Entra tenant might contain AI agents with or without a Microsoft Entra agent identity.

- **Agents with agent identities**: Agents created in Microsoft Entra Agent ID or using the latest iterations of systems like Microsoft Copilot Studio, Azure AI Foundry, and Security Copilot are created with agent identities. Agent identities have clear classification, richer metadata, and features designed to address the unique security challenges of AI agents.
- **Agents without agent identities**: Agents created in earlier versions of Copilot Studio and Azure AI Foundry might have been created as classic applications / service principals in your tenant. These applications / service principals might have tag values that denote them as AI agents, but they don't have Microsoft Entra agent identities. They're subject to the same policies, governance, and processes as all other applications / service principals in your tenant.

## Disabling agent identity considerations

Disabling an agent identity in your tenant might have broader consequences than simply stopping new AI agents from being created or used. Before you proceed, evaluate the following considerations:

- Existing agents running in your organization might begin to fail.
- Microsoft product experiences that assume agent identity availability (for example, Copilot Studio agents, Security Copilot scenario agents, Microsoft Entra Conditional Access Optimization Agent) might fail or fall back to standard service principals that lack agent-specific tracking and controls.

## Monitor for agent identity creation and activity

Before disabling an agent identity or agent identity blueprint, you should be aware of what kind of activity is associated with those identities. Agent identity activities are logged under the base identity types they originate from. For example, creating an agent identity shows up as *add service principal* and adding an agent identity blueprint shows up as *add application* in the audit logs.

To identify whether an audit event involves an agent identity, check the `agentType` property on the `initiatedBy` and `targetResources` fields. A value other than `notAgentic` indicates agent involvement.

The `agentSignIn` resource type provides descriptive information that identifies and classifies sign-in events as agentic. With this value you can determine when an agent identity was the subtype of the identity involved in an authentication event.

For more information, see [agent sign-in logs](sign-in-audit-logs-agents)

## Approaches to disabling agent identities

After reviewing agent activity, choose the approach that matches your scenario. Disabling agents in the Microsoft Entra admin center is object-scoped — it targets a specific blueprint or agent identity without affecting others. Conditional Access policies are tenant-wide enforcement that block token issuance for broad categories of identities, without modifying any agent identities or blueprints. The two approaches can be combined. Applying Conditional Access policies in your tenant requires the Microsoft Entra ID P1 license.

Conditional Access policies can block authentication and token issuance of agent identities. Applying the policies prevents existing and new agent identities from authenticating, but it doesn't prevent the creation of agent identities in your tenant.

We recommend running these policies in [report-only mode](/en-us/entra/identity/conditional-access/concept-conditional-access-report-only) to understand their impact before enforcing them.

**Disable agents in the Microsoft Entra admin center when:**

- You want to prevent an agent identity from receiving tokens and authenticating, but you need to keep the agent identity and its metadata in your tenant.

**Use Conditional Access policies when:**

- You want to prevent all agent identities across your tenant from authenticating, including those you didn't create, without modifying individual objects.
    - Policy 1: Block agent identity authentication.
- You want to prevent agents that act on behalf of users from receiving tokens (for example, agents performing delegated actions), without disabling the agent identity objects themselves
    - Policy 2: Block agent's user account authentication.
- You want to prevent human users from signing into agents or triggering agent actions on their behalf, while leaving agent-to-agent and autonomous flows unaffected
    - Policy 3: Block users signing into agents.
- You need to enforce a temporary, reversible, tenant-wide hold on all agent authentication for compliance or incident response purposes, apply all three policies in report-only mode first, then enforce them.

## Disable agent identities and agent identity blueprints in the Microsoft Entra admin center

To disable an agent identity:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Agent ID Administrator](../identity/role-based-access-control/permissions-reference#agent-id-administrator).
2. Browse to **Entra ID** &gt; **Agents** &gt; **Agent identities**.
3. Select the agent identity you want to disable then select **Disable**.

To disable an agent identity blueprint:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Agent ID Administrator](../identity/role-based-access-control/permissions-reference#agent-id-administrator).
2. Browse to **Entra ID** &gt; **Agents** &gt; **Agent blueprints**.
3. Select the agent identity blueprint you want to disable then select **Disable**.

## Create Conditional Access policies to disable agent activities

There are three policy templates you can use to block token issuance or prevent users from signing into agents. These policies can be created in the Microsoft Entra admin center or through the Microsoft Graph API. We recommend applying these policies in report-only mode first to understand their impact before enforcing them.

- Block token issuance to agent identities using Conditional Access &gt; Policy 1: Block agent identity authentication
- Block token issuance to agents' user accounts using Conditional Access &gt; Policy 2: Block agent's user account authentication
- Block users signing into agents using Conditional Access &gt; Policy 3: Block users signing into agents

### Policy 1: Block agent identity authentication

The following steps help create a Conditional Access policy to block issuance of access tokens requested using agent identities.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users, agents or workload identities**.
    1. Under **Include**, select **All agent identities**
    2. Under **Exclude**, select **None**
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Access controls** &gt; **Grant**.
    1. Select **Block**.
    2. Select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to create to enable your policy.

# [Microsoft Graph API](#tab/microsoft-graph-api)
Example JSON for creating the **Block agent identity authentication** policy with the Microsoft Graph APIs:

```http
POST https://graph.microsoft.com/beta/identity/conditionalAccess/policies
Content-type: application/json

{
    "displayName": "Block all agent identities from accessing resources",
    "conditions": {
        "clientApplications": {
            "includeAgentIdServicePrincipals": [
                "All"
            ],
            "excludeAgentIdServicePrincipals": [],
            "agentIdServicePrincipalFilter": null
        },
        "applications": {
            "includeApplications": [
                "All"
            ],
            "excludeApplications": []
        }
    },
    "grantControls": {
        "operator": "AND",
        "builtInControls": [
            "block"
        ]
    },
    "state": "enabledForReportingButNotEnforced"
}
```

---

### Policy 2: Block agent's user account authentication

The following steps help create a Conditional Access policy to block issuance of access tokens requested using agents' user accounts.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users, agents or workload identities**.
    1. Under **Include** &gt; **Select agents** &gt; **agents acting as users** &gt; select **All agents acting as users**
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Access controls** &gt; **Grant**.
    1. Select **Block access**.
    2. Select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to create to enable your policy.

# [Microsoft Graph API](#tab/microsoft-graph-api)
Example JSON for creating the **Block agent's user account authentication** policy with the Microsoft Graph APIs:

```http
POST https://graph.microsoft.com/beta/identity/conditionalAccess/policies
Content-type: application/json

{
    "displayName": "Block all agent users from accessing resources",
    "conditions": {
        "users": {
            "includeUsers": [
                "AllAgentIdUsers"
            ]
        },
        "applications": {
            "includeApplications": [
                "All"
            ]
        }
    },
    "grantControls": {
        "operator": "AND",
        "builtInControls": [
            "block"
        ]
    },
    "state": "enabledForReportingButNotEnforced"
}
```

---

### Policy 3: Block users signing into agents

The following steps help create a Conditional Access policy to block issuance of access tokens to agent resources when requested by human users. This blocks human users from signing into agents and agents performing actions on their behalf.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users, agents or workload identities**.
    1. Under **Include**, select **All users**
    2. Under **Exclude**:
        1. Select **None**
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All agent resources**.
7. Under **Access controls** &gt; **Grant**.
    1. Select **Block**.
    2. Select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to create to enable your policy.

# [Microsoft Graph API](#tab/microsoft-graph-api)
Example JSON for creating the **Block users signing into agents** policy with the Microsoft Graph APIs:

```http
POST https://graph.microsoft.com/beta/identity/conditionalAccess/policies
Content-type: application/json

{
    "displayName": "Block all users from accessing agent resources",
    "conditions": {
        "users": {
            "includeUsers": [
                "All"
            ]
        },
        "applications": {
            "includeApplications": [
                "AllAgentIdResources"
            ],
            "excludeApplications": []
        }
    },
    "grantControls": {
        "operator": "AND",
        "builtInControls": [
            "block"
        ]
    },
    "state": "enabledForReportingButNotEnforced"
}
```

---

## (Optional) Block creation of agent identities

The Conditional Access policies are sufficient to prevent all usage of agent identities in your tenant, including newly created agent identities. Should you wish to prevent creation of agent identities in your tenant, follow the steps in this section.

Agent identities can enter your tenant through various channels. For more information, see [Agent ID creation channels](agent-id-creation-channels). You can block creation of agent identities through the following methods.

- Block creation of agent identities in the Microsoft Entra admin center and other Microsoft Entra experiences.
- Block acquisition of agent identities from Independent Software Vendors (ISVs).
- Block creation of agent identities by Microsoft products and services.

### Block creation of agent identities in Microsoft Entra ID

To prevent users from creating agent identities in the Microsoft Entra admin center and other Microsoft Entra experiences:

1. Remove any eligible or active assignments to the **Agent ID Administrator** or **Agent ID Developer** built-in roles.
2. Remove any *oauth2PermissionGrants* or *appRoleAssignments* granted to service principals that allow creation of agent identities. Refer to the following table for the specific permissions.

| Permission | Type |
| --- | --- |
| `AgentIdentity.Create.All` | Application permission |
| `AgentIdentityBlueprint.Create` | Delegated and application permission |
| `AgentIdentityBlueprint.ReadWrite.All` | Delegated and application permission |
| `AgentIdentityBlueprintPrincipal.Create` | Delegated and application permission |
| `AgentIdentityBlueprintPrincipal.ReadWrite.All` | Delegated and application permission |
| `AgentIdUser.ReadWrite.IdentityParentedBy` | Delegated and application permission |
| `AgentIdUser.ReadWrite.All` | Delegated and application permission |
| `User.ReadWrite.All` | Delegated and application permission. These permissions can also be used to manage human user accounts. Removing this permission causes systems to lose access to manage human users. |

See the [Microsoft Graph permissions reference](/en-us/graph/permissions-reference) for full details of these permissions.

### Block acquisition of agent identities from ISVs

To prevent users from creating agent identities by granting consent to an ISVs agent identity blueprint, use Microsoft Entra [settings to disable user ability to consent to applications](/en-us/entra/identity/enterprise-apps/configure-user-consent). There's no method to prevent users from granting consent to agent identities without also affecting ability to grant consent to applications. Disabling user consent is broad and also blocks onboarding of legitimate non-agent SaaS apps that depend on user consent flows and granting permissions to existing non-agent apps.

If this impact is too high, keep user consent enabled and instead rely on the Conditional Access block policies to prevent tokens for unapproved ISV agent identities.

### Block creation of agent identities by Microsoft products and services

To block Microsoft products and services from creating agent identities in your tenant, you must use the settings available in each Microsoft product:

#### Security Copilot

To disable agent identity creation by Security Copilot, shut off Security Copilot by deleting all Security Compute Unit (SCU) capacity. This blocks both agents and Security Copilot itself. For more information, see [Security Copilot documentation](/en-us/copilot/security/). Users with the following roles can turn Security Copilot back on by creating SCU capacity:

- Billing Administrator
- Microsoft Entra Compliance Administrator
- Global Administrator
- Intune Administrator
- Security Administrator
- Purview Compliance Administrator
- Purview Data Governance Administrator
- Purview Organization Management.

To enable use of Security Copilot but block agent creation, you can use the following methods depending on the type of agents you want to block:

- To block Microsoft agents (For example, Microsoft Entra conditional access Agent), request users with relevant roles not to enable each agent. Roles that can enable agent currently include:
    - Security Administrator
    - Identity Governance Administrator
    - Lifecycle Workflows Administrator
    - Security Copilot Contributor
- To block third-party agents (agents not owned by Microsoft), remove all users from the Owner / Contributor role in any Security Copilot workspaces.

#### Copilot Studio

To disable use of Copilot Studio and creation of agent identities, you can restrict agent creation via licensing, RBAC, or data policies.

- Licensing:
    - Prevent users from signing up for free trials of Copilot Studio.
    - Don't assign Copilot Studio licenses to users.
- RBAC:
    - Prevent users from signing up for free trials, which prevents creation of trial environments.
    - Creation of Copilot Studio environments requires the Power Platform Administrator role. Remove access to environments and ability to create new environments.
- Data policies:
    - Apply policies that prevent agents from being published, so nobody can chat with an agent. This does **not** block agent creation.

See Copilot Studio documentation for details, which [recommends using data policies](/en-us/microsoft-copilot-studio/security-faq#can-i-disable-microsoft-copilot-studio-agent-creation-in-my-organization).

#### Azure AI Foundry

To disable creation of agent identities, prevent users from creating projects and agents in Azure AI Foundry, you can turn off user ability to create Azure subscriptions via free trials or pay-as-you-go. This enforces the following settings:

- Only Billing Administrator or Account Administrator roles can create subscriptions.
- Within a subscription, only the Azure AI Account Owner role can create Foundry projects.
- Within a project, users must have the Azure AI User role to create agents.

By not assigning these roles to users, users can't create agents or agent identities.

For more information, see [Azure AI Foundry documentation here](/en-us/azure/ai-foundry/concepts/rbac-azure-ai-foundry).

#### Microsoft Teams

To disable creation of agent identities via Microsoft Teams, use settings in the Teams admin center:

- Prevent users from adding apps/agents to Teams.
- Pivot by Microsoft apps, third-party apps, or custom apps.
- Enable specific apps/agents for specific users/groups as needed.

For more information, see [Teams admin center documentation](/en-us/microsoftteams/manage-apps).