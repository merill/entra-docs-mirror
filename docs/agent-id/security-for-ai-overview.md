---
layout: Conceptual
title: Microsoft Entra security for AI overview - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/security-for-ai-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how Microsoft Entra provides identity-based security controls for AI agents, applications, and services through authentication, governance, and Zero Trust policy enforcement.
ms.date: 2026-05-08T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: e4b1d11e-1ce9-4e33-6130-a0359eda1e02
document_version_independent_id: e4b1d11e-1ce9-4e33-6130-a0359eda1e02
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/security-for-ai-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/security-for-ai-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/security-for-ai-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c469d37a-64a0-7ae3-fe86-d54fd8dc833e
---

# Microsoft Entra security for AI overview - Microsoft Entra Agent ID | Microsoft Learn

AI agents—autonomous software systems that perceive their environment, make decisions, and take actions—expand organizational capabilities but introduce security challenges that differ from traditional application security. These capabilities require identity-based security controls that authenticate AI workloads, enforce access policies, and provide governance over nonhuman identities.

Microsoft Entra provides the identity control plane for securing AI systems. It extends identity capabilities to AI agents, applications, and services so that organizations can apply consistent authentication, authorization, and governance controls across human and nonhuman identities.

This article explains why AI systems need identity-based security, introduces the key Microsoft Entra capabilities that address these challenges, and links to detailed documentation for each area.

## Why AI systems need identity-based security

Organizations are deploying AI agents for increasingly diverse tasks, and each deployment model presents distinct security challenges:

### Interactive agents

Interactive agents perform specific tasks on demand on behalf of a signed-in user, often through a chat interface. Tasks include analyzing customer data for sales recommendations or answering support questions with escalation to human representatives. These agents are granted Microsoft Entra delegated permissions that allow them to act on behalf of users using the on-behalf-of (OBO) authentication flow. Common scenarios include customer support assistants, research helpers, and real-time collaboration agents.

### Autonomous agents

Autonomous agents operate independently using their own identity, not a human user's identity. These agents run in the background, making decisions and taking actions without human intervention, such as monitoring network logs for security operations, managing infrastructure deployments with autoscaling, or processing scheduled maintenance tasks. Autonomous agents authenticate directly with the Microsoft Entra ID platform using their agent identity and the client credentials flow.

### Agent's user account

An agent's user account is an optional account that pairs 1:1 with an agent identity. It functions with human user characteristics, including persistent identities and access to organizational resources such as mailboxes, calendars, Teams channels, and documents. Use an agent's user account only when the agent must access systems that require a user object. An agent's user account doesn't replace the agent identity — both must exist. For more information, see [Agent's user accounts](agent-users).

### Security challenges

Unlike applications that execute predetermined logic, AI agents make dynamic decisions and adapt behavior based on training data, input, and environment conditions. This adaptive behavior expands the organizational attack surface:

- **External accessibility**: Many AI agents interact with external users, third-party systems, or the public internet. This exposure creates potential pathways for adversaries to compromise agents and access organizational systems.
- **Permission escalation risk**: Agents are often provisioned with broad permissions to ensure capability. An agent analyzing financial data might receive access to all financial records, expense reports, and vendor contracts, which is broader than necessary for the specific task.
- **Autonomous decision-making**: Compromised agents that make autonomous decisions can take harmful actions. A supply chain agent with purchasing authority could place unauthorized orders. An infrastructure management agent could delete critical systems.
- **Prompt injection attacks**: AI agents are vulnerable to attacks that don't affect traditional applications. Prompt injection attacks manipulate agent behavior by inserting malicious instructions into data processed by the agent.
- **Agent-to-agent propagation**: Agents that interact with other agents can propagate compromise. If an orchestration agent is compromised, it can potentially target other agents to perform malicious actions.

Organizations must also demonstrate that AI systems operate within governance frameworks, comply with privacy regulations, and maintain audit trails documenting agent actions and decisions.

### Agent sprawl

Agent proliferation creates a governance challenge termed "agent sprawl", which is the uncontrolled expansion of agents across an organization without adequate visibility, management, or lifecycle controls. Agent sprawl emerges when business units create agents without formal IT oversight (shadow AI), when agents created for temporary purposes remain in production indefinitely, and when agent permissions exceed actual requirements and are never reviewed.

Uncontrolled agent sprawl leads to increased security risk from over-privileged agents with unclear ownership, compliance challenges when auditors expect governance over AI systems, and incident response difficulties when organizations can't quickly identify compromised agents.

### Agent security scenarios

Agent security challenges manifest differently depending on the agent's purpose and deployment context:

| Scenario | Description | Security challenge | Risk |
| --- | --- | --- | --- |
| **User-initiated agent** | Agents act on behalf of users, inheriting user capabilities and access rights. | Prevent agents from misusing inherited permissions; maintain user control and enable access revocation. | Compromised agents might perform unauthorized actions as the user, such as accessing files, sending communications, or manipulating data. |
| **Autonomous agent** | Agents operate with their own identities and permissions, independent of users. | Grant only necessary permissions for intended tasks; prevent agents from exceeding authorized scope. | Compromised agents might operate without constraint, placing unauthorized orders, modifying data, or accessing sensitive information. |
| **Agent's user account** | An agent's user account enables the agent to function as a human user with persistent identity, mailbox, and access to collaborative systems. | Maintain appropriate permission scope; prevent compromised agents from using team access to spread malware or manipulate decisions. | Compromised agents might access documents, participate in meetings under false pretenses, or send communications as trusted team members. |
| **Agent-to-agent** | Agents interact with other agents, such as an orchestration agent that delegates tasks to specialized agents. | Establish authenticated agent communication; ensure agents interact only with legitimate agents; maintain audit trails of interactions. | Unsecured communication allows adversaries to inject malicious agents or intercept or manipulate agent interactions. |

## Secure identities for AI agents

AI agents require purpose-built identity constructs that differ from traditional application identities. [Microsoft Entra Agent ID](what-is-microsoft-entra-agent-id) provides an identity and security framework designed for AI agents.

![Diagram showing illustration of security for AI landscape with Microsoft Entra Agent ID.](media/security-for-ai-overview/microsoft-entra-agent-identities-diagram.png)

Microsoft Entra Agent ID enables organizations to:

- **Register and manage agents**: Create and manage agent identity blueprints as templates and agent identities as individual instances with parent-child relationships, enabling centralized metadata management and automatic organization into security collections.
- **Assign secure, scalable identities**: The [Microsoft Entra Agent identity platform](identity-platform/what-is-agent-id-platform) enables you to assign identities to agents, autodiscover them across your organization, and manage all agent metadata in one place including capabilities, tasks, and protocols. It provides agent-to-agent discovery and authorization based on standard protocols such as Model Context Protocol (MCP) and agent-to-agent (A2A).
- **Log and monitor agent activity**: All authentication and actions performed by agents are logged in Microsoft Entra ID and viewable through the Microsoft Entra admin center for compliance and audit purposes.

For more information about agent identities as identity constructs, including how they differ from application and user identities, see [What are agent identities?](identity-platform/what-are-agent-identities).

## Control AI access with Zero Trust

Microsoft Entra applies Zero Trust identity controls to AI identities through Conditional Access and Identity Protection.

### Conditional Access for agents

Conditional Access enables organizations to define and enforce adaptive policies that evaluate agent context and risk before granting access to resources:

- Enforce adaptive access control policies for all agent patterns across assistive, autonomous, and agent user account types.
- Use real-time signals such as agent identity risk to control agent access to resources, with Microsoft Managed Policies providing a secure baseline by blocking high-risk agents.
- Deploy Conditional Access policies at scale using custom security attributes, while still supporting fine-grained controls for individual agents.

For more information, see [Conditional Access for agents](/en-us/entra/identity/conditional-access/agent-id).

### Identity Protection for agents

Microsoft Entra ID Protection detects and blocks threats by flagging anomalous activities involving agents:

- Detect agent identity risk derived from user risk and based on agents' own actions, including unusual or unauthorized activities.
- Provide risk signals to Conditional Access to enforce risk-based policies and session management controls.
- Provide risk signals to inform agent discoverability and access, with automatic remediation of compromised agents using preconfigured policies.

For more information, see [Identity Protection for agents](/en-us/entra/id-protection/concept-risky-agents).

## Govern AI identities and permissions

As organizations deploy more AI agents, identity governance becomes critical to prevent agent sprawl and maintain compliance. Microsoft Entra ID Governance extends lifecycle management, access reviews, and entitlement management to agent identities:

- Govern agent identities at scale, from deployment to expiration.
- Ensure sponsors and owners are assigned and maintained for each agent identity, preventing orphaned agent identities.
- Enforce that agent access to resources is intentional, auditable, and time-bound through access packages.
- Apply Conditional Access rules, permissions, and governance controls at the [blueprint level](identity-platform/agent-blueprint) so all current and future agent instances inherit them automatically, with the ability to disable an entire class of agents in a single operation.
- Maintain a complete inventory of all agent identities through centralized discovery and management in the Microsoft Entra admin center and [Microsoft Graph](/en-us/graph/api/resources/agentidentity), preventing shadow AI and enabling organizations to track agents across the full lifecycle — from registration and credential management through deactivation and decommissioning.

For more information, see [Identity governance for agents](/en-us/entra/id-governance/agent-id-governance-overview).

For a general overview of Microsoft Entra ID Governance, see [What is Microsoft Entra ID Governance?](/en-us/entra/id-governance/identity-governance-overview).

## Secure AI services and automation

Many AI workloads run as applications, services, or automation pipelines rather than as interactive agents. These workloads need secure, credential-free authentication to access enterprise resources.

Microsoft Entra workload identities provide identity and access management for software workloads. Organizations can use managed identities and federated credentials to authenticate AI services without managing secrets.

For more information, see [What are workload identities?](/en-us/entra/workload-id/workload-identities-overview).

## Secure generative AI architectures

Enterprise generative AI architectures require identity controls at every layer, from the client application to the AI model and the data sources it accesses. Microsoft Entra enforces authentication, authorization, and governance controls across these architectural components.

Network-level controls through Global Secure Access enforce consistent network security policies across users and agents:

- Log agent network activity to remote tools for audit and threat detection, and apply web categorization to control access to APIs and MCP servers.
- Restrict file uploads and downloads using file-type policies to minimize risk, and automatically block and alert on malicious destinations using threat intelligence-based filtering.
- Detect and block prompt injection attacks that attempt to manipulate agent behavior through malicious instructions.

For more information, see [Secure Web and AI Gateway for agents](/en-us/entra/global-secure-access/concept-secure-web-ai-gateway-agents).