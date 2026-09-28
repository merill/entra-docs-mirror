---
layout: Conceptual
title: Troubleshoot Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/backup/troubleshooting
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id
manager: dougeby
description: Diagnose and resolve common issues with Microsoft Entra Backup and Recovery, including backup access, difference reports, and recovery jobs
ms.date: 2026-03-02T00:00:00.0000000Z
ms.topic: troubleshooting
ai-usage: ai-assisted
locale: en-us
document_id: 882287b4-d8cb-850e-4e7a-73d1e9b6731d
document_version_independent_id: 882287b4-d8cb-850e-4e7a-73d1e9b6731d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/backup/troubleshooting.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: backup/troubleshooting
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/backup/troubleshooting.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9c89ae26-a940-0b8f-7d3e-89b78182ed92
---

# Troubleshoot Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn

This article helps you diagnose and resolve common issues when using Microsoft Entra Backup and Recovery, including backup access, difference report jobs, and recovery jobs.

## Before you begin

Verify these prerequisites before troubleshooting:

- Your tenant is a **workforce tenant** (External ID and B2C tenants aren't supported).
- Your tenant has **Microsoft Entra ID P1 or P2** licenses.
- You're signed in with an account that has the appropriate **Microsoft Entra Backup role**:
    - **Microsoft Entra Backup Reader**
    - **Microsoft Entra Backup Administrator**

The **Global Administrator** role also has the required permissions.

If these prerequisites aren't met, operations might fail with authorization errors or empty results.

## Issue: No backups are listed

This issue occurs when the backup list shows fewer backups than expected or displays duplicate timestamps.

### Symptoms

- Fewer than seven days of backups are visible, instead of the expected seven days.
- Two or more backups appear to have the same timestamp in the backup list.

### Possible causes

The oldest backup might age out earlier during service initialization, tenant onboarding, or transient backend conditions, temporarily resulting in fewer than seven visible days of backups. This condition doesn't indicate data loss or a backup failure.

### Resolution

No action is required. The service continues to create new backups automatically.

## Issue: Can't start a difference report or recovery job

This issue occurs when a difference report or recovery job fails to start because of a conflict, authorization failure, or unsupported object type.

### Symptoms

- Difference report or recovery job fails to start.
- An error indicates a conflict or authorization failure.
- The object type you want to use doesn't appear in the scoping filter drop-down.

### Possible causes

- Another difference report or recovery job is already running.
- The signed-in user doesn't have the required Microsoft Entra Backup role.
- The selected object type isn't supported for backup and recovery in the current release.

### Resolution

1. Check whether another difference report or recovery job is running. Only one job can run at a time.
2. Verify that your account has the appropriate role: **Microsoft Entra Backup Reader** for difference reports or **Microsoft Entra Backup Administrator** for recovery.
3. Confirm that the object type and object attributes you're trying to scope are supported. Only supported object types and attributes appear in the scoping filter.

## Issue: Difference report problems

This section helps troubleshoot common issues related to difference reports, including missing changes, long-running jobs, failed jobs, canceled jobs, and missing reports.

### Symptoms

- The difference report didn't include the changes for the object you were looking for.
- The difference report has been running for several hours, and you don't know when it finishes.
- The difference report state is "Failed."
- You can't find the difference report that you generated earlier.
- You selected **Cancel**, but the difference report still appears to be running.

### Possible causes

- The object or property isn't supported for preview in the current release.
- The object didn't change between the backup state and the current state.
- The difference report is processing a large number of objects or changes.
- Only one difference report or recovery job can run at a time.
- The report was canceled or failed before completion.
- Difference reports aren't retained indefinitely.

### Resolution

**If expected changes are missing:**

1. Confirm that the object type and properties are supported for the current release.
2. Verify that the object changed after the backup was taken.
3. Hard-deleted objects and unsupported properties aren't included.

**If the difference report is running for a long time:**

See the [estimated difference report generation time](backup-difference-report-recovery-model). Large tenants or large changesets might take longer to process.

- Allow the report to continue running unless cancellation is required.

**If the difference report failed:**

1. Review the job status and error message shown in the report details.
2. Retry the difference report using a narrower scope, such as a specific object type or object ID.
3. Ensure no other difference report or recovery job is running at the same time.

**If you can't find a previous difference report:**

Difference reports are tied to the backup they were created from.

1. Browse to the backup and check the list of difference report jobs associated with it.
2. If the report isn’t listed, it may no longer be available because difference reports are retained for seven days after their completion date.

**If the difference report continues running after cancellation:**

1. Cancellation is best-effort. Some processing might continue briefly after you select **Cancel**.
2. If the job remains in a running state, wait for the state to update before starting a new report.

## Issue: Recovery job issues

This issue occurs when a recovery job doesn't recover expected objects, runs longer than expected, or completes with warnings.

### Symptoms

- The recovery job didn't recover an object that appeared in the difference report.
- The recovery job has been running for several hours, and you don't know when it finishes.
- The recovery job state is "Completed with warnings."
- You canceled the recovery job, but the job still appears to be running.

### Possible causes

- The object or property shown in the difference report (for example, on-premises synced properties) isn't supported for recovery.
- The recovery job includes a large number of objects or changes.
- Only one difference report or recovery job can run at a time.
- The recovery job was canceled or interrupted while changes were still being processed.
- Some recovery actions might partially succeed before a failure or cancellation occurs.

### Resolution

1. Review the failed changes list from the recovery job details.
2. Retry recovery with a narrower scope, focusing on supported cloud-only objects.

## Issue: Can't find a recovery job, or not all links were recovered

This issue occurs when a previously completed recovery job is no longer visible or when only some links were recovered.

### Symptoms

- You can't find the recovery job that you ran yesterday.
- The recovery job shows that only some links or properties were recovered (for example, 1 out of 5), and others weren't.

### Possible causes

- Recovery job details are automatically removed seven days after the job completes.
- Some links aren't supported for recovery in the current release.
- Certain links depend on other objects or states that no longer exist.
- The recovery job completed with warnings, indicating partial success.

### Resolution

**If you can't find a recovery job you ran earlier:**

1. Find the **backup timestamp** that was used for the recovery.
2. Review **recovery history** to find **recovery jobs associated with that backup timestamp**.
3. If the job is no longer listed, it may no longer be available because recovery jobs are retained for seven days after their completion date.

**If not all links were recovered:**

1. Review the recovery job details for **warnings or failed link changes**.
2. Confirm that the links you expected to recover are supported in the current release.
3. Some links might not be recovered if:
    - The related object no longer exists.
    - The link type isn't supported.
4. Manually re-create any unsupported or failed links if necessary.

## Error conditions and messages

| Condition | Error code and message |
| --- | --- |
| Difference report queried with an invalid backup ID | **404 Not Found**: This isn't a valid timestamp for recovery. The provided timestamp should be in the list of available backups. |
| Job is queried with an invalid job ID | **404 Not Found** |
| A job is started while another difference report or recovery job is still running | **409 Conflict**: A recovery job is currently in progress. Wait for it to complete before initiating a new job. |
| Get changes while difference report hasn't finished | **400 Bad Request**: Job with identifier `{key}` must have completed successfully prior to enumerating changes. |
| Insufficient admin role | **403 Forbidden**: Authorization has been denied for this request. Check your credentials. |

## Known limitations

The following known limitations apply to Microsoft Entra Backup and Recovery in this release.

### Partial property coverage

Backup and recovery **don't** cover all properties of supported objects. This limitation includes read-only properties, system-generated properties, and properties that rely on specialized business logic. See the [supported properties list](scope-supported-objects-limitations) for details. Microsoft is expanding support for more properties over time.

### Tenant support scope

Microsoft Entra Backup and Recovery is supported for workforce tenants only. External ID and B2C tenants aren't supported.

### Hard-deleted objects

Hard-deleted objects **cannot** be recovered. These objects aren't included in the difference report and can't be recreated or restored through a recovery job. To reduce the risk of hard deletion, consider configuring [protected actions](/en-us/entra/identity/role-based-access-control/protected-actions-overview).

### On-premises synced objects

Users and groups synchronized from on-premises Active Directory can't be recovered with Microsoft Entra Backup and Recovery. These objects must be recovered directly in the on-premises Active Directory environment.

### Link recovery limitations

Only static group membership links are supported for recovery. Group owner links, user manager relationships, and sponsor links aren't supported.