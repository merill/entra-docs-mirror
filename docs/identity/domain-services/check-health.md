---
layout: Conceptual
title: Check the health of Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/check-health
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to check the health of a Microsoft Entra Domain Services managed domain and understand status messages.
ms.assetid: 8999eec3-f9da-40b3-997a-7a2587911e96
ms.topic: how-to
ms.date: 2025-01-21T00:00:00.0000000Z
locale: en-us
document_id: d6347876-e729-1f2b-d94b-6b8e842d9379
document_version_independent_id: aed5ad45-5be6-4d34-4c00-79ed913f26bd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/check-health.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/check-health
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/check-health.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: eda63c28-8cf6-ddbd-974d-4645b7b49fdb
---

# Check the health of Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Domain Services runs some background tasks to keep the managed domain healthy and up-to-date. These tasks include taking backups, applying security updates, and synchronizing data from Microsoft Entra ID. If there are issues with the Domain Services managed domain, these tasks may not successfully complete. To review and resolve any issues, you can check the health status of a managed domain using the Microsoft Entra admin center.

This article shows you how to view the Domain Services health status and understand the information or alerts shown.

## View the health status

The health status for a managed domain is viewed using the Microsoft Entra admin center. Information on the last backup time and synchronization with Microsoft Entra ID can be seen, along with any alerts that indicate a problem with the managed domain's health. To view the health status for a managed domain, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
2. Search for and select **Microsoft Entra Domain Services**.
3. Select your managed domain, such as *aaddscontoso.com*.
4. On the left-hand side of the Domain Services resource window, select **Health**. The following example screenshot shows a healthy managed domain and the status of the last backup and Microsoft Entra synchronization:

    ![Health page overview showing the Microsoft Entra Domain Services status](media/check-health/health-page.png)

The *Last evaluated* timestamp of the health page shows when the managed domain was last checked. The health of a managed domain is evaluated every hour. If you make any changes to a managed domain, wait until the next evaluation cycle to view the updated health status.

The status in the top right indicates the overall health of the managed domain. The status factors all of the existing alerts on your domain. The following table details the available status indicators:

| Status | Icon | Explanation |
| --- | --- | --- |
| Running | ![Green check mark for running](media/entra-domain-services-alerts/running-icon.png) | The managed domain is running correctly and doesn't have any critical or warning alerts. The domain may have informational alerts. |
| Needs attention (warning) | ![Yellow exclamation mark for warning](media/entra-domain-services-alerts/warning-icon.png) | There are no critical alerts on the managed domain, but there are one or more warning alerts that should be addressed. |
| Needs attention (critical) | ![Red exclamation mark for critical](media/entra-domain-services-alerts/critical-icon.png) | There are one or more critical alerts on the managed domain that must be addressed. You may also have warning and / or informational alerts. |
| Deploying | ![Blue circular arrows for deploying](media/entra-domain-services-alerts/deploying-icon.png) | The managed domain is being deployed. |

## Understand monitors and alerts

The health status for a managed domain show two types of information - *monitors*, and *alerts*. Monitors show the time that core background tasks were completed. Alerts provide information or suggestions to improve the stability of the managed domain.

### Monitors

Monitors are areas of a managed domain that are checked on a regular basis. If there are any active alerts for the managed domain, it may cause one of the monitors to report an issue. Domain Services currently has monitors for the following areas:

- Backup
- Synchronization with Microsoft Entra ID

#### Backup monitor

The backup monitor checks that automated regular backups of the managed domain successfully run. The following table details the available backup monitor status:

| Detail value | Explanation |
| --- | --- |
| Never backed up | This state is normal for new managed domains. The first backup should be created 24 hours after the managed domain is deployed. If this status persists, [open an Azure support request](/en-us/azure/active-directory/fundamentals/how-to-get-support). |
| Last backup was taken 1 to 14 days ago | This time range is the expected status for the backup monitor. Automated regular backups should occur in this period. |
| Last backup was taken more than 14 days ago. | A timespan longer than two weeks indicates there's an issue with the automated regular backups. Active critical alerts may prevent the managed domain from being backed up. Resolve any active alerts for the managed domain. If the backup monitor doesn't then update the status to report a recent backup, [open an Azure support request](/en-us/azure/active-directory/fundamentals/how-to-get-support). |

#### Synchronization with Microsoft Entra ID monitor

A managed domain regularly synchronizes with Microsoft Entra ID. The number of users and group objects, and the number of changes made in the Microsoft Entra directory since the last sync, affects how long it takes to synchronize. If the managed domain was last synchronized over three days ago, check for and resolve any active alerts. If the synchronization monitor doesn't update the status to show a recent sync after you address any active alerts, [open an Azure support request](/en-us/azure/active-directory/fundamentals/how-to-get-support).

### Alerts

Alerts are generated for issues in a managed domain that need to be addressed for the service to run correctly. Each alert explains the problem and gives a URL that outlines specific steps to resolve the issue. For more information on the possible alerts and their resolutions, see [Troubleshooting alerts](troubleshoot-alerts).

Health status alerts are categorized into the following levels of severity:

- **Critical alerts** are issues that severely impact the managed domain. These alerts should be addressed immediately. The Azure platform can't monitor, manage, patch, and synchronize the managed domain until the issues are resolved.
- **Warning alerts** notify you of issues that may impact the managed domain operations if the problem persists. These alerts also offer recommendations to secure the managed domain.
- **Informational alerts** are notifications that don't negatively impact the managed domain. Informational alerts provide some insight as to what's happening in the managed domain.