---
layout: Conceptual
title: Provisioning insights workbook - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/provisioning-workbook
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: This article describes the Azure Monitor workbook for provisioning.
ms.topic: concept-article
ms.date: 2025-04-09T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4af2fe14-f94b-bf6a-9f0d-d1baf7b0356b
document_version_independent_id: dbb274e2-1e79-6bd7-a4f0-a390a2b0abdb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/provisioning-workbook.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/provisioning-workbook
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/provisioning-workbook.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4489c86a-5707-3414-74af-7fd297dc35ac
---

# Provisioning insights workbook - Microsoft Entra ID | Microsoft Learn

The Provisioning workbook provides a flexible canvas for data analysis. This workbook brings together all of the provisioning logs from various sources and allows you to gain insight, in a single area. The workbook allows you to create rich visual reports within the Azure portal. To learn more, see [Microsoft Entra Workbooks overview](../monitoring-health/overview-workbooks).

This workbook is intended for Hybrid Identity Administrators who use provisioning to sync users from various data sources to various data repositories. It allows admins to gain insights into sync status and details.

This workbook:

- Provides a synchronization summary of users and groups synchronized from all of you provisioning sources to targets
- Provides and aggregated and detailed view of information captured by the provisioning logs.
- Allows you to customize the data to tailor it to your specific needs

## Enabling provisioning logs

You should already be familiar with Azure monitoring and Log Analytics. If not, jump over to learn about them and then come back to learn about application provisioning logs. To learn more about Azure monitoring, see [Azure Monitor overview](/en-us/azure/azure-monitor/overview). To learn more about Azure Monitor logs and Log Analytics, see [Overview of log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/log-query-overview) and [Provisioning Logs for troubleshooting cloud sync](../hybrid/cloud-sync/how-to-troubleshoot).

## Source and Target

At the top of the workbook, using the drop-down, specify the source and target identities.

Theses fields are the source and target of identities. The rest of the filters that appear are based on the selection of source and target. You can scope your search so that it is more granular using the additional fields. Use the table below as a reference for queries.

For example, if you wanted to see data from your cloud sync workflow, your source would be Active Directory and your target would be Microsoft Entra ID.

Note

Source and target are required. If you do not select a source and target, you won't see any data.

[![Screenshot of fields.](media/provisioning-workbook/fields-1.png)](media/provisioning-workbook/fields-1.png#lightbox)

| Field | Description |
| --- | --- |
| Source | The provisioning source repository |
| Target | The provisioning target repository |
| Time Range | The range of provisioning information you want to view. This can be anywhere from 4 hours to 90 days. You can also set a custom value. |
| Status | View the provisioning status such as Success or Skipped. |
| Action | View the provisioning actions taken such as Create or Delete. |
| App Name | Allows you to filter by the application name. In the case of Active Directory, you can filter by domains. |
| Job Id | Allows you to target specific Job Ids. |
| Sync type | Filter by type of synchronization such as object or password. |

Note

All of the charts and grids in Sync Summary, Sync Details, and Sync Details by grid, change based on source,target and the parameter selections.

## Sync Summary

The sync summary section provides a summary of your organizations synchronization activities. These activities include:

- Total synced objects by type
- Provisioning events by action
- Provisioning events by status
- Unique sync count by status
- Provisioning success rate
- Top provisioning errors

[![Screenshot of the synchronization summary.](media/provisioning-workbook/sync-summary-1.png)](media/provisioning-workbook/sync-summary-1.png#lightbox)

## Sync details

The sync details tab allows you to drill into the synchronization data and get more information. This information includes:

- Objects sync by status
- Objects synced by action
- Sync log details

Note

The grid is filterable on any of the above filters but you can also click the tiles under under **Objects synced by Status** and **Action**.

[![Screenshot of the synchronization details.](media/provisioning-workbook/sync-details-1.png)](media/provisioning-workbook/sync-details-1.png#lightbox)

You can further drill in to the sync log details for additional information.

Note

Clicking on the Source ID it will dive deeper and provide more information on the synchronized object.

## Sync details by cycle

The sync details by cycle tab allow you to get more granular with the synchronization data. This information includes:

- Objects sync by status
- Objects synced by action
- Sync log details

[![Screenshot of the synchronization details by cycle tab.](media/provisioning-workbook/sync-details-2.png)](media/provisioning-workbook/sync-details-2.png#lightbox)

You can further drill in to the sync log details for additional information.

Note

The grid is filterable on any of the above filters but you can also click the tiles under under **Objects synced by Status** and **Action**.

## Single user view

The user provisioning view tab allows you to get synchronization data on individual users.

Note

This section does not involve using source and target.

In this section, you enter a time range and select a specific user to see which applications a user has been provisioned or deprovisioned in.

Once you select a time range, it will filter for users that have events in that time range.

To target a specific user, you can add one of the following parameters, for that user.

- UPN
- UserID

[![Screenshot of the single user view.](media/provisioning-workbook/single-user-1.png)](media/provisioning-workbook/single-user-1.png#lightbox)

## Details

By clicking on the Source ID in the **Sync details** or the **Sync details by cycle** views, you can see additional information on the object synchronized.

[![Screenshot of the details of an object.](media/provisioning-workbook/details-1.png)](media/provisioning-workbook/details-1.png#lightbox)

## Custom queries

You can create custom queries and show the data on Azure dashboards. To learn how, see [Create and share dashboards of Log Analytics data](/en-us/azure/azure-monitor/logs/get-started-queries). Also, be sure to check out [Overview of log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/log-query-overview).

## Custom alerts

Azure Monitor lets you configure custom alerts so that you can get notified about key events related to Provisioning. For example, you might want to receive an alert on spikes in failures. Or perhaps spikes in disables or deletes. Another example of where you might want to be alerted is a lack of any provisioning, which indicates something is wrong.

To learn more about alerts, see [Azure Monitor Log Alerts](/en-us/azure/azure-monitor/alerts/alerts-create-new-alert-rule).