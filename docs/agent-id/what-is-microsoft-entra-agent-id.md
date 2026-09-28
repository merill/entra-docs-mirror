---
layout: Conceptual
title: What is Microsoft Entra Agent ID? - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/what-is-microsoft-entra-agent-id
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn about Microsoft Entra Agent ID, the identity and security framework that enables organizations to build, discover, govern, and protect AI agent identities at enterprise scale.
ms.date: 2026-04-14T00:00:00.0000000Z
ms.topic: concept-article
ms.reviewer: kylemar
ai-usage: ai-assisted
locale: en-us
document_id: 35f26b77-e69c-21d1-50b4-6fc5008bbd13
document_version_independent_id: 35f26b77-e69c-21d1-50b4-6fc5008bbd13
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/what-is-microsoft-entra-agent-id.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/what-is-microsoft-entra-agent-id
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/what-is-microsoft-entra-agent-id.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ec15a305-2674-187a-60d2-295a237ff9c2
---

# What is Microsoft Entra Agent ID? - Microsoft Entra Agent ID | Microsoft Learn

Microsoft Entra Agent ID is an identity and security framework that extends Microsoft Entra capabilities to AI agents. As organizations deploy assistive, autonomous, and user-like agents, they need purpose-built identity constructs to authenticate, authorize, govern, and protect these nonhuman identities. Microsoft Entra Agent ID addresses these needs by providing a unified platform for managing agent identities at enterprise scale.

[![Diagram showing the identity management, access protection, governance, and compliance capabilities that Microsoft Entra Agent ID provides for AI agents.](media/what-is-microsoft-entra-agent-id/microsoft-entra-agent-identity-capabilities.png)](media/what-is-microsoft-entra-agent-id/microsoft-entra-agent-identity-capabilities-expanded.png#lightbox)

Microsoft Entra Agent ID brings together identity management, access protection, governance, and compliance for AI agents.

## Agent identity platform

The [Microsoft Entra Agent identity platform](what-is-agent-id-platform) enables developers to create and manage [agent identities](what-are-agent-identities), which are specialized identity constructs built for AI agents. Agent identity blueprints serve as templates for creating individual agent identities with parent-child relationships, enabling consistent security policies across large numbers of agents. The platform supports standard protocols such as OAuth 2.0, Model Context Protocol (MCP), and agent-to-agent (A2A) for authentication and agent-to-agent communication.

Microsoft Entra Agent ID works with agents built on Microsoft and non-Microsoft platforms. Organizations can [integrate third-party agents](configure-third-party-agents) from platforms such as AWS Bedrock and n8n by using the Microsoft Entra ID Auth SDK (sidecar) or workload identity federation, giving every agent a governed identity regardless of where it was built.

## Security and governance for agents

Microsoft Entra Agent ID extends existing Microsoft Entra security and governance capabilities to agent identities. Agents receive the same identity-driven protections as users and workloads, including adaptive access policies, real-time risk detection, lifecycle management, and network-level controls. All agent authentication and activity is logged for compliance and audit.

For details on how these capabilities work for agents, see:

- [Microsoft Entra security for AI overview](security-for-ai-overview)
- [Conditional Access for agents](/en-us/entra/identity/conditional-access/agent-id)
- [Identity Protection for agents](/en-us/entra/id-protection/concept-risky-agents)
- [Identity governance for agents](/en-us/entra/id-governance/agent-id-governance-overview)
- [Network controls for agents](/en-us/entra/global-secure-access/concept-secure-web-ai-gateway-agents)
- [Sign-in and audit logs for agents](sign-in-audit-logs-agents)

## How to get started

Microsoft Entra Agent ID is a product within Microsoft Entra that provides the platform for creating and managing agent identities and agent identity blueprints. Agent ID is available for all Microsoft Entra customers.

[Microsoft Agent 365](/en-us/microsoft-agent-365/overview) enables agents to operate across Microsoft 365 services and enterprise workflows, which requires a **Microsoft Agent 365** license for each user. For pricing details, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing).

Extending Microsoft Entra security features to agents requires Microsoft Agent 365. Agent 365 is included with Microsoft 365 E7 and is available as an add-on to Microsoft E5/A5/Business Premium (or Microsoft Defender Suite + Microsoft Purview Suite). See our latest [Agent 365 product terms for more details](https://www.microsoft.com/licensing/terms/productoffering/Agent365/EAEAS#clause-2755-h3-1).