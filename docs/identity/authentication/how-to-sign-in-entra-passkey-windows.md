---
layout: Conceptual
title: Sign in with a Microsoft Entra passkey on Windows - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-sign-in-entra-passkey-windows
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to sign in with a Microsoft Entra passkey on Windows by using Windows Hello as a FIDO2 passkey provider for phishing-resistant authentication.
ms.topic: how-to
ms.date: 2026-07-05T00:00:00.0000000Z
ms.reviewer: kimhana
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: ea5a9d00-355c-7bed-9ef4-a193b79603f1
document_version_independent_id: ea5a9d00-355c-7bed-9ef4-a193b79603f1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-sign-in-entra-passkey-windows.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-sign-in-entra-passkey-windows
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-sign-in-entra-passkey-windows.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 27b234ed-fb21-86a4-43e5-6e994a0e7405
---

# Sign in with a Microsoft Entra passkey on Windows - Microsoft Entra ID | Microsoft Learn

This article covers how to sign in to Microsoft Entra ID with a Microsoft Entra passkey on Windows. A Microsoft Entra passkey on Windows is a device-bound passkey stored in the local Windows Hello container. For an overview of Microsoft Entra passkey on Windows and how it compares with Windows Hello for Business, see [Microsoft Entra passkey on Windows](how-to-authentication-entra-passkeys-on-windows).

## Sign in with a passkey on Windows

To sign in with a passkey on Windows, follow these steps:

1. Open your browser and go to the resource you're trying to access, such as [Office](https://www.office.com).
2. You can enter your username to sign in. If you most recently used a passkey to sign in, you're automatically prompted to sign in with a passkey. Otherwise, select **Other ways to sign in**, and then select **Face, fingerprint, PIN, or security key**.

    Alternatively, select **Sign-in options** to sign in without entering a username. If you chose **Sign-in options**, select **Face, fingerprint, PIN, or security key**. Otherwise, skip to the next step.
3. Your device opens a Windows Security dialog. Verify your identity by using Windows Hello (fingerprint, facial recognition, or PIN).

After verification, you're signed in to Microsoft Entra ID.