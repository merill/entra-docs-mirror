---
layout: Conceptual
title: Agent Registry convergence with Microsoft Agent 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/agent-registry-convergence
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how agent registry experiences are converging under Microsoft Agent 365, what the change means for Microsoft Entra Agent ID, and how to view all agents in your organization.
ms.topic: concept-article
ms.date: 2026-04-05T00:00:00.0000000Z
ms.reviewer: paparth
ai-usage: ai-assisted
locale: en-us
document_id: c91adf9e-2fb7-d0ec-166d-ef456315c42f
document_version_independent_id: c91adf9e-2fb7-d0ec-166d-ef456315c42f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/agent-registry-convergence.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/agent-registry-convergence
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/agent-registry-convergence.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/302444b9-4a43-4841-8014-3d9e4251ff15
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/bebd8809-dac1-4c22-83e2-66d98af8a94d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: c7ea904e-a5d3-57d6-49e2-f80f515d0b8f
---

# Agent Registry convergence with Microsoft Agent 365 | Microsoft Learn

Organizations are rapidly adopting AI agents across Microsoft platforms, partner ecosystems, and custom applications. As agents grow in number and capability, organizations need a centralized way to observe, govern, and secure them.

[Microsoft Agent 365](/en-us/microsoft-agent-365/overview) is Microsoft's control plane for AI agents. It helps organizations:

- Observe agents across the enterprise.
- Govern how agents access systems, data, and tools.
- Secure agents using Microsoft identity and security capabilities.

A key capability within Microsoft Agent 365 is the [agent registry](/en-us/microsoft-365/admin/manage/agent-registry), which provides a unified inventory of all agents operating in the organization, including both Microsoft and non-Microsoft agents.

## Registry convergence

Previously, agent visibility appeared across multiple portals, including Microsoft Entra and the Microsoft 365 admin center. Based on customer feedback, Microsoft is converging these registry experiences under Agent 365 to provide a simpler and more consistent management experience.

With this change:

- **Agent 365** becomes the unified registry and control plane for agents.
- **Microsoft Entra** continues to provide the identity foundation through Agent ID.

This approach gives customers one place to discover and manage agents, while continuing to use Microsoft Entra for agent identity and access control.

## Frequently asked questions

### Which registry should I use today?

Use Agent 365 to discover and manage all agents in your organization and monitor operational activity. Use Microsoft Entra to manage agent identities (Agent ID), apply identity governance and Conditional Access policies, and monitor identity-related security signals.

### What happens to the features announced as part of the Microsoft Entra Agent Registry?

The capabilities introduced with the Microsoft Entra Agent Registry continue to exist. Specifically:

- Agent identity capabilities remain part of Microsoft Entra Agent ID.
- Agent registration APIs remain supported.
- Identity governance and security controls for agents remain unchanged.

The change simplifies where customers see and manage all agents in their organization, while Microsoft Entra continues to provide identity and access management.

### Will I see the same agent inventory in the Microsoft Entra admin center?

The Microsoft Entra admin center focuses on identity and access management for agents. Identity administrators can see agents that have a Microsoft Entra Agent ID for viewing and managing them. The comprehensive agent inventory, including agents without a Microsoft Entra agent identity, is available in Agent 365.

### What can I manage in the Microsoft Entra admin center?

In the Microsoft Entra admin center, administrators can:

- View agents with Microsoft Entra agent identities.
- Manage agent identities, blueprints, and permissions.
- Apply Conditional Access, identity governance, and network security controls.
- Monitor identity-related security signals.

### Why should I go to Microsoft Agent 365 if I'm an identity administrator?

Identity administrators can optionally use Agent 365, via the Microsoft 365 admin center, to view all agents in the organization, while continuing to use the Microsoft Entra admin center to manage agent identities, access policies, and identity governance controls.

### Do I need a different role to view agents in Agent 365?

To see all agents in Agent 365 and Microsoft Entra Agent ID, users need the [AI Reader](../identity/role-based-access-control/permissions-reference#ai-reader) role. This role is intended for users who need visibility for monitoring or reporting access.

The [Agent ID Administrator](../identity/role-based-access-control/permissions-reference#agent-id-administrator) role is needed to manage or change agent identities.

### Is a license required?

Viewing all agents in the Microsoft 365 admin center doesn't require a specific license. Administrators only need the appropriate role, such as AI Reader (recommended least-privilege role) or AI Administrator, to access the inventory view.

Applying security and governance controls for agents, such as Conditional Access or identity governance policies, requires the appropriate licensing for [Microsoft Entra Agent ID](../fundamentals/licensing#microsoft-entra-agent-id).

### How do I get agent identity blueprints to appear in the Agent 365 registry?

After you create an agent identity blueprint, register it in the [Agent 365 registry](/en-us/microsoft-365/admin/manage/agent-registry) so administrators can discover, govern, and manage the agent from the Microsoft 365 admin center. In some scenarios, previously created agent identity blueprints may not appear in the registry. To ensure that all agent identity blueprints are registered, see [Register agents in the Agent 365 registry](create-blueprint#register-agents-in-the-agent-365-registry).

## How to view the complete agent inventory

To view the complete inventory of agents in your organization:

1. Go to the [Microsoft 365 admin center](https://admin.microsoft.com) as at least an [AI Reader](../identity/role-based-access-control/permissions-reference#ai-reader).
2. Select **Agents** from the navigation menu.
3. Select **All agents** to view the comprehensive list of agents in your tenant.