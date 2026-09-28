---
layout: Conceptual
title: Use Microsoft Entra Accounts - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/default-account
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Enable your external business partners and guest users to use their Microsoft Entra work or school accounts to sign in to your apps for B2B collaboration.
ms.topic: how-to
ms.date: 2026-03-27T00:00:00.0000000Z
ai-usage: ai-assisted
ms.collection: M365-identity-device-management
ms.custom: seo-july-2024
locale: en-us
document_id: 31c67f50-f66f-eb1e-80d8-a5c2d6fac18a
document_version_independent_id: 7ca3c676-d4f2-74d5-fb6d-008e6904ba16
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/default-account.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/default-account
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/default-account.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: a0d57147-7a79-8607-b392-eb6c848e08b3
---

# Use Microsoft Entra Accounts - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Microsoft Entra ID is available as an identity provider option for B2B collaboration by default. If an external guest user has a Microsoft Entra account through work or school, they can redeem your B2B collaboration invitations or complete your sign-up user flows using their Microsoft Entra account.

## Guest sign-in using Microsoft Entra accounts

If you want to enable guest users to sign in with their Microsoft Entra account, you can use either the invitation flow or a self-service sign-up user flow. No further configuration is required.

### Microsoft Entra account in the invitation flow

When you [invite a guest user](add-users-administrator) to B2B collaboration, you can specify their Microsoft Entra account as the **Email address** they use to sign in.

[![Screenshot of inviting a guest user using the Microsoft Entra account.](media/default-account/default-account-invite.png)](media/default-account/default-account-invite.png#lightbox)

### Microsoft Entra account in self-service sign-up user flows

Microsoft Entra account is an identity provider option for your self-service sign-up user flows. Users can sign up for your applications using their own Microsoft Entra accounts. First, [enable self-service sign-up](self-service-sign-up-user-flow) for your tenant, and then set up a user flow for the application.

[![Screenshot of Microsoft Entra account in a self-service sign-up user flow.](media/default-account/default-account-user-flow.png)](media/default-account/default-account-user-flow.png#lightbox)

## Verifying the application's publisher domain

As of November 2020, new application registrations show up as unverified in the user consent prompt unless [the application's publisher domain is verified](../identity-platform/howto-configure-publisher-domain), ***and*** the company’s identity has been verified with the Microsoft Partner Network and associated with the application. ([Learn more](../identity-platform/publisher-verification-overview) about this change.) For Microsoft Entra user flows, the publisher’s domain appears only when using a [Microsoft account](microsoft-account) or other Microsoft Entra tenant as the identity provider. To meet these new requirements, follow these steps:

1. [Verify your company identity using your Microsoft Partner Network (MPN) account](/en-us/partner-center/verification-responses). This process verifies information about your company and your company’s primary contact.
2. Complete the publisher verification process to associate your MPN account with your app registration using one of the following options:
    - If the app registration for the Microsoft account identity provider is in a Microsoft Entra tenant, [verify your app in the App Registration portal](../identity-platform/mark-app-as-publisher-verified).
    - If your app registration for the Microsoft account identity provider is in an Azure AD B2C tenant, [mark your app as publisher verified using Microsoft Graph APIs](../identity-platform/troubleshoot-publisher-verification#making-microsoft-graph-api-calls) (for example, using Graph Explorer).