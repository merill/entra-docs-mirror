---
layout: Conceptual
title: Microsoft Entra Agents | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-agents
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Learn about Microsoft Entra agents, AI-powered automation tools that enhance identity and access management operations.
keywords: 
ms.date: 2026-01-21T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: overview
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: b043a3b2-7926-963b-4613-af2c33a0de03
document_version_independent_id: b043a3b2-7926-963b-4613-af2c33a0de03
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-agents.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-agents
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-agents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 706a474b-05ad-77a4-44c9-1f417d4fb735
---

# Microsoft Entra Agents | Microsoft Learn

Microsoft Entra agents can automate many identity and access management operations in your organization to help reduce manual workloads. These agents work seamlessly with [Microsoft Security Copilot](/en-us/copilot/security/microsoft-security-copilot) to automate repetitive tasks, provide suggestions, and help administrators focus on higher-value strategic work.

Microsoft Entra agents analyze your identity environment, apply best practices, and take automated actions to improve your identity and access security posture and operational efficiency. They integrate directly with Microsoft Entra services, using your organization's identity data and configuration to provide contextual, actionable insights.

## What are Microsoft Entra agents?

Microsoft Entra agents are AI-powered tools that operate in your organization's identity environment to automate and optimize identity and access management tasks. The agents are grounded in the concepts and tasks for a specific product area, like Conditional Access. These agents can:

- **Automate routine tasks** - Handle time-consuming, repetitive identity and access management operations
- **Provide suggestions** - Analyze your environment and suggest improvements based on Microsoft best practices and Zero Trust principles
- **Operate autonomously** - Run on schedules or triggers to continuously monitor and optimize your identity infrastructure
- **Integrate seamlessly** - Work within your organization's existing Microsoft Entra workflows
- **Learn and adapt** - Improve suggestions over time, based on your environment and feedback

Each agent works a little differently, but at their core, they first analyze your current environment within the boundaries of the agent's capabilities. If the agent identifies a gap, opportunity, or potential issue, it can take action on your behalf. Each agent provides the context, reasoning, and activity history for how it came up with the suggestion.

Administrators can configure the agent to run automatically or trigger the agent to run manually.

Because each of the agents perform a specific set of tasks, they need a specific set of configurations to operate within the boundaries of that task. The administrator also needs certain Microsoft Entra roles to set up and manage the agent.

- **Agent identity**: A unique agent identity is created when the agent is turned on. Learn more about [agent identities](/en-us/entra/agent-id/what-are-agent-identities).
- **Roles**: Specific Microsoft Entra built-in roles are needed to turn on, view, and interact with the agent. Not all roles can perform the same tasks with an agent.
- **Permissions**: The agent identity is granted specific read and write permissions needed to perform its tasks. These permissions can't be changed or removed.
- **Role-based access**: The administrator needs specific roles to set up, manage, and use the agent.

## Available Microsoft Entra agents

The following agents are currently available for Microsoft Entra. Due to the fast pace at which these agents are released and updated, each agent might have features at various stages of availability. Preview features are added frequently.

### Conditional Access Optimization Agent

The [Conditional Access Optimization Agent](conditional-access-agent-optimization) ensures comprehensive user protection by analyzing your Conditional Access policies and recommending improvements. The agent evaluates your current policy configuration against Microsoft best practices and Zero Trust principles.

| Attribute | Description |
| --- | --- |
| Identity | A unique [agent identity](../agent-id/identity-professional/authorization-agent-id) for authorization is created when the agent is turned on.The agent uses this identity to scan your tenant's Conditional Access policies and configurations for gaps, overlap, and misconfigurations. |
| Licenses | [Microsoft Entra ID P1](../fundamentals/licensing) |
| Permissions | AuditLog.Read.AllCustomSecAttributeAssignment.Read.AllDeviceManagementApps.Read.AllDeviceManagementConfiguration.Read.AllGroupMember.Read.AllLicenseAssignment.Read.AllNetworkAccess.Read.AllPolicy.Create.ConditionalAccessROPolicy.Read.AllRoleManagement.Read.DirectoryUser.Read.All |
| Plugins | [Microsoft Entra](/en-us/entra/fundamentals/copilot-security-entra) |
| Products | [Microsoft Entra Conditional Access](/en-us/entra/identity/conditional-access/) |
| Role-based access | [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator) to configure the agent[Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) to use the agent |
| Trigger | Runs every 24 hours or triggered manually |

### Identity Risk Management Agent (Preview)

The [Identity Risk Management Agent](../id-protection/identity-risk-management-agent-get-started) in Microsoft Entra ID Protection helps administrators investigate potential risks, learn about potential effects, and take decisive action to protect their organization's critical assets.

| Attribute | Description |
| --- | --- |
| Identity | Uses [Microsoft Entra Agent ID](../agent-id/identity-professional/authorization-agent-id) for authorization |
| Licenses | [Microsoft Entra Agent ID](https://www.microsoft.com/security/business/identity-access/microsoft-entra-agent-id) |
| Permissions | Application.Read.AllPolicy.Read.AllGroup.ReadWrite.AllGroupMember.Read.AllUser.Read.AllPolicy.ReadWrite.ConditionalAccessCustomSecAttributeAssignment.Read.AllIdentityRiskyUser.Read.AllAuditLog.Read.All |
| Plugins | [Microsoft Entra](/en-us/entra/fundamentals/copilot-security-entra) |
| Products | [Security Copilot](/en-us/copilot/security/microsoft-security-copilot)[Microsoft Entra ID Protection](../id-protection/overview-identity-protection) |
| Role-based access | [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator) |
| Trigger | Runs every 24 hours, triggered manually, or continuous monitoring |

## Discover agents in the Security Store

[Security Store](/en-us/security/store/what-is-security-store) is embedded in the Microsoft Entra admin center, providing a centralized place to discover, purchase, and deploy Microsoft and partner-built agents and solutions. You can browse available agents and solutions, view details and requirements, and start the deployment process directly from the Entra portal.

For more information, see [Discover and deploy agents and solutions in Microsoft Entra](security-store-in-entra).

## Getting started with Microsoft Entra agents

### Prerequisites

- You must have available [security compute units (SCU)](/en-us/copilot/security/manage-usage).
    - In order to purchase security compute units, you need to have an Azure subscription. [Create your free Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Review [Privacy and data security in Microsoft Security Copilot](/en-us/copilot/security/privacy-data-security)

### Setup process

1. Enable Security Copilot using the [Security Copilot setup guide](/en-us/copilot/security/get-started-security-copilot).
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) using the least privileged role required for the agent you want to configure.
3. Browse to **Agents** and select **View details** for the agent you want to configure.

## Agents in the Microsoft ecosystem

While this article focuses on Microsoft Entra agents, similar agents are available across other Microsoft security products. For more information, see [Microsoft Intune](/en-us/intune/intune-service/copilot/security-copilot-agents-intune), [Microsoft Defender](/en-us/defender-xdr/security-copilot-agents-defender), and [Microsoft Purview](/en-us/purview/copilot-in-purview-agents).