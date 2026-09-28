---
layout: Conceptual
title: How to archive activity logs to a storage account - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-archive-logs-to-storage-account
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to archive Microsoft Entra activity logs to a storage account through Diagnostic settings.
ms.topic: how-to
ms.date: 2024-11-08T00:00:00.0000000Z
ms.reviewer: egreenberg
locale: en-us
document_id: 96b35262-d52a-00f0-e8f8-225322f9c156
document_version_independent_id: dd46aa98-a9b7-954e-77a5-1f2a0bcf3879
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-archive-logs-to-storage-account.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-archive-logs-to-storage-account
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-archive-logs-to-storage-account.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 77fe4037-b96f-0544-30de-ee2526b78715
---

# How to archive activity logs to a storage account - Microsoft Entra ID | Microsoft Learn

If you need to store Microsoft Entra activity logs for longer than the [default retention period](reference-reports-data-retention), you can archive your logs to a storage account. We recommend that you use a general storage account and not a Blob storage account. For storage pricing information, see the [Azure Storage pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=storage).

## Prerequisites

To use this feature, you need:

- An Azure subscription. If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An Azure storage account you have `ListKeys` permissions for. Learn how to [create a storage account](/en-us/azure/storage/common/storage-account-create).
- A user who's a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator) for the Microsoft Entra tenant.

## Archive logs to an Azure storage account

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostic settings**. You can also select **Export Settings** from either the **Audit Logs** or **Sign-ins** page.
3. Select **+ Add diagnostic setting** to create a new integration or select **Edit setting** for an existing integration.
4. Enter a **Diagnostic setting name**. If you're editing an existing integration, you can't change the name.
5. Select the log categories that you want to stream.

1. Under **Destination Details** select the **Archive to a storage account** check box.
2. Select the appropriate **Subscription** and **Storage account** from the menus.

    ![Screenshot of the diagnostic settings](media/howto-archive-logs-to-storage-account/diagnostic-settings-storage.png)

Note

The Diagnostic settings storage retention feature has been deprecated. If you're editing a diagnostic setting created when the retention option was available, those fields are still visible. For details on this change, see [**Migrate from diagnostic settings storage retention to Azure Storage lifecycle management**](/en-us/azure/azure-monitor/essentials/migrate-to-azure-storage-lifecycle-policy).

1. Select **Save** to save the setting.
2. Close the window to return to the diagnostic settings page.