---
layout: Conceptual
title: Authentication Branding - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/concept-branding-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to customize Microsoft-hosted sign-in and sign-up pages in Microsoft Entra External ID with company branding, text, and languages.
ms.topic: concept-article
ms.date: 2026-11-13T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange, msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: a1a00609-3577-7c9d-f83d-90e04759e5e1
document_version_independent_id: dee5126b-830e-e51e-0801-62a04bd22d33
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/concept-branding-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/concept-branding-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/concept-branding-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
platformId: e3252c7c-5035-8234-f033-3c504e44e751
---

# Authentication Branding - Microsoft Entra External ID | Microsoft Learn

After creating an external tenant, you can customize the Microsoft-hosted pages customers use to sign in, sign up, or sign out. The tenant comes with neutral branding that you can tailor to your company's needs. Add a background image or color, favicon, layout, header, and footer, or upload custom CSS. These settings customize the hosted authentication pages, not your application's interface. For more information, see [Customize the neutral branding in your external tenant](how-to-customize-branding-customers).

**Applies to external tenants:** Feature support varies by authentication approach and API or SDK version. Compare Microsoft-hosted authentication, Embedded native authentication, and Bring Your Own UX (BYO UX) in the [authentication approach overview](concept-choose-authentication-approach). Check feature availability in the [authentication support matrix](concept-supported-features-customers#authentication-approach-supportability).

If the custom company branding fails to load, the sign-in page reverts to the neutral branding.

The following list and image outline the elements of the neutral branding sign-in experience:

1. Background image and color.
2. Favicon.
3. Banner logo.
4. Footer as a page layout element.
5. Footer links, such as **Privacy & cookies** and **Terms of use**, and troubleshooting details available from the ellipsis menu.

    [![Screenshot of a neutral sign-in page with numbered branding elements.](media/how-to-customize-branding-customers/ciam-neutral-branding.png)](media/how-to-customize-branding-customers/ciam-neutral-branding.png#lightbox)

As a comparison, here’s how the [default Microsoft sign-in experience](../../fundamentals/how-to-customize-branding) in a Microsoft Entra ID tenant looks:

[![Screenshot of the Microsoft Entra ID default Microsoft branding.](media/how-to-customize-branding-customers/microsoft-branding.png)](media/how-to-customize-branding-customers/microsoft-branding.png#lightbox)

## Preview customization options

The [modern UX and customization overview](../customization-overview) covers the Fluent experience, Basic and Advanced styling, and custom HTML with optional JavaScript. These new capabilities are configured through application branding themes; this section doesn't extend them to default company branding. Microsoft retains control of authentication fields and actions.

These capabilities are scheduled to become available in preview on December 7, 2026, for external tenants with the preview enabled. The existing company-branding procedures continue to apply to default branding.

## Text customization

You can customize text for built-in attributes, such as Given Name, Surname, City, and Postal Code, on Microsoft-hosted sign-up and sign-in pages. Customize strings under **Company Branding** or through language customization in **User flows**. Both options modify the same JSON file, so the most recent change overrides the previous one.

## Language customization

Customize branding elements for users who sign in with a specific browser language. Elements you don't customize retain their defaults. Add language customizations under **Company Branding** or for a specific user flow under **User flows**. For supported languages and instructions, see [Customize the language of the authentication experience](how-to-customize-languages-customers).

## Microsoft Graph APIs

You can also manage company branding and configure all assets programmatically.

- For the default branding, use the [organizationalBranding resource type](/en-us/graph/api/resources/organizationalbranding) and its associated methods.
- To customize branding based on locale, use the [organizationalBrandingLocalization resource type](/en-us/graph/api/resources/organizationalbrandinglocalization) and its associated methods.