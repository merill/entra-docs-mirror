---
layout: Conceptual
title: Archive & report with Azure Monitor - entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-logs-and-reporting
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to archive logs and create reports with Azure Monitor in entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2024-07-15T00:00:00.0000000Z
ms.custom: devx-track-azurepowershell, sfi-ga-nochange
locale: en-us
document_id: 99e07c1a-ace1-9390-ace7-f142893274d5
document_version_independent_id: b4c79b75-4007-5472-6ae5-e7eb0584b000
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-logs-and-reporting.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-logs-and-reporting
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-logs-and-reporting.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7ad7a1d7-ab49-5103-acd9-52c2054d6d97
---

# Archive & report with Azure Monitor - entitlement management - Microsoft Entra ID Governance | Microsoft Learn

Microsoft Entra ID stores audit events for up for entitlement management and other Microsoft Entra ID Governance features to 30 days in the audit log. However, you can keep the audit data for longer than the default retention period, outlined in [How long does Microsoft Entra ID store reporting data?](../identity/monitoring-health/reference-reports-data-retention), by routing it to an Azure Storage account or using Azure Monitor. You can then use workbooks and custom queries and reports on this data.

This article outlines how to use Azure Monitor for audit log retention. To retain or report on Microsoft Entra objects, such as users or application role assignments, see [Customized reports in Azure Data Explorer (ADX) using data from Microsoft Entra ID](custom-entitlement-report-with-adx-and-entra-id).

## Configure Microsoft Entra ID to use Azure Monitor

Before you use the Azure Monitor workbooks, you must configure Microsoft Entra ID to send a copy of its audit logs to Azure Monitor.

Archiving Microsoft Entra audit logs requires you to have Azure Monitor in an Azure subscription. You can read more about the prerequisites and estimated costs of using Azure Monitor in [Microsoft Entra activity logs in Azure Monitor](../identity/monitoring-health/concept-log-monitoring-integration-options-considerations).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator). Make sure you have access to the resource group containing the Azure Monitor workspace.
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**.
3. Check if there's already a setting to send the audit logs to that workspace.
4. If there isn't already a setting, select **Add diagnostic setting**. Use the instructions in [Integrate Microsoft Entra logs with Azure Monitor logs](../identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs) to send the Microsoft Entra audit log to the Azure Monitor workspace.

    ![Diagnostics settings pane.](media/entitlement-management-logs-and-reporting/audit-log-diagnostics-settings.png)
5. After the log is sent to Azure Monitor, select **Log Analytics workspaces**, and select the workspace that contains the Microsoft Entra audit logs.
6. Select **Usage and estimated costs** and select **Data Retention**. Change the slider to the number of days you want to keep the data to meet your auditing requirements.

    ![Log Analytics workspaces pane.](media/entitlement-management-logs-and-reporting/log-analytics-workspaces.png)
7. Later, to see the range of dates held in your workspace, you can use the *Archived Log Date Range* workbook:

    1. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
    2. Expand the section **Microsoft Entra Troubleshooting**, and select on **Archived Log Date Range**.

## View events for an access package

To view events for an access package, you must have access to the underlying Azure monitor workspace (see [Manage access to log data and workspaces in Azure Monitor](/en-us/azure/azure-monitor/logs/manage-access#azure-rbac) for information) and in one of the following roles:

- Global Administrator
- Security Administrator
- Security Reader
- Reports Reader
- Application Administrator

Use the following procedure to view events:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../identity/role-based-access-control/permissions-reference#reports-reader). Make sure you have access to the resource group containing the Azure Monitor workspace.
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
3. If you have multiple subscriptions, select the subscription that contains the workspace.
4. Once you have selected the subscription, or if you only have one subscription, select the workbook named *Access Package Activity*.
5. In that workbook, select a time range (change to **All** if not sure), and select an access package ID from the drop-down list of all access packages that had activity during that time range. The events related to the access package that occurred during the selected time range is displayed.

    ![View access package events.](media/entitlement-management-logs-and-reporting/view-events-access-package.png)

    Each row includes the time, access package ID, the name of the operation, the object ID, UPN, and the display name of the user who started the operation. More details are included in JSON.
6. If you would like to see if there have been changes to application role assignments for an application that weren't due to access package assignments, such as by a Global Administrator directly assigning a user to an application role, then you can select the workbook named *Application role assignment activity*.

    ![View app role assignments.](media/entitlement-management-access-package-incompatible/workbook-ara.png)

## Create custom Azure Monitor queries using the Microsoft Entra admin center

You can create your own queries on Microsoft Entra audit events, including entitlement management events.

1. In Identity of the Microsoft Entra admin center, select **Logs** under the Monitoring section in the left navigation menu to create a new query page.
2. Your workspace should be shown in the upper left of the query page. If you have multiple Azure Monitor workspaces, and the workspace you're using to store Microsoft Entra audit events isn't shown, select **Select Scope**. Then, select the correct subscription and workspace.
3. Next, in the query text area, delete the string "search \*" and replace it with the following query:

    ```
    AuditLogs | where Category == "EntitlementManagement"
    ```
4. Then select **Run**.

    ![select Run to start query.](media/entitlement-management-logs-and-reporting/run-query.png)

The table shows the Audit log events for entitlement management from the last hour by default. You can change the "Time range" setting to view older events. However, changing this setting will only show events that occurred after Microsoft Entra ID was configured to send events to Azure Monitor.

If you would like to know the oldest and newest audit events held in Azure Monitor, use the following query:

```
AuditLogs | where TimeGenerated > ago(3653d) | summarize OldestAuditEvent=min(TimeGenerated), NewestAuditEvent=max(TimeGenerated) by Type
```

For more information on the columns that are stored for audit events in Azure Monitor, see [Interpret the Microsoft Entra audit logs schema in Azure Monitor](../identity/monitoring-health/overview-monitoring-health).

## Create custom Azure Monitor queries using Azure PowerShell

You can access logs through PowerShell after you configure Microsoft Entra ID to send logs to Azure Monitor. Then, send queries from scripts or the PowerShell command line, without needing to be a Global Administrator in the tenant.

### Ensure the user or service principal has the correct role assignment

Make sure you, the user or service principal that authenticates to Microsoft Entra ID, are in the appropriate Azure role in the Log Analytics workspace. The role options are either Log Analytics Reader or the Log Analytics Contributor. If you're already in one of those roles, then skip to Retrieve Log Analytics ID with one Azure subscription.

To set the role assignment and create a query, do the following steps:

1. In the Microsoft Entra admin center, locate the [Log Analytics workspace](https://entra.microsoft.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.OperationalInsights%2Fworkspaces).
2. Select **Access Control (IAM)**.
3. Then select **Add** to add a role assignment.

    ![Add a role assignment.](media/entitlement-management-logs-and-reporting/workspace-set-role-assignment.png)

### Install Azure PowerShell module

Once you have the appropriate role assignment, launch PowerShell, and [install the Azure PowerShell module](/en-us/powershell/azure/install-azure-powershell) (if you haven't already), by typing:

```azurepowershell
install-module -Name az -allowClobber -Scope CurrentUser
```

Now you're ready to authenticate to Microsoft Entra ID, and retrieve the ID of the Log Analytics workspace you're querying.

### Retrieve Log Analytics ID with one Azure subscription

If you have only a single Azure subscription, and a single Log Analytics workspace, then type the following to authenticate to Microsoft Entra ID, connect to that subscription, and retrieve that workspace:

```azurepowershell
Connect-AzAccount
$wks = Get-AzOperationalInsightsWorkspace
```

### Retrieve Log Analytics ID with multiple Azure subscriptions

[Get-AzOperationalInsightsWorkspace](/en-us/powershell/module/Az.OperationalInsights/Get-AzOperationalInsightsWorkspace) operates in one subscription at a time. So, if you have multiple Azure subscriptions, you want to make sure you connect to the one that has the Log Analytics workspace with the Microsoft Entra logs.

The following cmdlets display a list of subscriptions, and find the ID of the subscription that has the Log Analytics workspace:

```azurepowershell
Connect-AzAccount
$subs = Get-AzSubscription
$subs | ft
```

You can reauthenticate and associate your PowerShell session to that subscription using a command such as `Connect-AzAccount –Subscription $subs[0].id`. To learn more about how to authenticate to Azure from PowerShell, including non-interactively, see [Sign in with Azure PowerShell](/en-us/powershell/azure/authenticate-azureps).

If you have multiple Log Analytics workspaces in that subscription, then the cmdlet [Get-AzOperationalInsightsWorkspace](/en-us/powershell/module/az.operationalinsights/get-azoperationalinsightsworkspace) returns the list of workspaces. Then you can find the one that has the Microsoft Entra logs. The `CustomerId` field returned by this cmdlet is the same as the value of the "Workspace ID" displayed in the Microsoft Entra admin center in the Log Analytics workspace overview.

```powershell
$wks = Get-AzOperationalInsightsWorkspace
$wks | ft CustomerId, Name
```

### Send the query to the Log Analytics workspace

Finally, once you have a workspace identified, you can use [Invoke-AzOperationalInsightsQuery](/en-us/powershell/module/az.operationalinsights/invoke-azoperationalinsightsquery) to send a Kusto query to that workspace. These queries are written in [Kusto query language](/en-us/azure/data-explorer/kusto/query/).

For example, you can retrieve the date range of the audit event records from the Log Analytics workspace, with PowerShell cmdlets to send a query like:

```powershell
$aQuery = "AuditLogs | where TimeGenerated > ago(3653d) | summarize OldestAuditEvent=min(TimeGenerated), NewestAuditEvent=max(TimeGenerated) by Type"
$aResponse = Invoke-AzOperationalInsightsQuery -WorkspaceId $wks[0].CustomerId -Query $aQuery
$aResponse.Results |ft
```

You can also retrieve entitlement management events using a query like:

```azurepowershell
$bQuery = 'AuditLogs | where Category == "EntitlementManagement"'
$bResponse = Invoke-AzOperationalInsightsQuery -WorkspaceId $wks[0].CustomerId -Query $Query
$bResponse.Results |ft 
```

### Using query filters

You can include the `TimeGenerated` field to scope a query to a particular time range. For example, to retrieve the audit log events for entitlement management access package assignment policies being created or updated in the last 90 days, you can supply a query that includes this field as well the category and operation type.

```
AuditLogs | 
where TimeGenerated > ago(90d) and Category == "EntitlementManagement" and Result == "success" and (AADOperationType == "CreateEntitlementGrantPolicy" or AADOperationType == "UpdateEntitlementGrantPolicy") | 
project ActivityDateTime,OperationName, InitiatedBy, AdditionalDetails, TargetResources
```

For audit events of some services such as entitlement management, you can also expand and filter on the affected properties of the resources being changed. For example, you can view just those audit log records for access package assignment policies being created or updated, that don't require approval for users to have an assignment added.

```
AuditLogs | 
where TimeGenerated > ago(90d) and Category == "EntitlementManagement" and Result == "success" and (AADOperationType == "CreateEntitlementGrantPolicy" or AADOperationType == "UpdateEntitlementGrantPolicy") | 
mv-expand TargetResources | 
where TargetResources.type == "AccessPackageAssignmentPolicy" | 
project ActivityDateTime,OperationName,InitiatedBy,PolicyId=TargetResources.id,PolicyDisplayName=TargetResources.displayName,MP1=TargetResources.modifiedProperties | 
mv-expand MP1 | 
where (MP1.displayName == "IsApprovalRequiredForAdd" and MP1.newValue == "\"False\"") |
order by ActivityDateTime desc 
```