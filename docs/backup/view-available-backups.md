---
layout: Conceptual
title: View available backups in Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/backup/view-available-backups
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id
manager: dougeby
description: Learn how to view available backups for your tenant in Microsoft Entra Backup and Recovery, including backup frequency, retention, and next steps
ms.date: 2026-03-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
locale: en-us
document_id: efea1fa0-779a-040d-f032-ffd9e745fbe2
document_version_independent_id: efea1fa0-779a-040d-f032-ffd9e745fbe2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/backup/view-available-backups.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: backup/view-available-backups
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/backup/view-available-backups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: af2a55c0-7941-75b7-c3f6-d027d0aeeb27
---

# View available backups in Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn

This article describes how to view available backups for your tenant in Microsoft Entra Backup and Recovery.

Microsoft Entra backups provide a point-in-time view of supported tenant objects and their attributes. Backups help administrators review changes and recover from accidental or unwanted modifications.

Key characteristics of Backup and Recovery:

- **One backup per day**: Microsoft Entra automatically creates one backup each day for your tenant.
- **Retained for seven days**: Each backup is available for up to seven days from its timestamp.
- **Non-editable**: Backups can't be modified or deleted.

## Prerequisites

To view available backups in your tenant, you must have the **Microsoft Entra Backup Reader** role or a higher-privileged role.

## View backups

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Microsoft Entra Backup Reader**.
2. Browse to **Backup and recovery**. The **Overview** page shows feature highlights, alerts, and recent activity.

    ![Screenshot of the Backup and recovery Overview page in the Microsoft Entra admin center, showing feature highlights and alerts.](media/view-available-backups/backup-recovery-overview.png#lightbox)
3. Select **Backups** to view the list of available backups for your tenant. Each backup shows its timestamp and backup ID.

    ![Screenshot of the Backups page showing a list of five available backups with their timestamps and backup IDs.](media/view-available-backups/backups-list.png#lightbox)

From the **Backups** page, select a backup to [create a difference report](create-review-difference-reports) or [start a recovery](recover-objects).