---
layout: Conceptual
title: Use Microsoft Accounts - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/microsoft-account
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Enable your external business partners and guest users to use their Microsoft Account (MSA) to sign in to your apps for B2B collaboration.
ms.topic: how-to
ms.date: 2026-03-27T00:00:00.0000000Z
ai-usage: ai-assisted
ms.collection: M365-identity-device-management
ms.custom: seo-july-2024
locale: en-us
document_id: a8c91376-cbbb-ec1b-4318-bc870622e9e1
document_version_independent_id: 2354aa2d-0271-f7c8-6639-06d65250effe
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/microsoft-account.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/microsoft-account
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/microsoft-account.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bc774385-e42e-a4bc-47de-c228ef104fa2
---

# Use Microsoft Accounts - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Your B2B guest users can use their own personal Microsoft accounts for B2B collaboration without further configuration. Guest users can redeem your B2B collaboration invitations or complete your sign-up user flows using their personal Microsoft account.

Microsoft accounts are set up by a user to get access to consumer-oriented Microsoft products and cloud services, such as Outlook, OneDrive, Xbox LIVE, or Microsoft 365. The account is created and stored in the Microsoft consumer identity account system, run by Microsoft.

## Guest sign-in using Microsoft accounts

Microsoft account is available by default in the list of **External Identities** &gt; **All identity providers**. No further configuration is needed to allow guest users to sign in with their Microsoft account, using either the invitation flow, or a self-service sign-up user flow.

### Microsoft account in the invitation flow

When you [invite a guest user](add-users-administrator) to B2B collaboration, you can specify their Microsoft account as the email address they'll use to sign in.

![Screenshot of invite using a Microsoft account.](media/microsoft-account/microsoft-account-invite.png)

### Microsoft account in self-service sign-up user flows

Microsoft account is an identity provider option for your self-service sign-up user flows. Users can sign up for your applications using their own Microsoft accounts. First, you'll need to [enable self-service sign-up](self-service-sign-up-user-flow) for your tenant. Then you can set up a user flow for the application, and select Microsoft account as one of the sign-in options.

![Screenshot of the Microsoft account in a self-service sign-up user flow.](media/microsoft-account/microsoft-account-user-flow.png)

## Verifying the application's publisher domain

As of November 2020, new application registrations show up as unverified in the user consent prompt, unless [the application's publisher domain is verified](../identity-platform/howto-configure-publisher-domain), ***and*** the company’s identity has been verified with the Microsoft Partner Network and associated with the application. For Microsoft Entra External ID user flows, the publisher’s domain appears only when using a Microsoft account or another Microsoft Entra tenant as the identity provider. To meet these new requirements, follow the steps below:

1. [Verify your company identity using your Microsoft Partner Network (MPN) account](/en-us/partner-center/verification-responses). This process verifies information about your company and your company’s primary contact.
2. Complete the publisher verification process to associate your MPN account with your app registration using one of the following options:
    - If the app registration for the Microsoft account identity provider is in a Microsoft Entra tenant, [verify your app in the App Registration portal](../identity-platform/mark-app-as-publisher-verified).
    - If your app registration for the Microsoft account identity provider is in an Azure AD B2C tenant, [mark your app as publisher verified using Microsoft Graph APIs](../identity-platform/troubleshoot-publisher-verification#making-microsoft-graph-api-calls) (for example, using Graph Explorer).