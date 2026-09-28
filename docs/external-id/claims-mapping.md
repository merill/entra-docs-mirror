---
layout: Conceptual
title: B2B collaboration user claims mapping - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/claims-mapping
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Customize the user claims that are issued in the SAML token for Microsoft Entra B2B users.
ms.topic: concept-article
ms.date: 2025-04-09T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.custom: sfi-image-nochange
locale: en-us
document_id: 23b6318a-1d43-e98e-649a-33188c844506
document_version_independent_id: 3dc31b3e-d3ce-8937-d068-b1e460df4569
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/claims-mapping.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/claims-mapping
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/claims-mapping.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 901d5dde-a197-c907-e3d4-39eecd7e61e9
---

# B2B collaboration user claims mapping - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

With Microsoft Entra External ID, you can customize the claims that are issued in the SAML token for [B2B collaboration](what-is-b2b) users. When a user authenticates to the application, Microsoft Entra ID issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them. By default, this claim includes the user's user name, email address, first name, and family name.

In the [Microsoft Entra admin center](https://entra.microsoft.com), you can view or edit the claims that are sent in the SAML token to the application. To access the settings, browse to **Entra ID** &gt; **Enterprise apps** &gt; the application that's configured for single sign-on &gt; **Single sign-on**. See the SAML token settings in the **User Attributes** section.

![Screenshot of the SAML token attributes in the UI.](media/claims-mapping/view-claims-in-saml-token-attributes.png)

You might need to edit the claims issued in the SAML token for two reasons:

1. The application requires a different set of claim URIs or claim values.
2. The application requires the NameIdentifier claim to be different from the user principal name [(UPN)](../identity/hybrid/connect/plan-connect-userprincipalname#what-is-userprincipalname) stored in Microsoft Entra ID.

Learn how to add and edit claims in [Customizing claims issued in the SAML token for enterprise applications in Microsoft Entra ID](../identity-platform/saml-claims-customization).

## UPN claims behavior for B2B users

If you need to issue the UPN value as an application token claim, the actual claim mapping might behave differently for B2B users. If the B2B user authenticates with an external Microsoft Entra identity and you issue `user.userprincipalname` as the source attribute, Microsoft Entra ID issues the UPN attribute from the home tenant for this user.

For all [other external identity types](redemption-experience#invitation-redemption-flow), such as SAML/WS-Fed, Google, and Email one-time passcode (OTP) when you use `user.userprincipalname` as a claim, the system issues the user's UPN instead of their email address. If you want the actual UPN to be issued in the token claim for all B2B users, set `user.localuserprincipalname` as the source attribute instead.

Note

The behavior mentioned in this section is the same for both cloud-only B2B users and synced users who were [invited/converted to B2B collaboration](invite-internal-users).