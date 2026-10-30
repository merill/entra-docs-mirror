---
layout: Conceptual
title: Configure a Log Analytics workspace and a custom workbook - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/tutorial-configure-log-analytics-workspace
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to configure a Log Analytics workspace, create a workbook, and run Kusto queries in Microsoft Entra ID.
ms.topic: tutorial
ms.date: 2025-03-27T00:00:00.0000000Z
ms.reviewer: sandeo
locale: en-us
document_id: e02bd358-3558-fc11-7653-8730579b74bd
document_version_independent_id: 05bd9f03-0b3d-ffb4-f97d-312e8e301fb9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/tutorial-configure-log-analytics-workspace.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/tutorial-configure-log-analytics-workspace
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/tutorial-configure-log-analytics-workspace.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 57bd8ddf-9401-6db5-a720-9463e0ed6352
---

# Configure a Log Analytics workspace and a custom workbook - Microsoft Entra ID | Microsoft Learn

In this tutorial, you learn how to:

- Create a Log Analytics workspace
- Configure diagnostic settings to integrate sign-in logs with the Log Analytics workspace
- Run queries using the Kusto Query Language (KQL)

## Prerequisites

To analyze activity logs with Log Analytics, you need the following roles and requirements:

- [Microsoft Entra monitoring and health licensing](../../fundamentals/licensing#microsoft-entra-monitoring-and-health)
- [Access to create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/manage-access)
- The appropriate role for Azure Monitor:

    - Monitoring Reader
    - Log Analytics Reader
    - Monitoring Contributor
    - Log Analytics Contributor
- The appropriate role for Microsoft Entra ID:

    - Reports Reader
    - Security Reader
    - Global Reader
    - Security Administrator

## Create a Log Analytics workspace

In this step, you create a Log Analytics workspace, which is where you eventually send your sign-in logs. Before you can create the workspace, you need an [Azure resource group](/en-us/azure//azure-resource-manager/management/overview#resource-groups).

1. Sign in to the [Azure portal](https://portal.azure.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator) with [Log Analytics Contributor](/en-us/azure/azure-monitor/logs/manage-access#log-analytics-contributor) permissions.
2. Browse to **Log Analytics workspaces**.
3. Select **Create**.

    ![Screenshot of the Create button in the log analytics workspaces page.](media/tutorial-configure-log-analytics-workspace/create-new-workspace.png)
4. On the **Create Log Analytics workspace** page, perform the following steps:

    1. Select your subscription.
    2. Select a resource group.
    3. Give your workspace a name.
    4. Select your region.

    ![Screenshot of the details page of create new log analytics workspace.](media/tutorial-configure-log-analytics-workspace/create-new-workspace-details.png)
5. Select **Review + Create**.
6. Select **Create** and wait for the deployment. You might need to refresh the page to see the new workspace.

## Configure diagnostic settings

To send your identity log information to your new workspace, you need to configure diagnostic settings. There are different diagnostic settings options for Azure and Microsoft Entra, so for the next set of steps let's switch to the Microsoft Entra admin center to make sure everything is identity related.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**.
3. Select **Add diagnostic setting**.

    ![Screenshot of the Add diagnostic setting option.](media/tutorial-configure-log-analytics-workspace/add-diagnostic-setting.png)
4. On the **Diagnostic setting** page, perform the following steps:

    1. Provide a name for the diagnostic setting.
    2. Under **Logs**, select **AuditLogs** and **SigninLogs**.
    3. Under **Destination details**, select **Send to Log Analytics**, and then select your new log analytics workspace.
    4. Select **Save**.

    ![Screenshot of the select diagnostics settings options.](media/tutorial-configure-log-analytics-workspace/select-diagnostics-settings.png)

Your selected logs might take up to 15 minutes for the logs to populate in your Log Analytics workspace.

## Run queries in Log Analytics

With your logs streaming to your Log Analytics workspace, you can run queries using the **Kusto Query Language (KQL)**. The least privileged role to run queries is the **Reports Reader** role

1. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Log Analytics**.
2. In the **Search** textbox, type your query, and select **Run**.

### Kusto query examples

Take 10 random entries from the input data:

- `SigninLogs | take 10`

Look at the sign-ins where the Conditional Access was a success:

- `SigninLogs | where ConditionalAccessStatus == "success" | project UserDisplayName, ConditionalAccessStatus`

Count number of successes:

- `SigninLogs | where ConditionalAccessStatus == "success" | project UserDisplayName, ConditionalAccessStatus | count`

Aggregate count of successful sign-ins by user by day:

- `SigninLogs | where ConditionalAccessStatus == "success" | summarize SuccessfulSign-ins = count() by UserDisplayName, bin(TimeGenerated, 1d)`

View how many times a user does a certain operation in specific time period:

- `AuditLogs | where TimeGenerated > ago(30d) | where OperationName contains "Add member to role" | summarize count() by OperationName, Identity`

Pivot the results on operation name:

- `AuditLogs | where TimeGenerated > ago(30d) | where OperationName contains "Add member to role" | project OperationName, Identity | evaluate pivot(OperationName)`

Merge together Audit and Sign in Logs using an inner join:

- `AuditLogs |where OperationName contains "Add User" |extend UserPrincipalName = tostring(TargetResources[0].userPrincipalName) | |project TimeGenerated, UserPrincipalName |join kind = inner (SigninLogs) on UserPrincipalName |summarize arg_min(TimeGenerated, *) by UserPrincipalName |extend SigninDate = TimeGenerated`

View number of signs ins by client app type:

- `SigninLogs | summarize count() by ClientAppUsed`

Count the sign ins by day:

- `SigninLogs | summarize NumberOfEntries=count() by bin(TimeGenerated, 1d)`

Take five random entries and project the columns you wish to see in the results:

- `SigninLogs | take 5 | project ClientAppUsed, Identity, ConditionalAccessStatus, Status, TimeGenerated`

Take the top 5 in descending order and project the columns you wish to see:

- `SigninLogs | take 5 | project ClientAppUsed, Identity, ConditionalAccessStatus, Status, TimeGenerated`

Create a new column by combining the values to two other columns:

- `SigninLogs | limit 10 | extend RiskUser = strcat(RiskDetail, "-", Identity) | project RiskUser, ClientAppUsed`