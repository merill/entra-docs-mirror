---
layout: HowTo
title: Integrate Microsoft Entra logs with Azure Monitor logs - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: pmwongera
description: Learn how to integrate Microsoft Entra activity logs with Azure Monitor logs for querying and analysis.
ms.reviewer: egreenberg
ms.date: 2026-01-06T00:00:00.0000000Z
ms.topic: how-to
ms.custom:
- ge-structured-content-pilot
locale: en-us
document_id: b1eb6343-c4d6-6b06-f2eb-1c9435f997f3
document_version_independent_id: 7413b72d-8305-eb0f-3876-2fcb013c5196
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: HowTo
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: c26db741-1fe9-25e7-9527-8206fb8b3ea8
---

# Integrate Microsoft Entra logs with Azure Monitor logs - Microsoft Entra ID | Microsoft Learn

Using **diagnostic settings** in Microsoft Entra ID, you can integrate logs with Azure Monitor so your sign-in activity and the audit trail of changes within your tenant can be analyzed along with other Azure data.

This article provides the steps to integrate Microsoft Entra logs with Azure Monitor.

Use the integration of Microsoft Entra activity logs and Azure Monitor to perform the following tasks:

- Compare your Microsoft Entra sign-in logs against security logs published by Microsoft Defender for Cloud.
- Troubleshoot performance bottlenecks on your application's sign-in page by correlating application performance data from Azure Application Insights.
- Analyze the Identity Protection risky users and risk detections logs to detect threats in your environment.
- Identify sign-ins from applications still using the Active Directory Authentication Library (ADAL) for authentication. [Learn about the ADAL end-of-support plan.](../../identity-platform/msal-migration)

Note

Integrating Microsoft Entra logs with Azure Monitor automatically enables the Microsoft Entra data connector within Microsoft Sentinel.

## Prerequisites

To use this feature, you need:

- An Azure subscription. If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- At least the [Security Administrator](../role-based-access-control/permissions-reference#security-administrator) role in the Microsoft Entra tenant.

- A **Log Analytics workspace** in your Azure subscription. Learn how to [create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace).

- Permission to access data in a Log Analytics workspace. See [Manage access to log data and workspaces in Azure Monitor](/en-us/azure/azure-monitor/logs/manage-access) for information on the different permission options and how to configure permissions.

## Create a Log Analytics workspace

A Log Analytics workspace allows you to collect data based on a variety or requirements, such as geographic location of the data, subscription boundaries, or access to resources. Learn how to [create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace).

To learn how to set up a Log Analytics workspace for Azure resources outside of Microsoft Entra ID, see [Collect and view resource logs for Azure Monitor](/en-us/azure/azure-monitor/essentials/diagnostic-settings).

## Send logs to Azure Monitor

Use the following steps to send logs from Microsoft Entra ID to Azure Monitor logs.

Tip

Steps in this article might vary slightly based on the portal you start from.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**. You can also select **Export Settings** from either the **Audit Logs** or **Sign-ins** page.
3. Select **+ Add diagnostic setting** to create a new integration or select **Edit setting** for an existing integration.
4. Enter a **Diagnostic setting name**. If you're editing an existing integration, you can't change the name.
5. Select the log categories that you want to stream. For a description of each log category, see [What are the identity logs you can stream to an endpoint](concept-log-monitoring-integration-options-considerations).
6. Under **Destination Details** select the **Send to Log Analytics workspace** check box.
7. Select the appropriate **Subscription** and **Log Analytics workspace** from the menus.
8. Select the **Save** button.

    ![Screenshot of the diagnostics settings with some destination details shown.](media/howto-integrate-activity-logs-with-azure-monitor-logs/diagnostic-settings-log-analytics-workspace.png)

    For more information about when logs start appearing in your Log Analytics workspace, see [Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/platform/diagnostic-settings#time-before-telemetry-gets-to-destination).