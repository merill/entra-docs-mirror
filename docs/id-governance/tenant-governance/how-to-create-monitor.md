---
layout: Conceptual
title: Create a configuration monitor - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-create-monitor
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to create a configuration monitor in Microsoft Entra Tenant Governance to evaluate a tenant against a configuration baseline and report drift
ms.topic: how-to
ms.date: 2026-07-28T00:00:00.0000000Z
locale: en-us
document_id: 2f680669-2b4e-7274-2d76-03e42e4de963
document_version_independent_id: 2f680669-2b4e-7274-2d76-03e42e4de963
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-create-monitor.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-create-monitor
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-create-monitor.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: fae7c89f-eab0-366b-5396-d35031585c58
---

# Create a configuration monitor - Microsoft Entra ID Governance | Microsoft Learn

Configuration monitors evaluate a tenant against a configuration baseline and report configuration drift. Use a monitor when you want to track whether a tenant stays aligned with a known-good configuration.

## Prerequisites

- The tenant has licenses for **Tenant Governance Basic** or **Tenant Governance Premium**. For current licensing requirements, see [Microsoft Entra Tenant Governance licensing](licensing).
- Tenant Governance Basic includes a quota for the number of resources that you can monitor. If the resources in the monitor cause the tenant to exceed its quota, monitor creation fails. An organization gets additional quota for monitored resources for each Tenant Governance Premium license it has.
- The signed-in user is in a Microsoft Entra privileged role and has permission to create configuration monitors. The user must also have read permissions for the resource types included in the monitor's configuration baseline.
- The Tenant Configuration Management service has permissions for the workloads and resource types included in the monitor baseline. To assign or remove permissions for the service, see [Configure configuration management service permissions](how-to-set-up-permissions-tenant-monitoring).

## Start monitor creation

To start creating a configuration monitor, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a user with the required role and permissions.
2. Browse to **Tenant Governance** &gt; **Monitors**.
3. Select **New**.

## Complete the monitor wizard

Complete the wizard steps to configure and create the monitor:

1. On **Settings**, enter a unique monitor name of at least eight characters and an optional description.
2. On **Configuration baseline**, upload a baseline JSON file or select **Import from snapshot**. If you select **Import from snapshot**, search by snapshot name, select a snapshot, and then select **Import**. You can use the in-page editor to manually compose or edit the configuration baseline.
3. On **Permissions**, review whether the service has permission to:

    - Read the required Microsoft Graph resources, to monitor Microsoft Entra or Intune resources.
    - Authenticate to Exchange, to monitor Exchange, Defender, or Purview resources.
    - Use the **Teams Reader** role, to monitor Teams resources.

    Note

    This step doesn't evaluate whether the user is authorized to create a monitor with the selected resources. It also doesn't show or validate whether the permissions assigned to the configuration management service locally within Exchange Online, Defender, or Purview are sufficient to create a monitor with resources in those services.
4. On **Review**, review the summary and create the monitor.

After you create the monitor, it runs automatically on a periodic schedule. Monitor results are available after the monitor runs for the first time, between zero and six hours after creation.

To learn how to review monitor results and configuration drift, see [View monitor results and manage monitors](how-to-see-monitor-results).