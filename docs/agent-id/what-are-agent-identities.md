---
layout: Conceptual
title: What are agent identities? - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/what-are-agent-identities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn about agent identities, specialized identity constructs that enable secure authentication and authorization for AI agents in enterprise environments.
ms.topic: concept-article
ms.date: 2025-11-06T00:00:00.0000000Z
ms.reviewer: dastrock
locale: en-us
document_id: 7ebfb7b1-8e68-c7ae-fb71-03c3743c18a8
document_version_independent_id: 7ebfb7b1-8e68-c7ae-fb71-03c3743c18a8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/what-are-agent-identities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/what-are-agent-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/what-are-agent-identities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
platformId: 19168ee1-87e8-6ae7-1ca3-19b1f3695875
---

# What are agent identities? - Microsoft Entra Agent ID | Microsoft Learn

Agent identities are identity accounts within Microsoft Entra ID that provide unique identification and authentication capabilities for AI agents. As organizations increasingly deploy autonomous AI systems, identity models designed for human users and applications prove insufficient. Agent identities address this gap by providing a specialized identity construct built specifically for the unique requirements of AI agents operating at enterprise scale.

## What is an agent

In its most fundamental form, an agent is an application that attempts to achieve a goal by understanding its environment / context, making decisions and acting on them autonomously using available tools. Agents can act with or without human intervention when provided with proper goals or objectives.

Key components of an agent include:

- **Model**: Model based agents have language models that serve as the centralized decision maker for agent processes. Models can be general purpose, multimodal, or fine-tuned based on specific agent architecture needs.
- **Orchestration Layer**: The cyclical process that governs how the agent takes in information, performs internal reasoning, and uses that reasoning to inform its next action. This loop continues until the agent reaches its goal or a stopping point. Complexity varies from simple decision rules to chained logic.
- **Memory**: Memory in agents provides agents with more dynamic and up-to-date information, ensuring responses are accurate and relevant. This memory allows developers to provide more data in its original format to an agent, without requiring data transformations, model retraining, or fine-tuning. It differs from typical large language models (LLMs) that remain static, retaining only the knowledge they were initially trained on.
- **Tools**: Tools enable agents to interact with their environment and extend their capabilities. Tools can include web search, database access, APIs, file systems, or integrations with other software. Each tool requires careful consideration of security, permissions, and error handling. By using tools, agents can perform complex tasks, access information, and control external systems, making them more effective and adaptable.

Agent workflows are in whole or part planned and driven autonomously and independently of a human user. There are many types of agent workflows, from the ones initiated directly by a user, to the ones that operate autonomously. Subcomponents, skills, tools, or APIs used in those workflows might or might not themselves be agents.

## Why agent identities exist

The emergence of AI agents as autonomous enterprise systems introduces security and operational challenges that existing identity models can't adequately address. Agent identities help to address certain security challenges posed by AI agents, such as:

- The need to distinguish operations performed by AI agents from operations performed by workforce, customer, or workload identities.
- Enabling AI agents to gain right-sized access across systems.
- Preventing AI agents from gaining access to the most critical security roles and systems.
- Scaling identity management to large numbers of AI agents that might be quickly created and destroyed.

## Agent identities versus application identities

Application identities, typically represented as service principals in Microsoft Entra ID, were designed for services built and maintained by organizations. These identities carry the expectation of long-term stability, known ownership, and managed lifecycle.

Agents are often created dynamically through automation, user actions in tools like Copilot Studio, or API orchestration. An agent might exist for minutes during a specific task, or might be created and destroyed thousands of times per day as part of an automated workflow. Managing this level of dynamism with existing application identities creates operational complexity and security challenges.

Agent identities embrace this dynamic nature while providing appropriate security controls. Organizations can create agent identities in bulk, apply consistent policies to all agents, and retire agents without leaving orphaned credentials or permission assignments behind. The identity model is designed for scale and ephemerality rather than permanence.

## Agent identities versus human user identities

Human user identities are tied to authentication mechanisms humans use daily, such as passwords, multifactor authentication, and passkeys. Human users have data associated with them like mailboxes, teams, and organizational hierarchy.

Agent identities represent software systems, not human beings. They don't use human authentication mechanisms. However, certain scenarios require agents to appear and operate as if they're human users. For these scenarios, agent identities can be paired with agents' user accounts - special Microsoft Entra user accounts that maintain a one-to-one relationship with their paired agent identity. This distinction allows organizations to provide agents with a user identity when necessary for system compatibility, while still maintaining clear separation and appropriate security policies for AI-driven operations.

## What agent identities enable

Agent identities provide the foundation for secure, scalable AI agent deployment by enabling several key capabilities. Like other accounts, agent identities are primarily a means to access apps, web services, and other systems in your organization. An AI agent can use agent identities to:

- **Access web services**. Agents can request access tokens from Microsoft Entra, and use those tokens to access web services. Services can include Microsoft services such as Microsoft Graph, services built by your organization, and services purchased from third-party vendors.
- **Autonomous access**. Agents can act autonomously, using access rights given directly to the agent identity. Access rights can include Microsoft Graph permissions, Azure RBAC roles, Microsoft Entra directory roles, Microsoft Entra app roles, and more.
- **Delegated access**. Agents can act on behalf of human users, using access rights given to the user. The user has control over which rights are delegated to the agent identity.
- **Authenticate incoming messages**: Agents can accept requests from other clients, users, and agents. Those requests can be secured using access tokens issued by Microsoft Entra ID, allowing the agent to reliably identify the caller and make authorization decisions.

## Agent identities in practice

Several Microsoft products already use agent identities for authenticating AI agents. Two examples include:

- [**Entra conditional access optimization agent**](../identity/conditional-access/agent-optimization): When this agent is enabled in your tenant, it's given an agent identity. The Microsoft Entra conditional access optimization agent then uses its agent identity to query Microsoft Entra systems and inspect the tenant's configuration. All queries made by the agent are recorded as having been performed by an AI agent. The agent's activity is subject to any security policies enforced for agent identities. You can view the agent's identity in the Microsoft Entra admin center in the **Agent identities** tab.
- [**Agents built in Copilot Studio**](/en-us/copilot/security/agents-overview): In organizations that use Copilot Studio, users can quickly create AI agents using Copilot Studio's low-code tools. Each time an AI agent is created, the agent gets an agent identity in the Microsoft Entra tenant. The user who created the agent is recorded as its sponsor. The agent can then use its agent identity to send/receive chat messages to users, and connect to various systems like SharePoint or Dataverse. Any authentication performed by these agents is logged in Microsoft Entra ID as AI agents and viewable through the Microsoft Entra admin center.

## How to get started

Microsoft Entra Agent ID is a product within Microsoft Entra that provides the platform for creating and managing agent identities and agent identity blueprints. Agent ID is available for all Microsoft Entra customers.

[Microsoft Agent 365](/en-us/microsoft-agent-365/overview) enables agents to operate across Microsoft 365 services and enterprise workflows, which requires a **Microsoft Agent 365** license for each user. For pricing details, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing).

Extending Microsoft Entra security features to agents requires Microsoft Agent 365. Agent 365 is included with Microsoft 365 E7 and is available as an add-on to Microsoft E5/A5/Business Premium (or Microsoft Defender Suite + Microsoft Purview Suite). See our latest [Agent 365 product terms for more details](https://www.microsoft.com/licensing/terms/productoffering/Agent365/EAEAS#clause-2755-h3-1).