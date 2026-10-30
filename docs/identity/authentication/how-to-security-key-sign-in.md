---
layout: Conceptual
title: Sign in with a FIDO2 security key - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-security-key-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to sign in to Microsoft Entra ID with a FIDO2 security key. Sign in to web apps, Windows, and on-premises resources.
ms.topic: how-to
ms.date: 2026-07-05T00:00:00.0000000Z
ms.reviewer: kimhana
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 086ea8d0-8353-7e7f-9907-262c02993658
document_version_independent_id: 086ea8d0-8353-7e7f-9907-262c02993658
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-security-key-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-security-key-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-security-key-sign-in.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 49551872-ebb8-1c59-dd78-b57bca15c7fd
---

# Sign in with a FIDO2 security key - Microsoft Entra ID | Microsoft Learn

FIDO2 security keys are device-bound passkeys stored on a physical authenticator. The private key never leaves the security key, which provides strong protection against remote phishing attacks. Security keys come in a variety of form factors (USB, NFC, Bluetooth) and are recommended for highly regulated industries or users with elevated privileges.

For more information about the availability of passkey (FIDO2) authentication across native apps, web browsers, and operating systems, see [Support for FIDO2 authentication with Microsoft Entra ID](concept-fido2-compatibility).

## Sign in with a security key

1. Open your browser and go to the resource you're trying to access, such as [Office](https://www.office.com).
2. You can enter your username and select **Next** to sign in. If you most recently used a passkey to sign in, you're automatically prompted to sign in with a passkey.

    ![Screenshot that shows the Sign in page with a username and the Next button.](media/how-to-sign-in-passkey/sign-in-options-name.png)

    Or select **Sign-in options** &gt; **Face, fingerprint, PIN, or security key** to sign in without a username.

    ![Screenshots that show the Sign-in options button and the Face, fingerprint, PIN or security key option.](media/how-to-sign-in-passkey/sign-in-options-passkey.png)
3. Select **Security key**.

    [![Screenshot that shows the Choose a passkey dialog with Security key option.](media/how-to-security-key-sign-in/choose-passkey-security-key.png)](media/how-to-security-key-sign-in/choose-passkey-security-key.png#lightbox)
4. Your device opens a security window. Insert your FIDO2 security key if it's a USB key, or bring it near the reader if it's an NFC key.
5. To verify your identity, scan your fingerprint or enter your PIN when prompted by the operating system or browser dialog.
6. You're signed in with your work or school account.

## Known issues

### Orphaned passkey

An orphaned passkey occurs when a passkey remains on a security key but is no longer registered with Microsoft Entra ID. This typically happens if the passkey was deleted from a user's Security info or removed due to policy changes, but the local credential wasn't cleaned up.

If you're blocked from sign-in by an orphaned passkey:

1. Remove the orphaned passkey from the security key by using the security key's management tool.
2. Re-register a new passkey after cleanup.