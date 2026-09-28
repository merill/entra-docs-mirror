---
layout: Conceptual
title: Identity providers for workforce tenants - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/identity-providers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to use Microsoft Entra ID as your default identity provider for sharing with external users.
ms.topic: concept-article
ms.date: 2026-04-24T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
locale: en-us
document_id: 1f08b679-d6ba-7812-f9b6-9e2cb2d1dda6
document_version_independent_id: ca36294b-3c3f-4345-48d8-10ed73d26dff
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/identity-providers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/identity-providers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/identity-providers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 040e385a-f8c2-20df-4f0a-c996ab403b17
---

# Identity providers for workforce tenants - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Tip

This article applies to B2B collaboration in workforce tenants. For information about external tenants, see [Authentication methods and identity providers in external tenants](customers/concept-authentication-methods-customers).

An *identity provider* (IdP) creates, maintains, and manages identity information while providing authentication services to applications. When you share your apps and resources with external users, Microsoft Entra ID is the default identity provider for sharing. If you invite an external user who already has a Microsoft Entra account or Microsoft account, they can automatically sign in without further configuration on your part.

External ID offers various identity providers.

- **Microsoft Entra accounts**: Guest users can use their Microsoft Entra work or school accounts to redeem your B2B collaboration invitations or complete your sign-up user flows. [Microsoft Entra ID](default-account) is one of the allowed identity providers by default. No other configuration is needed to make this identity provider available for user flows.
- **Microsoft accounts**: Guest users can use their own personal Microsoft account (MSA) to redeem your B2B collaboration invitations. When setting up a [self-service sign-up](self-service-sign-up-overview) user flow, you can add [Microsoft Account](microsoft-account) as one of the allowed identity providers. No other configuration is needed to make this identity provider available for user flows.
- **Email one-time passcode**: When a guest redeems an invitation or accesses a shared resource, they can request a temporary code. This code is sent to their email address. Then they enter this code to continue signing in. The email one-time passcode feature authenticates B2B guest users when they can't be authenticated through other means. When setting up a self-service sign-up user flow, you can add **Email One-Time Passcode** as one of the allowed identity providers. Some setup is required; see [Email one-time passcode authentication](one-time-passcode).
- **Google**: Google federation allows external users to redeem invitations from you by signing in to your apps with their own Gmail accounts. Google federation can also be used in your self-service sign-up user flows. See how to [add Google as an identity provider](google-federation).

    Important

    - Since July 12, 2021, if Microsoft Entra B2B customers set up new Google integrations for self-service sign-up for custom or line-of-business applications, authentication with Google identities doesn't work until authentications are moved to system web views. [Learn more](google-federation#deprecation-of-web-view-sign-in-support).
    - Since September 30, 2021, Google has [deprecated embedded web-view sign-in support](https://developers.googleblog.com/2016/08/modernizing-oauth-interactions-in-native-apps.html). If your apps authenticate users with an embedded web view and you're using Google federation with [Azure AD B2C](/en-us/azure/active-directory-b2c/identity-provider-google) or Microsoft Entra B2B for [external user invitations](google-federation) or self-service sign-up, Google Gmail users can't authenticate. [Learn more](google-federation#deprecation-of-web-view-sign-in-support).
- **Facebook**: When building an app, you can configure self-service sign-up and enable Facebook federation so that users can sign up for your app using their own Facebook accounts. Facebook can only be used for self-service sign-up user flows and isn't available as a sign-in option when users are redeeming invitations from you. See how to [add Facebook as an identity provider](facebook-federation).
- **SAML/WS-Fed identity provider federation**: You can also set up federation with any external IdP that supports the SAML or WS-Fed protocols. SAML/WS-Fed IdP federation allows external users to use their own IdP-managed accounts to sign in to your apps or resources, without having to create new Microsoft Entra credentials. For more information, see [SAML/WS-Fed identity providers](direct-federation-overview). For detailed setup steps, see [Add federation with SAML/WS-Fed identity providers](direct-federation).

To configure federation with Google, Facebook, or a SAML/WS-Fed identity provider, you need to be at least an [External Identity Provider Administrator](../identity/role-based-access-control/permissions-reference#external-identity-provider-administrator) in your Microsoft Entra tenant.

## Adding social identity providers

Microsoft Entra ID is enabled by default for self-service sign-up, so users always have the option of signing up using a Microsoft Entra account. However, you can enable other identity providers, including social identity providers like Google or Facebook. To set up social identity providers in your Microsoft Entra tenant, you create an application at the identity provider and configure credentials. You obtain a client or app ID and a client or app secret, which you can then add to your Microsoft Entra tenant.

After you add an identity provider to your Microsoft Entra tenant:

- When you invite an external user to apps or resources in your organization, the external user can sign in using their own account with that identity provider.
- When you enable [self-service sign-up](self-service-sign-up-overview) for your apps, external users can sign up for your apps using their own accounts with the identity providers you added. They can select from the social identity providers options you made available on the sign-up page:

    ![Screenshot showing the sign-in screen with Google and Facebook options](media/identity-providers/sign-in-with-social-identity.png)

For an optimal sign-in experience, federate with identity providers whenever possible so you can give your invited guests a seamless sign-in experience when they access your apps.