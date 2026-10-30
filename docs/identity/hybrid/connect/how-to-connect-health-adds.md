---
layout: Conceptual
title: Using Microsoft Entra Connect Health with AD DS - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-health-adds
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This is the Microsoft Entra Connect Health page that will discuss how to monitor AD DS.
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.subservice: hybrid-connect
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2026-09-10T00:00:00.0000000Z
locale: en-us
document_id: fa141fe0-cd51-bcf7-b3b8-86fcf9e67982
document_version_independent_id: ef122da2-a7ea-e0e3-147a-9f39eec85da8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-health-adds.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-health-adds
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-health-adds.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 945200fb-a8b9-e270-206e-a51d3eb502f0
---

# Using Microsoft Entra Connect Health with AD DS - Microsoft Entra ID | Microsoft Learn

The following documentation is specific to monitoring Active Directory Domain Services with Microsoft Entra Connect Health. The supported versions of AD DS are Windows Server 2016, 2019, 2022, and 2025.

For more information on monitoring AD FS with Microsoft Entra Connect Health, see [Using Microsoft Entra Connect Health with AD FS](how-to-connect-health-adfs). Additionally, for information on monitoring Microsoft Entra Connect (Sync) with Microsoft Entra Connect Health see [Using Microsoft Entra Connect Health for Sync](how-to-connect-health-sync).

Open [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth), select **AD DS services**, and then select a service. The service page provides:

- An **Essentials** section with forest and monitoring information.
- Summary cards for domain controllers, replication status, and alerts.
- Performance charts for LDAP successful binds, NTLM authentications, and Kerberos authentications.

[![Screenshot of the Connect Health AD DS service overview with callouts for forest details, the domain controller list, and replication status.](media/how-to-connect-health-adds/connect-health-adds-overview.png)](media/how-to-connect-health-adds/connect-health-adds-overview.png#lightbox)

## Alerts for Microsoft Entra Connect Health for AD DS

The **Alerts** page lists active and resolved alerts related to your domain controllers. Select an alert row to open the details panel, which contains alert metadata, affected servers, resolution guidance, related documentation, and a feedback option.

Use the command bar to refresh the list, change the time range to include older resolved alerts, or open notification settings. You can also search the alert list.

## Domain Controllers Dashboard

On the service page, select **View all domain controllers** to open the domain controllers list. The list shows operational metrics and the health status of monitored domain controllers.

Use **Group by domain** or **Group by site** to understand the environment topology. You can search by domain controller name, domain, site, role, or status; include or exclude monitored and not-monitored domain controllers; and use **Choose columns** to customize the table.

## Replication Status Dashboard

On the service page, select **View replication details** to view the replication status and topology of monitored domain controllers. The page shows the status of the most recent replication attempt and can be grouped by domain or site. Use search to find a domain controller, and expand groups to review source and destination domain controllers, naming context, status, and the last attempted replication.

Select a replication error to open the **Replication Error Details** panel. The panel includes the source and target domain controllers, naming context, site, domain, last attempted and successful synchronization times, recommended fix, and related troubleshooting link when available.

## Monitoring

The service page shows 24-hour graphical trends for three default performance counters: LDAP successful binds, NTLM authentications, and Kerberos authentications. Compare the charts to identify authentication-volume changes, and then select **View detailed monitoring** for a metric to open a larger view and change the time range.

[![Screenshot of Connect Health AD DS monitoring with callouts for comparing LDAP, NTLM, and Kerberos trends and opening detailed monitoring.](media/how-to-connect-health-adds/connect-health-adds-performance-monitoring.png)](media/how-to-connect-health-adds/connect-health-adds-performance-monitoring.png#lightbox)

Select **View all Performance Metrics** to open the full collection. Use **Manage counters** to select the metrics you want to display, drag charts to reorder them, and select a chart to compare data for monitored domain controllers over the available time ranges.

## Related links

- [Microsoft Entra Connect Health](whatis-azure-ad-connect)
- [Microsoft Entra Connect Health Agent Installation](how-to-connect-health-agent-install)
- [Microsoft Entra Connect Health Operations](how-to-connect-health-operations)
- [Using Microsoft Entra Connect Health with AD FS](how-to-connect-health-adfs)
- [Using Microsoft Entra Connect Health for sync](how-to-connect-health-sync)
- [Microsoft Entra Connect Health FAQ](reference-connect-health-faq)
- [Microsoft Entra Connect Health Version History](reference-connect-health-version-history)