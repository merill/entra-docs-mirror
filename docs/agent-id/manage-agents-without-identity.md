---
layout: Conceptual
title: Manage agents with no agent identities | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/manage-agents-without-identity
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: This article explains how to manage registry-only agents that don't have associated agent identities in Microsoft Entra ID.
ms.date: 2026-05-01T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: jadedsouza
locale: en-us
document_id: b0b6b7ad-6d9f-64c4-a794-14851cdd8c27
document_version_independent_id: b0b6b7ad-6d9f-64c4-a794-14851cdd8c27
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/manage-agents-without-identity.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/manage-agents-without-identity
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/manage-agents-without-identity.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d4ec10ee-e6c7-3d88-97d7-cfd27a9e64ac
---

# Manage agents with no agent identities | Microsoft Learn

As an admin, you want to have a 360-degree view of your agents for both security and operational efficiency. Some agents will be represented in Microsoft Entra with an agent identity blueprint principal and agent identities, or as a service principal. It isn't uncommon to also have agents that are registered in the agent registry but don't have an associated Microsoft Entra agent identity. These agents are referred to as registry-only agents. They might be in the process of being onboarded or they may have registered in the registry without needing to use Microsoft Entra Agent ID as the agent's identity provider.

## Prerequisite

Agents only appear in the registry after you [publish your agent to the agent registry](identity-platform/publish-agents-to-registry).

## Navigate to your agent without an agent identity

To get to your agent without an agent identity's page, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. In the left-hand navigation pane, select **Entra ID** &gt; **Agents** &gt; **Agent registry (Preview)**.
3. To view the agent card details of a specific agent, select the **View more** link. It reveals the agent's card details that include:

    - **Name**: The name of the agent.
    - **Registry ID**: The unique identifier for the agent in the registry.
    - **Platform**: The platform that created the agent.
    - **Skills**: The capabilities or functionalities of the agent.
    - **Logo**: The logo of the agent.