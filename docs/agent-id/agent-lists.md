---
layout: Conceptual
title: View and filter agent identities in your tenant - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-lists
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Access Microsoft Entra admin center to view and filter agent identities. Streamline tenant oversight with search, filters, and column customization.
ms.topic: how-to
ms.date: 2026-05-01T00:00:00.0000000Z
ms.reviewer: alamaral
locale: en-us
document_id: 74060dbb-1ebb-ecae-caa4-b2e72ee909e7
document_version_independent_id: 74060dbb-1ebb-ecae-caa4-b2e72ee909e7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-lists.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-lists
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-lists.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 5307a932-b931-28b6-e791-798442fcb800
---

# View and filter agent identities in your tenant - Microsoft Entra Agent ID | Microsoft Learn

Microsoft Entra admin center provides you with a centralized interface to view and filter your agent identities. This comes with the ability to search, filter, sort, and customize columns to find specific agent identities in your tenant.

- To view and manage your agent identity blueprint principals, see [View and manage agent identity blueprints using Microsoft Entra admin center](manage-agent-blueprint).
- To view and manage agents registered in the Agent Registry without an identity, see [manage agent identity blueprints with no identities](manage-agents-without-identity).

## Prerequisites

To view agent identities in your Microsoft Entra tenant, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). No admin role is required for viewing.

To manage agent identities in your Microsoft Entra tenant, you need:

- Agent ID Administrator or Cloud Application Administrator role.
- You can also manage your agent identity if you're the owner of that agent identity, with or without the above roles.

## View a list of agent identities

To view agent identities in your tenant:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com)
2. Browse to **Entra ID** &gt; **Agents** &gt; **Agent identities**.
3. Select any agent identity you'd like to manage.

This page contains a list of all agent identities in your organization. This includes both [agent identity objects](agent-identities) and [agents using a service principal](agent-service-principals).

## Search for an agent identity

- To search for an agent identity, enter either the **name** or **object ID** of the agent identity you want to find in the search box.
- To look up an agent identity by its **Blueprint App ID**, add the **Blueprint App ID** filter. You can further refine the list using filters based on various criteria.

You can select an agent identity from this list to see information like:

- An overview of the agent identity, including:
    - The name, description, and logo for your agent identity
    - The status of that agent identity, and the ability to enable/disable a given agent identity
    - The link to the parent agent identity blueprint
- The list of owners and sponsors for that agent identity
- The agent's access via this agent identity's granted permissions and Microsoft Entra roles
- Audit logs and sign-in logs for that agent identity

## Select viewing options

To customize your view of agent identities, you can change filters or select which columns are shown for each agent identity. Not all columns are shown by default. To see all available columns and edit shown columns, select the **Choose columns** button. The table columns and their filter options are as follows:

| Column Name | Description | Sortable | Filterable | Special notes |
| --- | --- | --- | --- | --- |
| **Name** | Display name of the agent identity | ✓ | ✓ | Primary search field; clickable to view details of the agent identity |
| **Created On** | Date when the agent was created | ✓ | ✓ | Filter by "Last N days" |
| **Status** | Current operational state (Active, or Disabled) | ✓ | ✓ |  |
| **Object ID** | Unique identifier for agent identity | ✗ | ✓ |  |
| **View Access** | Direct link to agent identity's permissions | ✗ | ✗ | Navigates to the Agent's Access pane, on Permissions tab |
| **Blueprint App ID** | Unique identifier for the agent identity blueprint of this agent identity | ✗ | ✓ | Will be blank for [agents using service principals](agent-service-principals) |
| **Owners and Sponsors** | Direct link to the owners and sponsors for a given agent identity | ✗ | ✗ |  |
| **Uses agent identity** | Represents whether or not this agent has an agent identity object, or utilizes a service principal | ✗ | ✗ | If the answer is "yes," then it uses an agent identity object. If "no" this agent utilizes a service principal |