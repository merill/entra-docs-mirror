---
layout: Conceptual
title: Microsoft Entra Connect cloud sync insights workbook - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-cloud-sync-workbook
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes the Azure Monitor workbook for cloud sync.
ms.topic: concept-article
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ms.custom: sfi-image-nochange
locale: en-us
document_id: 83081d5d-6141-2774-b56d-7bada0b5f562
document_version_independent_id: 39949466-ba9c-34d6-e4e4-7e7655ce5590
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-cloud-sync-workbook.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-cloud-sync-workbook
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-cloud-sync-workbook.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d4a00294-47bc-2d4f-5640-cf64c16ad75a
---

# Microsoft Entra Connect cloud sync insights workbook - Microsoft Entra ID | Microsoft Learn

The cloud sync workbook provides a flexible canvas for data analysis. The workbook allows you to create rich visual reports within the Microsoft Entra admin center. To learn more, see Azure Monitor Workbooks overview.

This workbook is intended for Hybrid Identity Administrators who use cloud sync to sync users from AD to Microsoft Entra ID. It allows admins to gain insights into sync status and details.

The workbook can be accessed by select **Insights** on the left hand side of the cloud sync page.

Note

The Insights node is available at both the all configurations level and the individual configuration level. To view information on individual configurations select the Job Id for the configuration.

This workbook:

- Provides a synchronization summary of users and groups synchronized from AD to Microsoft Entra ID
- Provides a detailed view of information captured by the cloud sync provisioning logs.
- Allows you to customize the data to tailor it to your specific needs

| Field | Description |
| --- | --- |
| Date | The range that you want to view data on. |
| Status | View the provisioning status such as Success or Skipped. |
| Action | View the provisioning actions taken such as Create or Delete. |
| Job Id | Allows you to target specific Job Ids. This can be used to see individual configuration data if you have multiple configurations. |
| SyncType | Filter by type of synchronization such as object or password. |

## Enabling provisioning logs

You should already be familiar with Azure monitoring and Log Analytics. If not, jump over to learn about them, and then come back to learn about application provisioning logs. To learn more about Azure monitoring, see [Azure Monitor overview](/en-us/azure/azure-monitor/overview). To learn more about Azure Monitor logs and Log Analytics, see [Overview of log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/log-query-overview) and [Provisioning Logs for troubleshooting cloud sync](how-to-troubleshoot).

## Sync summary

The sync summary section provides a summary of your organizations synchronization activities. These activities include:

- Sync actions per day by action
- Sync actions per day by status
- Unique sync count by status
- Recent sync errors

[![Screenshot of the cloud sync summary.](media/how-to-cloud-sync-workbook/workbook-2.png)](media/how-to-cloud-sync-workbook/workbook-2.png#lightbox)

## Sync details

The sync details tab allows you to drill into the synchronization data and get more information. This information includes:

- Objects sync by status
- Sync log details

[![Screenshot of the cloud sync details.](media/how-to-cloud-sync-workbook/workbook-3.png)](media/how-to-cloud-sync-workbook/workbook-3.png#lightbox)

You can further drill in to the sync log details for additional information.

[![Screenshot of the log details.](media/how-to-cloud-sync-workbook/workbook-4.png)](media/how-to-cloud-sync-workbook/workbook-4.png#lightbox)

## Job Id

A Job Id is created for each configuration when it runs and is populated with data. You can look at individual configuration based on Job Id.

## Custom queries

You can create custom queries and show the data on Azure dashboards. To learn how, see [Create and share dashboards of Log Analytics data](/en-us/azure/azure-monitor/logs/get-started-queries). Also, be sure to check out [Overview of log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/log-query-overview).

## Custom alerts

Azure Monitor lets you configure custom alerts so that you can get notified about key events related to Provisioning. For example, you might want to receive an alert on spikes in failures. Or perhaps spikes in disables or deletes. Another example of where you might want to be alerted is a lack of any provisioning, which indicates something is wrong.

To learn more about alerts, see [Azure Monitor Log Alerts](/en-us/azure/azure-monitor/alerts/alerts-create-new-alert-rule).