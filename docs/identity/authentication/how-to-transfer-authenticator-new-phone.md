---
layout: Conceptual
title: Transfer Microsoft Authenticator to a new phone - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-transfer-authenticator-new-phone
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to back up and restore Microsoft Authenticator account entries when you switch to a new phone, including passkey setup steps.
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: matursca
ms.collection: M365-identity-device-management
locale: en-us
document_id: d665d2b8-e591-a79e-f3db-f7a5d1384fe7
document_version_independent_id: d665d2b8-e591-a79e-f3db-f7a5d1384fe7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-transfer-authenticator-new-phone.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-transfer-authenticator-new-phone
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-transfer-authenticator-new-phone.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
platformId: f846d81e-7e99-2d98-8c14-8b607da3ff97
---

# Transfer Microsoft Authenticator to a new phone - Microsoft Entra ID | Microsoft Learn

Microsoft Authenticator helps make sign-in more secure and convenient by supporting multifactor authentication, verification codes, passwordless sign-in, and passkeys. When you get a new phone, you can recover supported account entries and continue using secure sign-in methods by backing up and restoring these methods. Work or school accounts require additional sign-in and setup steps after restore. Complete the transfer before you erase, trade in, or recycle your old phone.

For work or school accounts, backup and restore transfers the account name so you can recognize the account on the new phone. You still need to sign in again to complete setup. Passkeys are handled separately from Authenticator account backup. If a passkey was saved only to the old phone, add a new passkey for the new phone. If a passkey was saved to a synced credential manager, it might be available after you sign in to that credential manager.

Important

Keep your old phone until you confirm that you can sign in to the accounts and resources you use most often from the new phone.

Use the following steps to back up Microsoft Authenticator on your old phone, restore it on your new phone, and set up passkeys again when needed.

## Back up Microsoft Authenticator on iOS

To back up Authenticator on an iOS device, enable iCloud Drive, Keychain, and Backup for Authenticator.

1. Enable iCloud Drive on your iOS device.
2. Enable iCloud Keychain on your iOS device.
3. Enable iCloud Backup on your iOS device.
4. Go to **Apple Account** &gt; **iCloud** &gt; **Saved to iCloud** and search for **Authenticator**.
5. Turn on the **Authenticator** toggle.

## Back up Microsoft Authenticator on Android

To back up your Authenticator account entries on an Android device:

1. Open Microsoft Authenticator.
2. Open the menu and select **Settings**.
3. Turn on **Cloud Backup**.
4. Select a Microsoft personal account where the backup will be stored.
5. Tap **OK**.

Note

If you saved the backup to the wrong account, or need to change the recovery account, delete the existing backup and create a new backup.

## Expected behavior after restore

### Work or school accounts

- Only the account name is restored.
- To complete setup on the new phone, open the account and sign in again.
- You might see red text that says **"Sign in to add your account."**

    ![Screenshot of a restored work account in Microsoft Authenticator showing the Sign in to add your account message.](media/how-to-transfer-authenticator-new-phone/authenticator-sign-in-to-add-account.jpg)
- If passkeys are enforced for the account, set up a passkey for the new phone before removing the old device.

Steps to set up a passkey on the new phone:

1. If you still have access to the old device, use it to sign in first.
2. Go to **Security info** at https://aka.ms/mysecurityinfo, select **Add sign-in method**, and choose **Passkey** or **Passkey in Microsoft Authenticator**.
3. Follow the prompts to create and save the new passkey.
4. Test sign-in with the new passkey.
5. After the new passkey works, remove old passkeys or devices that you no longer use.

Note

If the passkey was saved to a synced credential manager, such as Microsoft Password Manager, Google Password Manager, or Apple iCloud Keychain, you might not need to create a new passkey. Verify the passkey is available before removing the old device.

If your IT admin doesn't allow self-service passkey setup, contact your admin or help desk for the approved recovery or registration process.

### Personal Microsoft accounts

- If the account uses only a one-time password code that refreshes every 30 seconds, the verification code entry is restored.
- If the account also uses passwordless sign-in, only the account name is restored and you must sign in again to complete setup.

### Third-party accounts (Amazon, Facebook, Gmail, etc.)

- These accounts typically use a one-time password code that refreshes every 30 seconds.
- The verification code entry is restored.

## Troubleshoot common issues

| Issue | Resolution |
| --- | --- |
| **"Sign in to add your account."** | Expected for work or school accounts after restore. Open the account and sign in again. |
| **Restore from backup isn't available.** | Verify backup was enabled on the old phone, you're using the same recovery account, and you're restoring to the same device type. |
| **No passkeys are available.** | Ensure the new phone has a screen lock enabled and that Bluetooth and internet connectivity are available for cross-device sign-in. |
| **A passkey can no longer be used.** | Create a new passkey and remove obsolete passkeys only after the new method is working. |