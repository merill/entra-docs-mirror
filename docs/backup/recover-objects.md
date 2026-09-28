---
layout: Conceptual
title: Recover objects using Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/backup/recover-objects
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id
manager: dougeby
description: Learn how to recover objects to a previous state using Microsoft Entra Backup and Recovery from difference reports or backups
ms.date: 2026-03-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
locale: en-us
document_id: 96ecf955-6557-0248-4750-8bf653164001
document_version_independent_id: 96ecf955-6557-0248-4750-8bf653164001
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/backup/recover-objects.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: backup/recover-objects
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/backup/recover-objects.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5ae35c05-ad20-3404-e914-52f79fc7d836
---

# Recover objects using Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn

Learn how to recover objects to a previously known-good state by using Microsoft Entra Backup and Recovery. Recovery includes restoring, soft-deleting, and updating supported objects and attributes.

Key details:

- A recovery ID identifies the recovery job.
- Backups are created automatically once per day. Only retained backups are available for recovery and for generating difference reports.
- Only one recovery runs at a time. If another job (recovery job or difference report) is already running, you must wait for it to complete or cancel it before starting a new one.
- **Recovery History** retains recovery details for seven days after the recovery completion date.
- Audit logs record all recovery actions.

## Prerequisites

The tenant must meet the [Backup and Recovery prerequisites](overview#prerequisites), including **Microsoft Entra ID P1 or P2** licenses. To recover objects, you need the **Microsoft Entra Backup Administrator** role.

## Recover from a difference report

Use this method when you already created a difference report and reviewed the changes.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Microsoft Entra Backup Administrator**.
2. Go to **Backup and recovery** &gt; **Difference reports**. Select a completed difference report.

    ![Screenshot of the Difference Reports page showing three completed reports with available backups.](media/recover-objects/difference-reports-select.png#lightbox)

    Difference reports compare the selected backup with the current tenant state and show changed attributes and links.
3. After inspecting the objects listed in the difference report, select **Recover** to start recovery.

    ![Screenshot of the Recover from difference report dialog showing the list of objects that will be recovered, with the Recover button at the bottom.](media/recover-objects/recover-from-difference-report.png#lightbox)

    If you recover from a difference report that was created with scoping filters, recovery automatically uses the same scope and doesn't allow additional filtering. To recover a different set of objects, start from the backups page and run difference report to review changes.
4. (Optional) To recover a single high-priority object without initiating a full recovery job, open the object's changed attributes panel and select **Recover this object**.

    ![Screenshot of the View changed attributes panel for a user object, with a confirmation dialog asking to recover the specific object.](media/recover-objects/recover-single-object.png#lightbox)

    Difference reports are a point-in-time comparison. If objects are modified in the tenant after the report is created, those changes aren't reflected in the report. When you recover from a difference report, recovery applies to the tenant's most current state. This might result in a different set of changes than the difference report shows.

## Recover directly from a backup

Creating a difference report lets you preview changes before recovery. To skip this step, recover directly from a backup. Only retained backups are listed on the **Backups** page.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Microsoft Entra Backup Administrator**.
2. Go to **Backup and recovery** &gt; **Backups**. Select a backup and select **Recover backup**.

    ![Screenshot of the Backups page with a backup selected and the Recover backup button visible in the toolbar.](media/recover-objects/recover-backup-select.png#lightbox)
3. (Optional) Apply scoping filters to limit the objects included in recovery. Choose one of these options:

    - **Recover all objects in their previous state**: Recovers all supported objects in the tenant.

        ![Screenshot of the Recover backup dialog with the Recover all objects in their previous state option selected and the cursor on the Recover button.](media/recover-objects/recover-backup-all-objects.png#lightbox)
    - **Recover only certain types of objects**: Limits recovery to selected object types, such as Users or Conditional Access Policies.

        ![Screenshot of the Recover backup dialog with Recover only certain types of objects selected and type options shown.](media/recover-objects/recover-backup-object-types.png#lightbox)
    - **Recover only specific objects by their ID**: Limits recovery to specific objects by their object IDs. Enter up to 100 object IDs across different object types.

        ![Screenshot of the Recover backup dialog with Recover only specific objects by ID selected and object ID entries shown.](media/recover-objects/recover-backup-object-ids.png#lightbox)
4. Select **Recover** to start the recovery job.

Warning

Recovery actions apply directly to your tenant and can't be undone automatically. Review changes in a difference report before starting recovery. The recovery job records all changes in audit logs.

## Cancel a recovery

Cancel a recovery job while it's running. Any recovery actions completed before cancelation remain in effect.

1. Go to **Backup and recovery** &gt; **Recovery History**.
2. Select the in-progress recovery job, and then select **Cancel**.

    ![Screenshot of the Recovery History page showing completed and in-progress recovery jobs, with the Cancel button visible in the toolbar.](media/recover-objects/cancel-recovery-job.png#lightbox)

Note

- Soft-deleted users, Microsoft 365 Groups, cloud security groups, application registrations, and service principals can be restored for 30 days. For more information, see [Soft deletion in Microsoft Entra Backup and Recovery](soft-deletion). Backup and Recovery restores supported properties and links from retained backups.
- Hard-deleted objects can't be recovered. Use Protected Actions to prevent unwanted hard deletions in your tenant.