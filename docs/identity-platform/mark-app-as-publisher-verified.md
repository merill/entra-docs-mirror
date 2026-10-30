---
layout: Conceptual
title: Mark an app as publisher verified - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/mark-app-as-publisher-verified
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Describes how to mark an app as publisher verified. When an application is marked as publisher verified, it means that the publisher (application developer) verified the authenticity of their organization using a Cloud Partner Program (CPP) account that completed the verification process and associated this CPP account with that application registration.
manager: dougeby
ms.custom: 
ms.date: 2024-05-31T00:00:00.0000000Z
ms.reviewer: 
ms.topic: how-to
locale: en-us
document_id: b7d486f8-cf31-28d3-e611-54d3d3be21de
document_version_independent_id: 79bb799f-6cda-b98f-ddfd-b15ce4125136
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/mark-app-as-publisher-verified.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/mark-app-as-publisher-verified
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/mark-app-as-publisher-verified.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8fbcf615-d297-308f-f83e-750559ed509d
---

# Mark an app as publisher verified - Microsoft identity platform | Microsoft Learn

When an app registration has a verified publisher, it means that the publisher of the app has [verified](/en-us/partner-center/verification-responses) their identity using their Microsoft AI Cloud Partner Program account and has associated this account with their app registration. This article describes how to complete the [publisher verification](publisher-verification-overview) process.

## Quickstart

If you're already enrolled in the [Microsoft AI Cloud Partner Program](/en-us/partner-center/intro-to-cloud-partner-program-membership) and have met the [prerequisites](publisher-verification-overview#requirements), you can get started right away:

1. Sign into the [App Registration portal](https://aka.ms/PublisherVerificationPreview) using [multifactor authentication](../identity/authentication/concept-mfa-licensing)
2. Choose an app and select **Branding & properties**.
3. Select **Add Partner ID to verify publisher** and review the listed requirements.
4. Enter your Partner One ID and select **Verify and save**.

For more details on specific benefits, requirements, and frequently asked questions see the [overview](publisher-verification-overview).

## Mark your app as publisher verified

Make sure you meet the [prerequisites](publisher-verification-overview#requirements), then follow these steps to mark your app as Publisher Verified.

1. Sign in using [multifactor authentication](../identity/authentication/concept-mfa-licensing) to an organizational (Microsoft Entra) account authorized to make changes to the app you want to mark as Publisher Verified and on the Microsoft AI Cloud Partner Program Account in Partner Center.

    - The Microsoft Entra user must have one of the following [roles](../identity/role-based-access-control/permissions-reference): Application Administrator or Cloud Application Administrator.
    - The user in Partner Center must have the following [roles](/en-us/partner-center/permissions-overview): Microsoft AI Cloud Partner Program Admin or Accounts Admin.
2. Navigate to the **App registrations** blade:
3. Select on an app you would like to mark as Publisher Verified and open the **Branding & properties** blade.
4. Ensure the app’s [publisher domain](howto-configure-publisher-domain) is set.
5. Ensure that either the publisher domain or a DNS-verified [custom domain](../fundamentals/add-custom-domain) on the tenant matches the domain of the email address used during the verification process for your CPP account.
6. Select **Add Partner ID to verify publisher** near the bottom of the page.
7. Enter the **Partner ID** for:

- A valid Cloud Partner Program account that has completed the verification process.

    - The Partner global account (PGA) for your organization.

1. Select **Verify and save**.
2. Wait for the request to process, this may take a few minutes.
3. If the verification was successful, the publisher verification window closes, returning you to the **Branding & properties** blade. You see a blue verified badge next to your verified **Publisher display name**.
4. Users who get prompted to consent to your app start seeing the badge soon after you've gone through the process successfully, although it may take some time for updates to replicate throughout the system.
5. Test this functionality by signing into your application and ensuring the verified badge shows up on the consent screen. If you're signed in as a user who has already granted consent to the app, you can use the *prompt=consent* query parameter to force a consent prompt. This parameter should be used for testing only, and never hard-coded into your app's requests.
6. Repeat these steps as needed for any more apps you would like the badge to be displayed for. You can use Microsoft Graph to do this more quickly in bulk, and PowerShell cmdlets are available soon. See [Making Microsoft API Graph calls](troubleshoot-publisher-verification#making-microsoft-graph-api-calls) for more info.

That’s it! Let us know if you have any feedback about the process, the results, or the feature in general.