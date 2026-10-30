---
layout: Conceptual
title: Configure accidental deletion prevention with Active Directory - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/accidental-deletes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes how you can configure accidental deletion prevention for the synchronization tools with Active Directory.
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
locale: en-us
document_id: db9dd64a-7f7c-e264-4bcd-9bfcae7c952c
document_version_independent_id: ba18564e-3421-9d97-83f9-421b3e5a7a83
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/accidental-deletes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/accidental-deletes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/accidental-deletes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: e0e4b494-4c13-b16d-1d8f-cb32f98a076c
---

# Configure accidental deletion prevention with Active Directory - Microsoft Entra ID | Microsoft Learn

When installing either cloud sync or Microsoft Entra Connect, this feature is enabled by default and configured to not allow an export with more than 500 deletes. This feature is designed to protect you from accidental configuration changes and changes to your on-premises directory that would affect many users and other objects.

You can change the default behavior and tailor it to your organizations needs.

## Configure accidental delete prevention with cloud sync

To use the new feature, follow the steps below.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Under **Configuration**, select your configuration.
2. Select **View default properties**.
3. Click the pencil next to **Basics**
4. On the right, fill in the following information.
    - **Notification email** - email used for notifications
    - **Prevent accidental deletions** - check this box to enable the feature
    - **Accidental deletion threshold** - enter the number of objects to stop synchronization and send a notification

For more information, see [Accidental delete prevention with cloud sync](cloud-sync/how-to-accidental-deletes)

## Configure accidental delete prevention with Microsoft Entra Connect

The default value of 500 objects can be changed with PowerShell using `Enable-ADSyncExportDeletionThreshold`, which is part of the [AD Sync module](connect/reference-connect-adsync) installed with Microsoft Entra Connect. You should configure this value to fit the size of your organization. Since the sync scheduler runs every 30 minutes, the value is the number of deletes seen within 30 minutes.

For more information, see [Accidental delete prevention with Microsoft Entra Connect](connect/how-to-connect-sync-feature-prevent-accidental-deletes).