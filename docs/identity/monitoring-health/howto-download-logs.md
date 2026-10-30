---
layout: Conceptual
title: How to download logs in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-download-logs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: How to download the audit, sign-in, and provisioning log data for manual storage in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2024-11-08T00:00:00.0000000Z
ms.reviewer: egreenberg
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4f4de390-e6c9-e024-75a9-23d97659fe63
document_version_independent_id: 4bf2b46d-778b-7b7e-09c5-2ca1e8f5105e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-download-logs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-download-logs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-download-logs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: f8f5e6a2-a1eb-b443-11f4-fccca44a9884
---

# How to download logs in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The Microsoft Entra admin center gives you access to three types of activity logs:

- **[Sign-ins](concept-sign-ins)**: Information about sign-ins and how your resources are used by your users.
- **[Audit](concept-audit-logs)**: Information about changes applied to your tenant such as users and group management or updates applied to your tenant’s resources.
- **[Provisioning](concept-provisioning-logs)**: Activities performed by a provisioning service, such as the creation of a group in ServiceNow or a user imported from Workday.

Microsoft Entra ID stores activity logs for a specific period, depending on your license. For more information, see [Microsoft Entra data retention](reference-reports-data-retention). By downloading the logs, you can control how long logs are stored. This article explains how to download activity logs in Microsoft Entra ID.

## Prerequisites

- A working Microsoft Entra tenant with the appropriate Microsoft Entra license associated with it.
    - For a full list of license requirements, see [Microsoft Entra monitoring and health licensing](../../fundamentals/licensing#microsoft-entra-monitoring-and-health).
- The option to download logs is available in all editions of Microsoft Entra ID.
- Downloading logs programmatically with Microsoft Graph requires a [premium license](../../fundamentals/licensing#microsoft-entra-monitoring-and-health).
- [Reports Reader](../role-based-access-control/permissions-reference#reports-reader) is the least privileged role required to view Microsoft Entra activity logs.

## Log download considerations

Before you download logs, review the following considerations and tips:

- Microsoft Entra ID supports the following formats for your download:
    - **CSV**
    - **JSON**
- Timestamps in the downloaded files are based on UTC.
- You can download up to 100,000 sign-in or provisioning records per file.
- You can download up to 250,000 audit records per file.
- Set your filter before you download the logs to narrow the dataset.

Note

The Microsoft Entra admin center download service will time out if you attempt to download large data sets. Generally, data sets smaller than 250,000 for audit logs and 100,000 for sign-in and provisioning logs work well with the browser download feature.

If you face issues completing large downloads in the browser, use the [**reporting API**](/en-us/graph/api/resources/azure-ad-auditlog-overview) to download the data or [**send the logs to an endpoint through diagnostic settings**](howto-configure-diagnostic-settings).

Note

The columns in the downloaded logs do not change. The output contains all details of the audit or sign-in log, *regardless of the columns you customized in the Microsoft Entra admin center*. If you set a custom filter, however, the output in the downloaded logs contain only the results that match the filter.

## How to download activity logs

You can access the activity logs from the **Monitoring and health** section of Microsoft Entra ID or from the area of Microsoft Entra ID where you're working.

For example, if you're in the **Groups** or **Licenses** section of Microsoft Entra ID, you can access the audit logs for those specific activities directly from that area. When you access the audit logs in this way, the filter categories are automatically set. If you're in **Groups**, the audit log filter category is set to **GroupManagement**.

![Screenshot of the licenses area of Microsoft Entra ID with the Audit logs option highlighted.](media/howto-download-logs/audit-logs-from-licenses.png)

### Audit logs

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Audit logs**.
3. Select **Download**.
4. In the panel that opens, select the **Format**.
5. Optionally provide a unique file name.
6. Select the **Download** button. The download processes and sends the file to your default download location.

    ![Screenshot of the audit log download process.](media/howto-download-logs/audit-log-download.png)

### Sign-in logs

The options covered in this section align with the preview experience for sign-in logs.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
3. Select the **Download** button and select either **JSON** or **CSV**.

    ![Screenshot of the download button options for sign-in logs.](media/howto-download-logs/sign-in-logs-download.png)
4. Optionally provide a unique file name for each file you need to download.
5. Select the **Download** button for one or more of the logs. The download processes and sends the file to your default download location.

    - Interactive sign-ins
    - Interactive sign-ins with only the [authentication details](concept-sign-in-log-activity-details#) included
    - Non-interactive sign-ins
    - Non-interactive sign-ins with only the [authentication details](concept-sign-in-log-activity-details#authentication-details) included
    - Application sign-ins
    - Managed identity

    ![Screenshot of the download options for the sign-in logs.](media/howto-download-logs/sign-in-log-download-options.png)

### Provisioning logs

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Provisioning logs**.
3. Select the **Download** button and select either **JSON** or **CSV**.
4. Optionally provide a unique file name for each file you need to download.
5. Select the **Download** button for one or more of the logs. The download processes and sends the file to your default download location.

    - Provisioning logs
    - Provisioning logs with the provisioning steps
    - Provisioning logs with modified properties

    ![Screenshot of the download options for the provisioning logs.](media/howto-download-logs/provisioning-logs-download-options.png)