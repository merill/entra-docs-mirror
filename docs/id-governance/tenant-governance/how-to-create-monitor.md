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
description: Learn how to create a configuration monitor for your home tenant or a governed tenant in Microsoft Entra Tenant Governance.
ms.topic: how-to
ms.date: 2026-11-10T00:00:00.0000000Z
ai-usage: ai-assisted
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

Configuration management supports operations in the home tenant and in other tenants that are connected through governance relationships.

## Prerequisites

- Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../../identity/role-based-access-control/permissions-reference#global-administrator).
- The tenant has licenses for **Tenant Governance Basic** or **Tenant Governance Premium**. Basic includes monitoring in the home tenant and governed tenants; Premium isn't required solely for cross-tenant monitoring. For licensing requirements and resource capacity, see [Microsoft Entra Tenant Governance licensing](licensing).
- You have read permissions for the resource types included in the monitor's configuration baseline.
- The Tenant Configuration Management service has permissions for the workloads and resource types included in the monitor baseline. To assign or remove permissions for the service, see [Configure configuration management service permissions](how-to-set-up-permissions-tenant-monitoring).
- For monitoring another tenant, an active [governance relationship](governance-relationships) connects your tenant to the governed tenant. Configure the required delegated permissions and ensure that your delegated roles allow you to read the selected resources in that tenant.

## Start monitor creation

To start creating a configuration monitor, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../../identity/role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Tenant Governance**. Under **Tenant management**, select **Monitors** for the home tenant. Under **Other tenants**, select **Monitors (Preview)** for a governed tenant.
3. Select **New monitor**.

[![Screenshot of the monitor list with the New monitor command and Tenant Governance navigation.](../media/tenant-governance-configuration-management/monitors-overview.png)](../media/tenant-governance-configuration-management/monitors-overview.png#lightbox)

## Complete the monitor wizard

Complete the wizard steps to configure and create the monitor:

1. For a governed-tenant monitor, select the target tenant on **Tenants**. This step isn't shown for home-tenant monitors, which use your current tenant.
2. On **Settings**, enter a monitor name and an optional description. Governed-tenant monitor names must contain 8 to 256 characters and use only letters, numbers, and spaces.
3. On **Configuration baseline**, upload a baseline JSON file, select **Import from snapshot**, or select a configuration baseline template. If you select **Import from snapshot**, search by snapshot name, select a snapshot, and then select **Import**. You can use the in-page editor to manually compose or edit the configuration baseline.
4. On **Permissions**, review the service's application permissions and role assignments for the selected target tenant, including whether the service has permission to:

    - Read the required Microsoft Graph resources, to monitor Microsoft Entra or Intune resources.
    - Authenticate to Exchange, to monitor Exchange, Defender, or Purview resources.
    - Use the **Teams Reader** role, to monitor Teams resources.

    Note

    This step is read-only. It doesn't evaluate whether the user is authorized to create a monitor with the selected resources. It also doesn't show or validate whether the permissions assigned to the configuration management service locally within Exchange Online, Defender, or Purview are sufficient to create a monitor with resources in those services.
5. If readiness shows missing permissions, configure them on **Configuration management permissions**, and then review readiness again. For another tenant, also verify that the governance relationship and delegated access are active.
6. On **Review**, verify the target tenant and baseline, review the summary, and create the monitor.

After you create the monitor, it runs automatically on its schedule. Results are available after the first run completes. The home-tenant wizard in earlier versions of the experience shows **Permissions** before **Configuration baseline**, rather than starting with **Settings**.

To learn how to review monitor results and configuration drift, see [View monitor results and manage monitors](how-to-see-monitor-results).

## Troubleshoot other-tenant monitoring (Preview)

The governed-tenant monitor list shows the target tenant for each monitor.

[![Screenshot of governed-tenant monitors showing the target tenant and status of each monitor.](../media/tenant-governance-configuration-management/governed-tenant-monitors.png)](../media/tenant-governance-configuration-management/governed-tenant-monitors.png#lightbox)

If the target tenant isn't available, verify the governance relationship and your access to that tenant. If creation or a later run fails, review the error and permission readiness for the target workload. Relationship changes, removed consent, or missing workload-specific roles can prevent later runs even if monitor creation succeeded.