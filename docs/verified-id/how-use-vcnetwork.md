---
layout: Conceptual
title: Use the Microsoft Entra Verified ID Network - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/how-use-vcnetwork
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: In this article, you learn how to use the Microsoft Entra Verified ID Network to verify credentials.
documentationCenter: ''
ms.topic: how-to
ms.date: 2025-04-30T00:00:00.0000000Z
locale: en-us
document_id: 09cc8810-1988-d2d9-1216-902e78da73ca
document_version_independent_id: 42df28c1-64de-65c2-39af-83b05889f0b6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/how-use-vcnetwork.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/how-use-vcnetwork
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/how-use-vcnetwork.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
platformId: 6be761d4-3b92-361d-f92f-463925370f2b
---

# Use the Microsoft Entra Verified ID Network - Microsoft Entra Verified ID | Microsoft Learn

## Overview

The Microsoft Entra Verified ID Network simplifies the verification of credentials by streamlining the discovery of issuers' decentralized identifiers (DIDs) and credential types. This article reviews the steps required to use the network.

## Prerequisites

To use the Microsoft Entra Verified ID Network, you need to:

- Complete [Getting started](verifiable-credentials-configure-tenant) and the subsequent [tutorial set](verifiable-credentials-configure-tenant).

## What is the Microsoft Entra Verified ID Network?

In this scenario, Proseware is a verifier. Woodgrove is the issuer. The verifier needs to know Woodgrove's issuer DID and the verifiable credential type that represents Woodgrove employees before it can create a presentation request for a verified credential for Woodgrove employees. The necessary information might come from some kind of manual exchange between the companies, but this approach would be both manual and complex.

The Microsoft Entra Verified ID Network makes this process easier. Woodgrove, as an issuer, can publish credential types to the Microsoft Entra Verified ID Network. Proseware, as the verifier, can search for published credential types and schemas in the Microsoft Entra Verified ID Network. With this information, Woodgrove can create a [presentation request](presentation-request-api#presentation-request-payload) and easily invoke the Request Service API.

![Diagram that shows Microsoft DID implementation overview.](media/decentralized-identifier-overview/did-overview.png)

## How do I use the Microsoft Entra Verified ID Network?

1. On the start page of **Microsoft Entra Verified ID** in the **Azure portal**, you have a quickstart named **Verification request**. Selecting **Start** takes you to a page where you can browse the Verifiable Credentials Network.

    ![Screenshot that shows the Verified ID Network quickstart.](media/how-use-vcnetwork/vcnetwork-quickstart.png)
2. When you choose **Select first issuer**, a panel opens on the right side of the screen where you can search for issuers by their linked domains. If you're looking for something from Woodgrove, enter **woodgrove** in the search text box. After you select an issuer in the list, the available credential types appear in the lower part labeled **Step 2**. Select the type you want to use and select **Add** to return to the first screen. If the expected linked domain isn't in the list, it means that the linked domain isn't verified yet. If the list of credentials is empty, it means that the issuer verified the linked domain but hasn't published any credential types yet.

    ![Screenshot that shows Verified ID Network Search and select.](media/how-use-vcnetwork/vcnetwork-search-select.png)
3. On the first screen, Woodgrove is now in the issuer list. The next step is to select **Review**.

    ![Screenshot that shows the verified ID Network list of issuers.](media/how-use-vcnetwork/vcnetwork-issuer-list.png)
4. The **Review** screen displays a skeleton presentation request JSON payload for the Request Service API. The important pieces of information are the DID inside the `acceptedIssuers` collection and the `type` value. This information is needed to create a presentation request. The request prompts the user for a credential of a certain type issued by a trusted organization.

    ![Screenshot that shows the Verified ID Network issuer's details.](media/how-use-vcnetwork/vcnetwork-issuer-details.png)

## How do I make my linked domain searchable?

Linked domains that are verified are searchable. Unverified domains aren't searchable.

## How do I make my credential types visible in the list?

Each credential type that was created has an attribute named `availableInVcDirectory` that makes it visible in the list. You can update this attribute to make the credential type visible or not. For more information, see [Admin API reference](admin-api#contract-type).

## What is public when a credential type is made visible?

When you make a credential type available in the Microsoft Entra Verified ID Network, only the **issuing DID**, the credential **type**, and its **schema** are made public. This information was already public before making it visible because of how decentralized identities work. Making the credential type visible makes it searchable in the Microsoft Entra Verified ID Network.