---
layout: Conceptual
title: How to use enriched Microsoft 365 logs - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-view-enriched-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: View performance, experience, and availability insights for Microsoft 365 apps routed through Microsoft Entra Internet Access. Integrate enriched log data with Log Analytics or Microsoft Sentinel for network diagnostics and security analysis.
ms.topic: how-to
ms.date: 2026-05-27T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 025acd7e-54e5-5de7-d41f-8af02a835f40
document_version_independent_id: 3352d1ac-9e15-c7eb-6cdc-ba0f8ca80475
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-view-enriched-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-view-enriched-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-view-enriched-logs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e2c9f30c-00ec-44c0-846c-b20dbfb3283f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/702271fe-87d7-4493-828b-2d6fde3de8ab
platformId: ddc148d2-244c-cb33-e820-9e537006143a
---

# How to use enriched Microsoft 365 logs - Global Secure Access | Microsoft Learn

## Overview

With your Microsoft traffic flowing through the Microsoft Entra Internet Access for Microsoft Services, you want to gain insights into the performance, experience, and availability of the Microsoft 365 apps your organization uses. With Global Secure Access, Microsoft 365 Audit logs can be easily enriched with the information you need to gain these insights. You can integrate the logs with a third-party security information and event management (SIEM) tool for further analysis.

This article describes the information in the logs and how to use them for the above insights.

## Prerequisites

To use the enriched logs, you need the following roles, configurations, and subscriptions:

### Required roles and permissions

- A **Security Administrator** role is required to export Global Secure Access Network Traffic Logs in Diagnostic Settings.

### Required configurations

- **Microsoft Profile** - Ensure the Microsoft traffic profile is enabled. Microsoft traffic forwarding profile is required to capture traffic directed to Microsoft 365 services, which is fundamental for log enrichment.
- **Tenant sending data** - Confirms that traffic, as configured in forwarding profiles, is accurately tunneled to the Global Secure Access service.
- **Diagnostic Settings Configuration** - Set up Microsoft Entra diagnostic settings to channel the logs to a designated endpoint, like a Log Analytics workspace or Sentinel workspace. The requirements for each endpoint differ and are outlined in the Configure Diagnostic settings section of this article.
- **Export the OfficeActivity log table** - The OfficeActivity table must be exported to the same LogAnalytics or Microsoft Sentinel workspace as the GSA traffic logs, or another third-party SIEM or Log system.

### Required subscriptions

- The product requires licensing to enable the traffic forwarding profile for Microsoft Services. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

You must configure the endpoint for where you want to route the logs prior to configuring Diagnostic settings. The requirements for each endpoint vary and are described in the Configure Diagnostic settings section.

## What the logs provide

Microsoft 365 audit logs provide information about Microsoft 365 workloads, so you can review network diagnostic data, performance data, and security events relevant to Microsoft 365 apps. With the enriched properties from Global Secure Access log data includes device information related to the user activities. For example, if access to Microsoft 365 is blocked for a user in your organization, you need visibility into how the user's device is connecting to your network.

These logs provide:

- Additional information added to original logs
- Accurate IP address

After you enable the Microsoft traffic forwarding profile and configure diagnostic settings, the logs include the device ID, operating system, and original IP address. Enriched SharePoint logs provide information on files that were downloaded, uploaded, deleted, modified, or recycled. Deleted or recycled list items are also included in the enriched logs.

## How to view the logs

Viewing enriched Microsoft 365 audit logs is a one-time, two-step process. First, you need to collect Global Secure Access Network Traffic logs and Microsoft 365 Unified Audit logs to the same endpoint (Microsoft Sentinel is the recommended workspace). Second, you need to create your own join query to correlate the data between the two tables or use Global Secure Access OOTB Enriched Microsoft 365 Logs workbook that already applies the needed queries.

Note

At this time, only SharePoint Online logs are available for log enrichment.

Note

MS365 audit logs have undergone a feature change. Instead of creating a separate new stream of logs, you can now leverage the two existing log tables — Microsoft 365 OfficeActivity and Global Secure Access NetworkAccessTraffic tables — then combine the data using a Unique Token ID.

### Configure Diagnostic settings

To view the enriched Microsoft 365 logs, you must export or stream the logs to an endpoint, such as a Log Analytics workspace or a SIEM tool. The endpoint must be configured before you can configure Diagnostic settings.

### Configure an endpoint

- To integrate logs with Log Analytics, you need a Log Analytics workspace.

    - [Create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace).
    - [Integrate logs with Log Analytics](/en-us/azure/active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics)
- To stream logs to a SIEM tool, you need to create an Azure event hub and an event hub namespace.

    - [Set up an Event Hubs namespace and an event hub](/en-us/azure/event-hubs/event-hubs-create).
    - [Stream logs to an event hub](/en-us/azure/active-directory/reports-monitoring/tutorial-azure-monitor-stream-logs-to-event-hub)
- To archive logs to a storage account, you need an Azure storage account that you have `ListKeys` permissions for.

    - [Create an Azure storage account](/en-us/azure/storage/common/storage-account-create).
    - [Archive logs to a storage account](/en-us/azure/active-directory/reports-monitoring/quickstart-azure-monitor-route-logs-to-storage-account)

### Send logs to an endpoint

With your endpoint created, you can configure Diagnostic settings.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](/en-us/azure/active-directory/roles/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**.
3. Select **Add Diagnostic setting**.
4. Give your diagnostic setting a name.
5. Select `NetworkAccessTrafficLogs`.
6. Select the **Destination details** for where you'd like to send the logs. Choose any or all of the following destinations. More fields appear, depending on your selection.

    - **Send to Log Analytics workspace:** Select the appropriate details from the menus that appear.
    - **Archive to a storage account:** Provide the number of days you'd like to retain the data in the **Retention days** boxes that appear next to the log categories. Select the appropriate details from the menus that appear.
    - **Stream to an event hub:** Select the appropriate details from the menus that appear.
    - **Send to partner solution:** Select the appropriate details from the menus that appear.