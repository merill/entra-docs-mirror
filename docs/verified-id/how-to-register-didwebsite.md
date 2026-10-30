---
layout: Conceptual
title: Register your website ID - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/how-to-register-didwebsite
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn how to register your website ID for did:web.
documentationCenter: ''
ms.topic: how-to
ms.date: 2024-12-18T00:00:00.0000000Z
locale: en-us
document_id: 55734629-bf11-ae27-2bce-6b2d666dd6ab
document_version_independent_id: 4ab43fde-5562-a32b-aea1-867848dbfb3a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/how-to-register-didwebsite.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/how-to-register-didwebsite
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/how-to-register-didwebsite.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 3d88a081-95fd-83ba-9143-16d77fed9a98
---

# Register your website ID - Microsoft Entra Verified ID | Microsoft Learn

## Overview

This article covers the steps to register your decentralized ID (DID) for did:web.

## Prerequisites

- Complete verifiable credentials onboarding with **web** as the selected trust system.
- Complete the linked domain setup. Without completing this step, you can't perform this registration step.

## Why do you need to register your decentralized ID?

For the web trust system, you need to register your DID to be able to issue and verify your credentials. You have to make this information available on your website and complete this registration. Otherwise, your public key isn't made public.

## How do you register your decentralized ID?

1. Go to the **Verified ID** page in the **Azure portal**.
2. On the leftmost menu, select **Setup**.
3. On the middle menu, under **Register decentralized ID**, select **Update**.

    ![Screenshot that shows the website registration page.](media/how-to-register-didwebsite/how-to-register-didwebsite-domain.png)
4. Copy or download the DID document that appears in the box.

    ![Screenshot that shows did.json.](media/how-to-register-didwebsite/how-to-register-didwebsite-diddoc.png)
5. Upload the DID document JSON file to `/.well-known/did.json` on your web server.
6. After the file is available on your web server, select **Refresh registration status** to verify that the system can request the file.

## When is the DID document in the did.json file used?

The DID document contains the public keys for your issuer and is used during both issuance and presentation. For example, Microsoft Authenticator, working as the wallet, uses the public keys to validate the signature of an issuance or presentation request.

## When does the did.json file need to be republished to the web server?

The DID document in the `did.json` file must be republished if you change the linked domain or if you rotate your signing keys.

## How can you verify that the registration is working?

The portal verifies that `did.json` is reachable and correct when you select **Refresh registration status**. You should also consider verifying that you can request that URL in a browser to avoid errors like not using HTTPS, a bad TLS/SSL certificate, or the URL not being public. If the `did.json` file can't be requested anonymously in a browser or via tools such as `curl`, without warnings or errors, the portal won't be able to complete the **Refresh registration status** step.

Note

If you're experiencing problems refreshing your registration status, you can troubleshoot it by running `curl -Iv https://<your-domain>/.well-known/did.json` (for example, `https://verifiedid.contoso.com/.well-known/did.json`) on a machine with Ubuntu OS. Windows Subsystem for Linux with Ubuntu also works. If curl fails, refreshing the registration status won't work.