---
layout: Conceptual
title: How to configure Microsoft Entra diagnostic settings - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-configure-diagnostic-settings
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to configure Microsoft Entra diagnostic settings to integrate activity logs with SIEM tools.
ms.topic: how-to
ms.date: 2025-06-16T00:00:00.0000000Z
ms.reviewer: egreenberg
locale: en-us
document_id: 24828128-a7b7-ee94-84ee-a83684babf2b
document_version_independent_id: 24828128-a7b7-ee94-84ee-a83684babf2b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-configure-diagnostic-settings.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-configure-diagnostic-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-configure-diagnostic-settings.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b9b30f1c-c18d-e604-5aad-6a17014edd14
---

# How to configure Microsoft Entra diagnostic settings - Microsoft Entra ID | Microsoft Learn

Using **diagnostic settings** in Microsoft Entra ID, you can integrate logs with Azure Monitor, stream logs to an event hub, or archive logs to a storage account. You can create multiple diagnostic settings to send activity logs to different destinations.

This article provides the steps to configure Microsoft Entra diagnostic settings for activity logs.

## Prerequisites

To configure diagnostic settings, you need:

- An Azure subscription. If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Security Administrator](../role-based-access-control/permissions-reference#security-administrator) access to create general diagnostic settings for the Microsoft Entra tenant.
- [Attribute Log Administrator](../role-based-access-control/permissions-reference#attribute-log-administrator) access to create diagnostic settings for [custom security attribute](../../fundamentals/custom-security-attributes-overview) logs.
- A destination that is already set up. For example, if you want to stream logs to an event hub, you need to create the event hub before you can configure the diagnostic settings.

## How to access diagnostic settings

This article provides the steps to access diagnostic settings for the Microsoft Entra logs. If you need to configure diagnostic settings for Azure Monitor or Azure resources outside of Microsoft Entra ID, see [Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/diagnostic-settings).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**. The **General** settings appear by default.
3. Any existing diagnostic settings appear in the table. Select **edit settings** to change an existing setting, or select **Add diagnostic setting** to create a new setting.

    ![Screenshot of the Microsoft Entra diagnostic settings page.](media/howto-configure-diagnostic-settings/diagnostic-settings-start.png)

### Custom security attributes

The custom security attributes logs are a subset of the standard audit logs. You must have the **Attribute Log Administrator** role active to configure diagnostic settings for the custom security attributes. For more information, see [Custom security attributes overview](../../fundamentals/custom-security-attributes-overview).

To configure diagnostic settings for the custom security attribute audit logs, select **Custom security attributes**. The process to configure diagnostic settings is the same for both categories of logs.

![Screenshot of the custom security attributes page for diagnostic settings.](media/howto-configure-diagnostic-settings/custom-security-attributes.png)

Tip

Microsoft recommends that you keep your custom security attribute audit logs separate from your directory audit logs so that attribute assignments are not revealed inadvertently.

## Select the logs and destination

When you create or edit a diagnostic setting, you can choose which logs to include and where to send them.

### Log categories

You can select one, some, or all of the available logs. Some logs might be part of a preview feature. Even if you select a log category, you might not see any data until the feature is generally available. For a description of the available logs, see [Log options for streaming to endpoints](concept-diagnostic-settings-logs-options).

![Screenshot of the log categories in diagnostic settings.](media/howto-configure-diagnostic-settings/diagnostic-settings-log-categories.png)

### Destination details

You can send logs to a Log Analytics workspace, stream logs to an event hub, or archive logs to a storage account. Through Azure Native ISV services, you can send logs to services through the Azure Marketplace. For more information, see [Azure Native ISV services overview](/en-us/azure/partner-solutions/overview).

You must have a destination set up prior to configuring diagnostic settings.

- [Configure a Log Analytics workspace](tutorial-configure-log-analytics-workspace)
- [Create an event hub](/en-us/azure/event-hubs/event-hubs-create)
- [Create a storage account](/en-us/azure/storage/common/storage-account-create)

When you select a destination, more fields appear. Select the appropriate subscription and destination from the fields that appear.

![Screenshot of the destination options in diagnostic settings.](media/howto-configure-diagnostic-settings/diagnostic-settings-destination-details.png)

For details on configuring diagnostic settings for a specific destination, see the following articles:

- [Integrate logs with Azure monitor logs](howto-integrate-activity-logs-with-azure-monitor-logs)
- [Stream logs to an event hub](howto-stream-logs-to-event-hub)
- [Archive logs to an Azure storage account](howto-archive-logs-to-storage-account)

## Basic process

The basic steps for configuring diagnostics settings are as follows:

Note

It might take up to three days for the logs to start appearing in the destination.

1. To create a new diagnostic setting, select **Add diagnostic setting**.
2. Provide a name.
3. Select the logs you want to include.
4. Select the destination and subscription from the dropdown menus that appear.
5. Select the **Save** button.

    ![Screenshot of the create diagnostic settings page, with several logs selected to go to a Log Analytics workspace.](media/howto-configure-diagnostic-settings/diagnostic-settings-save.png)