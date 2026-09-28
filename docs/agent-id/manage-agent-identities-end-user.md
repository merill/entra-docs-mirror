---
layout: Conceptual
title: Manage agents in end user experience | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/manage-agent-identities-end-user
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to manage agent identities in the end user experience within Microsoft Entra. View, control, and take action on agents you own or sponsor with ease.
ms.custom: entra-id-governance
ms.topic: how-to
ms.date: 2026-05-01T00:00:00.0000000Z
locale: en-us
document_id: 48e61b50-8716-cccf-588a-ac81773b7417
document_version_independent_id: 48e61b50-8716-cccf-588a-ac81773b7417
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/manage-agent-identities-end-user.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/manage-agent-identities-end-user
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/manage-agent-identities-end-user.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 57d2229a-eb98-d1c5-408a-187a78710133
---

# Manage agents in end user experience | Microsoft Learn

The Manage Agents feature in Microsoft Entra lets you view and control, [agent identities you own or sponsor](agent-owners-sponsors-managers). [Agents identities](what-are-agent-identities) are special identities, such as bots or automated processes, that act on behalf of users or teams. With the manage agents feature, you can easily see which agents you’re responsible for, review their details, and take action to enable, disable, or request access for them.

Note

This article is for agent identity owners and sponsors. The **Manage agents** menu only appears for users who own or sponsor at least one agent identity. For tenant-wide management by administrators, see [Manage agent identities in your organization](manage-agent-identities-admin).

## Manage agents as an agent identity owner or sponsor

1. Sign in to the [My Account end user portal](https://myaccount.microsoft.com/) as either an owner or sponsor of at least one agent identity.
2. If you haven’t opted in to the new homepage yet, select **Use new version** in the banner.

    Note

    If you’re already using the new homepage, the banner still appears with the message "You’re using the new version of the account homepage" and a **Use previous version** button.
3. In the left menu, select **Manage agents**.

    Note

    This menu item will only appear if you're an owner or sponsor of at least one agent identity.
4. Choose either the **Agents you sponsor** or **Agents you own** tab to view your agents. ![Screenshot of the managed agents page in the My Account portal.](media/manage-agent/manage-agents-list.png)
5. Select an agent to view details about it. ![Screenshot of the manage agent view.](media/manage-agent/manage-agent-view.png)

## Enable or disable an agent

1. To disable an agent, select it from the list and choose **Disable agent**. This blocks users from being able to access it and prevents it from being issued tokens. This has the same effect as disabling the agent from the admin center.
2. To re-enable, select the agent that is disabled and choose **Enable agent**. This allows users to access it, and allows it to be issued tokens. Note that sponsors can't re-enable agents. They will need an owner or admin's help if one of their agents needs to be re-enabled.

## Request an access package on behalf of an agent identity

As the owner or sponsor of an agent identity, you can request an access package for that agent identity by doing the following steps:

1. Sign in to the My Access portal at https://myaccess.microsoft.com.
2. On the My Access Portal page, select **Access packages**.
3. On the Access packages page, locate the access package you want to request for an agent identity to have, and select **Request**.
4. On the Request pane under **Request details**, select **Requesting for Sponsored agent** or **Requesting for Owned agent**.
5. Select the agent identity and then select **Continue**.