---
layout: Conceptual
title: Learn about Secure Web and AI Gateway for Microsoft Copilot Studio agents - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-secure-web-ai-gateway-agents
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about the features and benefits of our Secure Web and AI Gateway for agents in Global Secure Access.
ms.reviwer: fgomulka
ms.topic: concept-article
ms.date: 2025-11-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: f844eba2-4ff7-131c-3c03-de5abd3c2947
document_version_independent_id: f844eba2-4ff7-131c-3c03-de5abd3c2947
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-secure-web-ai-gateway-agents.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-secure-web-ai-gateway-agents
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-secure-web-ai-gateway-agents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c389ea6b-b6a0-46df-93a1-1e21f25e19e7
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19ada1b6-705b-4ed7-aad0-bffd1bd03dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ac311436-9d89-80b8-28c5-01fbe547280d
---

# Learn about Secure Web and AI Gateway for Microsoft Copilot Studio agents - Global Secure Access | Microsoft Learn

As organizations adopt autonomous and interactive AI agents to perform tasks previously handled by humans, administrators need visibility and control over agent network activity. Global Secure Access for agents provides network security controls for Microsoft Copilot Studio agents, enabling you to apply the same security policies to agents that you use for users.

With Global Secure Access for agents, you can regulate how agents use knowledge, tools, and actions to access external resources. You can apply network security policies including web content filtering, threat intelligence filtering, and network file filtering to agent traffic.

## How network security for Copilot Studio agents works

To enforce network security controls on Copilot Studio agents, you forward agent traffic to Global Secure Access's globally distributed proxy service. You enable traffic forwarding in the Power Platform Admin Center on a per-environment or per-environment-group basis.

Agent traffic forwarding applies to multiple traffic types, including:

- HTTP Node traffic
- Custom connectors
- MCP Server Connector

Once agent traffic is forwarded to Global Secure Access, you can apply security policies to the traffic. The service evaluates agent traffic against your configured security policies, similar to how it evaluates user traffic.

![Diagram showing agent traffic flowing through Global Secure Access to protected resources.](media/concept-secure-web-ai-gateway-agents/agent-traffic-flow.png)

## Security policies for agents

Security policies for agents are configured using the baseline profile in Global Secure Access. The baseline profile applies security policies at the tenant level, ensuring consistent security controls across all agent traffic.

## How to get started

Microsoft Entra Agent ID is a product within Microsoft Entra that provides the platform for creating and managing agent identities and agent identity blueprints. Agent ID is available for all Microsoft Entra customers.

[Microsoft Agent 365](/en-us/microsoft-agent-365/overview) enables agents to operate across Microsoft 365 services and enterprise workflows, which requires a **Microsoft Agent 365** license for each user. For pricing details, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing).

Extending Microsoft Entra security features to agents requires Microsoft Agent 365. Agent 365 is included with Microsoft 365 E7 and is available as an add-on to Microsoft E5/A5/Business Premium (or Microsoft Defender Suite + Microsoft Purview Suite). See our latest [Agent 365 product terms for more details](https://www.microsoft.com/licensing/terms/productoffering/Agent365/EAEAS#clause-2755-h3-1).