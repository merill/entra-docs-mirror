---
layout: Conceptual
title: Target agent identities in Conditional Access policies - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/howto-target-agent-identities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how to select and target agent identities in Microsoft Entra Conditional Access policies using the object picker, blueprints, and custom security attributes.
ms.topic: how-to
ms.date: 2026-06-02T00:00:00.0000000Z
ms.reviewer: kvenkit
ms.custom: msecd-doc-authoring-1012
ai-usage: ai-assisted
locale: en-us
document_id: 6f382dd5-9e58-0f16-1eaa-916443774baf
document_version_independent_id: 6f382dd5-9e58-0f16-1eaa-916443774baf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/howto-target-agent-identities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/howto-target-agent-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/howto-target-agent-identities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 5436b733-663d-2651-1584-817a140eb67c
---

# Target agent identities in Conditional Access policies - Microsoft Entra ID | Microsoft Learn

Conditional Access policies for agent identities let you control how AI agents access corporate resources. As your organization deploys more agents, you need policies that target the right agents, evaluate the right signals, and enforce the right controls. To learn more about how Conditional Access policies for agents work for different scenarios, see [Conditional Access policies for agents](agent-id).

This article walks through each section of the Conditional Access policy builder for agents:

- Selecting which agents the policy applies to
- Choosing target resources
- Configuring conditions
- Setting access controls.

Each section builds on the previous one to form a complete policy.

## Prerequisites

- One of the following license plans:
    - **Microsoft 365 E7**, which includes Agent 365 and Microsoft Entra Suite, to provide governance of user and agent identities.
    - **Microsoft Agent 365** license paired with at least Microsoft Entra P1 or Microsoft 365 E3.
- [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator) to create and manage Conditional Access policies
- At least one agent identity registered in your tenant

## Create a Conditional Access policy for agent identities

Policies that target agent identities introduce unique assignment options, conditions, and control limitations that differ from user-targeted policies.

- [Configure policy for autonomous agent access](policy-autonomous-agents)
- [Configure policy for on-behalf-of agent access](policy-on-behalf-of-agents)

To create a new Conditional Access policy for agent identities:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.

## Assignments

The first agent-specific configuration is selecting which agents the policy applies to.

1. Under **Assignments**, select **Users, agents (Preview) or workload identities**.
2. Under **What does this policy apply to**, select **Agents**. [![Screenshot of the Conditional Access policy builder showing the agent selection options.](media/howto-target-agent-identities/agent-policy-select-agents.png)](media/howto-target-agent-identities/agent-policy-select-agents.png#lightbox)
3. Select the agent identity option for your scenario:
    - **All agent identities**: Applies the policy to every agent identity in your tenant.
    - **All agent users (Preview)**: Applies the policy to every agent's user account in your tenant.
    - **Select agent identities**: Choose individual agents or select agents based on custom security attributes.
    - **Select agent users (Preview)**: Choose individual agents' user accounts or select agents' user accounts based on custom security attributes.

### Considerations for selecting agent assignments

Keep in mind the following important details when selecting agent assignments:

- Policies targeting all users don't include agent's user accounts.
- The **agent users** option targets agents' user accounts. This option is currently in Preview.
- Agent-based policies apply when agents access resources using their own identity, not on behalf of a user.
- Targeting a blueprint automatically covers all agent identities derived from it, including ones added in the future. For more information about targeting agent identity blueprints, see [Conditional Access for agent identities: Agent identity blueprints](agent-id#conditional-access-policies-and-agent-identity-blueprints).

## Target resources

Target resources define which resources the policy protects when agents attempt to access them. Selecting target resources for agent policies follows the same principles as targeting resources for user policies. The resource must have an enterprise application (service principal) in your Microsoft Entra ID tenant. This requirement applies regardless of the data access pattern or resource type, including Microsoft Graph, MCP servers, Open API tools, and custom tools you build. For more information, see [Targeting resources with Conditional Access](concept-conditional-access-cloud-apps).

For custom MCP servers, Open API-based tools, or other custom tool types, register the tool as an application in Microsoft Entra ID and expose its permissions. For more information, see [How to configure an application to expose a web API](../../identity-platform/quickstart-configure-app-expose-web-apis).

1. Under **Target resources**, select the resources you want to protect.
2. Under **Include**, select one of the following:
    - **All agent resources**: Applies the policy when agents access any agent-specific resource.
    - **All resources (formerly 'All cloud apps')**: Applies the policy when agents access any resource protected by Microsoft Entra ID.
    - **Select resources**: Choose specific resources the agent needs to access.

## Network

The network settings control agent access based on where they run, such as cloud-hosted virtual machines or endpoints with a Global Secure Access client. This option is only available when the policy targets **All agent users (Preview)** and **Select agent users (Preview)**.

**Compliant network** works for agents' user accounts on endpoints because the hosted environment can have a [Global Secure Access](/en-us/entra/global-secure-access/overview-what-is-global-secure-access) client installed. The Global Secure Access client provides the network location signal that Conditional Access evaluates. Agents running in cloud infrastructure without a Global Secure Access client can't provide this signal.

1. Under **Network**, set **Configure** to **Yes** to enable the network location options.
2. Under **Include**, select one of the following:
    - **Any location**: The policy applies regardless of where the agent runs.
    - **All Compliant Network locations**: The policy applies only to agents connecting from compliant network locations. [![Screenshot of the Conditional Access policy builder showing the network options for agent users.](media/howto-target-agent-identities/agent-policy-agent-users-network.png)](media/howto-target-agent-identities/agent-policy-agent-users-network.png#lightbox)

## Conditions

Conditions are the signals that Conditional Access evaluates when deciding whether to apply a policy. The available conditions depend on whether the policy targets agent identities, agents' user accounts, or users in OBO flows.

Not all agents run the same way. Some agents run directly from the cloud similar to SaaS applications (for example, Copilot Studio hosted agents) with no associated device. Others run on managed endpoints. This distinction determines which Conditional Access controls can be enforced. For more information about agents, see [What is Windows 365 for Agents?](/en-us/windows-365/agents/introduction-windows-365-for-agents).

Device compliance and compliant network controls depend on signals that only an endpoint can provide. A Cloud PC enrolled in Microsoft Intune can prove its compliance. An agent running directly from the cloud like a managed service has no device to check, so a policy requiring device compliance would block it with no path to remediation.

Admins with access to [ID Protection](../../id-protection/overview-identity-protection) can evaluate agent risk as part of a Conditional Access policy. Agent risk shows the likelihood that an agent is compromised. For more information, see [ID Protection for agents](../../id-protection/concept-risky-agents).

### Conditions for agent identities

When an agent identity is targeted in a policy (either all agent identities or individually selected agent identities), the only condition available is **Agent risk (Preview)**. For more information, see [ID Protection for agents](../../id-protection/concept-risky-agents).

1. Under **Conditions** set **Configure** to **Yes**
2. Select the agent risk levels (high, medium, low) needed for the policy to be enforced.

### Conditions for agents' user accounts

When you target agents' user accounts in Conditional Access, the following conditions are available. These conditions don't apply to agent identities or agent identity blueprints. For the full condition reference, see [Conditional Access: Conditions](concept-conditional-access-conditions).

- **Agent risk (Preview)**: Evaluate whether the agent is likely compromised and enforce risk-based access decisions.
- **Agent execution environments (Preview)**: Scope policies to agent's user account sessions initiated from endpoints.
- **Device platforms**: Restrict agents to specific operating systems. Only applies to agents running on endpoints.
- **Filter for devices**: Restrict agents to specific admin-approved devices. Only applies to agents running on endpoints.
- **Network**: Enforce compliant network locations. Only applies to agents on endpoints with a Global Secure Access client.

Keep in mind the following important details when selecting conditions for agents' user accounts:

- The 'Device platforms' and 'Filter for devices' conditions require device information and only apply to agents running on endpoints, including local devices and cloud-hosted virtual machines.
- Because the 'agent user' options are in preview, these conditions should also be considered as preview capabilities.
- The 'Network' condition is only available for agents running on endpoints with a Global Secure Access client.

#### Agent execution environments

Configure restrictions based on where the agent user is executed. The **Agent execution environments (Preview)** condition provides a way for administrators to scope a policy to only apply when the agent's user account session is initiated from an endpoint. When a policy uses this condition, agents that are not running on a device are excluded from evaluation, preventing unintended blocking.

1. Under **Conditions**, set **Configure** to **Yes** to enable the agent execution environments.
2. Under **Include**select the execution environments that apply to your agents:
    - **All agent user sessions**
    - **Agent user sessions initiated from endpoints**[![Screenshot of the Conditional Access policy builder showing the agent execution environments options.](media/howto-target-agent-identities/agent-policy-agent-execution-environment.png)](media/howto-target-agent-identities/agent-policy-agent-execution-environment-expanded.png#lightbox)

#### Device platforms

Apply the policy to selected device platforms.

1. Under **Device platforms**, set **Configure** to **Yes** to enable device platform selection.
2. Under **Include**select the device platforms that apply to your agents:
    - **Any device**
    - **Select device platforms**: Android, iOS, Windows Phone, Windows, macOS, Linux

#### Filter for devices

Configure a filter to apply the policy to specific devices.

1. Under **Filter for devices**, set **Configure** to **Yes** to enable device filtering.
2. Select whether to **Include filtered devices in policy** or **Exclude filtered devices from policy**.
3. Use the rule builder or rule syntax text box to create or edit the filter rule.

## Access controls

Access controls determine what happens when conditions are met. For more information, see [How to Configure Grant Controls](concept-conditional-access-grant).

### Controls for agent identities

- **Block access**: The only available option for agent identities, because there's no interactive remediation possible.

### Controls for agent users

- **Block access**: Deny the agent user account access to resources.
- **Grant access**with:
    - **Require device to be marked as compliant**: Requires agents to run on Intune-managed compliant devices, such as Windows 365 Cloud PCs for Agents. For more information, see[What is Windows 365 for Agents?](/en-us/windows-365/agents/introduction-windows-365-for-agents). [![Screenshot of the Conditional Access policy builder showing the grant option for device compliance.](media/howto-target-agent-identities/agent-policy-grant-device-compliant.png)](media/howto-target-agent-identities/agent-policy-grant-device-compliant.png#lightbox)

Important

Agents running directly in cloud infrastructure may not provide device compliance signals. To avoid unintended blocking, apply device compliance policies only to agents running on endpoints using the **Agent execution environments** condition.