---
layout: Conceptual
title: Configure Verified ID settings for an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-verified-id-settings
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to configure verified ID settings for an access package in entitlement management.
editor: HANKI
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2024-10-17T00:00:00.0000000Z
ms.reviewer: hanki
ms.custom: sfi-ga-nochange
locale: en-us
document_id: ad50dbdc-6e8c-1160-c4b3-8314bcc1e887
document_version_independent_id: 50f770d4-f204-6a8f-fca7-8de4d694400b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-verified-id-settings.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-verified-id-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-verified-id-settings.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://authoring-docs-microsoft.poolparty.biz/devrel/2624a017-7337-44fa-9494-a407bb0e59fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://authoring-docs-microsoft.poolparty.biz/devrel/a438284e-c3c3-4c36-ab0b-aa7c244b912c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 2e6c041a-a91e-24f4-8be6-efa89b41a193
---

# Configure Verified ID settings for an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

When setting up an access package policy, admins can specify whether it’s for users in the directory, connected organizations, or any external user. Entitlement Management determines if the person requesting the access package is within the scope of the policy.

Sometimes you might want users to present extra identity proofs during the request process such as a training certification, work authorization, or citizenship status. As an access package manager, you can require that requestors present a verified ID containing those credentials from a trusted issuer. Approvers can then quickly view if a user’s verifiable credentials were validated at the time that the user presented their credentials and submitted the access package request.

As an access package manager, you can include verified ID requirements for an access package at any time by editing an existing policy or adding a new policy for requesting access.

This article describes how to configure the verified ID requirement settings for an access package.

## Prerequisites

Before you begin, you must set up your tenant to use the [Microsoft Entra Verified ID service](../verified-id/decentralized-identifier-overview). You can find detailed instructions on how to do that here: [Configure your tenant for Microsoft Entra Verified ID](../verified-id/verifiable-credentials-configure-tenant-quick).

## License requirements

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Create an access package with verified ID requirements

To add a verified ID requirement to an access package, you must start from the access package’s requests tab. Follow these steps to add a verified ID requirement to a new access package.

**Prerequisite role**: Global Administrator

Note

Identity Governance Administrator, User Administrator, Catalog owner, or Access package manager will be able to add verified ID requirements to access packages soon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, select **+ New access package**.
4. On the **Requests** tab, scroll to the **Required Verified Ids** section.
5. Select **+ Add issuer** and choose an issuer from the Microsoft Entra Verified ID network. If you want to issue your own credentials to users, see: [Issue Microsoft Entra Verified ID credentials from an application](../verified-id/verifiable-credentials-configure-issuer). ![Select issuer for Microsoft Entra Verified ID.](media/entitlement-management-verified-id-settings/select-issuer.png)
6. Select the **credential type(s)** you want users to present during the request process. ![Screenshot of credential types for Microsoft Entra Verified ID.](media/entitlement-management-verified-id-settings/issuer-credentials.png)

    Note

    If you select multiple credential types from one issuer, users are required to present credentials of all selected types. Similarly, if you include multiple issuers, users are required to present credentials from each of the issuers you include in the policy. To give users the option of presenting different credentials from various issuers, configure separate policies for each issuer/credential type you accept.
7. Select **Add** to add the verified ID requirement to the access package policy.
8. If you want users to complete a Face Check, select **Require Face Check**. This asks users requesting the access package to perform a real-time, privacy compliant selfie check against the photo that is stored on their Verified ID. Once you select the checkbox, it asks you to select the claim name that maps to the photo on the ID. For more information on Face Check, see [Use Face Check with Microsoft Entra Verified ID](../verified-id/using-facecheck).

    ![Screenshot of the require face check option.](media/entitlement-management-verified-id-settings/require-face-check.png)
9. Once you finish configuring the rest of the settings, you can review your selections on the **Review + create** tab. You can see all verified ID requirements for this access package policy in the **Verified IDs** section. ![Screenshot of a list of verified IDs.](media/entitlement-management-verified-id-settings/verified-ids-list.png)

## Request an access package with verified ID requirements

Once an access package is configured with a verified ID requirement, end-users who are within the scope of the policy are able to request access using the My Access portal. Similarly, approvers are able to see the claims of the VCs presented by requestors when reviewing requests for approval.

The requestor steps are as follows:

1. Go to [`myaccess.microsoft.com`](https://myaccess.microsoft.com) and sign in.
2. Search for the access package you want to request access to (you can browse the listed packages or use the search bar at the top of the page) and select **Request**.
3. If the access package requires you to present a verified ID, you should see a grey information banner as shown here: ![Screenshot of the present verified ID for access package option.](media/entitlement-management-verified-id-settings/present-verified-id-access-package.png)
4. Select **Request Access**. You should now see a QR code. Use your phone to scan the QR code. This launches Microsoft Authenticator, where you're prompted to share your credentials. ![Screenshot of use QR code for verified IDs.](media/entitlement-management-verified-id-settings/verified-id-qr-code.png)
5. If Face Check is required for the access package, the requesting user needs to perform a real-time selfie check against the photo stored on their Verified ID. Face Check protects user privacy by sharing only the match results and not any sensitive identity data.
6. After you share your credentials, My Access will automatically take you to the next step of the request process.

## Entitlement Management and Verified ID Security Partner integration

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, select **+ New access package**.
4. On the **Requests** tab, scroll to the **Required Verified Ids** section.
5. Select **+ Add issuer** and choose an issuer from the Microsoft Entra Verified ID network. If you want to issue your own credentials to users, see: [Issue Microsoft Entra Verified ID credentials from an application](../verified-id/verifiable-credentials-configure-issuer). ![Screenshot of issuer verified ID in an access package.](media/entitlement-management-verified-id-settings/access-package-id-verified.png)
6. Step1 allows the selection of issuers under two types - "Select the type of issuer".

    1. Microsoft Entra Verified ID Network - this could be any Microsoft Entra Verified ID issuer from the drop-down list ![Screenshot of verified ID Network issuer option.](media/entitlement-management-verified-id-settings/verified-id-network-issuer.png)
    2. Security Partners (Third Party providers) - Government ID verification partners that are available via [Microsoft Security Store](/en-us/security/store/what-is-security-store) integration. This is a simple select to configure option where you could add presentation of Verified ID issued from one of the selected IDV partners. The following drop-down selection requires the administrator to purchase the respective Identity verification offer from the partner ![Screenshot of issuer security partners list.](media/entitlement-management-verified-id-settings/issuer-security-partners.png)
7. For "Microsoft Entra Verified ID Network" selection in Step1: Search for the issuer and then Select the **credential type(s)** you want users to present during the request process.
8. For "Security Partners (Third Party providers)" selection in Step1, If the admin is selecting the issuer for the first time, they'll get a link to Security Store to purchase the offer. ![Screenshot of verification partner option.](media/entitlement-management-verified-id-settings/issuer-verification-partner.png)

    Note

    If you select multiple credential types from one issuer, users are required to present credentials of all selected types. Similarly, if you include multiple issuers, users are required to present credentials from each of the issuers you include in the policy. To give users the option of presenting different credentials from various issuers, configure separate policies for each issuer/credential type you accept.
9. Select **Add** to add the verified ID requirement to the access package policy.
10. If you want users to complete a Face Check, select **Require Face Check**. This asks users requesting the access package to perform a real-time, privacy compliant selfie check against the photo that is stored on their Verified ID. Once you select the checkbox, it asks you to select the claim name that maps to the photo on the ID. For more information on Face Check, see: [Using Face Check with Microsoft Entra Verified ID and unlocking high assurance verifications at scale](../verified-id/using-facecheck). ![Screenshot of face check option with verified ID.](media/entitlement-management-verified-id-settings/face-check-verified-id.png)
11. Complete rest of the settings for this access package policy.