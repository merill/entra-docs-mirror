---
layout: Conceptual
title: CSS reference guide for customizing company branding - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/reference-company-branding-css-template
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: pmwongera
description: Reference guide for the CSS template selectors for customizing Microsoft Entra sign-in page company branding.
ms.topic: reference
ms.date: 2026-08-18T00:00:00.0000000Z
ms.reviewer: almars
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 1195b356-cae4-4f18-2a80-2d371a9fc0b3
document_version_independent_id: d0833ad4-5c00-d025-6cdd-0c0dd3e1c286
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/reference-company-branding-css-template.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/reference-company-branding-css-template
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/reference-company-branding-css-template.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: bac80ad7-ca8a-18c4-8f92-4b9d644516d4
---

# CSS reference guide for customizing company branding - Microsoft Entra | Microsoft Learn

Configuring your company branding for the user sign-in process provides a seamless experience in your applications that use Microsoft Entra ID as the identity and access management service. Use this CSS reference guide if you're using the [CSS template](https://download.microsoft.com/download/7/2/7/727f287a-125d-4368-a673-a785907ac5ab/custom-styles-template-013023.css) as part of the [customize company branding](reference-company-branding-css-template) process.

Important

Tenants created after January 5, 2026, don't have custom CSS available for company branding in Microsoft Entra ID. After July 21, 2026, tenants created before January 6, 2026, that don't already use custom CSS can't configure custom CSS.

Microsoft Entra External ID tenants aren't affected.

## Deprecation of custom CSS layout and positioning properties

To align with the [Microsoft Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative) and its focus on identity security and phishing resistance, Microsoft Entra ID is retiring support for custom CSS *layout and positioning properties* in company branding. These properties control where elements appear on the sign-in page and how they're layered, sized, and displayed. For example, they can move, overlap, resize, or hide page content. Retiring them keeps sign-in page layouts consistent and predictable in Microsoft Entra ID.

This change is the first step toward retiring the custom CSS feature entirely. Microsoft plans to provide advance notice, recommended migration paths, and future advanced customization options before that retirement.

For more information, see the blog post [Microsoft Entra ID enhances security of branded sign-ins](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/microsoft-entra-id-enhances-security-of-branded-sign-ins/4537471).

### Timeline

- **After July 21, 2026**: Tenants created before January 6, 2026, that don't already use custom CSS can't configure custom CSS.
- **Later**: The affected layout and positioning properties will be deprecated globally. After deprecation, these properties are blocked and no longer function.
- **Eventually**: Custom CSS will be fully retired. Microsoft will share more guidance, including recommended migration paths, before retirement.

### Who's affected

This change affects organizations whose Microsoft Entra ID tenant uses any of the deprecated layout and positioning properties in their custom CSS. Microsoft Entra External ID tenants aren't affected. After July 21, 2026, tenants created before January 6, 2026, that don't already use custom CSS can't configure custom CSS.

Microsoft notifies affected customers directly in advance.

### Deprecated properties

If your custom CSS uses any of the following properties, remove them from your configuration. These properties don't have a supported migration or replacement.

- `position` (including `top`, `right`, `bottom`, `left`, and `z-index`)
- `margin` (including `margin-top`, `margin-bottom`, `margin-left`, and `margin-right`)
- `transform`
- `opacity`
- `overflow`
- `filter`
- `pointer-events`
- `clip-path`
- `mix-blend-mode`
- `translate`
- `-webkit-transform`
- `-moz-transform`
- `-ms-transform`
- `-o-transform`
- `scale`
- `rotate`
- `perspective`
- `display`
- `visibility`
- `inset`
- `zoom`
- `offset`
- `offset-path`
- `offset-distance`
- `margin-block`
- `margin-block-start`
- `margin-block-end`
- `margin-inline`
- `margin-inline-start`
- `margin-inline-end`
- `order`
- `grid-area`
- `grid-column`
- `grid-column-start`
- `grid-column-end`
- `grid-row`
- `grid-row-start`
- `grid-row-end`
- `isolation`
- `overflow-x`
- `overflow-y`
- `overflow-block`
- `overflow-inline`
- `content-visibility`
- `clip`
- `mask`
- `mask-image`
- `-webkit-mask`
- `-webkit-mask-image`

### Check and update your custom CSS

To inspect your current CSS file, on the **Custom branding** page in the Microsoft Entra admin center at https://entra.microsoft.com, select **Edit**. On the **Layout** tab, under **Custom CSS**, select **Download**. Review the downloaded file for the properties listed in Deprecated properties.

To check all company branding localizations, use Microsoft Graph to export your current company branding configuration, and then check it with the tenant branding inspector tool. You need a Global Administrator or Branding Administrator account.

1. Go to [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), and then sign in to your tenant.
2. If you don't already know your tenant ID, send a `GET` request to the following URL, and then copy the `id` value from the response:

    ```http
    https://graph.microsoft.com/v1.0/organization
    ```
3. Send a `GET` request to the following URL to return all configured company branding localizations. Replace `<tenant-id>` with your tenant ID:

    ```http
    https://graph.microsoft.com/v1.0/organization/<tenant-id>/branding/localizations
    ```
4. Copy the response, or export it to a JSON file.
5. Go to the [tenant branding inspector tool](https://entra-branding-tools.github.io/tenant-branding-inspector/).
6. Paste the copied response, or upload the exported JSON file, into the tool. The tool lists each locale and the deprecated properties that it uses.

To remove the deprecated properties, edit the downloaded CSS file, upload it to the **Company Branding** page in the [Microsoft Entra admin center](https://entra.microsoft.com), and then save your changes. To validate the visual impact before you update production, apply the changes in a test tenant first.

## HTML selectors

The following CSS styles become the default body and link styles for the whole page. Styles that you apply to other links or text override these selectors.

- `body` - Styles for the whole page
- Styles for links:
    - `a, a:link` - All links
    - `a:hover` - When the mouse is over the link
    - `a:focus` - When the link has focus
    - `a:focus:hover` - When the link has focus *and* the mouse is over the link
    - `a:active` - When the link is being clicked

## Microsoft Entra CSS selectors

Use the following CSS selectors to configure the details of the sign-in experience.

Note

To customize internal navigation links, use the new custom CSS selector: `.ext-link`.

- `.ext-background-image` - Container that includes the background image in the default lightbox template
- `.ext-header` - Header at the top of the container
- `.ext-header-logo` - Header logo at the top of the container

    ![Screenshot of the sign-in screen with the .ext-header and .ext-header-logo areas highlighted.](media/reference-company-branding-css-template/header-logo.png)
- `.ext-middle` - Style for the full-screen background that aligns the sign-in box vertically to the middle and horizontally to the center
- `.ext-vertical-split-main-section` - Style for the container of the partial-screen background in the vertical split template that contains both a sign-in box and a background (This style is also known as the Active Directory Federation Services (ADFS) template.)
- `.ext-vertical-split-background-image-container` - Sign-in box background in the vertical split/ADFS template
- `.ext-sign-in-box` - Sign-in box container
- `.ext-title` - Title text

    ![Screenshot of the sign-in box, with the portion of the box that is styled with the .ext-sign-in-box selector.](media/reference-company-branding-css-template/sign-in-box-title.png)
- `.ext-subtitle` - Subtitle text
- Styles for links:

    - `.ext-link` - Internal navigation links
- Styles for primary buttons:

    - `.ext-button.ext-primary` - Primary button default style
    - `.ext-button.ext-primary:hover` - When the mouse is over the button
    - `.ext-button.ext-primary:focus` - When the button has focus
    - `.ext-button.ext-primary:focus:hover` - When the button has focus *and* the mouse is over the button
    - `.ext-button.ext-primary:active` - When the button is being clicked

    ![Screenshot of the sign-in box with the primary - Next - button highlighted.](media/reference-company-branding-css-template/primary-button.png)
- Styles for secondary buttons:

    - `.ext-button.ext-secondary` - Secondary buttons
    - `.ext-button.ext-secondary:hover` - When the mouse is over the button
    - `.ext-button.ext-secondary:focus` - When the button has focus
    - `.ext-button.ext-secondary:focus:hover` - When the button has focus *and* the mouse is over the button
    - `.ext-button.ext-secondary:active` - When the button is being clicked

    ![Screenshot of the sign-in box at the Sign-in options step, with the secondary - Back - button highlighted.](media/reference-company-branding-css-template/secondary-button.png)
- `.ext-error` - Error text

    ![Screenshot of the sign-in box with error text highlighted.](media/reference-company-branding-css-template/error-text.png)
- Styles for text boxes:

    - `.ext-input.ext-text-box` - Text boxes
    - `.ext-input.ext-text-box.ext-has-error` - When there's a validation error associated with the text box
    - `.ext-input.ext-text-box:hover` - When the mouse is over the text box
    - `.ext-input.ext-text-box:focus` - When the text box has focus
    - `.ext-input.ext-text-box:focus:hover` - When the text box has focus *and* the mouse is over the text box

    ![Screenshot of the sign-in box with the text box with sample text highlighted.](media/reference-company-branding-css-template/ext-text-box.png)
- `.ext-boilerplate-text` - Custom message text at the bottom of the sign-in box
- `.ext-promoted-fed-cred-box` - Sign-in options text box

    ![Screenshot of the sign-in box with the optional boilerplate text area highlighted.](media/reference-company-branding-css-template/boilerplate-fed-cred.png)
- Styles for the footer:

    - `.ext-footer` - Footer area at the bottom of the page
    - `.ext-footer-links` - Links area in the footer at the bottom of the page
    - `.ext-footer-item` - Link items (such as "Terms of use" or "Privacy & cookies") in the footer at the bottom of the page
    - `.ext-debug-item` - Debug details ellipsis in the footer at the bottom of the page