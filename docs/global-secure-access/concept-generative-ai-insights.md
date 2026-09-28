---
layout: Conceptual
title: Generative AI Insights in Global Secure Access (preview) - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-generative-ai-insights
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: jenniferf-skc
ms.author: jfields
ms.service: global-secure-access
manager: dougeby
description: Learn how Generative AI Insights in Global Secure Access provides unified network telemetry for Generative AI prompt requests and Model Context Protocol (MCP) traffic.
ms.topic: concept-article
ms.date: 2026-06-04T00:00:00.0000000Z
ms.reviewer: kerenSemel
ai-usage: ai-assisted
locale: en-us
document_id: 314a3ae8-4ced-2c48-ec1b-5ffaa20b9a1a
document_version_independent_id: 314a3ae8-4ced-2c48-ec1b-5ffaa20b9a1a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-generative-ai-insights.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-generative-ai-insights
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-generative-ai-insights.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: ed19b1ce-691d-a476-3c8a-bef19a9c03df
---

# Generative AI Insights in Global Secure Access (preview) - Global Secure Access | Microsoft Learn

Generative AI Insights in Microsoft Entra Global Secure Access is a unified telemetry surface for Generative AI activity that flows through Internet Access. It captures both **GenAI prompt requests** sent to supported AI applications and **Model Context Protocol (MCP)** traffic between AI agents and remote MCP servers. Security and identity admins get a single page in the Microsoft Entra admin center where they can review prompt content, MCP operations, and the user identity, destination, and transaction that produced each event.

Important

Generative AI Insights logging is currently in preview. For more information, see the [Microsoft Entra preview terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Why Generative AI Insights matters

Generative AI changes how users and agents interact with internet services. Prompts can carry sensitive data, and MCP gives agents new ways to call tools and exchange data with remote servers. Both flows often bypass traditional logging because they ride inside encrypted HTTPS sessions.

Generative AI Insights gives you network-level visibility into both flows so you can:

- **See what's being sent** to supported Generative AI apps, including the full prompt content.
- **Discover MCP servers**, including private and shadow servers, by inspecting the MCP protocol itself rather than relying on an app catalog.
- **Attribute activity** to a specific user, destination URL, and transaction.
- **Stream events to your SIEM**, including Microsoft Sentinel, for long-term retention, correlation, and detection.

## How Generative AI Insights works

Generative AI Insights uses the inline network inspection capabilities of Global Secure Access to log GenAI prompt and MCP activity as it passes through Internet Access.

- **Prompt logging** uses TLS inspection to extract the prompt body from encrypted requests to supported GenAI applications. Each event records the prompt content, user identity, timestamp, destination URL, and the related Global Secure Access transaction ID.
- **MCP logging** uses deep packet inspection to identify MCP traffic by the protocol itself, without depending on a cloud app catalog. Because identification doesn't rely on a known-app list, Global Secure Access discovers unknown, private, and shadow MCP servers.
- **Copilot Studio integration** logs MCP traffic without the need to enable and configure TLS inspection. When the [Global Secure Access integration with Microsoft Copilot Studio](concept-secure-web-ai-gateway-agents) is enabled, agent traffic routes through Global Secure Access and MCP events are captured directly.

## What Generative AI Insights captures

Each Generative AI Insights event includes the following fields:

| Field | Description |
| --- | --- |
| **Activity** | The traffic type. **Prompt** for GenAI prompt requests, **MCP** for Model Context Protocol traffic. |
| **Sub-activity** | The specific operation. For prompts, the GenAI application or interaction type. For MCP, the protocol method, such as `initialize`, `tools/list`, `tools/call`, `prompts/list`, or `prompts/get`. |
| **Content** | The payload, such as the prompt body or the MCP request or response. The content field stores up to 65 KB per event. |
| **Destination URL** | The URL of the GenAI service or remote MCP server. |
| **Create date time** | Timestamp when the event was recorded. |
| **Event ID** | A unique identifier for the event. For MCP, the request and response for the same operation share the same event ID. |
| **Event Type** | For MCP, indicates whether the entry is a **Request** or a **Response**. |
| **MCP Client Name** | The name reported by the MCP client. Use the destination URL as the reliable identifier. |
| **MCP Server Name** | The name reported by the MCP server. Use the destination URL as the reliable identifier. |
| **Session ID** | The session identifier. Multiple events can occur within the same session. |
| **Transaction ID** | The related Global Secure Access traffic log transaction, used to correlate Generative AI Insights events with traffic logs. |
| **User Principal Name** | The user or identity whose traffic was inspected. |

## Supported Generative AI applications

Prompt logging supports the following Generative AI applications:

- Microsoft Copilot
- Copilot (public)
- ChatGPT
- Claude
- Grok
- Mistral
- Cohere
- Pi
- Qwen
- Meta AI
- Gemini

## Generative AI Insights vs. Shadow AI discovery

Generative AI Insights and [Shadow AI discovery](concept-shadow-ai-discovery) are complementary. Use both together for layered visibility.

| Aspect | Shadow AI discovery | Generative AI Insights |
| --- | --- | --- |
| Purpose | Discover which Generative AI SaaS apps users access. | Log the content and operations sent to GenAI apps and MCP servers. |
| Detection method | Cloud app catalog match against network traffic. | TLS inspection (prompt) and deep packet inspection (MCP). |
| Granularity | Application-level — which app, by which user, how often. | Event-level — full prompt or MCP payload, per request and response. |
| Catalog dependency | Yes — relies on the Microsoft Defender for Cloud Apps catalog. | No — MCP detection works on the protocol itself, so it discovers private and shadow MCP servers. |
| Surfacing | Application Usage Analytics. | Generative AI Insights logs page in **Global Secure Access** &gt; **Monitor**. |

## Stream Generative AI Insights to a SIEM

Generative AI Insights events are exposed as a Microsoft Entra diagnostic settings category. You can stream them to Azure Monitor Log Analytics or Microsoft Sentinel for long-term retention, correlation with other signals, and detection rules.

- **Diagnostic settings category**: `NetworkAccessGenerativeAIInsights`
- **Sentinel / Log Analytics table**: [`NetworkAccessGenerativeAIInsights`](/en-us/azure/azure-monitor/reference/tables/networkaccessgenerativeaiinsights)

For configuration steps, see [Microsoft Sentinel integration](how-to-sentinel-integration).

## Limitations

- MCP logging captures only traffic to **remote** MCP servers. Local MCP servers running on a device aren't visible because their traffic doesn't have a network footprint that Global Secure Access can inspect.
- Prompt and MCP content extraction requires [TLS inspection](concept-transport-layer-security), except in the Copilot Studio integration path, where MCP traffic is logged without TLS inspection.
- The MCP client name and MCP server name might be missing on some events when the name isn't included in the protocol payload. Use the destination URL as the reliable identifier.