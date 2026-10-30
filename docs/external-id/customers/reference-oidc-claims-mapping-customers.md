---
layout: Conceptual
title: Set up claims mapping for OIDC - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/reference-oidc-claims-mapping-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to configure the standard OpenID Connect claims with the claims your identity provider provides in your external tenant.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.reviewer: brozbab
ms.custom: it-pro, sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: d098fb6e-5798-1575-2105-f3e054587039
document_version_independent_id: d098fb6e-5798-1575-2105-f3e054587039
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/reference-oidc-claims-mapping-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/reference-oidc-claims-mapping-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/reference-oidc-claims-mapping-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d8f61404-3763-d9d6-6c14-fc8bcbb99335
---

# Set up claims mapping for OIDC - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In the OpenID Connect protocol, claims communicate information about the end user. Claims are pieces of user information that an identity provider includes in the ID token it issues for that user. The ID token contains claims about the end user. During sign-up, these claims help uniquely identify the user and provide additional profile information. The values are stored in the corresponding user attributes in your directory.

To set up claims mapping, create an identity provider (IdP) in your Microsoft Entra External ID tenant. The IdP configuration includes the **Claims mapping** section, where you can map standard OpenID Connect (OIDC) claims to the claims your identity provider provides in the ID token.

![Screenshot of the Configure OpenID Connect identity provider page in the Microsoft Entra admin center, highlighting the Claims mapping section.](media/reference-oidc-claims-mapping-customers/oidc-claims-mapping.png)

## Claim and attribute mappings

Use the following table to map standard OpenID Connect claims to corresponding user flow attributes and your IdP claims.

| OIDC Standard Claim | User flow attribute | Description |
| --- | --- | --- |
| sub | N/A | Subject - Identifier for the end-user at the Issuer. |
| name | Display Name | Full name in displayable form including all name parts, possibly including titles and suffixes, ordered according to the end-user's locale and preferences. |
| given\_name | First Name | Given name(s) or first name(s) of the end-user. |
| family\_name | Last Name | Surname(s) or family name of the end-user. |
| email (required by default) | Email | Preferred email address. You can [make it optional](how-to-custom-oidc-federation-customers#make-email-optional-for-external-identity-provider-sign-up) for external IdP sign-up scenarios. |
| email\_verified | N/A | Indicates whether the identity provider verified the end-user's email address. `true` means the identity provider took affirmative steps to ensure the email address was controlled by the end-user at the time the verification was performed. If the email claim is present, a value of `true` is required for account creation. If the email claim isn't present and [email is configured as optional](how-to-custom-oidc-federation-customers#make-email-optional-for-external-identity-provider-sign-up), account creation proceeds without an email address. |
| phone\_number | Phone number | The claim provides the phone number for the user. |
| phone\_number\_verified | N/A | In the received ID token, the value of this claim is true if the end-user's phone number has been verified; otherwise, false. When this claim value is true, this means that your identity provider took affirmative steps to verify the phone number. |
| street\_address | Street Address | Full mailing address, formatted for display or use on a mailing label. In the token response, this field MAY contain multiple lines, separated by newlines. Newlines can be represented either as a carriage return/line feed pair ("\r\n") or as a single line feed character ("\n"). |
| locality | City | City or locality. |
| region | State or Province | State, province, prefecture, or region. |
| postal\_code | ZIP or Postal Code | Zip code or postal code. |
| country | Country or Region | Country name. |

Note

For claims from the identity provider to be stored on the user object, the corresponding user flow attributes must be included in the user flow. First, map your external identity provider claims with the OIDC standard claims. Second, enable the corresponding user flow attributes in the user flow that the identity provider is attached to. If you don't want an attribute to be visible to the user during sign-up, you can [hide the attribute](how-to-define-custom-attributes#configure-attribute-visibility-and-editability-with-microsoft-graph) while still keeping it in the user flow so the claim value is stored.

## Review the identity provider

After you add the claims mapping, review the OIDC configuration on the **Review** tab. The **Review** tab displays the claims list and corresponding user flow attributes that you mapped to your IdP claims.

![Screenshot of the Review tab showing mapped OIDC claims and corresponding user flow attributes before saving the identity provider configuration.](media/reference-oidc-claims-mapping-customers/review-oidc-config.png)