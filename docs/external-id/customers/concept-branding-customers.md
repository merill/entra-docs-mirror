---
layout: Conceptual
title: Customize the company branding - Microsoft Entra External ID | Microsoft Learn
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
description: Learn how to customize the sign-in and sign-up experiences for your customers.
ms.topic: concept-article
ms.date: 2025-01-07T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange
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
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e3252c7c-5035-8234-f033-3c504e44e751
---

# Customize the company branding - Microsoft Entra External ID | Microsoft Learn

Note

The branding customizations described in this article apply to **browser-delegated authentication**, where users sign in through a Microsoft-hosted sign-in page. If you use [native authentication](concept-choose-authentication-approach), you build and control the sign-in UI directly in your app, so branding is managed in your application code.

After creating a new external tenant, you can customize the appearance of your web-based applications for customers who sign in, sign up, or sign out to personalize their end-user experience. The external tenant comes with a default neutral branding that doesn’t include any existing Microsoft branding. However, this neutral default branding can be customized to meet your company’s specific needs. You have the flexibility to add a custom background image or color, favicon, layout, header, and footer to your authentication experience. You can add each custom branding property individually to the custom sign-in page, or you can upload a custom CSS. For more information, see [Customize the neutral branding in your external tenant](how-to-customize-branding-customers).

If the custom company branding fails to load, the sign-in page reverts to the neutral branding.

The following list and image outline the elements of the neutral branding sign-in experience:

1. Background image and color.
2. Favicon.
3. Banner logo.
4. Footer as a page layout element.
5. Footer hyperlinks, for example, Privacy & cookies, Terms of use and troubleshooting details also known as ellipsis in the right bottom corner of the screen.

    [![Screenshot of the neutral branding.](media/how-to-customize-branding-customers/ciam-neutral-branding.png)](media/how-to-customize-branding-customers/ciam-neutral-branding.png#lightbox)

As a comparison, here’s how the [default Microsoft sign-in experience](../../fundamentals/how-to-customize-branding) in a Microsoft Entra ID tenant looks:

[![Screenshot of the Microsoft Entra ID default Microsoft branding.](media/how-to-customize-branding-customers/microsoft-branding.png)](media/how-to-customize-branding-customers/microsoft-branding.png#lightbox)

## Text customization

You might have different requirements for the information you want to collect during sign-up and sign-in. The external tenant comes with a built-in set of information stored in attributes, such as Given Name, Surname, City, and Postal Code. In the external tenant, we have two options to add custom text to the sign-up and sign-in experience. The function is available under each user flow during language customization and also under **Company Branding**. Although we have two ways to customize strings, both ways modify the same JSON file. The most recent change made either via **User flows** or via **Company Branding** will always override the previous one.

## Language customization

You can create a personalized sign-in experience for users who sign in using a specific browser language by customizing the branding elements. If you don't make any changes to the elements, the default elements will be displayed. In the tenant, you can add a custom language to the sign-in experience under **Company Branding** or to a specific user flow under **User flows**. The language customization is available for a list of languages. For more information, see [Customize the language of the authentication experience](how-to-customize-languages-customers).

## Microsoft Graph APIs

You can also manage company branding and configure all assets programmatically.

- For the default branding, use the [organizationalBranding resource type](/en-us/graph/api/resources/organizationalbranding) and its associated methods.
- To customize branding based on locale, using the [organizationalBrandingLocalization resource type](/en-us/graph/api/resources/organizationalbrandinglocalization) resource type and its associated methods.