---
layout: Conceptual
title: 'Microsoft Entra Connect Sync: Enable AD recycle bin - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sync-recycle-bin
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic recommends the use of AD Recycle Bin feature with Microsoft Entra Connect.
keywords: AD Recycle Bin, accidental deletion, source anchor
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 9e7d79fd-44ad-22ac-94fe-42bdaa20c886
document_version_independent_id: afe820dc-1581-f375-1b5e-4f693f34936a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sync-recycle-bin.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sync-recycle-bin
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sync-recycle-bin.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 8ee559d1-b459-baf9-b7a4-b5281d5b12b7
---

# Microsoft Entra Connect Sync: Enable AD recycle bin - Microsoft Entra ID | Microsoft Learn

We recommend that you enable the Active Directory Recycle Bin feature for your on-premises instances of Active Directory (AD) that are synchronized to Microsoft Entra ID.

If you accidentally deleted an on-premises AD user object and restore it using the feature, Microsoft Entra ID restores the corresponding Microsoft Entra user object. For information about restoring Active Directory objects, see [Scenario overview for restoring deleted Active Directory objects](/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379542%28v=ws.10%29).

To learn how to enable the Active Directory Recycle Bin feature, see [Active Directory Administrative Center enhancements](/en-us/windows-server/identity/ad-ds/get-started/adac/introduction-to-active-directory-administrative-center-enhancements--level-100-#ad_recycle_bin_mgmt).

## Benefits of enabling the AD recycle bin

This feature helps with restoring Microsoft Entra user objects by doing the following:

- If you accidentally deleted an on-premises AD user object, the corresponding Microsoft Entra user object is deleted in the next sync cycle. By default, Microsoft Entra ID keeps the deleted Microsoft Entra user object in soft-deleted state for 30 days.
- If you have on-premises AD Recycle Bin feature enabled, you can restore the deleted on-premises AD user object without changing its Source Anchor value. When the recovered on-premises AD user object is synchronized to Microsoft Entra ID, Microsoft Entra ID restores the corresponding soft-deleted Microsoft Entra user object. For information about Source Anchor attribute, refer to article [Microsoft Entra Connect: Design concepts](plan-connect-design-concepts#sourceanchor).
- If you do not have on-premises AD Recycle Bin feature enabled, you may be required to create an AD user object to replace the deleted object. If Microsoft Entra Connect Synchronization Service is configured to use system-generated AD attribute (such as ObjectGuid) for the Source Anchor attribute, the newly created AD user object won't have the same Source Anchor value as the deleted AD user object. When the newly created AD user object is synchronized to Microsoft Entra ID, Microsoft Entra ID creates a new Microsoft Entra user object instead of restoring the soft-deleted Microsoft Entra user object.

Note

By default, Microsoft Entra ID keeps deleted Microsoft Entra user objects in soft-deleted state for 30 days before they are permanently deleted. However, administrators can accelerate the deletion of such objects. Once the objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.