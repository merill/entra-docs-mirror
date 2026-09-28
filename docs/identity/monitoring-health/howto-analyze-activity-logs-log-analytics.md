---
layout: Conceptual
title: Analyze activity logs using Log Analytics - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-analyze-activity-logs-log-analytics
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to analyze audit, sign-in, and provisioning logs Microsoft Entra ID using Log Analytics queries.
ms.topic: how-to
ms.date: 2026-02-27T00:00:00.0000000Z
ms.reviewer: egreenberg
ms.custom: sfi-image-nochange
locale: en-us
document_id: 7b7f4494-1ed0-73a2-e082-f75f47fecc00
document_version_independent_id: 87ac78a7-6c23-36a9-ce75-341ae1f6ecb0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-analyze-activity-logs-log-analytics.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-analyze-activity-logs-log-analytics
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-analyze-activity-logs-log-analytics.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6b52ea7b-6529-fb3c-37db-106dcb06fffb
---

# Analyze activity logs using Log Analytics - Microsoft Entra ID | Microsoft Learn

After you [integrate Microsoft Entra activity logs with Azure Monitor logs](howto-integrate-activity-logs-with-azure-monitor-logs), you can use the power of Log Analytics and Azure Monitor logs to gain insights into your environment.

- Compare your Microsoft Entra sign-in logs against security logs published by Microsoft Defender for Cloud.
- Troubleshoot performance bottlenecks on your application’s sign-in page by correlating application performance data from Azure Application Insights.
- Analyze the Identity Protection risky users and risk detections logs to detect threats in your environment.

This article describes to analyze the Microsoft Entra activity logs in your Log Analytics workspace.

## Prerequisites

To analyze activity logs with Log Analytics, you need:

- A working Microsoft Entra tenant with a Microsoft Entra ID P1 or P2 license associated with it.
- A Log Analytics workspace *and* access to that workspace
- The appropriate roles for Azure Monitor *and* Microsoft Entra ID

### Log Analytics workspace

You must create a [Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace). There are several factors that determine access to Log Analytics workspaces. You need the right roles for the workspace *and* the resources sending the data.

For more information, see [Manage access to Log Analytics workspaces](/en-us/azure/azure-monitor/logs/manage-access).

### Azure Monitor roles

Azure Monitor provides [two built-in roles](/en-us/azure/azure-monitor/roles-permissions-security#monitoring-reader) for viewing monitoring data and editing monitoring settings. Azure role-based access control (RBAC) also provides two Log Analytics built-in roles that grant similar access.

- **View**:

    - Monitoring Reader
    - Log Analytics Reader
- **View and modify settings**:

    - Monitoring Contributor
    - Log Analytics Contributor

For more information on the Azure Monitor built-in roles, see [Roles, permissions, and security in Azure Monitor](/en-us/azure/azure-monitor/roles-permissions-security#monitoring-reader).

For more information on the Log Analytics roles, see [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles#log-analytics-contributor)

### Microsoft Entra roles

Read only access allows you to view Microsoft Entra ID log data inside a workbook, query data from Log Analytics, or read logs in the Microsoft Entra admin center. Update access adds the ability to create and edit diagnostic settings to send Microsoft Entra data to a Log Analytics workspace.

- **Read**:

    - Reports Reader
    - Security Reader
    - Global Reader
- **Update**:

    - Security Administrator

For more information on Microsoft Entra built-in roles, see [Microsoft Entra built-in roles](../role-based-access-control/permissions-reference).

## Access Log Analytics

To view the Microsoft Entra ID Log Analytics, you must already be sending your activity logs from Microsoft Entra ID to a Log Analytics workspace. This process is covered in the [How to integrate activity logs with Azure Monitor](howto-integrate-activity-logs-with-azure-monitor-logs) article.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Log Analytics**. A default search query runs.

    ![Default query](media/howto-analyze-activity-logs-log-analytics/default-query.png)
3. Expand the **LogManagement** category to view the list of log related queries.
4. Select or hover over the name of a query to view a description and other useful details.
5. Expand a query from the list to view the schema.

    ![Screenshot of the schema of a query.](media/howto-analyze-activity-logs-log-analytics/log-analytics-query-schema.png)

## Query activity logs

You can run queries against the activity logs being routed to a Log Analytics workspace. For example, to get a list of applications with the most sign-ins from last week, enter the following query and select the **Run** button.

```kusto
SigninLogs 
| where CreatedDateTime >= ago(7d)
| summarize signInCount = count() by AppDisplayName
| sort by signInCount desc 
```

To find risky sign-in events, use the following query:

```kusto
SigninLogs
| where RiskState contains "atRisk"
```

To get the top audit events over the last week, use the following query:

```kusto
AuditLogs 
| where TimeGenerated >= ago(7d)
| summarize auditCount = count() by OperationName 
| sort by auditCount desc 
```

To summarize the count of provisioning events per day, by action:

```kusto
AADProvisioningLogs
| where TimeGenerated > ago(7d)
| summarize count() by Action, bin(TimeGenerated, 1d)
```

Take 100 provisioning events and project key properties:

```kusto
AADProvisioningLogs
| extend SourceIdentity = parse_json(SourceIdentity)
| extend TargetIdentity = parse_json(TargetIdentity)
| extend ServicePrincipal = parse_json(ServicePrincipal)
| where tostring(SourceIdentity.identityType) == "Group"
| project tostring(ServicePrincipal.Id), tostring(ServicePrincipal.Name), ModifiedProperties, JobId, Id, CycleId, ChangeId, Action, SourceIdentity.identityType, SourceIdentity.details, TargetIdentity.identityType, TargetIdentity.details, ProvisioningSteps
| take 100
```

## Multiple sign-in records in Log Analytics

When you analyze Microsoft Entra ID sign-in logs, you might notice that Log Analytics shows multiple records for a single user sign-in, while the Microsoft Entra ID sign-in logs view displays only one. This behavior is expected.

### Why multiple records appear

During an interactive sign-in, a user might generate several requests that all share the same correlation ID. For example:

1. The user tries to sign in and is prompted for multifactor authentication (MFA).
2. The first MFA attempt fails.
3. The user retries MFA and succeeds.

In the Microsoft Entra ID sign-in logs, these related requests are merged into a single sign-in event. The portal aggregates all activity with the same correlation ID and reports the final outcome, so the sign-in appears as successful.

Every request is sent individually, which means Log Analytics shows:

- The intermediate failure entries.
- The final successful entry.

All entries share the same correlation ID.

### Interpret these logs

Because Log Analytics displays each request, it might seem like there are duplicates. However, these entries are distinct steps of a single sign-in flow.

To interpret these events correctly:

1. Group all records by correlation ID.
2. Use the final status for that correlation ID as the effective result.
3. Optionally, merge records in KQL to create an aggregated view similar to the Microsoft Entra admin center.

The following example shows how to merge records by correlation ID:

```kusto
SigninLogs
| summarize
    FirstSeen = min(TimeGenerated),
    LastSeen = max(TimeGenerated),
    FinalStatus = arg_max(TimeGenerated, ResultType, ConditionalAccessStatus),
    Count = count()
    by CorrelationId, UserPrincipalName
```