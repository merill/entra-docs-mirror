---
layout: Conceptual
title: Create configuration snapshots - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-create-snapshots
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to capture tenant configuration in Microsoft Entra Tenant Governance and use snapshots for baseline templates, deployments, and monitors.
ms.topic: how-to
ms.date: 2026-11-10T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 9cc6c6cd-c379-0b0d-b692-0f24982ce593
document_version_independent_id: 9cc6c6cd-c379-0b0d-b692-0f24982ce593
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-create-snapshots.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-create-snapshots
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-create-snapshots.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 9d3cec28-64b5-4baa-0a7f-a00ee94552ab
---

# Create configuration snapshots - Microsoft Entra ID Governance | Microsoft Learn

Configuration snapshots capture the current state of selected tenant configuration resources. Create a snapshot when you want to establish a configuration baseline for monitoring configuration drift of a tenant in a known-good configuration, or to collect configuration data for audit evidence.

Use a snapshot as the starting point for a configuration baseline template, deployment, or monitor: **snapshot &gt; template or baseline &gt; deployment or monitor**. A snapshot captures actual settings, not necessarily approved settings. Review and edit the captured baseline before reusing it.

## Prerequisites

- Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../../identity/role-based-access-control/permissions-reference#global-administrator).
- The tenant has licenses for **Tenant Governance Basic** or **Tenant Governance Premium**. For current licensing requirements, see [Microsoft Entra Tenant Governance licensing](licensing).
- Tenant Governance Basic includes a quota for the number of resources that you can snapshot. A tenant gets additional quota for snapshotted resources for each Tenant Governance Premium license it has. If your tenant exceeds its monthly quota, you can't create new snapshots.
- You have read permissions for every resource type included in the snapshot.
- The Tenant Configuration Management service has service authorization for every workload and resource type included in the snapshot. To assign or remove permissions for the service, see [Configure configuration management service permissions](how-to-set-up-permissions-tenant-monitoring).

## Create a snapshot

To create a configuration snapshot, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../../identity/role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Tenant Governance** &gt; **Snapshots**.
3. Select **New snapshot**.
4. On the service and resource selection step, select the resource types to include in the snapshot.
5. On **Settings**, enter a display name of 8 to 32 characters using only letters, numbers, and spaces, and an optional description.
6. On **Permissions**, review whether the service has permission to:

    - Read the required Microsoft Graph resources, to snapshot Microsoft Entra or Intune resources.
    - Authenticate to Exchange, to snapshot Exchange, Defender, or Purview resources.
    - Use the **Teams Reader** role, to snapshot Teams resources.

    Note

    This step doesn't evaluate whether the user is authorized to create a snapshot with the selected resources. It also doesn't show or validate whether the permissions assigned to the configuration management service locally within Exchange Online, Defender, or Purview are sufficient to create a snapshot with resources in those services.
7. On **Review and create**, review the summary and create the snapshot.

## Check snapshot status

Snapshot creation is asynchronous. A snapshot progresses from **Not started** to **In progress**. Select **Refresh** in the command bar to check progress until the snapshot succeeds, fails, or is partially successful. The time it takes to complete a snapshot is roughly proportional to the number of resources being snapshotted.

The snapshot list shows creation and expiration times alongside each snapshot's status.

[![Screenshot of snapshots with the New snapshot command, status, creation time, and expiration time.](../media/tenant-governance-configuration-management/snapshots.png)](../media/tenant-governance-configuration-management/snapshots.png#lightbox)

## View snapshot details

To view the details of a completed snapshot, follow these steps:

1. Open a completed snapshot from the snapshots list.
2. On the **Overview** tab, review the name, description, creation time, completion time, expiration time, status, and included resource counts. Errors, if any, appear on this page. You can expand an error to see details.
3. On the **Configuration baseline** tab, view or download the generated configuration baseline JSON.

Important

Snapshot jobs and their generated snapshots are retained for 7 days. Download and store the baseline JSON before expiration if you need to reuse it.

## Use a snapshot as a baseline template (Preview)

To turn captured settings into a reusable standard, follow these steps:

1. Open a completed snapshot and review its status and errors. If it's partially successful, identify any missing resources before using it as a baseline.
2. On **Configuration baseline**, download the generated JSON.
3. Review the resource settings and update them to reflect your approved configuration.
4. [Create a configuration baseline template](how-to-use-configuration-baseline-templates#create-a-template) by uploading the reviewed JSON or importing the snapshot.

Store approved baseline versions separately from the snapshot so that snapshot expiration doesn't remove your source configuration.

## Create a monitor from a snapshot

To create a configuration monitor from a completed snapshot, follow these steps:

1. Open a completed snapshot.
2. Select **Create as monitor**.
3. The monitor creation wizard opens with the snapshot baseline imported. Snapshot-only fields, such as `@odata` metadata and object ID, are removed from the baseline. Continue with the remaining steps in the monitor creation experience, such as setting a name for the monitor and reviewing permissions, as described in [Create a configuration monitor](how-to-create-monitor).

## Create a deployment from a snapshot baseline (Preview)

To apply captured configuration to a target tenant, follow these steps:

1. Open a completed snapshot and review or download its baseline JSON.
2. Start a [configuration deployment](how-to-create-configuration-deployment).
3. Select the home tenant or another tenant connected through a governance relationship.
4. Import the snapshot, upload the reviewed JSON, or use a template created from it.
5. Review tenant-specific resource references, proposed settings, and permission readiness before creating the deployment.

Creating a snapshot doesn't change the target tenant. A deployment applies the baseline settings and requires the corresponding write permissions.