---
layout: Conceptual
title: Configuration deployments (Preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/configuration-deployments
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how configuration deployments apply baseline settings to home and governed tenants in Microsoft Entra Tenant Governance.
ms.topic: concept-article
ms.date: 2026-11-12T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: f658efb8-5d81-4922-06d7-4fdc46f5d338
document_version_independent_id: f658efb8-5d81-4922-06d7-4fdc46f5d338
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/configuration-deployments.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/configuration-deployments
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/configuration-deployments.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 3c401296-a534-30b1-75e3-5dfcda97e98c
---

# Configuration deployments (Preview) - Microsoft Entra ID Governance | Microsoft Learn

A configuration deployment applies baseline-defined settings to a target tenant. Use Configuration deployments to apply baseline-defined configuration to the home tenant or governed tenants.

Use deployments to roll out approved settings, establish a known-good configuration, or apply controlled changes. Unlike a monitor, which evaluates configuration, a deployment changes resource settings.

The deployment list shows the source template, target tenant, and status for each deployment.

[![Screenshot of configuration deployments with source templates, target tenants, and statuses.](../media/tenant-governance-configuration-management/configuration-deployments.png)](../media/tenant-governance-configuration-management/configuration-deployments.png#lightbox)

## Supported resources

Configuration deployments currently support only the following 23 resource types: 15 Microsoft Entra resources and 8 Exchange resources. This list doesn't apply to resource support for snapshots or monitoring.

### Microsoft Entra resources (15)

- `microsoft.entra.conditionalaccesspolicy`
- `microsoft.entra.namedlocationpolicy`
- `microsoft.entra.authorizationpolicy`
- `microsoft.entra.authenticationmethodpolicy`
- `microsoft.entra.authenticationmethodpolicyemail`
- `microsoft.entra.authenticationmethodpolicyfido2`
- `microsoft.entra.authenticationmethodpolicysms`
- `microsoft.entra.authenticationmethodpolicyvoice`
- `microsoft.entra.authenticationmethodpolicyx509`
- `microsoft.entra.crosstenantaccesspolicyconfigurationdefault`
- `microsoft.entra.crosstenantaccesspolicyconfigurationpartner`
- `microsoft.entra.externalidentitypolicy`
- `microsoft.entra.roledefinition`
- `microsoft.entra.securitydefaults`
- `microsoft.entra.tenantdetails`

### Exchange resources (8)

- `microsoft.exchange.accepteddomain`
- `microsoft.exchange.antiphishpolicy`
- `microsoft.exchange.casmailboxplan`
- `microsoft.exchange.hostedcontentfilterpolicy`
- `microsoft.exchange.mailboxplan`
- `microsoft.exchange.malwarefilterpolicy`
- `microsoft.exchange.owamailboxpolicy`
- `microsoft.exchange.safelinkspolicy`

## Baseline and target tenant

Create a deployment from baseline JSON, a snapshot, or a configuration baseline template. Review the resource properties and dependencies before applying the baseline.

Configuration management supports operations in the home tenant and in other tenants that are connected through governance relationships. For a governed tenant, verify the active relationship, delegated access, and workload permissions. A relationship alone doesn't grant permission to change every resource.

## Deployment status

A deployment is asynchronous. Use its status and resource-level results to determine the outcome.

The deployment list displays **Running** or **Completed**. These lifecycle states don't describe whether every resource was applied successfully. Review the run outcome on **Deployment results**, and use **Resource deployment failures** to inspect errors.

| Execution outcome | Meaning | Next action |
| --- | --- | --- |
| **In progress** | The deployment is applying configuration. | Wait for completion and review available resource outcomes. |
| **Successful** | The execution reports successful completion. | Use a monitor to validate alignment with the baseline. |
| **Partially successful** | Some configuration changes succeeded and others didn't. | Review each failed resource and resolve its error before retrying. |
| **Failed** | The deployment didn't complete successfully. | Review errors and actual resource state before planning another deployment. |

Don't treat a failed or partially successful deployment as proof that no settings changed. Inspect resource outcomes and the target tenant before retrying. Don't assume that deployment failure rolls back successful changes.

The following details view illustrates a partially successful deployment and its baseline version.

[![Screenshot of deployment details with the template version and a partial-success status.](../media/tenant-governance-configuration-management/configuration-deployment-details.png)](../media/tenant-governance-configuration-management/configuration-deployment-details.png#lightbox)

## Validate after deployment

Create or update a monitor for the deployed baseline and target tenant. A successful monitor evaluation provides evidence that the actual configuration aligns with the expected values. Later monitor runs detect changes after deployment.

On **Ongoing monitoring** in the deployment wizard, select **Yes** to create a separate monitor from the same configuration. If monitor creation fails, the deployment can still exist; review the warning and create the monitor separately.

Workload-specific systems remain the source of truth for the resource state.