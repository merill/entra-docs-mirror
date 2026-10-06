---
layout: Conceptual
title: View Generative AI Insights logs in Global Secure Access (preview) - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-view-generative-ai-insights-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to view, filter, and export Generative AI Insights logs in Microsoft Entra Global Secure Access to monitor GenAI prompts and Model Context Protocol traffic.
ms.topic: how-to
ms.date: 2026-06-04T00:00:00.0000000Z
ms.reviewer: kerenSemel
ai-usage: ai-assisted
locale: en-us
document_id: 10316446-83c2-0f6d-b4d8-efaeb63c62a3
document_version_independent_id: 10316446-83c2-0f6d-b4d8-efaeb63c62a3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-view-generative-ai-insights-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-view-generative-ai-insights-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-view-generative-ai-insights-logs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 336be9de-025a-ea24-4e0c-6c08123effb5
---

# View Generative AI Insights logs in Global Secure Access (preview) - Global Secure Access | Microsoft Learn

The Generative AI Insights logs page in Microsoft Entra Global Secure Access is the unified surface for Generative AI activity flowing through Internet Access. From a single page, you can review GenAI prompt requests sent to supported applications, Model Context Protocol (MCP) traffic between AI agents and remote MCP servers, and the user, destination, and transaction behind each event. This article walks through accessing the page, filtering events, inspecting per-event details, and exporting results.

For background on what Generative AI Insights captures and how it works, see [Generative AI Insights in Global Secure Access](concept-generative-ai-insights).

Important

Generative AI Insights logging is currently in preview. For more information, see the [Microsoft Entra preview terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Prerequisites

- A Microsoft Entra tenant with a Global Secure Access license. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access).
- One of the following roles: [Global Secure Access Administrator](reference-role-based-permissions#global-secure-access-administrator) or [Global Secure Access Log Reader](reference-role-based-permissions#global-secure-access-log-reader).
- Internet Access traffic forwarding enabled for the users or devices you want to monitor.
- For prompt logging and for MCP logging on end-user devices, [TLS inspection](how-to-transport-layer-security) must be enabled. TLS inspection isn't required for MCP traffic from Microsoft Copilot Studio agents when the [Global Secure Access integration with Copilot Studio](concept-secure-web-ai-gateway-agents) is enabled.

## Open the Generative AI Insights logs page

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Secure Access Log Reader](reference-role-based-permissions#global-secure-access-log-reader).
2. Browse to **Global Secure Access** &gt; **Monitor** &gt; **Generative AI Insights**.

The page displays a list of GenAI prompt and MCP events captured from your tenant, with the most recent events at the top.

## Filter events

Use the filter controls at the top of the page to narrow the view.

- **Activity**. Switch between event types. Select **Prompt** to see only GenAI prompt requests, or **MCP** to see only Model Context Protocol traffic.
- **Sub-activity**. Filter by a specific operation. For prompts, the GenAI application or interaction type. For MCP, the protocol method, such as `initialize`, `tools/list`, `tools/call`, `prompts/list`, or `prompts/get`.
- **Destination URL**. Filter by a specific GenAI service or MCP server URL to focus on activity for one destination.
- **User**. Filter by user principal name to see all GenAI prompts and MCP operations from a specific user.

You can combine filters to scope the view, for example **Activity = MCP** plus a specific destination URL to review every operation against one MCP server.

## Column reference

The Generative AI Insights logs page surfaces the following columns. The same fields are available when you stream events to Log Analytics or Microsoft Sentinel.

| Column | Description |
| --- | --- |
| **Create date time** | Timestamp when the event was recorded. |
| **Activity** | The traffic type — **Prompt** or **MCP**. |
| **Sub-activity** | The specific operation, such as a GenAI application name or an MCP protocol method. |
| **Content** | The payload, such as the prompt body or MCP request or response. Stored up to 65 KB per event. |
| **Destination URL** | The URL of the GenAI service or remote MCP server. The destination URL is the reliable identifier for an MCP server. |
| **Event ID** | A unique identifier for the event. For MCP, the request and response for the same operation share the same event ID. |
| **Event Type** | For MCP, indicates whether the entry is a **Request** or a **Response**. |
| **MCP Client Name** | The name reported by the MCP client. Might be missing if the client doesn't include it in the payload. |
| **MCP Server Name** | The name reported by the MCP server. Might be missing if the server doesn't include it in the payload. |
| **Session ID** | The session identifier. Multiple events can share the same session. |
| **Transaction ID** | The related Global Secure Access traffic log transaction. Use it to correlate Generative AI Insights events with [traffic logs](how-to-view-traffic-logs). |
| **User Principal Name** | The user or identity whose traffic was inspected. |

## View event details

Select any row to open the details pane for that event.

The details pane shows:

- The full **Content** of the prompt or MCP payload, including the prompt body, MCP request arguments, or MCP response payload.
- Correlation IDs — **Event ID**, **Session ID**, and **Transaction ID** — that you can use to match a request with its response and to pivot to the corresponding [traffic log](how-to-view-traffic-logs) entry.
- For MCP `initialize` responses, the server-reported tools and capabilities.

## Export logs

To export the current view for offline analysis or sharing:

1. Apply the filters you want.
2. Select **Export**.
3. Save the resulting file.

You can export up to 100,000 records per export.

For long-term retention and detection, stream Generative AI Insights events to Microsoft Sentinel or Azure Monitor Log Analytics by using the `NetworkAccessGenerativeAIInsights` diagnostic settings category. For configuration steps, see [Microsoft Sentinel integration](how-to-sentinel-integration).

## Discover shadow MCP servers

Because MCP detection uses deep packet inspection rather than a cloud app catalog, the Generative AI Insights logs page surfaces previously unknown, private, and shadow MCP servers.

To review discovered MCP servers:

1. Open the **Generative AI Insights** logs page.
2. Set **Activity** to **MCP**.
3. Review unique values in the **Destination URL** column to identify MCP servers in use.
4. Select an `initialize` response event for a server to view the tools and capabilities it advertises.
5. To block traffic to a risky MCP server, use [URL filtering](how-to-configure-web-content-filtering) to deny access to that server's URL.

For a deeper walkthrough of MCP-specific operations, see [View MCP traffic logs](how-to-view-model-context-protocol-logging).

## Troubleshoot

| Issue | Likely cause and fix |
| --- | --- |
| The page is empty. | Verify that traffic forwarding is enabled, that users have generated GenAI or MCP traffic, and that [TLS inspection](how-to-transport-layer-security) is enabled for end-user devices. |
| No prompt events appear, but users access supported GenAI apps. | Prompt logging requires TLS inspection. Confirm that the destination isn't excluded from your TLS inspection policy. |
| MCP events show no MCP client name or server name. | The name isn't guaranteed to be present in every payload. Use **Destination URL** as the reliable MCP server identifier. |
| Local MCP server activity is missing. | MCP logging captures traffic only to **remote** MCP servers. Local MCP servers don't have a network footprint that Global Secure Access can inspect. |