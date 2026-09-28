---
layout: Conceptual
title: Register a passkey with a FIDO2 security key - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-register-passkey-with-security-key
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to register a passkey with a FIDO2 security key in Microsoft Entra ID. Use Security info or a prompted sign-in flow.
ms.topic: how-to
ms.date: 2026-07-05T00:00:00.0000000Z
ms.reviewer: kimhana
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 0d13f3cb-016f-5325-a9ab-e78858822658
document_version_independent_id: 0d13f3cb-016f-5325-a9ab-e78858822658
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-register-passkey-with-security-key.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-register-passkey-with-security-key
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-register-passkey-with-security-key.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: e23bc863-b1f9-57b4-1612-02234a0ea837
---

# Register a passkey with a FIDO2 security key - Microsoft Entra ID | Microsoft Learn

FIDO2 security keys are device-bound passkeys stored on a physical authenticator. The private key never leaves the security key, which provides strong protection against remote phishing attacks. Security keys are recommended for highly regulated industries or users with elevated privileges.

This article shows how to register a passkey as an authentication method by using a FIDO2 security key. After registration, you can [sign in with the security key](how-to-security-key-sign-in).

## First-time registration

To register a passkey for the first time, open [Security info](https://mysignins.microsoft.com/security-info) in a web browser to complete the registration.

1. Open a web browser and sign in to [Security info](https://mysignins.microsoft.com/security-info).
2. Sign in with multifactor authentication (MFA).
3. Tap **Add sign-in method** &gt; **Choose a method** &gt; **Passkey**.
4. Tap **Next**.
5. Select where you want to save your passkey (FIDO2).

    Note

    Options displayed vary depending on your browser and device operating system. If the device where you started the registration process supports passkeys (FIDO2), you'll be asked to save the passkey to that device. Select **Use another device** or **More options** to display additional ways for you to save the passkey.
6. (Optional) If you previously set up a passkey (FIDO2) on a mobile device and selected the option to remember that device for quicker sign-in, the device name might appear as a selectable option. In this case, do the following steps:

    1. Choose **Security key**.
    2. Follow the prompts to connect your security key and provide a PIN or biometric method.
    3. After you complete these steps, you're redirected to the **My Security info** screen, where you can change the default name for the new sign-in method.
    4. Select **Done** to finish registering the new method.

## Prompted registration

If your organization requires you to register a passkey (FIDO2), you're prompted after sign-in.

1. When you see the prompt to add a passkey (FIDO2), tap **Next**.
2. You're directed to `login.microsoftonline.com`.
3. Select where you want to save your passkey (FIDO2).

    Note

    Options displayed vary depending on your browser and device operating system. If the device where you started the registration process supports passkeys (FIDO2), you'll be asked to save the passkey (FIDO2) to that device. Select **Use another device** or **More options** to display additional ways for you to save the passkey.
4. (Optional) If you previously set up a passkey (FIDO2) on a mobile device and selected the option to remember that device for quicker sign-in, the device name might appear as a selectable option. In this case, do the following steps:

    1. Choose **Security key**.
    2. Follow the prompts to connect your security key and provide a PIN or biometric method.
    3. After you complete these steps, you're redirected to the **My Security info** screen, where you can change the default name for the new sign-in method.
    4. Select **Done** to finish registering the new method.