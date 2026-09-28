---
layout: Conceptual
title: Shadow AI discovery in Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-shadow-ai-discovery
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how Shadow AI discovery in Global Secure Access provides network-based visibility into unsanctioned AI applications and tools used in your organization.
ms.topic: concept-article
ms.date: 2026-06-04T00:00:00.0000000Z
ms.reviewer: kerenSemel
ai-usage: ai-assisted
locale: en-us
document_id: 093e369b-863e-5a57-da41-f846abfe28a8
document_version_independent_id: 093e369b-863e-5a57-da41-f846abfe28a8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-shadow-ai-discovery.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-shadow-ai-discovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-shadow-ai-discovery.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: b8e7f3ab-eb0b-2845-5bfd-960dac87f8e2
---

# Shadow AI discovery in Global Secure Access - Global Secure Access | Microsoft Learn

Shadow AI discovery in Microsoft Entra Global Secure Access is a network-based feature that provides visibility into unsanctioned AI applications and tools used in your organization. It identifies traffic to AI services like ChatGPT, Claude, SaaS MCP servers, and AI Model Provider frameworks (for example, DeepSeek, Anthropic Claude API) by analyzing network traffic. Shadow AI discovery lets administrators see which generative AI apps or tools employees are using without IT approval.

## Why shadow AI discovery matters

Unmanaged AI usage can introduce serious risks, including:

- **Data leakage** — Sensitive data might be sent to external AI services.
- **Compliance violations** — Unsanctioned tools could violate regulatory requirements.
- **Uncontrolled AI tools activity** — Self-directed AI tools might lead to unintended actions without oversight.

Shadow AI discovery helps mitigate these risks by revealing unsanctioned AI usage so that security teams can take action, such as educating users or enforcing policies. It ensures you're not left guessing which AI applications are in use — you can clearly see them.

## How shadow AI discovery works

Global Secure Access analyzes network traffic to identify generative AI applications and tools that users in your organization access. The discovery process works by:

- **Analyzing network traffic** — Global Secure Access inspects internet and Microsoft 365 traffic to detect connections to known generative AI applications, SaaS MCP servers, and AI Model Provider frameworks.
- **Cataloging applications** — Discovered applications are matched against the Microsoft Defender for Cloud Apps cloud app catalog, which categorizes applications and assigns risk scores based on general, security, compliance, and legal factors.
- **Surfacing insights** — IT admins can view all discovered generative AI applications, the users who access them, usage statistics, and risk scores through the Application Usage Analytics dashboard.

## Key capabilities

With shadow AI discovery, you can:

- **Discover generative AI applications and tools** — Identify all generative AI applications that users access across internet and Microsoft 365 traffic, including AI chatbots, AI Model Provider APIs, and SaaS MCP servers.
- **Assess risk** — Review risk scores and detailed risk factors for each discovered AI application, including security, compliance, and legal assessments.
- **Analyze usage patterns** — Understand which users access AI applications, how often, and how much data is transferred.
- **Monitor data exposure** — Track bytes sent and received to generative AI applications to identify potential data leakage.
- **Take action** — Use insights to educate users, create policies that block or monitor specific AI applications, and enforce compliance with your organization's security requirements.

## Access shadow AI discovery

Shadow AI discovery insights are surfaced in the Application Usage Analytics of Global Secure Access.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Log Reader](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-log-reader).
2. Browse to **Global Secure Access** &gt; **Applications** &gt; **Insights and Analytics**.
3. Use the **Generative AI apps and tools** filter or toggle to highlight detected AI applications and view details like usage statistics and risk scores.

The Global Secure Access dashboard also features widgets that summarize shadow AI usage at a glance, such as the number of AI apps accessed and usage trends over time.

## Shadow AI vs. shadow IT

| Aspect | Shadow IT | Shadow AI |
| --- | --- | --- |
| Definition | Unauthorized use of any IT applications or services | Unauthorized use of generative AI applications and tools specifically |
| Primary risk | Data sprawl, security gaps, compliance violations | Data leakage to AI models, compliance violations, uncontrolled AI tools activity |
| Examples | Personal cloud storage, unauthorized SaaS tools | AI chatbots, AI Model Provider APIs, SaaS MCP servers, AI code generators |
| Detection | Application discovery and cloud app analytics | Generative AI apps and tools filtering in application usage analytics |

## Shadow AI discovery vs. Generative AI Insights

Shadow AI discovery and [Generative AI Insights](concept-generative-ai-insights) are complementary. Shadow AI discovery uses the Microsoft Defender for Cloud Apps cloud app catalog to identify which Generative AI SaaS applications users access. Generative AI Insights uses TLS inspection and deep packet inspection to log the actual prompt content and Model Context Protocol (MCP) operations sent to those services. Use both together for layered visibility — Shadow AI discovery for application-level inventory and risk scoring, and Generative AI Insights for event-level prompt and MCP payloads.