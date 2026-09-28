---
layout: Conceptual
title: How to use workbooks with Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-use-workbooks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Workbooks provide rich, interactive reports for Global Secure Access. Learn how to integrate workbooks with log analytics for Global Secure Access.
ms.topic: how-to
ms.date: 2026-06-04T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 77531804-4b7d-8d09-38b7-d42e05d32fa7
document_version_independent_id: 77531804-4b7d-8d09-38b7-d42e05d32fa7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-use-workbooks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-use-workbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-use-workbooks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 53103726-4ca9-d4be-c9c4-c7a5ca45c1d5
---

# How to use workbooks with Global Secure Access - Global Secure Access | Microsoft Learn

## Overview

Workbooks combine text, log queries, metrics, and parameters into rich interactive reports. Any team member with access to the required Azure resources can create and edit workbooks. For more information about Azure Workbooks, see [Overview of Azure Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview).

## Prerequisites

- Administrators who interact with **Global Secure Access**features must have one or more of the following role assignments depending on the tasks they're performing.
    - The [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference) role to manage the Global Secure Access features.
    - The [Security Administrator](/en-us/azure/active-directory/roles/permissions-reference#security-administrator) to create, edit, and use workbooks.
- An existing Log Analytics workspace. For more information about Log Analytics, see [Overview of Log Analytics in Azure Monitor](/en-us/azure/azure-monitor/logs/log-analytics-overview).
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## Export Global Secure Access information to Log Analytics

Global Secure Access workbooks integrate with Log Analytics. This integration allows you to monitor and analyze logs effectively. For more information about Global Secure Access log integration with Log Analytics, see [Integrate Microsoft Entra logs with Azure Monitor logs](../identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs).

For information on how to send log information to Log Analytics, see [Send logs to Azure Monitor](../identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs#send-logs-to-azure-monitor).

The Global Secure Access categories are:

| Log type | Diagnostic settings category |
| --- | --- |
| Traffic logs | `NetworkAccessTrafficLogs` |
| Audit logs (Preview) | `AuditLogs` |
| Enriched Microsoft 365 logs (Preview) | `EnrichedOffice365AuditLogs` |
| Remote Network Health Logs (Preview) | `RemoteNetworkHealthLogs` |
| Generative AI Insights logs (Preview) | `NetworkAccessGenerativeAIInsights` |

[![Screenshot of the Microsoft Entra diagnostic settings, with the Global Secure Access logs categories selected.](media/how-to-use-workbooks/add-diagnostic-setting.png)](media/how-to-use-workbooks/add-diagnostic-setting.png#lightbox)

## View Global Secure Access workbooks

In the Microsoft Entra admin center, navigate to **Global Secure Access** &gt; **Monitor** &gt; **Workbooks** to view predefined workbooks. Note that you won't see the workbooks unless logging data has been captured.

**Network Traffic Insights workbook** - Provides an overview of all traffic logs within your network, offering insights into data transfer, anomalies, and potential threats.

**Remote Network Health workbook** - Monitors the health and performance of remote networks, ensuring that all remote connections are reliable and secure.

**Clients Activity and Status workbook** - Offers an overview of the clients connected to your network, including their health status and activity levels.

**Discovered Application Segments workbook** - Identifies and categorizes application segments discovered within your network, aiding in effective monitoring and management of applications.

**Enriched Microsoft 365 Logs workbook** - Provides a detailed view of Microsoft 365 log data, enriched with contextual information to enhance visibility into user activities and potential security threats.