---
layout: Conceptual
title: Learn how Provisioning logs integrate with Azure Monitor - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/application-provisioning-log-analytics
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to integrate Microsoft Entra Provisioning logs with Azure Monitor logs and use the associated workbooks.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: arvinh
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8f92fb91-8836-bbed-569e-c07661beae97
document_version_independent_id: c45e65db-c688-c61c-103c-54fea44666ed
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/application-provisioning-log-analytics.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/application-provisioning-log-analytics
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/application-provisioning-log-analytics.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/9949a35d-c893-4f91-bf98-ae940fc30f5f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/21f7bb14-0703-4e59-a64b-65dd13773dd3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bff6d8f8-6b8c-0fd2-a0f4-bff12003e5fc
---

# Learn how Provisioning logs integrate with Azure Monitor - Microsoft Entra ID | Microsoft Learn

Provisioning integrates with Azure Monitor logs and Log Analytics. With Azure monitoring you can do things like create workbooks, also known as dashboards, store provisioning logs for 30+ days, and create custom queries and alerts. This article discusses how provisioning logs integrate with Azure Monitor logs. To learn more about how provisioning logs work in general, see [provisioning logs](../monitoring-health/concept-provisioning-logs).

## Enabling provisioning logs integration

If you're not already familiar with Azure Monitor and Log Analytics, explore the following resources and then come back to learn about integrating application provisioning logs with Azure Monitor logs.

- [Azure Monitor overview](/en-us/azure/azure-monitor/overview)
- [Configure a Log Analytics workspace](../monitoring-health/tutorial-configure-log-analytics-workspace)
- [Integrate activity logs with Azure Monitor logs](../monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs)

To integrate provisioning logs with Azure Monitor logs:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. [Create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace).
3. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**.

    [![Screenshot of accessing diagnostic settings.](media/application-provisioning-log-analytics/diagnostic-settings.png)](media/application-provisioning-log-analytics/diagnostic-settings.png#lightbox)
4. Choose the logs you want to stream, select the **Send to Log Analytics workspace** option, and complete the fields.

    [![Screenshot of enabling application provisioning logs.](media/application-provisioning-log-analytics/enable-log-analytics.png)](media/application-provisioning-log-analytics/enable-log-analytics.png#lightbox)
5. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Log Analytics** and begin querying the data.

Note

It can take some time before logs appear in Log Analytics after first enabling the integration. If you receive an error that the subscription is not registered to use *microsoft.insights* then check back after a few minutes.

## Understanding the data

The underlying data stream that Provisioning sends log viewers is almost identical. Azure Monitor logs gets nearly the same stream as the Microsoft Entra admin center and the Microsoft Graph API. There are a few differences in the log fields as outlined in the following table. Log Analytics might display more events than the logs in the Microsoft Entra admin center. To learn more about these fields, see [List provisioningObjectSummary](/en-us/graph/api/provisioningobjectsummary-list?preserve-view=true&amp;tabs=http&amp;view=graph-rest-beta).

| Azure Monitor logs | Azure portal UI | Azure API |
| --- | --- | --- |
| errorDescription | reason | resultDescription |
| status | resultType | resultType |
| activityDateTime | TimeGenerated | TimeGenerated |

## Microsoft Entra workbooks

Microsoft Entra identity workbooks provide a flexible canvas for data analysis. They also provide for the creation of rich visual reports within the Azure portal. To learn more, see [Microsoft Entra workbooks](../monitoring-health/overview-workbooks).

The **Provisioning Analysis** and **Provisioning Insights** are two of the prebuilt workbooks available. To view the data, ensure that all the filters (timeRange, jobID, appName) are populated. Also confirm the app was provisioned, otherwise there isn't any data in the logs.

[![Application provisioning workbooks](media/application-provisioning-log-analytics/workbooks.png)](media/application-provisioning-log-analytics/workbooks.png#lightbox)

[![Application provisioning dashboard](media/application-provisioning-log-analytics/report.png)](media/application-provisioning-log-analytics/report.png#lightbox)

## Custom queries

You can create custom queries and show the data in your workbooks. To learn how, see [Get started with log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/get-started-queries) and [Log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/log-query-overview).

Here are some samples to get started with application provisioning log queries.

Query the logs for a user a based on their ID in the source system:

```kusto
AADProvisioningLogs
| extend SourceIdentity = parse_json(SourceIdentity)
| where tostring(SourceIdentity.Id) == "49a4974bb-5011-415d-b9b8-78caa7024f9a"
```

Summarize count per ErrorCode:

```kusto
AADProvisioningLogs
| summarize count() by ErrorCode = ResultSignature
```

Summarize count of events per day by action:

```kusto
AADProvisioningLogs
| where TimeGenerated > ago(7d)
| summarize count() by Action, bin(TimeGenerated, 1d)
```

Take 100 events and project key properties:

```kusto
AADProvisioningLogs
| extend SourceIdentity = parse_json(SourceIdentity)
| extend TargetIdentity = parse_json(TargetIdentity)
| extend ServicePrincipal = parse_json(ServicePrincipal)
| where tostring(SourceIdentity.identityType) == "Group"
| project tostring(ServicePrincipal.Id), tostring(ServicePrincipal.Name), ModifiedProperties, JobId, Id, CycleId, ChangeId, Action, SourceIdentity.identityType, SourceIdentity.details, TargetIdentity.identityType, TargetIdentity.details, ProvisioningSteps
| take 100
```

Retrieve groups with skipped members due to problems resolving references.

```kusto
AADProvisioningLogs
| where TimeGenerated >= ago(10d)
| where JobId == "Azure2Azure.73f0883f-d67d-4af1-ac8a-45367f8982e0.5ef3be57-f45f-451g-88c4-68a7fda680bb" // Customize by adding a specific app JobId
| extend SourceIdentity = parse_json(SourceIdentity)
| extend ProvisioningSteps = parse_json(ProvisioningSteps)
| where tostring(SourceIdentity.identityType) == "Group"
| where ProvisioningSteps matches regex "UnableToResolveReferenceAttributeValue"
| parse tostring(ProvisioningSteps.[2].description) with "We were unable to assign " userObjectId " as the members of " groupDisplayName "." *
| project groupDisplayName, userObjectId,  JobId
| take 100
```

Summarize actions by application.

```kusto
AADProvisioningLogs
| where TimeGenerated > ago(30d)
| where JobId == "Azure2Azure.73f0883f-d67d-4af1-ac8a-45367f8982e0.5ef3be57-f45f-451g-88c4-68a7fda680bb" // Customize by adding a specific app JobId
| extend ProvisioningSteps = parse_json(ProvisioningSteps)
| extend eventName = tostring(ProvisioningSteps.[-1].name)
| summarize count() by eventName, JobId
| order by JobId asc
| take 5
```

Identify spikes in specific operations.

```kusto
AADProvisioningLogs
| where TimeGenerated > ago(30d)
| where JobId == "scim.73f0883f-d67d-4af1-ac8a-45367f8982e0.5ef3be57-f45f-451g-88c4-68a7fda680bb" // Customize by adding a specific app JobId
| extend ProvisioningSteps = parse_json(ProvisioningSteps)
| extend eventName = tostring(ProvisioningSteps.[-1].name)
| summarize count() by eventName, bin(TimeGenerated, 1d)
| render timechart
```

## Custom alerts

Azure Monitor lets you configure custom alerts so that you can get notified about key events related to Provisioning. For example, you might want to receive an alert on spikes in failures spikes in disables or deletes. You might also want to be alerted if there's a lack of any provisioning, which indicates something is wrong.

To learn more about alerts, see [Azure Monitor Log Alerts](/en-us/azure/azure-monitor/alerts/alerts-create-new-alert-rule). There are many options and configurations, so review the full documentation. But at a high-level, here's how you can create an alert:

1. From Log Analytics, select **+ New alert rule**.
2. On the **Condition** tab, select the **View result and edit query in Logs** link.
3. Enter a query you want to alert on, and complete the necessary fields to create the alert.

To create an alert when there's a spike in failures:

```kusto
AADProvisioningLogs
| where JobId == "string" // Customize by adding a specific app JobId
| where ResultType == "Failure"
```

There might be an issue that caused the provisioning service to stop running. Use the following query to detect when there are no provisioning events during a given time interval.

```kusto
AADProvisioningLogs
| take 1
```

To create an alert when there's a spike in disables or deletes:

```kusto
AADProvisioningLogs
| where Action in ("Disable", "Delete")
```

## Community contributions

We're taking an open source and community-based approach to application provisioning queries and dashboards. Build a query, alert, or workbook that you think is useful to others, then publish it to the [AzureMonitorCommunity GitHub repo](https://github.com/microsoft/AzureMonitorCommunity). Shoot us an email with a link. We review and publish queries and dashboards to the service so others benefit too. Contact us at provisioningfeedback@microsoft.com.