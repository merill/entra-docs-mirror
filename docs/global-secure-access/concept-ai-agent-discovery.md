---
layout: Conceptual
title: AI agent discovery in Global Secure Access (preview) - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-ai-agent-discovery
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: jenniferf-skc
ms.author: jfields
ms.service: global-secure-access
manager: dougeby
description: Learn how AI agent discovery in Global Secure Access provides network-level visibility into managed and shadow AI agents reaching the internet from your environment.
ms.topic: concept-article
ms.date: 2026-06-02T00:00:00.0000000Z
ms.reviewer: kerenSemel
ai-usage: ai-assisted
locale: en-us
document_id: 47759872-0045-2987-bb37-a1f37acea508
document_version_independent_id: 47759872-0045-2987-bb37-a1f37acea508
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-ai-agent-discovery.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-ai-agent-discovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-ai-agent-discovery.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c389ea6b-b6a0-46df-93a1-1e21f25e19e7
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19ada1b6-705b-4ed7-aad0-bffd1bd03dfa
platformId: 3a9d7695-bed4-8cd3-58c6-1301ce307a5d
---

# AI agent discovery in Global Secure Access (preview) - Global Secure Access | Microsoft Learn

AI agent discovery in Microsoft Entra Global Secure Access gives security teams a network-level view of AI agents reaching the internet from your environment — both managed and shadow — with attribution back to the user, device, and process that initiated the activity. Discovery covers local agents (both managed and unmanaged) running on endpoints where the Global Secure Access client is installed, and Microsoft Copilot Studio agents.

AI agent discovery uses the existing network inspection of Global Secure Access, so you get coverage without deploying anything new.

Important

AI agent discovery is currently in preview. For more information, see the [Microsoft Entra preview terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Why AI agent discovery matters

AI agents increasingly act autonomously or on behalf of users, accessing data, calling APIs, and reaching external services without direct user interaction. When agents run outside the visibility of identity and endpoint controls, security teams can't answer basic questions: Which agents are running in our environment? Who or what is using them? Are they sanctioned? What tools is each agent using? What APIs is the agent calling?

AI agent discovery helps you answer those questions by:

- **Surfacing every agent reaching the internet**, including managed agents you've sanctioned and shadow agents you haven't.
- **Attributing activity** back to the user, device, and process that initiated the agent's traffic.
- **Distinguishing managed from shadow agents** by using Microsoft Entra Agent ID to classify each discovered agent.
- **Revealing destinations and traffic volume** so you can see which external endpoints each agent is trying to access and how much network activity it generates.

## How AI agent discovery works

Global Secure Access inspects internet-bound network traffic to identify AI agent activity. Because Global Secure Access already sits inline in the network path, discovery doesn't require new agents, sensors, or endpoint changes.

The discovery process:

- **Inspects internet traffic** flowing through Global Secure Access from your users and devices.
- **Identifies AI agents**, including local agents running on endpoints with the Global Secure Access client and Microsoft Copilot Studio agents.
- **Classifies each agent** as managed or shadow (unmanaged) based on whether it's registered with Microsoft Entra Agent ID.
- **Attributes activity** to the originating user, device, and process so you can investigate and respond.

## What's included in the preview

The preview of AI agent discovery includes:

- **AI Agent Discovery widget** on the Global Secure Access overview dashboard. The widget summarizes the total number of agents, managed agents, shadow agents, and new agents detected in the last seven days.
- **AI Agent Discovery blade** with the aggregated agent inventory across the tenant.
- **Managed vs. unmanaged (shadow) classification** by using Microsoft Entra Agent ID.

## Managed vs. shadow agents

| Aspect | Managed agents | Shadow agents |
| --- | --- | --- |
| Definition | AI agents registered with Microsoft Entra Agent ID and sanctioned by your organization. | AI agents reaching the internet from your environment that aren't registered or sanctioned. |
| Visibility | Tracked in your agent inventory with full identity and policy context. | Discovered through network traffic inspection only. |
| Examples | Sanctioned Microsoft Copilot Studio agents and registered local agents. | Unmanaged local agents such as OpenClaw or Ollama running on user devices. |

## Prerequisites

To discover AI agents, your environment must meet the following requirements:

- **Local agents**: The Global Secure Access client must be installed on the endpoint, with internet access forwarding policy and TLS inspection enabled.
- **Microsoft Copilot Studio agents**: The Microsoft Copilot Studio integration with Global Secure Access must be enabled.

## Access AI agent discovery

AI agent discovery insights are available in the Global Secure Access experience in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Log Reader](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-log-reader).
2. Browse to **Global Secure Access** &gt; **Overview** to see the **AI Agent Discovery** widget summarizing total agents, managed agents, shadow agents, and new agents from the last seven days.
3. Select the widget, or browse to **Global Secure Access** &gt; **AI Agent Discovery**, to open the AI Agent Discovery blade and review the aggregated agent inventory across your tenant.