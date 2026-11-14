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
description: Learn how to configure application permissions, delegated permissions, and roles for configuration management in home and governed tenants.
ms.topic: how-to
ms.date: 2026-11-12T00:00:00.0000000Z
ai-usage: ai-assisted
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
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: b7434e81-131e-9bf2-3020-a4ca16e619b3
---

# Configure configuration management service permissions - Microsoft Entra ID Governance | Microsoft Learn

Use the **Configuration management permissions** page to assign or remove permissions for the Tenant Configuration Management service. The service uses these permissions for snapshots, deployments, and monitors. Templates store baseline definitions; operations that use those definitions require the corresponding workload permissions.

Configure service permissions before running an operation that includes the corresponding workload resources. Missing permissions can cause incomplete snapshots, deployment failures, or failed monitor runs.

When you create a monitor or snapshot, the **Permissions** step shows whether the service has the least-privilege permissions for the resource types you selected. This step is read-only. If the wizard shows that required least-privilege permissions are missing, use the **Configuration management permissions** page to add them.

## Prerequisites

- Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator) to grant application or delegated permissions and assign Microsoft Entra roles to the service principal.
- For operations in another tenant, an active [governance relationship](governance-relationships) and delegated administration access for the target tenant and workload. Review both relationship-level and workload-specific access in [Cross-tenant delegated administration](cross-tenant-delegated-administration).

## Choose application or delegated permissions

Use the **Application permissions** tab for app-only access used by the service to capture snapshots and run monitors. Use **Entra roles** for Microsoft Entra roles assigned to the service principal.

Use the **Delegated permissions** tab for configuration deployments. Deployments call workload APIs on behalf of the signed-in administrator and require delegated write permissions. Application permissions and roles assigned to the service principal don't satisfy the deployment wizard's delegated permission check. The administrator must also have the required workload roles.

For governed-tenant operations, also configure delegated administration through the governance relationship. This cross-tenant access doesn't replace the background service's application permissions for monitoring. Permission readiness for monitoring checks application permissions and service principal role assignments in the selected tenant; deployment readiness checks delegated write permissions.

## Open Configuration management permissions

To open the permissions page, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **Tenant Governance** &gt; **Configuration management permissions**.

[![Screenshot of the Application permissions tab with permissions and the Add permissions command.](../media/tenant-governance-configuration-management/application-permissions.png)](../media/tenant-governance-configuration-management/application-permissions.png#lightbox)

## Assign application permissions and roles

Assign permissions based on the workloads that contain the resources you want to snapshot, deploy, or monitor:

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

## Assign delegated permissions

Use the **Delegated permissions** tab to configure delegated access required by the operation and target workload:

1. Open **Configuration management permissions**.
2. Select the **Delegated permissions** tab.
3. Select **Add delegated permission**.
4. Select the delegated permissions required for the feature and target workload.
5. Grant admin consent when prompted as a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator) or [Global Administrator](../../identity/role-based-access-control/permissions-reference#global-administrator).
6. Verify that the permissions appear in the list. Review their grant state on **Permissions** in the deployment wizard.

[![Screenshot of the Delegated permissions tab with sample permissions and the Add permissions command.](../media/tenant-governance-configuration-management/delegated-permissions.png)](../media/tenant-governance-configuration-management/delegated-permissions.png#lightbox)

For other-tenant operations, also verify that the governance relationship is active and that the signed-in user has the delegated roles required in the governed tenant. Consent alone doesn't grant the user workload access.

If readiness shows missing permissions, resolve them before running the operation. The governed-tenant wizard's permission check is informational; reaching **Review** doesn't prove that all permissions or administrator roles are sufficient. A readiness check doesn't replace validation of service-local permissions in Exchange Online, Defender, or Purview.

## Remove permissions

Select the **Application permissions**, **Delegated permissions**, or **Entra roles** tab as appropriate. Select the checkbox next to the permission or role, and then select **Remove** in the command bar.

Removing permissions can affect later monitor runs or deployments that depend on them, including operations targeting governed tenants.