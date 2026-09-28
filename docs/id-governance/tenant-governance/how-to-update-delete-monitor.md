---
layout: Conceptual
title: Update or delete a monitor - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-update-delete-monitor
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to update or delete a configuration monitor in Microsoft Entra Tenant Governance when baselines or requirements change
ms.topic: how-to
ms.date: 2026-03-05T00:00:00.0000000Z
locale: en-us
document_id: eaef8f10-735f-2825-16f2-692ee082a4da
document_version_independent_id: eaef8f10-735f-2825-16f2-692ee082a4da
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-update-delete-monitor.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-update-delete-monitor
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-update-delete-monitor.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 5cfdcd15-a834-e0fd-3bb6-ca8e37224929
---

# Update or delete a monitor - Microsoft Entra ID Governance | Microsoft Learn

This article describes how to update or delete a configuration monitor in the [Microsoft Entra admin center](https://entra.microsoft.com). You might update a monitor when your configuration baseline changes. Delete a monitor when the monitored resources are no longer important for your organization's security or compliance requirements.

## Prerequisites

- Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Administrator](../../identity/role-based-access-control/permissions-reference#global-administrator).
- Your tenant must have a license for Microsoft Entra Tenant Governance.
- At least one configuration monitor must exist in your tenant.

## Update a monitor

To update an existing configuration monitor:

1. Browse to **Tenant Governance** &gt; **Configuration management** &gt; **Monitors**.
2. Find the monitor you want to update and select the edit (pencil) icon next to its name.

The update wizard uses the same steps as creating a monitor: **Permissions** → **Configuration baseline** → **Review**.

When you update an existing configuration monitor, the updated settings replace the existing monitor definition.

Important

When you update an existing monitor, Tenant Governance automatically deletes all previously generated monitor results and configuration drifts. The updated monitor records results and drifts again each time it runs.

## Delete a monitor

Deleting a monitor can't be undone. When you delete a monitor, Tenant Governance also immediately deletes all associated monitor results and configuration drifts.

To delete a configuration monitor:

1. Browse to **Tenant Governance** &gt; **Configuration management** &gt; **Monitors**.
2. Find the monitor you want to delete.
3. Select the checkbox next to the monitor's name, then select **Delete** in the command bar. Alternatively, hover over the monitor name and select the delete icon that appears.
4. In the confirmation dialog, select **Delete**.