---
layout: Conceptual
title: Using Microsoft Entra Connect Health with sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-health-sync
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This is the Microsoft Entra Connect Health page that discusses how to monitor Microsoft Entra Connect Sync.
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.subservice: hybrid-connect
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2026-09-10T00:00:00.0000000Z
ms.custom: H1Hack27Feb2017, msecd-doc-authoring-1012
locale: en-us
document_id: aae4a269-20bf-c570-e96b-126bcc230b83
document_version_independent_id: efcaf518-1d36-c359-5a2b-fc39d57c2c10
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-health-sync.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-health-sync
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-health-sync.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7aac3d7e-4ed2-fc0b-3c97-3cce2a17f29b
---

# Using Microsoft Entra Connect Health with sync - Microsoft Entra ID | Microsoft Learn

The following documentation is specific to monitoring Microsoft Entra Connect (Sync) with Microsoft Entra Connect Health. For information on monitoring AD FS with Microsoft Entra Connect Health see [Using Microsoft Entra Connect Health with AD FS](how-to-connect-health-adfs). Additionally, for information on monitoring Active Directory Domain Services with Microsoft Entra Connect Health see [Using Microsoft Entra Connect Health with AD DS](how-to-connect-health-adds).

## Prerequisites

Before you use Microsoft Entra Connect Health for sync, install the Microsoft Entra Connect Health agent on each Microsoft Entra Connect Sync server. The agent is supported on Windows Server 2016, 2019, 2022, and 2025. For installation steps, requirements, and the full list of supported Windows Server versions, see [Install the Microsoft Entra Connect Health agents](how-to-connect-health-agent-install).

Important

Microsoft Entra Connect Health for Sync requires Microsoft Entra Connect Sync V2. If you're still using Azure AD Connect V1, you must upgrade to the latest version. Azure AD Connect V1 was retired on August 31, 2022. Microsoft Entra Connect Health for Sync stopped working with Azure AD Connect V1 in December 2022.

Open [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth), select **Sync services**, and then select a service. The overview brings together server health, active and recently resolved alerts, synchronization errors, and data freshness status. Select a server, alert summary, or sync error card to open the corresponding details.

[![Screenshot of the Connect Health Sync service overview with callouts for monitored servers, alert summary, and synchronization error status.](media/how-to-connect-health-sync/connect-health-sync-service-overview.png)](media/how-to-connect-health-sync/connect-health-sync-service-overview.png#lightbox)

## Alerts for Microsoft Entra Connect Health for sync

The **Alerts** page lists active and resolved alerts. Use the time-range control to include older resolved alerts, and use search to filter the list. Select an alert row to open the details panel, which contains alert metadata, affected servers, resolution guidance, related documentation, and a feedback option.

### Limited Evaluation of Alerts

If Microsoft Entra Connect is NOT using the default configuration (for example, if Attribute Filtering is changed from the default configuration to a custom configuration), then the Microsoft Entra Connect Health agent won't upload the error events related to Microsoft Entra Connect.

This limits the evaluation of alerts by the service. You'll see a banner that indicates this condition in the [Microsoft Entra admin center](https://entra.microsoft.com) under your service.

To change this setting, open the sync service, select **Settings** on the command bar, enable monitoring in the settings panel, and select **Save**.

## Sync Insight

Admins frequently want to know how long it takes to synchronize changes to Microsoft Entra ID and how many changes occur. The server health page provides the following performance charts:

- Latency of sync operations
- Object Change trend

### Sync Latency

This feature provides a graphical trend of latency of the sync operations (such as import and export) for connectors. This provides a quick and easy way to understand the latency of your operations. The latency is larger if you have a large set of changes occurring. Additionally, it provides a way to detect anomalies in the latency that may require further investigation.

Select **View detailed monitoring** on the **Run profile latency** chart to open a larger view and change the displayed time range.

### Sync Object Changes

This feature provides a graphical trend of the number of changes that are being evaluated and exported to Microsoft Entra ID. Today, trying to gather this information from the sync logs is difficult. The chart gives you, not only a simpler way of monitoring the number of changes that are occurring in your environment, but also a visual view of the failures that are occurring.

Select **View detailed monitoring** on the **Export statistics** chart to open a larger view and change the displayed time range.

## Object Level Synchronization Error Report

This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Microsoft Entra ID using Microsoft Entra Connect.

- The report covers errors recorded by the sync client (Microsoft Entra Connect version [2.5.79.0 or higher](reference-connect-version-history))
- It includes the errors that occurred in the last synchronization operation on the sync engine. ("Export" on the Microsoft Entra Connector.)
- Microsoft Entra Connect Health agent for sync must have outbound connectivity to the required end points for the report to include the latest data.
- The report is **updated after every 30 minutes** using the data uploaded by Microsoft Entra Connect Health agent for sync. It provides the following key capabilities

    - Categorization of errors
    - List of objects with error per category
    - All the data about the errors at one place
    - Side by side comparison of Objects with error due to a conflict
    - Download the error report as a CSV file

[![Screenshot of the Connect Health Sync errors page with callouts for command bar actions, error categories, and the error list.](media/how-to-connect-health-sync/connect-health-sync-errors.png)](media/how-to-connect-health-sync/connect-health-sync-errors.png#lightbox)

### Categorization of Errors

The report categorizes the existing synchronization errors in the following categories:

| Category | Description |
| --- | --- |
| Duplicate Attribute | Errors when Microsoft Entra Connect attempts create or update objects with duplicated values of one or more attributes in Microsoft Entra ID that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName. |
| Data Mismatch | Errors when the soft-match fails to match objects that result in synchronization errors. |
| Data Validation Failure | Errors due to invalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Microsoft Entra ID. |
| Federated Domain Change | Errors when accounts use a different federated domain. |
| Large Attribute | Errors when one or more attributes are larger than the allowed size, length or count. |
| Other | All other errors that don't fit in the above categories. Based on feedback, this category splits into sub categories. |

### List of objects with error per category

Select a category tile to filter the error list. You can also search the selected category, sort supported columns, expand a row for more details, and change the number of results displayed per page.

### Error Details

Following data is available in the detailed view for each error

- Highlighted conflicting attribute
- Identifiers for the *AD Object* involved
- Identifiers for the *Microsoft Entra Object* involved (as applicable)
- Error description and how to fix

### Download the error report as CSV

Select **Export** on the command bar to download a CSV file that contains the recorded sync errors.

### Diagnose and remediate sync errors

For supported duplicate-attribute sync error scenarios that involve a user source anchor update, select **Fix this error** for an item to start the guided **Fix Synchronization Error** experience. For more information, see [Diagnose and remediate duplicated attribute sync errors](how-to-connect-health-diagnose-sync-errors).