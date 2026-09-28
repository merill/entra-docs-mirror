---
layout: Conceptual
title: Soft deletion in Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/backup/soft-deletion
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id
manager: dougeby
description: Learn what soft deletion is, how it relates to Microsoft Entra Backup and Recovery, and what recovery can and can't do
ms.date: 2026-03-02T00:00:00.0000000Z
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: 0eac9edd-b48b-0626-9213-6b74f6ad791a
document_version_independent_id: 0eac9edd-b48b-0626-9213-6b74f6ad791a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/backup/soft-deletion.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: backup/soft-deletion
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/backup/soft-deletion.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 715b36ff-3601-fc26-2c87-132adbb3cfbf
---

# Soft deletion in Microsoft Entra Backup and Recovery - Microsoft Entra | Microsoft Learn

Soft deletion is a foundational data protection capability in Microsoft Entra that helps organizations recover from accidental or malicious deletions. Instead of immediately and permanently removing an object, soft deletion places the object into a recoverable state for a limited retention period. During this time, the object can be restored with its properties and relationships intact.

Soft deletion is a core building block of Microsoft Entra Backup and Recovery, enabling reliable recovery without recreating objects or reconfiguring access models. For an overview of deletion and recovery concepts, see [Recover from deletions](/en-us/entra/architecture/recover-from-deletions).

This article explains what soft deletion is, how it relates to Backup and Recovery, and what recovery can, and can't, do.

## What is soft deletion?

When an object that supports soft deletion is deleted, Microsoft Entra doesn't immediately remove it from the directory. Instead, it transitions into a soft-deleted state:

- The object is no longer active and can't be used for authentication or authorization.
- Microsoft Entra retains the object's data for a 30-day period.
- You can restore the object during the retention window, returning it to its previous active state.

## Soft deletion and Backup and Recovery

Microsoft Entra Backup and Recovery builds on soft deletion to provide a comprehensive recovery experience.

### How backup works

Microsoft Entra continuously records changes to supported directory objects. If an object is soft deleted, the backup captures the change and restores the object when you use that backup for recovery. To learn which objects support soft deletion, see [Recover from deletions in Microsoft Entra ID](/en-us/entra/architecture/recover-from-deletions#properties-maintained-with-soft-delete).

These backups are Microsoft-managed and don't require you to export or manage your own copies. Backups capture object state over time, enabling recovery to a known-good point.

### How recovery works

During a recovery operation:

- Microsoft Entra uses **backups** to determine the correct object state.
- Backup and Recovery **restores soft-deleted objects** rather than recreating them.
- Backup and Recovery **soft deletes** objects added after the backup was taken.
- Object identifiers, properties, and supported relationships are preserved.

Important

Microsoft never hard deletes customer objects as part of the recovery process. Recovery operations always rely on restoring soft-deleted objects or rolling objects back to a previous state. During recovery, Backup and Recovery soft deletes new objects added after the selected backup. This approach helps reduce the risk of accidental and malicious misconfigurations following recovery. For scenarios where you shouldn't soft delete one or more objects, apply filters to control which objects are in scope of recovery.

This approach avoids the risks and operational burden of object re-creation, such as:

- Loss of object IDs
- Broken dependencies
- Manual reconfiguration of access or policies by administrators

### Soft delete versus hard delete

Understanding the difference between soft deletion and hard deletion is critical for recovery planning.

| Deletion type | What happens | Can it be recovered? |
| --- | --- | --- |
| **Soft delete** | Object is retained in a deleted state for a limited time | Yes, within the retention window |
| **Hard delete** | Object is permanently removed from the directory | No |

If an object is **hard deleted**, it's permanently removed and **can't be recovered**. The only option is to create a new object, which results in a new object ID and loss of prior configuration and relationships.

Microsoft Entra Backup and Recovery **doesn't support recovery of hard-deleted objects**. Organizations can use capabilities such as Microsoft Entra Conditional Access to add a layer of protection for sensitive permissions, including hard deletion of directory objects. For more information, see [What are protected actions in Microsoft Entra ID?](/en-us/entra/identity/role-based-access-control/protected-actions-overview).

### Why soft deletion matters

Soft deletion is essential to building a resilient identity system because it:

- Enables fast recovery from mistakes and attacks
- Preserves object integrity and relationships
- Reduces downtime and operational risk
- Forms the foundation for reliable Backup and Recovery

When combined with soft deletion, Microsoft Entra Backup and Recovery enables organizations to recover from unintended or malicious attribute changes and deletions. Recovery never permanently deletes customer data.