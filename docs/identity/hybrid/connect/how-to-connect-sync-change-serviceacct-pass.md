---
layout: Conceptual
title: 'Microsoft Entra Connect Sync:  Changing the ADSync service account - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sync-change-serviceacct-pass
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic document describes the encryption key and how to abandon it after the password is changed.
keywords: Azure AD sync service account, password
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: 099337ce-2b90-61a9-5a68-6bee3408154d
document_version_independent_id: e5707bd0-6547-0156-2aab-18c427f06782
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sync-change-serviceacct-pass.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sync-change-serviceacct-pass
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sync-change-serviceacct-pass.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 78833619-cb7d-60e7-e62f-403aff3808bd
---

# Microsoft Entra Connect Sync:  Changing the ADSync service account - Microsoft Entra ID | Microsoft Learn

If you change the ADSync service account password, the Synchronization Service doesn't start correctly until you abandon the encryption key and reinitialized the ADSync service account password.

Important

If you use Connect with a build from 2017 March or earlier, then you should not reset the password on the service account since Windows destroys the encryption keys for security reasons. You can't change the account to any other account without reinstalling Microsoft Entra Connect. If you upgrade to a build from 2017 April or later, then it is supported to change the password on the service account, but you can't change the account used.

Microsoft Entra Connect, as part of the Synchronization Services uses an encryption key to store the passwords of the AD DS Connector account and ADSync service account. These accounts are encrypted before they're stored in the database.

The encryption key used is secured using [Windows Data Protection (DPAPI)](/en-us/previous-versions/ms995355%28v=msdn.10%29). DPAPI protects the encryption key using the **ADSync service account**.

If you need to change the service account password you can use the procedures in Abandoning the ADSync service account encryption key to accomplish this. These procedures should also be used if you need to abandon the encryption key for any reason.

## Issues that arise from changing the password

There are two things that need to be done when you change the service account password.

First, you need to change the password under the Windows Service Control Manager. Until this issue is resolved, you see the following issues:

- If you try to start the Synchronization Service in Windows Service Control Manager, you receive the error "**Windows could not start the Microsoft Entra ID Sync service on Local Computer**". **Error 1069: The service did not start due to a logon failure.**"
- Under Windows Event Viewer, the system event log contains an error with **Event ID 7038** and message “**The ADSync service was unable to log on as with the currently configured password due to the following error: The user name or password is incorrect.**"

Second, under specific conditions, if the password is updated, the Synchronization Service can no longer retrieve the encryption key via DPAPI. Without the encryption key, the Synchronization Service can't decrypt the passwords required to synchronize to/from on-premises AD and Microsoft Entra ID. You see errors such as:

- Under Windows Service Control Manager, if you try to start the Synchronization Service and it can't retrieve the encryption key, it fails with error “**Windows could not start the Microsoft Entra ID Sync on Local Computer. For more information, review the System Event log. If this is a non-Microsoft service, contact the service vendor, and refer to service-specific error code -21451857952**.”
- Under Windows Event Viewer, the Application event log contains an error with **Event ID 6028** and error message *"The server encryption key cannot be accessed."*

To ensure that you don't receive these errors, follow the procedures in Abandoning the ADSync service account encryption key when changing the password.

## Abandoning the ADSync service account encryption key

Important

The following procedures only apply to Microsoft Entra Connect build 1.1.443.0 or older. This can't be used for newer versions of Microsoft Entra Connect because abandoning the encryption key is handled by Microsoft Entra Connect itself when you change the AD sync service account password so the following steps are not needed in the newer versions.

Use the following procedures to abandon the encryption key.

### What to do if you need to abandon the encryption key

If you need to abandon the encryption key, use the following procedures to accomplish that.

1. Stop the Synchronization Service
2. Abandon the existing encryption key
3. Provide the password of the AD DS Connector account
4. Reinitialize the password of the ADSync service account
5. Start the Synchronization Service

#### Stop the Synchronization Service

First you can stop the service in the Windows Service Control Manager. Make sure that the service isn't running when attempting to stop it. If it is, wait until it completes and then stop it.

1. Go to Windows Service Control Manager (START → Services).
2. Select **Microsoft Entra ID Sync** and click Stop.

#### Abandon the existing encryption key

Abandon the existing encryption key so that new encryption key can be created:

1. Sign in to your Microsoft Entra Connect Server as administrator.
2. Start a new PowerShell session.
3. Navigate to folder: `'$env:ProgramFiles\Microsoft Azure AD Sync\bin\'`
4. Run the command: `./miiskmu.exe /a`

![Screenshot that shows PowerShell after running the command.](media/how-to-connect-sync-change-serviceacct-pass/key5.png)

#### Provide the password of the AD DS Connector account

As the existing passwords stored inside the database can no longer be decrypted, you need to provide the Synchronization Service with the password of the AD DS Connector account. The Synchronization Service encrypts the passwords using the new encryption key:

1. Start the Synchronization Service Manager (START → Synchronization Service). ![Sync Service Manager](media/how-to-connect-sync-change-serviceacct-pass/startmenu.png)
2. Go to the **Connectors** tab.
3. Select the **AD Connector** that corresponds to your on-premises AD. If you have more than one AD connector, repeat the following steps for each of them.
4. Under **Actions**, select **Properties**.
5. In the pop-up dialog, select **Connect to Active Directory Forest**:
6. Enter the password of the AD DS account in the **Password** textbox. If you don't know its password, you must set it to a known value before performing this step.
7. Click **OK** to save the new password and close the pop-up dialog. ![Screenshot that shows the &quot;Connect to Active Directory Forest&quot; page in the &quot;Properties&quot; window.](media/how-to-connect-sync-change-serviceacct-pass/key6.png)

#### Reinitialize the password of the Entra ID Connector account

You can't directly provide the password of the Microsoft Entra service account to the Synchronization Service. Instead, you need to use the cmdlet **Add-ADSyncAADServiceAccount** to reinitialize the Microsoft Entra service account. The cmdlet resets the account password and makes it available to the Synchronization Service:

1. Sign in to the Microsoft Entra Connect Sync server and open PowerShell.
2. To provide the Microsoft Entra Global Administrator credentials, run `$credential = Get-Credential`.
3. Run the cmdlet `Add-ADSyncAADServiceAccount -AADCredential $credential`.

    If the cmdlet is successful, the PowerShell command prompt appears.

The cmdlet resets the password for the service account and updates it both in Microsoft Entra ID and the sync engine.

#### Start the Synchronization Service

Now that the Synchronization Service has access to the encryption key and all the passwords it needs, you can restart the service in the Windows Service Control Manager:

1. Go to Windows Service Control Manager (START → Services).
2. Select **Microsoft Entra ID Sync** and click Restart.