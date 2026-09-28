---
layout: Conceptual
title: Review recovery history in Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/backup/review-recovery-history
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id
manager: dougeby
description: Learn how to review recovery operations performed in your tenant using the Recovery History page in Microsoft Entra Backup and Recovery
ms.date: 2026-03-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
locale: en-us
document_id: 0be012e7-1972-3be1-877c-afbb4e03ceef
document_version_independent_id: 0be012e7-1972-3be1-877c-afbb4e03ceef
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/backup/review-recovery-history.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: backup/review-recovery-history
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/backup/review-recovery-history.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e98663c3-a311-ece8-284e-6432ffdffef6
---

# Review recovery history in Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn

Learn how to review past recovery operations in your tenant by using the Recovery History page in Microsoft Entra Backup and Recovery.

Recovery history includes:

- The final status of the recovery.
- The backup point used for each recovery.
- The start and completion time of the recovery.
- The number of objects and links modified.

Use recovery history for recent operational review and troubleshooting. Recovery history data is retained for up to seven days after the recovery completion time.

## Prerequisites

To view available recovery history in your tenant, you must sign in with at least the **Microsoft Entra Backup Reader** role.

## Review recovery history

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Microsoft Entra Backup Reader**.
2. In the left navigation pane, select **Recovery History** under **Backup and recovery**.

    ![Screenshot of the Recovery History page showing recovery operations with Status, Backup timestamp, Recovery started, and Modified objects columns.](media/review-recovery-history/recovery-history-page.png#lightbox)

    The Recovery History page displays all recent recovery operations in your tenant. From this page:

    - View the **Recovery ID** for each operation.
    - Check the **Status**.
    - See the **Backup timestamp** and **Backup ID** used.
    - Review when the recovery started and completed.
    - See how many objects and links the recovery modified.
    - Filter or search recovery records to narrow results.

    ![Screenshot of the Recovery History page showing multiple recovery operations with status and timestamp details.](media/review-recovery-history/recovery-history-details.png#lightbox)

Note

The system automatically removes recovery history seven days after recovery completes.

### Recovery statuses

Recovery operations move through these statuses as the system applies changes to the tenant. These statuses indicate the progress and outcome of the recovery job:

| Status | Description |
| --- | --- |
| **Loading data** | The system is loading data from the selected backup to prepare for recovery. If you already used the backup to create a difference report or a prior recovery, this step might finish quickly. |
| **In progress** | The system is applying recovery actions to restore objects to the backup state. The duration of this step depends on the number and type of changes being applied. |
| **Completed** | The recovery completed successfully, and the system applied all supported changes. |
| **Completed with warnings** | The recovery completed, but some changes couldn't be applied. Review the failed changes to understand which objects weren't restored and why. |
| **Failed** | The recovery couldn't be completed due to an error. The system might not have applied some changes. |
| **Canceled** | The recovery was canceled before completion. |

## Review failed changes

If a recovery operation partially succeeds, the **Status** column shows **Completed with warnings**, allowing you to identify objects that weren't recovered. Select **Completed with warnings** to view the details of the changes that were not recovered.

![Screenshot of the Recovery History page with a Completed with Warnings entry highlighted in the Status column.](media/review-recovery-history/recovery-completed-with-warnings.png#lightbox)

Select **Changed Attributes** or **Changed Links** of an object to view the details of the failure.

![Screenshot of the Failed recovery changes page showing recovery job details and a failed object with Error Code 400.](media/review-recovery-history/failed-recovery-changes.png#lightbox)

**Value at recovery attempt** shows the attribute value at the time the recovery was attempted. **Backup value** shows the value the recovery service attempted to restore.

![Screenshot of the View failed changed attributes flyout showing error details and attribute value comparison.](media/review-recovery-history/failed-changed-attributes.png#lightbox)

Use failed recovery entries to:

- Identify which recovery operation and object didn't complete successfully.
- Confirm the backup point that was used.
- View failure details that explain why the recovery didn't succeed.

Note

Failed recovery records remain available for seven days after the recovery completion date.