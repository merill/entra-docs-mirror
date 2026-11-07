---
layout: Conceptual
title: Configure Hard Deletion Protection in Microsoft Entra (preview) - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/backup/configure-hard-deletion-protection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: tazkiaafra
ms.author: tazkiaafra
ms.service: entra-id
manager: dougeby
description: Learn how to protect supported Microsoft Entra objects from permanent deletion during the first seven days after they're soft deleted.
ms.date: 2026-10-12T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1026
ai-usage: ai-generated
locale: en-us
document_id: 95d87412-58ef-7690-65ab-e39ac6799bf0
document_version_independent_id: 95d87412-58ef-7690-65ab-e39ac6799bf0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/backup/configure-hard-deletion-protection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: backup/configure-hard-deletion-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/backup/configure-hard-deletion-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
platformId: 187a90cd-0f8b-e47d-070d-3975cfd6fa6c
---

# Configure Hard Deletion Protection in Microsoft Entra (preview) - Microsoft Entra | Microsoft Learn

Hard Deletion Protection helps protect critical Microsoft Entra objects from immediate permanent deletion. When you enable protection for an object, the object can still be soft deleted and restored. However, it can't be permanently deleted during the first seven days after it's soft deleted.

Identity administrators can use this article to enable Hard Deletion Protection and view protected objects. To complete the task, you need the **Microsoft Entra Backup Administrator** role and an existing supported object.

Important

Hard Deletion Protection is in preview.

Protection is permanent. After you enable Hard Deletion Protection for an object, you can't remove or undo the protection.

If you enable protection unintentionally, soft delete the object and wait seven days before you permanently delete it.

## Prerequisites

- An active Microsoft Entra user with the **Microsoft Entra Backup Administrator** role.
- No additional license is required for the currently supported object types.

Hard Deletion Protection supports:

- Users (on-premises synchronized users aren't supported).
- Cloud-only groups.
- Applications.
- Service principals.

Note

Microsoft Entra Agent ID objects are supported through their underlying user, application, and service principal object types.

## Understand deletion and restoration behavior

Hard Deletion Protection doesn't prevent soft deletion. It gives you time to investigate and restore an object before permanent deletion is allowed.

- The seven-day protection window starts at the time the object is soft deleted.
- Attempts to permanently delete the object during the seven-day window are blocked.
- After the seven-day window ends, the object can be permanently deleted.
- If you restore the object, Hard Deletion Protection remains enabled.
- If the restored object is soft deleted again, a new seven-day protection window starts.
- Enabling Hard Deletion Protection is recorded in the Microsoft Entra audit logs.

When a selected set includes a protected object, the permanent-deletion action is blocked.

## Enable Hard Deletion Protection

In the Microsoft Entra admin center, you can protect up to 20 objects of one object type in each operation. Objects that already have protection enabled aren't available for selection.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Microsoft Entra Backup Administrator**.
2. Browse to **Backup and recovery** &gt; **Hard deletion protection**.

    ![Screenshot of the Hard deletion protection page with the Add protection button and permanent-protection warning.](media/configure-hard-deletion-protection/hard-deletion-protection-page.png#lightbox)
3. Select **Add protection**.
4. Select one supported object type.
5. Search for and select up to 20 objects of that type.

    ![Screenshot of the Select objects pane with Users selected, an Add control for object IDs, and the permanent-protection warning.](media/configure-hard-deletion-protection/select-hard-deletion-protection-objects.png#lightbox)
6. Review the permanent-protection warning, and then select **Save**.
7. Review the protected-object counts on the **Hard deletion protection** page. To view protected objects of a specific type, select the corresponding link.