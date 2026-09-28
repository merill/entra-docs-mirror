---
layout: Conceptual
title: 'Microsoft Entra Connect Sync:  Changing the AD DS account password - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sync-change-addsacct-pass
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic document describes how to update Microsoft Entra Connect after the password of the AD DS account is changed.
keywords: AD DS account, Active Directory account, password
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: e4cc6454-3032-ab48-03eb-598756383166
document_version_independent_id: 1b4fee9a-01ef-eacd-6189-ccb0c3320657
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sync-change-addsacct-pass.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sync-change-addsacct-pass
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sync-change-addsacct-pass.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 2926347e-193a-fbe3-756f-3cdf6201cca6
---

# Microsoft Entra Connect Sync:  Changing the AD DS account password - Microsoft Entra ID | Microsoft Learn

The AD DS connector account refers to the user account used by Microsoft Entra Connect to communicate with on-premises Active Directory. If you change the password of the AD DS connector account in AD, you must update Microsoft Entra Connect Synchronization Service with the new password. Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you'll encounter the following errors:

- In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.
- Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.

## How to update the Synchronization Service with new password for AD DS connector account

To update the Synchronization Service with the new password:

1. Start the Synchronization Service Manager (START → Synchronization Service). ![Sync Service Manager](media/how-to-connect-sync-change-addsacct-pass/startmenu.png)
2. Go to the **Connectors** tab.
3. Select the **AD Connector** that corresponds to the AD DS connector account for which its password was changed.
4. Under **Actions**, select **Properties**.
5. In the pop-up dialog, select **Connect to Active Directory Forest**:
6. Enter the new password of the AD DS connector account in the **Password** textbox.
7. Click **OK** to save the new password and close the pop-up dialog.
8. Restart the **Microsoft Entra ID Sync** service under Windows Service Control Manager. This is to ensure that any reference to the old password is removed from the memory cache.