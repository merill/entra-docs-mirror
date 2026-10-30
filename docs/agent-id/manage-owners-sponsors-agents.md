---
layout: Conceptual
title: Add and manage owners and sponsors for agent identities and blueprints - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/manage-owners-sponsors-agents
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to add and manage owners and sponsors for agent identity blueprints and agent identities in the Microsoft Entra admin center.
ms.topic: how-to
ms.date: 2026-04-28T00:00:00.0000000Z
ms.reviewer: arluca
ai-usage: ai-assisted
locale: en-us
document_id: 126afa81-b111-1c01-060e-be139e13ffd2
document_version_independent_id: 126afa81-b111-1c01-060e-be139e13ffd2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/manage-owners-sponsors-agents.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/manage-owners-sponsors-agents
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/manage-owners-sponsors-agents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b0567c8a-f46b-aaf5-fd4b-835f5f51936f
---

# Add and manage owners and sponsors for agent identities and blueprints - Microsoft Entra Agent ID | Microsoft Learn

Owners and sponsors play distinct governance roles for agent identity blueprints and agent identities in Microsoft Entra ID. Owners are technical administrators who can manage the configuration and operations of an agent. Sponsors are business owners who are accountable for the agent's purpose, lifecycle decisions, and access reviews.

This article walks you through adding and removing owners and sponsors using the Microsoft Entra admin center. For more information about the roles and responsibilities of owners and sponsors, see [owners, sponsors, and managers](agent-owners-sponsors-managers).

## Prerequisites

To manage owners and sponsors, you must:

- Have the [Agent ID Administrator](../identity/role-based-access-control/permissions-reference#agent-id-administrator) role.
- Be an existing owner of the agent identity blueprint or agent identity you want to manage.

## Add an owner or sponsor to an agent blueprint

When managing agent identity blueprint owners and sponsors, you can assign them to either the agent identity blueprint or the agent blueprint principal using the respective tabs.

Note

When you use a dynamic membership group as a sponsor, it can take up to 24 hours after a membership rule change or a user property change before the authorization check on sponsorship succeeds. Plan accordingly when assigning dynamic groups as sponsors for agent identities or blueprints.

[![Screenshot of the owners and sponsors page for a blueprint showing the list of owners and sponsors with their roles.](media/manage-owners-sponsors-agents/blueprint-owners-sponsors.png)](media/manage-owners-sponsors-agents/blueprint-owners-sponsors.png#lightbox)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Agent ID Administrator](../identity/role-based-access-control/permissions-reference#agent-id-administrator) or owner of the agent identity blueprint.
2. Browse to **Entra ID** &gt; **Agents** &gt; **Agent blueprints**.
3. Select the blueprint you want to manage.
4. Under **Access** select **Owners and sponsors**.
5. Select either the **Agent blueprint** or **Agent blueprint principal** tab, depending on which you want to manage.
6. Select **Add** &gt; **Add owner** or **Add sponsor**, depending on which you want to add.
7. Search for and select the users and groups (for sponsors only) you want to add.
8. Select **Add**.

## Add an owner or sponsor to an agent identity

The process for adding owners and sponsors to individual agent identities is similar to blueprints.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Agent ID Administrator](../identity/role-based-access-control/permissions-reference#agent-id-administrator) or owner of the agent identity.
2. Browse to **Entra ID** &gt; **Agents** &gt; **Agent identities**.
3. Select the agent identity you want to manage.
4. Under **Access** select **Owners and sponsors**.
5. Select **Add** &gt; **Add owner** or **Add sponsor** depending on which you want to add.
6. Search for and select the users and groups (for sponsors only) you want to add.
7. Select **Add**.

## Remove an owner or sponsor

### Remove from blueprints

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Agent ID Administrator](../identity/role-based-access-control/permissions-reference#agent-id-administrator) or owner of the agent identity blueprint.
2. Browse to **Entra ID** &gt; **Agents** &gt; **Agent blueprints**.
3. Select the blueprint you want to manage.
4. Select **Owners and sponsors** from the left menu.
5. Select either the **Agent blueprint** or **Agent blueprint principal** tab, depending on which you want to manage.
6. Select the checkbox next to the owner or sponsor you want to remove.
7. Select **Remove**.

### Remove from agent identities

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Agent ID Administrator](../identity/role-based-access-control/permissions-reference#agent-id-administrator) or owner of the agent identity.
2. Browse to **Entra ID** &gt; **Agents** &gt; **Agent identities**.
3. Select the agent identity you want to manage.
4. Under **Access** select **Owners and sponsors**.
5. Select the checkbox next to the owner or sponsor you want to remove.
6. Select **Remove**.