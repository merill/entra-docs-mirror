---
layout: Conceptual
title: Restore or permanently remove recently deleted user - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/users-restore
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: How to view restorable users, restore a deleted user, or permanently delete a user with Microsoft Entra ID.
ms.topic: how-to
ms.date: 2026-06-18T00:00:00.0000000Z
ms.reviewer: jeffsta
ms.custom: ge-structured-content-pilot, sfi-image-nochange
locale: en-us
document_id: c5e84642-81dc-3659-e1cc-68523f1b76f6
document_version_independent_id: f5b4f426-d18a-6dd0-888d-0fc5a7c8e695
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/users-restore.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/users-restore
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/users-restore.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 6f1ac286-cd0d-df5a-98a7-9428c9f71e33
---

# Restore or permanently remove recently deleted user - Microsoft Entra | Microsoft Learn

## Overview

After you delete a user, the account remains in a suspended state for 30 days. During that 30-day window, the user account can be restored, along with all its properties.

After that 30-day window passes, the permanent deletion process automatically starts and can't be stopped. During this time, the management of soft-deleted users is blocked. This limitation also applies to restoring a soft-deleted user via a match during tenant sync cycle for on-premises hybrid scenarios.

You can view your restorable users, restore a deleted user, or permanently delete a user using the Microsoft Entra admin center.

Important

You can delete users synced from your on-premises environment in Microsoft Entra ID for security purposes. However, Microsoft Entra ID isn't the source of authority for synced users. If the user still exists in your on-premises directory, the sync engine may restore the user during the next synchronization cycle. After a user is permanently deleted, neither you nor Microsoft Support can restore them.

## Prerequisites

You must have at least the following role to restore and permanently delete users.

## View your restorable users

You can see all the users that were deleted less than 30 days ago. These users can be restored.

### To view your restorable users

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**, and then select **Deleted users**.

    If you don't see **Deleted users**, use the Microsoft Entra admin center search box to search for and select **Deleted users**.
3. Review the list of users that are available to restore.

    [![Screenshot of the Users - Deleted users page, with users that can still be restored.](media/users-restore/users-deleted-users-view-restorable.png)](media/users-restore/users-deleted-users-view-restorable.png#lightbox)

## Restore a recently deleted user

When a user account is deleted from the organization, the account is in a suspended state. All of the account's organization information is preserved. When you restore a user, this organization information is also restored.

Note

Once a user is restored, licenses that were assigned to the user at the time of deletion are also restored even if there are none available. If you're consuming more licenses than you purchased, your organization could be temporarily out of compliance for license usage.

### To restore a user

1. On the **Deleted users** page, search for and select one of the available users. For example, *Mary Parker*.
2. Select **Restore user**.

    [![Screenshot of the Users - Deleted users page, with Restore user option highlighted.](media/users-restore/users-deleted-users-restore-user.png)](media/users-restore/users-deleted-users-restore-user.png#lightbox)

## Permanently delete a user

You can permanently delete a user from your organization without waiting the 30 days for automatic deletion. A permanently deleted user can't be restored by anyone, including Microsoft customer support.

Note

If you permanently delete a user by mistake, you have to create a new user and manually enter all the previous information. For more information about creating a new user, see [Add or delete users](how-to-create-delete-users).

### To permanently delete a user

1. On the **Deleted users** page, search for and select one of the available users. For example, *Rae Huff*.
2. Select **Delete permanently**.

    [![Screenshot of the Users - Deleted users page, with Delete user option highlighted.](media/users-restore/users-deleted-users-permanent-delete-user.png)](media/users-restore/users-deleted-users-permanent-delete-user.png#lightbox)