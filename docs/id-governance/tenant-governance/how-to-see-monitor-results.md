---
layout: Conceptual
title: View monitor results and manage monitors - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-see-monitor-results
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to view monitor results and configuration drifts and manage configuration monitors in Microsoft Entra Tenant Governance
ms.topic: how-to
ms.date: 2026-07-28T00:00:00.0000000Z
locale: en-us
document_id: 73c81c93-3ecd-0ec5-b05d-4b037528fb41
document_version_independent_id: 73c81c93-3ecd-0ec5-b05d-4b037528fb41
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-see-monitor-results.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-see-monitor-results
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-see-monitor-results.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: a72ab563-ab3a-dd7a-b259-8c102292e2af
---

# View monitor results and manage monitors - Microsoft Entra ID Governance | Microsoft Learn

Use the monitor experience to review monitor definitions, monitor run results, configuration drifts, baseline details, permissions readiness, settings, and audit logs. This article describes how to use the monitor pages after a monitor is created.

## Prerequisites

- At least one configuration monitor exists in the tenant.
- You can sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with a role that can view Tenant Governance monitor data.
- The Tenant Configuration Management service has the permissions required to run the monitor. If a monitor run fails because of missing service permissions, [update the service permissions](how-to-set-up-permissions-tenant-monitoring) before you rely on later run results.

## View monitors

To view the configuration monitors in your tenant, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Tenant Governance** &gt; **Monitors**.
3. On the **Monitors** tab, review monitor definitions, create a monitor, refresh the list, or select a monitor to open its details.

## View monitor results

To review the results of monitor runs, follow these steps:

1. Select the **Monitor results** tab.
2. Review the monitor name, monitor ID, start time, completion time, run status, and number of detected drifts.

A monitor result summarizes a single monitor run. Use this page to identify failed or partially successful runs, and to find runs that detected configuration drift.

## View configuration drifts

To review the configuration drifts a monitor detected, follow these steps:

1. Select the **Configuration drifts** tab.
2. Review the monitor, resource name, resource type, drifted properties, and first detection time.

A drift record identifies the resource and property that differ from the baseline. Use this page when you need to decide which workload administration experience to use for remediation.

## Manage a monitor

To review and manage an individual monitor, follow these steps:

1. Select a monitor from the monitor list.
2. On **Overview**, review the **Details**, **Monitoring**, and **Audit** cards. **Details** shows the display name, description, creation date, and the services whose resources are monitored. The **Monitoring** card shows the last monitor run time, resource type, count, and configuration drifts. The **Audit** card shows audit events, such as monitor creation and update events, from the last 30 days, and the date of the last audit event.
3. On **Monitor results**, review the run history for the selected monitor.
4. On **Configuration drifts**, review the drift records for the selected monitor.
5. On **Baseline**, view, edit, or download the monitor baseline JSON.
6. On **Permissions**, review the service authorization readiness.
7. On **Settings**, view and manage the display name and description for the monitor.
8. On **Audit logs**, review the create and update events for the monitor.

## Correct configuration drift

Tenant Governance reports drift, but remediation happens in the administration experience that owns the drifted resource. For example, use the Microsoft Entra admin center or Microsoft Graph PowerShell to update a Conditional Access policy, or use the Exchange admin center or Exchange Online PowerShell to update an Exchange transport rule.

After you remediate drift, the next monitor run evaluates the tenant again and confirms that the actual resource state matches the baseline.