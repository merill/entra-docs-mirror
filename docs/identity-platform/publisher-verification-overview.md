---
layout: Conceptual
title: Publisher verification overview - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/publisher-verification-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about benefits, program requirements, and frequently asked questions in the publisher verification program for the Microsoft identity platform.
manager: dougeby
ms.date: 2024-08-13T00:00:00.0000000Z
ms.reviewer: 
ms.topic: concept-article
locale: en-us
document_id: f83478f0-0faa-2e10-37f2-819ad2351445
document_version_independent_id: 3ffd5b35-a3d7-5dca-dc8b-acec1d85ec3c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/publisher-verification-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/publisher-verification-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/publisher-verification-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5cc0626f-4b32-b6f5-9f45-b0d0c1e1c17b
---

# Publisher verification overview - Microsoft identity platform | Microsoft Learn

Publisher verification gives app users and organization admins information about the authenticity of the developer's organization, who publishes an app that integrates with the Microsoft identity platform.

When an app has a verified publisher, this means that the organization that publishes the app has been verified as authentic by Microsoft. Verifying an app includes using a Microsoft AI Cloud Partner Program (CPP), formerly known as Microsoft Partner Network (MPN), account that's been [verified](/en-us/partner-center/verification-responses) and associating the verified PartnerID with an app registration.

When the publisher of an app has been verified, a blue *verified* badge appears in the Microsoft Entra consent prompt for the app and on other webpages:

![Screenshot that shows an example of a Microsoft app consent prompt.](media/publisher-verification-overview/consent-prompt.png)

The following video describes the process:

Publisher verification primarily is for developers who build multitenant apps that use [OAuth 2.0 and OpenID Connect](v2-protocols) with the [Microsoft identity platform](v2-overview). These types of apps can sign in a user by using OpenID Connect, or they can use OAuth 2.0 to request access to data by using APIs like [Microsoft Graph](https://developer.microsoft.com/graph/).

## Benefits

Publisher verification for an app has the following benefits:

- **Increased transparency and risk reduction for customers**. Publisher verification helps customers identify apps that are published by developers they trust to reduce risk in the organization.
- **Improved branding**. A blue *verified* badge appears in the Microsoft Entra app [consent prompt](application-consent-experience), on the enterprise apps page, and in other app elements that users and admins see.
- **Smoother enterprise adoption**. Organization admins can configure [user consent policies](../identity/enterprise-apps/configure-user-consent) that include publisher verification status as primary policy criteria.

Note

Beginning November 2020, if [risk-based step-up consent](../identity/enterprise-apps/configure-risk-based-step-up-consent) is enabled, users can't consent to most newly registered multitenant apps that *aren't* publisher verified. The policy applies to apps that were registered after November 8, 2020, which use OAuth 2.0 to request permissions that extend beyond the basic sign-in and read user profile, and which request consent from users in tenants that aren't the tenant where the app is registered. In this scenario, a warning appears on the consent screen. The warning informs the user that the app was created by an unverified publisher and that the app is risky to download or install.

## Requirements

App developers must meet a few requirements to complete the publisher verification process. Many Microsoft partners will have already satisfied these requirements.

- The developer must have a Partner One ID for a valid [Microsoft AI Cloud Partner Program](https://partner.microsoft.com/membership) account that has completed the [verification](/en-us/partner-center/verification-responses) process. The CPP account must be the [partner global account (PGA)](/en-us/partner-center/account-structure#the-top-level-is-the-partner-global-account-pga) for the developer's organization.

    Note

    The CPP account you use for publisher verification can't be your partner location Partner One ID. Currently, location Partner One IDs aren't supported for the publisher verification process.
- The app that's to be publisher verified must be registered by using a Microsoft Entra work or school account. Apps that are registered by using a Microsoft account can't be publisher verified.
- The Microsoft Entra tenant where the app is registered must be associated with the PGA. If the tenant where the app is registered isn't the primary tenant associated with the PGA, complete the steps to [set up the CPP PGA as a multitenant account and associate the Microsoft Entra tenant](/en-us/partner-center/multi-tenant-account#add-an-azure-ad-tenant-to-your-account).
- The app must be registered in a Microsoft Entra tenant and have a [publisher domain](howto-configure-publisher-domain) set. The feature is not supported in Azure AD B2C tenant.
- The domain of the email address that's used during CPP account verification must either match the publisher domain that's set for the app or be a DNS-verified [custom domain](../fundamentals/add-custom-domain) that's added to the Microsoft Entra tenant. (**NOTE**\_\_: the app's publisher domain can't be \*.onmicrosoft.com to be publisher verified)
- The user who initiates verification must be authorized to make changes both to the app registration in Microsoft Entra ID and to the CPP account in Partner Center. The user who initiates the verification must have one of the required roles in both Microsoft Entra ID and Partner Center.

    - In Microsoft Entra ID, this user must be a member of one of the following [roles](../identity/role-based-access-control/permissions-reference): Application Administrator or Cloud Application Administrator.
    - In Partner Center, this user must have one of the following [roles](/en-us/partner-center/permissions-overview): CPP Partner Admin or Account Admin.
- The user who initiates verification must sign in by using [Microsoft Entra multifactor authentication](../identity/authentication/howto-mfa-getstarted).
- The publisher must consent to the [Microsoft identity platform for developers Terms of Use](/en-us/legal/microsoft-identity-platform/terms-of-use).

Developers who have already met these requirements can be verified in minutes. No charges are associated with completing the prerequisites for publisher verification.

## Publisher verification in national clouds

Publisher verification currently isn't supported in national clouds. Apps that are registered in national cloud tenants can't be publisher verified at this time.

## Frequently asked questions

Review frequently asked questions about the publisher verification program. For common questions about requirements and the process, see [Mark an app as publisher verified](mark-app-as-publisher-verified).

- **What does publisher verification *not* tell me about the app or its publisher?** The blue *verified* badge doesn't imply or indicate quality criteria you might look for in an app. For example, you might want to know whether the app or its publisher have specific certifications, comply with industry standards, or adhere to best practices. Publisher verification doesn't give you this information. Other Microsoft programs, like [Microsoft 365 App Certification](/en-us/microsoft-365-app-certification/overview), do provide this information. Verified publisher status is only one of the several criteria to consider while evaluating the security and [OAuth consent requests](../identity/enterprise-apps/manage-consent-requests) of an application.
- **How much does publisher verification cost for the app developer? Does it require a license?** Microsoft doesn't charge developers for publisher verification. No license is required to become a verified publisher.
- **How does publisher verification relate to Microsoft 365 Publisher Attestation and Microsoft 365 App Certification?**[Microsoft 365 Publisher Attestation](/en-us/microsoft-365-app-certification/docs/attestation) and [Microsoft 365 App Certification](/en-us/microsoft-365-app-certification/docs/certification) are complementary programs that help developers publish trustworthy apps that customers can confidently adopt. Publisher verification is the first step in this process. All developers who create apps that meet the criteria for completing Microsoft 365 Publisher Attestation or Microsoft 365 App Certification should complete publisher verification. The combined programs can give developers who integrate their apps with Microsoft 365 even more benefits.
- **Is publisher verification the same as the Microsoft Entra application gallery?** No. Publisher verification complements the [Microsoft Entra application gallery](../identity/enterprise-apps/v2-howto-app-gallery-listing), but it's a separate program. Developers who fit the publisher verification criteria should complete publisher verification independently of participating in the Microsoft Entra application gallery or other programs.