---
layout: Conceptual
title: Configure configuration management service permissions - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-set-up-permissions-tenant-monitoring
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to assign or remove the application permissions and roles that the Tenant Configuration Management service uses to create snapshots and run monitors
ms.topic: how-to
ms.date: 2026-07-28T00:00:00.0000000Z
locale: en-us
document_id: 9833a04f-cc60-4c73-1d5d-235f5d754bfe
document_version_independent_id: 9833a04f-cc60-4c73-1d5d-235f5d754bfe
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-set-up-permissions-tenant-monitoring.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-set-up-permissions-tenant-monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-set-up-permissions-tenant-monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b7434e81-131e-9bf2-3020-a4ca16e619b3
---

# Configure configuration management service permissions - Microsoft Entra ID Governance | Microsoft Learn

Use the **Configuration management permissions** page to assign or remove permissions for the Tenant Configuration Management service. The service uses these permissions to create snapshots and run monitors.

Configure service permissions before you create snapshots or monitors that include the corresponding workload resources. Missing service permissions can cause a snapshot to be incomplete or a monitor run to fail.

When you create a monitor or snapshot, the **Permissions** step shows whether the service has the least-privilege permissions for the resource types you selected. This step is read-only. If the wizard shows that required least-privilege permissions are missing, use the **Configuration management permissions** page to add them.

## Prerequisites

- A Microsoft Entra role that can assign or remove app-only permissions for service principals in your tenant, such as [Global Administrator](../../identity/role-based-access-control/permissions-reference#global-administrator) or [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator). To see which roles can perform this task, see the [Microsoft Entra built-in roles reference](../../identity/role-based-access-control/permissions-reference).

## Open Configuration management permissions

To open the permissions page, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Tenant Governance** &gt; **Configuration management permissions**.

## Assign permissions

Assign permissions based on the workloads that contain the resources you want to snapshot or monitor:

- **Microsoft Entra ID or Intune resources**: On the **Application permissions** tab, add the app-only permissions for the relevant Microsoft Graph resources.

    - For the permissions required to snapshot or monitor Microsoft Entra resources, see [Supported Microsoft Entra resources for Tenant Configuration Management](/en-us/graph/utcm-entra-resources).
    - For the permissions required to snapshot or monitor Intune resources, see [Supported Microsoft Intune resources for Tenant Configuration Management](/en-us/graph/utcm-intune-resources).
- **Teams resources**: On the **Entra roles** tab, assign the **Teams Reader** Microsoft Entra role.
- **Exchange Online resources**: On the **Application permissions** tab, assign **Exchange.ManageAsApp**. Then use Exchange Online PowerShell to assign Exchange roles to the Tenant Configuration Management service principal. For the steps, see [App-only authentication in Exchange Online PowerShell and Security & Compliance PowerShell](/en-us/powershell/exchange/app-only-auth-powershell-v2#step-2-assign-api-permissions-to-the-application).

    For the permissions required to snapshot or monitor Exchange resources, see [Supported Microsoft Exchange resources for Tenant Configuration Management](/en-us/graph/utcm-exchange-resources).
- **Defender or Purview resources**: On the **Application permissions** tab, assign **Exchange.ManageAsApp**. Then use Security & Compliance PowerShell to assign Security and Compliance (Defender and Purview) roles to the Tenant Configuration Management service principal. For the steps, see [Connect to Security & Compliance PowerShell](/en-us/powershell/exchange/connect-to-scc-powershell).

    For the permissions required to snapshot or monitor Defender or Purview resources, see [Supported Microsoft Security and Compliance resources for Tenant Configuration Management](/en-us/graph/utcm-securityandcompliance-resources).

Note

The **Configuration management permissions** page doesn't show workload permissions that are assigned to the service within Exchange Online, Defender, or Purview. Use Exchange Online PowerShell or Security & Compliance PowerShell to assign and remove those permissions.

## Remove permissions

To remove a permission or a Microsoft Entra role, select the checkbox next to its name, and then select **Remove** in the command bar.