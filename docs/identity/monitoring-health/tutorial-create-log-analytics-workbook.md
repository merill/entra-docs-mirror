---
layout: Conceptual
title: Create a Log Analytics custom workbook - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/tutorial-create-log-analytics-workbook
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to create a Log Analytics custom workbook for enhanced analysis and alerting in Microsoft Entra ID.
ms.topic: tutorial
ms.date: 2025-03-27T00:00:00.0000000Z
ms.reviewer: sandeo
locale: en-us
document_id: a8500038-8b59-2634-91c2-1194d0e3632e
document_version_independent_id: a8500038-8b59-2634-91c2-1194d0e3632e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/tutorial-create-log-analytics-workbook.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/tutorial-create-log-analytics-workbook
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/tutorial-create-log-analytics-workbook.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b18554bf-4801-3c7e-5b6e-443dd2f9138c
---

# Create a Log Analytics custom workbook - Microsoft Entra ID | Microsoft Learn

In this tutorial, you learn how to:

- Create a custom workbook
- Add a query to an existing workbook template

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

If you haven't already created a Log Analytics workspace, complete the [Configure Log Analytics workspace](tutorial-configure-log-analytics-workspace) tutorial.

## Create a custom workbook

In addition to querying the data with Kusto Query Language (KQL), you can create a custom workbook for further analysis and alerting. The least privileged role to create or update a workbook is the **Security Administrator** role.

1. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
2. In the **Quickstart** section, select **Empty**.

    ![Screenshot of the blank workbook in the Quick start section.](media/tutorial-create-log-analytics-workbook/quick-start.png)
3. From the **Add** menu, select **Add text**.

    ![Screenshot of the Add text menu option.](media/tutorial-create-log-analytics-workbook/add-text.png)
4. In the textbox, enter `# Client apps used in the past week` and select **Done Editing**.

    ![Screenshot shows the text and the Done Editing button.](media/tutorial-create-log-analytics-workbook/workbook-text.png)
5. Below the text window, open the **Add** menu and select **Add query**.

    ![Screenshot of the Add query menu option.](media/tutorial-create-log-analytics-workbook/add-query.png)
6. In the query textbox, enter: `SigninLogs | where TimeGenerated > ago(7d) | project TimeGenerated, UserDisplayName, ClientAppUsed | summarize count() by ClientAppUsed`
7. Select **Run Query**.

    ![Screenshot shows the Run Query button.](media/tutorial-create-log-analytics-workbook/run-workbook-query.png)
8. In the toolbar, from the **Visualization** menu select **Pie chart**.

    ![Screenshot showing the Pie chart menu option.](media/tutorial-create-log-analytics-workbook/pie-chart.png)
9. Select **Done Editing** at the top of the page.
10. Select the **Save** icon to save your workbook.
11. In the dialog box that appears, enter a title, select a Resource group, and select **Apply**.

## Add a query to a workbook template

You can add Kusto queries to your workbook. The example is based on a query that shows the distribution of successful and failed sign-ins with applied Conditional Access policies. The least privileged role to create or update a workbook is the **Security Administrator** role.

1. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
2. In the **Conditional Access** section, select **Conditional Access Insights and Reporting**.

    ![Screenshot shows the Conditional Access Insights and Reporting option.](media/tutorial-create-log-analytics-workbook/conditional-access-template.png)
3. In the toolbar, select **Edit**.

    ![Screenshot shows the Edit button.](media/tutorial-create-log-analytics-workbook/edit-workbook-template.png)
4. In the toolbar, select the three dots next to the Edit button, then **Add**, and then **Add query**.

    ![Add workbook query](media/tutorial-create-log-analytics-workbook/add-custom-workbook-query.png)
5. In the query textbox, enter: `SigninLogs | where TimeGenerated > ago(20d) | where ConditionalAccessPolicies != "[]" | summarize dcount(UserDisplayName) by bin(TimeGenerated, 1d), ConditionalAccessStatus`
6. Select **Run Query**.

    ![Screenshot shows the Run Query button to run this query.](media/tutorial-create-log-analytics-workbook/run-workbook-insights-query.png)
7. From the **Time Range** menu, select **Set in query**.
8. From the **Visualization** menu, select **Bar chart**.
9. Select **Advanced Settings**.

    ![Screenshot of the time range, visualization, and advanced setting options.](media/tutorial-create-log-analytics-workbook/select-query-options.png)
10. In the **Chart title** field, enter `Conditional Access status over the last 20 days` and select **Done Editing**.

    ![Set chart title](media/tutorial-create-log-analytics-workbook/set-chart-title.png)

Your Conditional Access success and failure chart displays a color-coded snapshot of your tenant.