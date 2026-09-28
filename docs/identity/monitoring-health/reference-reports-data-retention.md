---
layout: Conceptual
title: Microsoft Entra data retention - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/reference-reports-data-retention
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the data retention policies for the Microsoft Entra audit, sign-in, and provisioning logs.
ms.topic: reference
ms.date: 2026-01-06T00:00:00.0000000Z
ms.reviewer: dhanyahk
locale: en-us
document_id: 5975a65a-630f-a2ab-7cc8-268e278a057b
document_version_independent_id: ed2cdee0-9a1e-c435-a172-054896ec35f8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/reference-reports-data-retention.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/reference-reports-data-retention
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/reference-reports-data-retention.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: eff4d325-d9db-9c92-d2a4-8122321606ae
---

# Microsoft Entra data retention - Microsoft Entra ID | Microsoft Learn

In this article, you learn about the data retention policies for the different activity reports in Microsoft Entra ID.

## When does Microsoft Entra ID start collecting data?

| Microsoft Entra Edition | Collection Start |
| --- | --- |
| Microsoft Entra ID P1  Microsoft Entra ID P2  Microsoft Entra Workload ID Premium | When you sign up for a subscription |
| Microsoft Entra ID Free | The first time you open [Microsoft Entra ID](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](overview-monitoring-health) |

If you already have activities data with your free license, then you can see it immediately on upgrade. If you don’t have any data, then it will take up to three days for the data to show up in the reports after you upgrade to a premium license.

- For security signals, the collection process starts when you opt in to use the **Identity Protection Center**.
- For Microsoft Graph activity logs, the collection process starts when the [log category is enabled in diagnostic settings](howto-integrate-activity-logs-with-azure-monitor-logs#send-logs-to-azure-monitor).

## How long does Microsoft Entra ID store the data?

Log storage within Microsoft Entra varies by report type and license type. You can retain the audit and sign-in activity data for longer than the default retention period outlined in the previous table by routing it to an Azure storage account using Azure Monitor. For more information, see [Archive Microsoft Entra logs to an Azure storage account](howto-archive-logs-to-storage-account).

Note

Microsoft Entra ID audit and sign-in logs are separate from the Microsoft 365 Unified Audit Log (UAL). UAL retention is managed through Microsoft Purview Audit and is not affected by Microsoft Entra ID licensing changes.

### Activity reports

| Report | Microsoft Entra ID Free | Microsoft Entra ID P1 | Microsoft Entra ID P2 |
| --- | --- | --- | --- |
| Audit logs | Seven days | 30 days | 30 days |
| Sign-ins | Seven days | 30 days | 30 days |
| Microsoft Entra multifactor authentication usage | 30 days | 30 days | 30 days |
| Microsoft Graph activity logs\* | NA | Must be integrated with storage or analytics tools | Must be integrated with storage or analytics tools |

\*Microsoft Graph activity logs are only available for Microsoft Entra ID P1 and P2 licenses. Data isn't retained unless it's archived to a storage account or integrated with analytics tools.

### Security signals

| Report | Microsoft Entra ID Free | Microsoft Entra ID P1 | Microsoft Entra ID P2 |
| --- | --- | --- | --- |
| Risky users | No limit | No limit | No limit |
| Risky sign-ins | 7 days | 30 days | 90 days |

Note

Organizations with Microsoft 365 E5, Office 365 E5, Microsoft Purview Suite, or E5 eDiscovery and Audit add-on licenses can also use Microsoft Purview Audit (Premium) to retain Microsoft Entra ID audit logs beyond the default period, providing an alternative to exporting logs to Azure Storage. For more information, see [Manage audit log retention policies with Microsoft Purview](/en-us/purview/audit-log-retention-policies).

Note

Risky users and workload identities are not deleted until the risk has been remediated.

### Microsoft Entra External ID logs

In the [Microsoft Entra External ID Basic plan](https://azure-int.microsoft.com/pricing/details/microsoft-entra-external-id/), logs are retained for 7 days. For more information, see [Supported features in workforce and external tenants](/en-us/entra/external-id/customers/concept-supported-features-customers#activity-logs-and-reports). To retain logs for longer periods, use [Azure Monitor](/en-us/entra/external-id/customers/how-to-azure-monitor) in your external tenant.

## Can I see last month's data after getting a premium license?

**No**, you can't. Azure stores up to seven days of activity data for a free version. When you switch from a free to a premium version, you can only see up to 7 days of data.

Note

Log retention changes aren't retroactive. When you upgrade from Microsoft Entra ID Free to P1 or P2, only data still within the free retention period (up to seven days) is available. Data that has already expired can't be recovered unless it was previously archived.