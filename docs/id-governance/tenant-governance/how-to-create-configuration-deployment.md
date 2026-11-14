---
layout: Conceptual
title: Create a configuration deployment (Preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-create-configuration-deployment
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to deploy baseline configuration to home and governed tenants and handle partial or failed deployments in Microsoft Entra Tenant Governance.
ms.topic: how-to
ms.date: 2026-11-12T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: f7567ec6-0367-6fc4-5fe4-a40ee3cfb901
document_version_independent_id: f7567ec6-0367-6fc4-5fe4-a40ee3cfb901
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-create-configuration-deployment.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-create-configuration-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-create-configuration-deployment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 583aea87-6fa6-f2ea-cb76-b27fca7fefde
---

# Create a configuration deployment (Preview) - Microsoft Entra ID Governance | Microsoft Learn

Use Configuration deployments to apply baseline-defined configuration to the home tenant or governed tenants. You can create a deployment from baseline JSON, a snapshot, or a configuration baseline template.

## Prerequisites

- Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../../identity/role-based-access-control/permissions-reference#global-administrator).
- The tenant has licenses for **Tenant Governance Basic** or **Tenant Governance Premium**. See [Microsoft Entra Tenant Governance licensing](licensing).
- A reviewed baseline containing only [resources supported for configuration deployments](configuration-deployments#supported-resources) and the settings you want to apply. Currently, only the listed 15 Microsoft Entra and 8 Exchange resource types are supported.
- Delegated write permissions granted to the Tenant Configuration Management service and administrator roles for the selected workload resources. Deployments run on behalf of the signed-in administrator. Application permissions, service principal role assignments, or monitoring read permissions alone aren't sufficient.
- For another tenant, an active [governance relationship](governance-relationships), required delegated permissions, and workload access in the target tenant.

Review [Tenant Governance licensing](licensing) and [Configure configuration management service permissions](how-to-set-up-permissions-tenant-monitoring) before starting.

## Start a deployment

To start creating a deployment, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../../identity/role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Tenant Governance**. Under **Tenant management**, select **Configuration deployments** for the home tenant. Under **Other tenants**, select **Configuration deployments** for a governed tenant.
3. Select **Deploy configuration**.

[![Screenshot of the deployment list with the Deploy configuration command and target tenants.](../media/tenant-governance-configuration-management/configuration-deployments.png)](../media/tenant-governance-configuration-management/configuration-deployments.png#lightbox)

## Complete the deployment wizard

Configure the baseline and target tenant:

1. For a governed-tenant deployment, select the target tenant on **Tenants**. This step isn't shown for home-tenant deployments, which use your current tenant.
2. On **Settings**, enter the deployment name and an optional description.
3. On **Configuration baseline**, upload baseline JSON, import a snapshot, or select a configuration baseline template.
4. Review tenant-specific resource references, dependencies, and the settings that the deployment will change.
5. On **Permissions**, review delegated write permission readiness for the selected workload and tenant. Application permissions and roles assigned to the service principal don't satisfy this check. Separately verify the signed-in administrator's workload roles, which aren't evaluated on this step.
6. On **Ongoing monitoring**, choose whether to monitor for configuration drift after provisioning. Select **Yes** to create a separate monitor from the same configuration, or **No** to deploy without creating a monitor.
7. On **Review**, confirm the target tenant, baseline, and ongoing monitoring choice, and select **Deploy configuration**.

Repeat the process for additional governed tenants, reviewing tenant-specific values and permissions for each target.

Important

A deployment changes resource settings in the selected tenant. Review the baseline and impact before confirming, particularly when deploying settings captured from a different tenant.

## Track deployment status

Open the deployment details and refresh to track progress. The deployment list shows **Running** or **Completed** for the deployment lifecycle. **Completed** doesn't establish that every resource was deployed successfully. Open **Deployment results** to review execution outcomes and **Resource deployment failures** to investigate failed resources.

| Status | What to do |
| --- | --- |
| **In progress** | Track progress until the deployment completes. |
| **Successful** | Validate the resulting configuration with a monitor. |
| **Partially successful** | Identify successful changes and review errors for failed resources. |
| **Failed** | Review error details and actual resource state before another attempt. |

A failed or partially successful deployment doesn't prove that no changes were applied. Don't assume successful changes were rolled back.

The details view shows the baseline version, target tenant, and deployment outcome.

[![Screenshot of deployment details showing the target tenant, baseline version, and execution status.](../media/tenant-governance-configuration-management/configuration-deployment-details.png)](../media/tenant-governance-configuration-management/configuration-deployment-details.png#lightbox)

## Handle failed or partially successful deployments

To address deployment errors, follow these steps:

1. Open the deployment details and identify failed resources and their errors.
2. Review which resources succeeded and confirm their current state in the target tenant.
3. Resolve the reported permission, dependency, or baseline issues. For another tenant, also verify the governance relationship and delegated access.
4. Review the baseline against the current tenant state before attempting changes again.
5. For a completed home-tenant deployment, use **Redeploy** to apply its stored configuration again. For a governed-tenant deployment, use the configuration update flow or create a new deployment; a standalone **Redeploy** action isn't available.
6. Review the new outcome, then use a monitor to verify baseline alignment.

An accepted configuration update isn't proof that another deployment execution completed. Refresh the deployment and check **Deployment results** before submitting the same change again.

## Verify the deployed configuration

Create or update a [configuration monitor](how-to-create-monitor) for the deployment baseline and target tenant. Review a completed monitor run and any remaining drift.

If you selected **Yes** on **Ongoing monitoring**, verify that the separate monitor was created. A warning that ongoing monitoring couldn't be created doesn't undo the deployment. Resolve the monitor error and create a monitor separately if needed.