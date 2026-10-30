---
layout: Conceptual
title: Create Custom Reports Using Application Data - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/custom-entitlement-report-with-other-sources
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This tutorial describes how to create customized reports in Azure Data Explorer by using data from more sources in addition to Microsoft Entra
ms.topic: tutorial
ms.date: 2025-04-11T00:00:00.0000000Z
locale: en-us
document_id: 2e40c7f3-57ad-588c-064d-4b12e047bcec
document_version_independent_id: 2e40c7f3-57ad-588c-064d-4b12e047bcec
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/custom-entitlement-report-with-other-sources.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/custom-entitlement-report-with-other-sources
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/custom-entitlement-report-with-other-sources.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/26e1a60c-4ce1-41de-b2d1-e5f3b7e68e6e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad3bd485-5ca9-4865-afde-baec02586899
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 712f7e67-45e0-a45f-31d2-64dea01f41d8
---

# Create Custom Reports Using Application Data - Microsoft Entra ID Governance | Microsoft Learn

The tutorial [Create customized reports in Azure Data Explorer by using data from Microsoft Entra](custom-entitlement-report-with-adx-and-entra-id) shows how to create customized reports in [Azure Data Explorer](/en-us/azure/data-explorer/data-explorer-overview) by using data from Microsoft Entra ID and Microsoft Entra ID Governance services.

You can also bring in data to Azure Data Explorer from sources beyond Microsoft Entra. Scenarios for this capability include:

- An admin wants to view events in the audit log with additional details about users, access packages, or other objects which aren't part of the audit record itself.
- An admin wants to view all users added to an application from Microsoft Entra ID and their access rights in the application's own repository, such as a SQL database.

These types of reports aren't built into Microsoft Entra ID. However, you can create these reports yourself by extracting data from Microsoft Entra ID and combining data by using custom queries in Azure Data Explorer.

## Query data in Azure Monitor

If you're sending the audit, sign-in, or other Microsoft Entra logs to Azure Monitor, you can incorporate those logs from that Azure Monitor Log Analytics workspace in your queries, without needing to copy the data into Azure Data Explorer. For more information on the relationship between Azure Monitor and Azure Data Explorer, see [Query data in Azure Monitor using Azure Data Explorer](/en-us/azure/data-explorer/query-monitor-data).

This example builds upon the tutorial to [populate Azure Data Explorer from Microsoft Entra ID Governance](custom-entitlement-report-with-adx-and-entra-id), and shows joining the Microsoft Entra audit log stored in Azure Monitor as `AuditLogs` with the Microsoft Entra access packages stored in Azure Data Explorer as `EntraAccessPackages`.

1. Sign in to the Microsoft Entra admin center.
2. Select [Diagnostic settings](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/DiagnosticSettingsMenuBlade/%7E/General).
3. Select the Log Analytics workspace where you're sending your logs.
4. On the Log Analytics workspace overview, record the subscription ID, the name of the resource, and the name of the workspace.
5. Sign in to the Azure portal.
6. Go to the [Azure Data Explorer web UI](https://dataexplorer.azure.com/home).
7. Ensure that your Azure Data Explorer cluster is listed.
8. Select **+ Add** &gt; **Connection**.
9. In the **Add Connection** window, enter the URL in the Log Analytics workspace. The URL is formed from the cloud-specific host name, subscription ID, resource group name, and workspace name of the Azure Monitor Log Analytics workspace, as described in [Add a Log Analytics workspace](/en-us/azure/data-explorer/query-monitor-data#add-a-log-analytics-workspaceapplication-insights-resource-to-azure-data-explorer-client-tools).
10. After the connection is established, your Log Analytics workspace appears on the left pane with your native Azure Data Explorer cluster.

    Select **Query**, and then select your Azure Data Explorer cluster.
11. On the query pane, refer to the Azure Monitor tables that contain the Microsoft Entra logs in your Azure Data Explorer queries. For example:

    ```kusto
    let CL1 = 'https://ade.loganalytics.io/subscriptions/*subscriptionid*/resourcegroups/*resourcegroupname*/providers/microsoft.operationalinsights/workspaces/*workspacename*';
    cluster(CL1).database('*workspacename*').AuditLogs | where Category == "EntitlementManagement"  and OperationName == "Fulfill access package assignment request"
    | mv-expand TargetResources | where TargetResources.type == 'AccessPackage' | project ActivityDateTime,APID = toguid(TargetResources.id)
    | join EntraAccessPackages on $left.APID == $right.Id
    | limit 100
    ```

## Bring in data from other sources

You can [create additional tables](/en-us/azure/data-explorer/create-table-wizard) in Azure Data Explorer to ingest data from other sources. If the data is in a JSON file (similar to the preceding examples) or a CSV file, you can create the table at the time that you first [get data from the file](/en-us/azure/data-explorer/get-data-file). After the table is created, you can also [use LightIngest to ingest data into Azure Data Explorer](/en-us/azure/data-explorer/lightingest) from a JSON or CSV file.

For more information on data ingestion, see [Azure Data Explorer data ingestion overview](/en-us/azure/data-explorer/ingest-data-overview).

### Example: Combine app assignments from Microsoft Entra and a second source to create a report of all users who had access to an application between two dates

This report illustrates how you can combine data from two separate systems to create custom reports in Azure Data Explorer. It aggregates data about users, their roles, and other attributes from two systems into a unified format for analysis or reporting.

The following example assumes that a table named `salesforceAssignments` was populated with data that came from another application. The table has the columns `UserName`, `Name`, `EmployeeId`, `Department`, `JobTitle`, `AppName`, `Role`, and `CreatedDateTime`.

```kusto
// Define the date range and service principal ID for the query 

let startDate = datetime("2023-06-01"); 
let endDate = datetime("2024-03-13"); 
let servicePrincipalId = "<your service principal-id>"; 

// Pre-process AppRoleAssignments with specific filters and projections 
let processedAppRoleAssignments = AppRoleAssignments 
    | where ResourceId == servicePrincipalId and todatetime(CreatedDateTime) between (startDate .. endDate) 
    | extend AppRoleId = tostring(AppRoleId) 
    | project PrincipalId, AppRoleId, CreatedDateTime, ResourceDisplayName; // Exclude DeletedDateTime and keep ResourceDisplayName 

// Pre-process AppRoles to get RoleDisplayName for each role 
let processedAppRoles = AppRoles 
    | mvexpand AppRoles 
    | project AppRoleId = tostring(AppRoles.Id), RoleDisplayName = tostring(AppRoles.DisplayName); 

// Main query: Process EntraUsers by joining with processed role assignments and roles 
EntraUsers 
    | join kind=inner processedAppRoleAssignments on $left.ObjectID == $right.PrincipalId // Join with role assignments 
    | join kind=inner processedAppRoles on $left.AppRoleId == $right.AppRoleId // Join with roles to get display names 

    // Summarize to get the latest record for each unique combination of user and role attributes 
    | summarize arg_max(AccountEnabled, *) by UserPrincipalName, DisplayName, tostring(EmployeeId), Department, JobTitle, ResourceDisplayName, RoleDisplayName, CreatedDateTime 

    // Final projection of relevant fields, including source indicator and report date 
    | project UserPrincipalName, DisplayName, EmployeeId=tostring(EmployeeId), Department, JobTitle, AccountEnabled=tostring(AccountEnabled), ResourceDisplayName, RoleDisplayName, CreatedDateTime, Source="EntraUsers", ReportDate = now() 

// Union with processed salesforceAssignments to create a combined report 
| union ( 
    salesforceAssignments 

    // Project fields from salesforceAssignments to align with the EntraUsers data structure 
    | project UserPrincipalName = UserName, DisplayName = Name, EmployeeId = tostring(EmployeeId), Department, JobTitle, AccountEnabled = "N/A", ResourceDisplayName = AppName, RoleDisplayName = Role, CreatedDateTime, Source = "salesforceAssignments", ReportDate = now() 
) 
```