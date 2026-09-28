---
layout: Conceptual
title: Register a Microsoft Entra passkey on Windows - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-register-entra-passkey-windows
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to register a Microsoft Entra passkey on Windows by using Windows Hello as a FIDO2 passkey provider for phishing-resistant sign-in.
ms.topic: how-to
ms.date: 2026-07-05T00:00:00.0000000Z
ms.reviewer: kimhana
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 81b7e508-481a-4c76-5ac1-179b206b212c
document_version_independent_id: 81b7e508-481a-4c76-5ac1-179b206b212c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-register-entra-passkey-windows.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-register-entra-passkey-windows
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-register-entra-passkey-windows.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5717abce-88c6-42bd-821b-0d6370225d52
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b472b5d5-52dd-4477-99f9-23fa324788f7
platformId: 4401603c-2803-879a-a853-f2a34bff79f4
---

# Register a Microsoft Entra passkey on Windows - Microsoft Entra ID | Microsoft Learn

This article shows how to register a Microsoft Entra passkey on Windows. A Microsoft Entra passkey on Windows is a device-bound passkey stored in the local Windows Hello container. Unlike synced passkeys, a passkey on Windows doesn't sync across devices — each device requires a separate passkey registration. This approach enables phishing-resistant sign-in with a Windows Hello biometric or PIN, without requiring the device to be Microsoft Entra joined or registered.

For an overview of Microsoft Entra passkey on Windows and how it compares with Windows Hello for Business, see [Microsoft Entra passkey on Windows](how-to-authentication-entra-passkeys-on-windows).

## Prerequisites

Confirm these requirements before you register:

- Your administrator enabled passkeys (FIDO2) and created a passkey profile that allows Windows Hello AAGUIDs. For configuration steps, see [Configure a profile for Microsoft Entra passkey on Windows](how-to-authentication-entra-passkeys-on-windows#configure-a-profile-for-microsoft-entra-passkey-on-windows).
- The device runs a supported version of Windows.
- Attestation must not be enforced in the passkey profile.

For the list of supported Windows Hello passkey AAGUIDs, see [Supported Windows Hello passkey AAGUIDs](how-to-authentication-entra-passkeys-on-windows#supported-windows-hello-passkey-aaguids).

## Register a passkey on Windows

To register a passkey on your Windows device, follow these steps:

1. Open a web browser and sign in to [Security info](https://mysignins.microsoft.com/security-info).
2. Sign in with multifactor authentication (MFA).
3. Tap **Add sign-in method** &gt; **Choose a method** &gt; **Passkey**.
4. Tap **Next**.
5. Select where you want to save your passkey (FIDO2).

    Note

    Options displayed vary depending on your browser and device operating system. If the device where you started the registration process supports passkeys (FIDO2), you'll be asked to save the passkey to that device. Select **Use another device** or **More options** to display additional ways for you to save the passkey.

    ![Screenshot of the dialog where to save your passkey (FIDO2) in My Security info.](media/how-to-register-passkey-with-security-key/choose-where-store-passkey.png)

After verification, Windows creates the passkey and stores it in the local Windows Hello container. You can now use this passkey to sign in to Microsoft Entra ID.

Note

If a Windows Hello for Business credential already exists for the same account, passkey registration might fail. For more information, see [Microsoft Entra passkey on Windows](how-to-authentication-entra-passkeys-on-windows#faq).