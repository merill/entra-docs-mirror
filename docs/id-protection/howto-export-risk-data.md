---
layout: Conceptual
title: Export and use Microsoft Entra ID Protection data - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/howto-export-risk-data
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Learn about the many long-term data storage and monitoring options for exporting risk data from Microsoft Entra ID Protection.
ms.topic: how-to
ms.date: 2025-09-30T00:00:00.0000000Z
ms.reviewer: cokoopma
ms.custom: sfi-image-nochange
locale: en-us
document_id: 14f075d9-b1f5-3de1-29df-9323cfc2d72a
document_version_independent_id: b33007d8-8761-2930-72ea-fa8e6cf52c27
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/howto-export-risk-data.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/howto-export-risk-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/howto-export-risk-data.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: f49bb745-8fe6-fee2-6ece-923420c09712
---

# Export and use Microsoft Entra ID Protection data - Microsoft Entra ID Protection | Microsoft Learn

Microsoft Entra ID stores reports and security signals for a defined period of time. When it comes to risk information, that period might not be long enough.

| Report / Signal | Microsoft Entra ID Free | Microsoft Entra ID P1 | Microsoft Entra ID P2 |
| --- | --- | --- | --- |
| Audit logs | 7 days | 30 days | 30 days |
| Sign-ins | 7 days | 30 days | 30 days |
| Microsoft Entra multifactor authentication usage | 30 days | 30 days | 30 days |
| Risky sign-ins | 7 days | 30 days | 30 days |

This article describes the available methods for exporting risk data from Microsoft Entra ID Protection for long-term storage and analysis.

## Prerequisites

To export risk data for storage and analysis, you need:

- An Azure subscription to create a Log Analytics workspace, Azure event hub, or Azure storage account. If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- The [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator) role is the least privileged role required to **configure diagnostic settings for the Microsoft Entra tenant**.

## Diagnostic settings

Organizations can choose to store or export **RiskyUsers**, **UserRiskEvents**, **RiskyServicePrincipals**, **ServicePrincipalRiskEvents**, **RiskyAgents**, and **AgentRiskEvents** data by configuring diagnostic settings in Microsoft Entra ID to export the data. You can integrate the data with a Log Analytics workspace, archive data to a storage account, stream data to an event hub, or send data to a partner solution.

The endpoint you select for exporting the logs must be set up before you can configure diagnostic settings. For a quick summary of the methods available for log storage and analysis, see [How to access activity logs in Microsoft Entra ID](../identity/monitoring-health/howto-access-activity-logs).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**.
3. Select **+ Add diagnostic setting**.
4. Enter a **Diagnostic setting name**, select the log categories that you want to stream, select a previously configured destination, and select **Save**.

[![Screenshot of the diagnostic settings screen in Microsoft Entra ID.](media/howto-export-risk-data/change-diagnostic-setting-in-portal.png)](media/howto-export-risk-data/change-diagnostic-setting-in-portal.png#lightbox)

You might need to wait around 15 minutes for the data to start appearing in the destination you selected. For more information, see [How to configure Microsoft Entra diagnostic settings](../identity/monitoring-health/howto-configure-diagnostic-settings).

## Log Analytics

Integrating risk data with Log Analytics provides robust data analysis and visualization capabilities. The high-level process for using Log Analytics to analyze risk data is as follows:

1. [Create a Log Analytics workspace](../identity/monitoring-health/tutorial-configure-log-analytics-workspace).
2. [Configure Microsoft Entra diagnostic settings to export the data](../identity/monitoring-health/howto-configure-diagnostic-settings).
3. [Query the data in Log Analytics](/en-us/azure/azure-monitor/logs/get-started-queries).

You need to configure a Log Analytics workspace before you can export and then query the data. Once you configured a Log Analytics workspace and exported the data with diagnostic settings, go to [Microsoft Entra admin center](https://entra.microsoft.com) &gt; **Entra ID** &gt; **Monitoring & health** &gt; **Log Analytics**. Then, with Log Analytics, you can query data using built-in or custom Kusto queries.

Important

The names you select in **diagnostic settings** are not the same as the **table names** you use in Kusto (KQL) queries.

- **Diagnostic setting category** = what you enable for export
- **Log Analytics table name** = what you query (usually prefixed with `AAD`)

### Diagnostic setting categories vs Log Analytics table names

Use this mapping when you enable export and when you write queries:

| Report / signal | Diagnostic setting category (enable export) | Log Analytics table name (use in queries) | Table reference |
| --- | --- | --- | --- |
| Risky users | `RiskyUsers` | `AADRiskyUsers` | [AADRiskyUsers](/en-us/azure/azure-monitor/reference/tables/aadriskyusers) |
| Risk detections (users) | `UserRiskEvents` | `AADUserRiskEvents` | [AADUserRiskEvents](/en-us/azure/azure-monitor/reference/tables/aaduserriskevents) |
| Risky workload identities | `RiskyServicePrincipals` | `AADRiskyServicePrincipals` | [AADRiskyServicePrincipals](/en-us/azure/azure-monitor/reference/tables/aadriskyserviceprincipals) |
| Workload identity detections | `ServicePrincipalRiskEvents` | `AADServicePrincipalRiskEvents` | [AADServicePrincipalRiskEvents](/en-us/azure/azure-monitor/reference/tables/aadserviceprincipalriskevents) |
| Risky agents | `RiskyAgents` | `AADRiskyAgents` | [AADRiskyAgents](/en-us/azure/azure-monitor/reference/tables/aadriskyagents) |
| Agent identity detections | `AgentRiskEvents` | `AADAgentRiskEvents` | [AADAgentRiskEvents](/en-us/azure/azure-monitor/reference/tables/aadagentriskevents) |

Note

Log Analytics only has visibility into data as it is streamed. Events prior to enabling the sending of events from Microsoft Entra ID don't appear.

### Sample queries

[![Screenshot of Log Analytics view showing an AADUserRiskEvents query for the top 5 events.](media/howto-export-risk-data/log-analytics-view-query-user-risk-events.png)](media/howto-export-risk-data/log-analytics-view-query-user-risk-events.png#lightbox)

In the previous image, the following query was run to show the most recent five risk detections triggered.

```kusto
AADUserRiskEvents
| take 5
```

Another option is to query the AADRiskyUsers table to see all risky users.

```kusto
AADRiskyUsers
```

View the count of high risk users by day:

```kusto
AADUserRiskEvents
| where TimeGenerated > ago(30d)
| where RiskLevel has "high"
| summarize count() by bin (TimeGenerated, 1d)
```

View helpful investigation details, such as user agent string, for detections that are high risk and aren't remediated or dismissed:

```kusto
AADUserRiskEvents
| where RiskLevel has "high"
| where RiskState has "atRisk"
| mv-expand ParsedFields = parse_json(AdditionalInfo)
| where ParsedFields has "userAgent"
| extend UserAgent = ParsedFields.Value
| project TimeGenerated, UserDisplayName, Activity, RiskLevel, RiskState, RiskEventType, UserAgent,RequestId
```

Access more queries and visual insights based on AADUserRiskEvents and AADRisky Users logs in the [Impact analysis of risk-based access policies workbook](workbook-risk-based-policy-impact).

### Risk analysis

Organizations can reduce security operations center (SOC) workloads and support overhead with risk-based Conditional Access policies. Learn more in the following video, **Mastering risk analysis with Microsoft Entra ID Protection**.

## Storage account

By routing logs to an Azure storage account, you can keep data for longer than the default retention period.

1. [Create an Azure storage account](/en-us/azure/storage/common/storage-account-create).
2. [Archive Microsoft Entra logs to a storage account](../identity/monitoring-health/howto-archive-logs-to-storage-account).

## Azure Event Hubs

Azure Event Hubs can look at incoming data from sources like Microsoft Entra ID Protection and provide real-time analysis and correlation.

1. [Create an Azure event hub](/en-us/azure/event-hubs/event-hubs-create).
2. [Stream Microsoft Entra logs to an event hub](../identity/monitoring-health/howto-stream-logs-to-event-hub).

## Microsoft Sentinel

Organizations can choose to [connect Microsoft Entra data to Microsoft Sentinel](/en-us/azure/sentinel/data-connectors/azure-active-directory-identity-protection) for security information and event management (SIEM) and security orchestration, automation, and response (SOAR).

1. [Create a Log Analytics workspace](../identity/monitoring-health/tutorial-configure-log-analytics-workspace).
2. [Configure Microsoft Entra diagnostic settings to export the data](../identity/monitoring-health/howto-configure-diagnostic-settings).
3. [Connect data sources to Microsoft Sentinel](/en-us/azure/sentinel/configure-data-connector).