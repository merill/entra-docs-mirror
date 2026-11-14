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
description: Learn how to update or delete home-tenant and governed-tenant monitors, including the impact on results and drift records.
ms.topic: how-to
ms.date: 2026-11-12T00:00:00.0000000Z
ai-usage: ai-assisted
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

These actions apply to monitors targeting the home tenant or other tenants connected through governance relationships. Check the monitor's target tenant before updating or deleting it.

## Prerequisites

- Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../../identity/role-based-access-control/permissions-reference#global-administrator).
- The tenant has licenses for **Tenant Governance Basic** or **Tenant Governance Premium**. Basic includes monitors targeting the home tenant and governed tenants. See [Microsoft Entra Tenant Governance licensing](licensing).
- At least one configuration monitor must exist in your tenant.
- For a monitor targeting another tenant, verify the governance relationship and required delegated permissions. Workload permissions must remain valid for subsequent runs.

## Update a monitor

To update an existing configuration monitor:

1. Browse to **Tenant Governance**. Under **Tenant management**, select **Monitors** for the home tenant. Under **Other tenants**, select **Monitors (Preview)** for a governed tenant.
2. Open the monitor and confirm the target tenant.
3. Use **Settings** to update its name or description, or **Baseline** to update its configuration.

Review the monitor settings, target tenant, baseline, and permission readiness in the update wizard. You can update the baseline by using JSON, a snapshot, or a configuration baseline template, as available in the wizard. For details about baseline selection and tenant scope, see [Create a configuration monitor](how-to-create-monitor).

Changing the tenant filter in the monitor list doesn't retarget an existing monitor. The governed tenant is read-only when you edit a monitor. Create a new monitor to target a different tenant.

When you update an existing configuration monitor, the updated settings replace the existing monitor definition.

Important

A baseline update hides previous monitor results and drift records. A name or description update is a metadata-only change; it doesn't replace the baseline. Preserve required evidence before changing the baseline.

These update types also apply to monitors targeting governed tenants. New results and drifts are produced on later runs. Updating a monitor changes its definition, not the configuration of the resources it monitors. Use a deployment to change resource settings.

For a template-linked monitor, the baseline is read-only. Edit the source template and use **Apply latest**, when available, to apply a new version after reviewing parameter values.

## Delete a monitor

Deleting a monitor can't be undone and stops future runs for that monitor. Preserve any associated monitor results and drift records you need before deletion. Don't rely on a deleted monitor as your history archive.

To delete a configuration monitor:

1. Browse to **Tenant Governance**. Under **Tenant management**, select **Monitors** for the home tenant. Under **Other tenants**, select **Monitors (Preview)** for a governed tenant.
2. Confirm the target tenant.
3. Find the monitor you want to delete.
4. Select the checkbox next to the monitor's name, then select **Delete** in the command bar. Alternatively, hover over the monitor name and select the delete icon that appears.
5. In the confirmation dialog, select **Delete**.
6. Select a monitor to enable **Delete** in the command bar.

[![Screenshot of a selected monitor with the Delete command enabled in the command bar.](../media/tenant-governance-configuration-management/selected-monitor.png)](../media/tenant-governance-configuration-management/selected-monitor.png#lightbox)

Deleting an other-tenant monitor removes the selected monitor from its target tenant. It doesn't delete resources in the governed tenant, revert previously applied configuration, or terminate the governance relationship. Other monitors aren't affected.

Permission or relationship changes can prevent later runs of a governed-tenant monitor. Review those dependencies when you update the monitor; don't interpret a failed run as confirmation that no drift exists.