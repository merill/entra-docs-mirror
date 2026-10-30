---
layout: Conceptual
title: 'Microsoft Entra Connect: Troubleshoot object synchronization - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/tshoot-connect-objectsync
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to troubleshoot issues with object synchronization by using the troubleshooting task.
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6eed7051-4764-0329-00d1-d5b4c228e52b
document_version_independent_id: 7eea09df-c36f-f8ea-b853-89a8793204e5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/tshoot-connect-objectsync.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/tshoot-connect-objectsync
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/tshoot-connect-objectsync.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 61837bf6-a7ba-9824-3e80-4e2be4501e33
---

# Microsoft Entra Connect: Troubleshoot object synchronization - Microsoft Entra ID | Microsoft Learn

This article provides steps for troubleshooting issues with object synchronization by using the troubleshooting task. To see how troubleshooting works in Microsoft Entra Connect, watch a [short video](https://aka.ms/AADCTSVideo).

## Troubleshooting task

For Microsoft Entra Connect deployments of version 1.1.749.0 or later, use the troubleshooting task in the wizard to troubleshoot object sync issues. For earlier versions, you can [troubleshoot manually](tshoot-connect-object-not-syncing).

### Run the troubleshooting task in the wizard

To run the troubleshooting task:

1. Open a new Windows PowerShell session on your Microsoft Entra Connect server by using the Run as Administrator option.
2. Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.
3. Start the Microsoft Entra Connect wizard.
4. Go to **Additional Tasks** &gt; **Troubleshoot**, and then select **Next**.
5. On the **Troubleshooting** page, select **Launch** to start the troubleshooting menu in PowerShell.
6. In the main menu, select **Troubleshoot Object Synchronization**.

![Screenshot that shows the Troubleshoot object sync option highlighted in Microsoft Entra Connect.](media/tshoot-connect-objectsync/objsynch11.png)

### Troubleshoot input parameters

The troubleshooting task requires the following input parameters:

- **Object Distinguished Name**: The distinguished name of the object that needs troubleshooting.
- **AD Connector Name**: The name of the Windows Server Active Directory (Windows Server AD) forest where the object resides.
- Microsoft Entra tenant Hybrid Identity Administrator credentials.

![Screenshot that shows the credentials dialog on a PowerShell terminal background.](media/tshoot-connect-objectsync/objsynch1.png)

### Understand the results of the troubleshooting task

The troubleshooting task performs the following checks:

- Detect user principal name (UPN) mismatch if the object is synced to Microsoft Entra ID.
- Check whether object is filtered due to domain filtering.
- Check whether object is filtered due to organizational unit (OU) filtering.
- Check whether object sync is blocked due to a linked mailbox.
- Check whether the object is in a dynamic distribution group that isn't intended to be synced.

The rest of the article describes specific results that are returned by the troubleshooting task. In each case, the task provides an analysis followed by recommended actions to resolve the issue.

## Detect UPN mismatch if the object is synced to Microsoft Entra ID

Check for the UPN mismatch issues that are described in the next sections.

### UPN suffix is not verified with the Microsoft Entra tenant

When the UPN or alternate login ID suffix isn't verified with the Microsoft Entra tenant, Microsoft Entra ID replaces the UPN suffixes with the default domain name `onmicrosoft.com`. To resolve this issue, add the UPN suffix as a verified domain on your tenant. For more information visit [Managing custom domain names in your Microsoft Entra ID](../../users/domains-manage).

![Screenshot that shows an example of an unverified UPN suffix error in PowerShell.](media/tshoot-connect-objectsync/objsynch2.png)

### Microsoft Entra tenant DirSync feature SynchronizeUpnForManagedUsers is disabled

When the Microsoft Entra tenant DirSync feature SynchronizeUpnForManagedUsers is disabled, Microsoft Entra ID doesn't allow sync updates to the UPN or alternate login ID for licensed user accounts that use managed authentication. To learn how to enable SynchronizeUpnForManagedUsers feature, visit [Microsoft Entra Connect Sync service features](how-to-connect-syncservice-features).

![Screenshot that shows an example of a UPN sync for managed users error in PowerShell.](media/tshoot-connect-objectsync/objsynch4.png)

## Object is filtered due to domain filtering

Check for the domain filtering issues that are described in the next sections.

### Domain is not configured to sync

The object is out of scope because the domain hasn't been configured. In the example in the following figure, the object is out of sync scope because the domain that it belongs to is filtered from sync.

![Screenshot that shows an example of an error caused by a domain that's not in sync scope.](media/tshoot-connect-objectsync/objsynch5.png)

### Domain is configured to sync but is missing run profiles or run steps

The object is out of scope because the domain is missing run profiles or run steps. In the example in the following figure, the object is out of sync scope because the domain that it belongs to is missing run steps for the Full Import run profile.

![Screenshot that shows an example of an error caused by missing run steps.](media/tshoot-connect-objectsync/objsynch6.png)

## Object is filtered due to OU filtering

The object is out of sync scope because of the OU filtering configuration. In the example in the following figure, the object belongs to `OU=NoSync,DC=bvtadwbackdc,DC=com`. This OU is not included in the sync scope.

![Screenshot that shows an example of an OU filtering error in PowerShell.](media/tshoot-connect-objectsync/objsynch7.png)

## Linked mailbox issue

A linked mailbox is supposed to be associated with an external primary account that's located in a different trusted account forest. If the primary account doesn't exist, Microsoft Entra Connect doesn't sync the user account that corresponds to the linked mailbox in the Exchange forest to the Microsoft Entra tenant.

![Screenshot that shows an example of a linked mailbox error in PowerShell.](media/tshoot-connect-objectsync/objsynch12.png)

## Dynamic distribution group issue

Due to various differences between on-premises Windows Server AD and Microsoft Entra ID, Microsoft Entra Connect doesn't sync dynamic distribution groups to the Microsoft Entra tenant.

![Screenshot that shows an example of a dynamic distribution group error in PowerShell.](media/tshoot-connect-objectsync/objsynch13.png)

## HTML report

In addition to analyzing the object, the troubleshooting task generates an HTML report that includes everything that's known about the object. The HTML report can be shared with the support team for further troubleshooting if needed.

![Screenshot that shows an example of an HTML report in PowerShell.](media/tshoot-connect-objectsync/objsynch8.png)