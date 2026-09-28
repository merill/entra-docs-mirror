---
layout: Conceptual
title: Face Check with Microsoft Entra Verified ID pricing - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/verified-id-pricing
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: Learn about Face Check with Microsoft Entra Verified ID billing model. Learn how to enable the Face Check add-on in your tenant by linking your Microsoft Azure subscription.
ms.topic: concept-article
ms.date: 2026-03-24T00:00:00.0000000Z
locale: en-us
document_id: 96a4e37d-4c68-4df5-4bda-642a7398fe4c
document_version_independent_id: 96a4e37d-4c68-4df5-4bda-642a7398fe4c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/verified-id-pricing.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/verified-id-pricing
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/verified-id-pricing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2624a017-7337-44fa-9494-a407bb0e59fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a438284e-c3c3-4c36-ab0b-aa7c244b912c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: f3dc8299-7e9d-578d-610c-81d2708c990e
---

# Face Check with Microsoft Entra Verified ID pricing - Microsoft Entra Verified ID | Microsoft Learn

Face Check with Microsoft Entra Verified ID pricing is based on unique Face Check verifications performed by the verifying authority during the billing cycle. There are two options to enable Face Check add-on on a workforce tenant:

- Enable as a Microsoft Entra Suite trial or paid subscriber. Face Check is included as a full capability in the Microsoft Entra Suite.
- Or enable in pay-as-you-go where your Azure subscription received charges per each individual Face Check verification performed from your tenant.

In this article, learn about the Face Check billing model and linking your Verified ID authority to an Azure subscription.

Important

This article provides information on how the Verified ID service emits billing services on Face Check usage. For the latest information on pricing, see [Microsoft Entra pricing](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## What do I need to do?

To take advantage of the consumptive billing, your Verified ID authority must be linked to an Azure subscription.

| **If your Verified ID authority is:** | **You need to:** |
| --- | --- |
| A Verified ID authority not yet linked to a subscription | Link your Verified ID authority to an Azure subscription to activate consumptive billing. |
| A Verified ID authority linked to a subscription | Do nothing. You're automatically billed monthly for Face Check verifications. |

## About monthly Face Check verifications billing

In your Microsoft Entra Verified ID, you can verify credentials from issuer authorities that you trust. Additionally, with Face Check, your organization can perform high-assurance verifications securely, simply, and at scale by performing facial matching between a user’s real-time selfie and a photo.

Verified ID generates individual billing events for each unique verification performed by the platform, whether that verification succeeds or fails. The following matrix provides further clarity on Face Check verification scenarios that are billed:

| **Face Check Verification scenario** | **Emits billing event (yes/no)** |
| --- | --- |
| Verification request fails after reading QR Code | No |
| Verification request returns service error: The Verified ID service is unable to process the verification request | No |
| Verification request returns failed face matching: Processing the face matching between the biometric data and the credential data failed | Yes |
| Verification request returns a face matching score | Yes |

## Link your Verified ID authority to a subscription

1. Go to the **Verified ID** overview page. Scroll down to the new **Add-ons** section and **Enable** the Face Check add-on. ![Screenshot of the Face Check add-on.](media/using-facecheck/face-check-add-on.png)
2. In the **Link a subscription** section, select a **Subscription**, a **Resource group**, and the **Resource location**. Then select **Validate**. If there are no subscriptions listed, see [What if I can't find a subscription?](using-facecheck#what-if-i-cant-find-a-subscription)![Screenshot subscription linking for Face Check.](media/using-facecheck/face-check-subscription-linking.png)
3. **Enable** the add-on once the information is validated. ![Screenshot of using Face Check.](media/using-facecheck/face-check-add-on-enabled.png)

## What if I can't find a subscription?

If no subscriptions are available in the Link a subscription pane, here are some possible reasons:

You don't have the appropriate permissions. Be sure to sign in with an Azure account that is assigned at least the Contributor role within the subscription or a resource group within the subscription.

A subscription exists, but it isn't associated with your directory yet. You can [associate an existing subscription to your tenant](/en-us/entra/fundamentals/how-subscriptions-associated-directory) and then repeat the steps for linking it to your tenant.

No subscription exists. In the Link a subscription pane, you can create a subscription by selecting the link. If you don't already have a subscription, you might create one here. After you create a new subscription, you'll need to [create a resource group](/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal) in the new subscription, and then repeat the steps for linking it to your tenant.