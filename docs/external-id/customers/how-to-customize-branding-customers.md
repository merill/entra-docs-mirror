---
layout: Conceptual
title: Customize Hosted Page Branding - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-customize-branding-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Customize Microsoft-hosted authentication pages in Microsoft Entra External ID with company logos, background images, colors, and sign-in text.
ms.topic: how-to
ms.date: 2026-11-13T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange, msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: c092d2aa-a71a-443c-9635-ea66b05fed3f
document_version_independent_id: 39a22444-d600-57a5-5ffa-a91c052da320
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-customize-branding-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-customize-branding-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-customize-branding-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 98738a55-756d-9763-41ff-357068487810
---

# Customize Hosted Page Branding - Microsoft Entra External ID | Microsoft Learn

After creating an external tenant, configure **Company branding** to customize its Microsoft-hosted authentication pages. Add background images, colors, company logos, and text to create a consistent sign-in experience across your apps. You can also manage company branding programmatically with Microsoft Graph. Before you begin, ensure you have an external tenant, a registered application, and a user flow, as described in Prerequisites.

**Applies to external tenants:** Feature support varies by authentication approach and API or SDK version. Compare Microsoft-hosted authentication, Embedded native authentication, and Bring Your Own UX (BYO UX) in the [authentication approach overview](concept-choose-authentication-approach). Check feature availability in the [authentication support matrix](concept-supported-features-customers#authentication-approach-supportability).

## Prerequisites

- If you haven't already created your own Microsoft Entra external tenant, create one now.
- [Register an application](/en-us/entra/identity-platform/quickstart-register-app).
- [Create a user flow](how-to-user-flow-sign-up-sign-in-customers).
- Review the file size requirements for each image you want to add. You might need a photo editor to resize images. PNG is preferred, but JPG is accepted.

## Review preview customization options

For guidance on the modern Fluent experience, Basic and Advanced styling, and custom HTML, see the [modern UX and customization overview](../customization-overview). Those preview capabilities use application branding themes, not the default-branding procedure below.

These capabilities are scheduled to become available in preview on December 7, 2026, for external tenants with the preview enabled. Continue using the default-branding instructions below to customize that experience.

## Branding elements

Your tenant starts with neutral branding that doesn't include preexisting Microsoft branding. Customize individual branding properties to suit your company. If custom company branding fails to load, the sign-in page reverts to neutral branding.

You can customize this neutral branding with a custom background image or color, favicon, layout, header, and footer. You can also customize the sign-in form and add custom text to different instances or upload [custom CSS](../../fundamentals/reference-company-branding-css-template). The following image displays the neutral default branding of the tenant. You can find the numbered branding elements and their corresponding descriptions after the image.

[![Screenshot of a neutral sign-in page with numbered branding elements.](media/how-to-customize-branding-customers/ciam-neutral-branding.png)](media/how-to-customize-branding-customers/ciam-neutral-branding.png#lightbox)

1. Neutral background.
2. Favicon.
3. Banner logo.
4. Footer as a page layout element.
5. Footer hyperlinks, such as **Privacy & cookies** and **Terms of use**.

## How to customize the default sign-in experience

To customize the default sign-in, sign-up, and sign-out pages, edit the company branding settings. You can also upload [custom CSS](../../fundamentals/reference-company-branding-css-template).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Organizational Branding Administrator](../../identity/role-based-access-control/permissions-reference#organizational-branding-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the external tenant you created earlier from the **Directories + subscriptions** menu.
3. Browse to **Company branding** either by using the search bar or by navigating to **Entra ID** &gt; **Custom Branding**.
4. On the **Default sign-in** tab, select **Edit**.

    ![Screenshot of the company branding edit button.](media/how-to-customize-branding-customers/company-branding-default-edit-button.png)

### To customize the sign-in page background and layout

Configure the background and layout to control how Microsoft-hosted pages display your branding:

1. On the **Basics** tab, modify any of the background elements.

    - **Favicon** – The icon that displays in the web browser tab.
    - **Background image** – The large image that displays on the sign-in page. If you upload an image, it scales and crops to fill the browser window.
    - **Page background color** – The color that replaces the background image whenever the image can’t be loaded, for example due to connection latency.

    [![Screenshot of the company branding basics tab.](media/how-to-customize-branding-customers/company-branding-basics-tab.png)](media/how-to-customize-branding-customers/company-branding-basics-tab.png#lightbox)
2. Select **Next: Layout** to continue customizing or **Review + save** to save your changes.
3. On the **Layout** tab, select the placement of web page elements on the sign-in page.

    - **Template** – Choose whether the background displays full-screen or partial-screen.
    - **Header** – Show or hide the header.
    - **Footer** – Show or hide the footer.
    - **Custom CSS** – Upload a CSS file to customize colors, fonts, text size, element positions, and display across devices and screen sizes.

    [![Screenshot of the company branding layout tab.](media/how-to-customize-branding-customers/company-branding-layout-tab.png)](media/how-to-customize-branding-customers/company-branding-layout-tab.png#lightbox)
4. Select **Next: Header** to continue customizing or **Review + save** to save your changes.

### To customize the logo, privacy link, and terms of use

Configure the header and footer to display your logo and policy links:

1. On the **Header** tab, select the logo to display in the header of the sign-in page.

    ![Screenshot of the company branding header tab.](media/how-to-customize-branding-customers/company-branding-header-tab.png)
2. Select **Next: Footer** to continue customizing or **Review + save** to save your changes.
3. On the **Footer** tab, you can customize the URLs and link text for the privacy and terms of use hyperlinks that appear in the footer of the sign-in page.

    - **Privacy & Cookies** – Select the checkbox next to Privacy & Cookies to display this hyperlink in the footer. The Microsoft default privacy link displays unless you enter your own hyperlink Display text and URL.
    - **Terms of Use** – Select the checkbox next to Terms of Use to display this hyperlink in the footer. The Microsoft terms of use link displays unless you enter your own hyperlink Display text and URL.

    [![Screenshot of the company branding footer tab.](media/how-to-customize-branding-customers/company-branding-footer-tab.png)](media/how-to-customize-branding-customers/company-branding-footer-tab.png#lightbox)
4. Select **Next: Sign-in form** to continue customizing or **Review + save** to save your changes.

### To customize the sign-in form

Configure logos, hint text, and page text for the sign-in form:

1. On the **Sign-in form** tab, configure elements of the sign-in form:

    - **Banner logo** – Displays on the sign-in page and in the user’s access panel.
    - **Square logo (light theme)** – Represents user accounts in your organization.
    - **Square logo (dark theme)** – Upload an alternative to the light theme square logo for use on dark backgrounds.

    [![Screenshot of the company branding sign-in form tab.](media/how-to-customize-branding-customers/company-branding-sign-in-form-tab.png)](media/how-to-customize-branding-customers/company-branding-sign-in-form-tab.png#lightbox)
2. Scroll to the lower half of the page and configure more elements of the sign-in form:

    - **Username hint text** – The hint text that displays in the username input field on the sign-in page (not recommended if guest users sign in to your app).
    - **Sign-in page text** – Appears at the bottom of the sign-in and sign-up pages. Guidelines:

        - Use a maximum of 1,024 characters.
        - Don't include sensitive information.
        - Use this syntax to format text:
            - Hyperlink: `[text](link)`
            - Bold: `**text** or __text__`
            - Italics: `*text* or _text_`
            - Underline: `++text++`

### To customize self-service password reset

Configure the password reset link on Microsoft-hosted sign-in pages:

1. Scroll to the **Self-service password reset** section to configure options for showing, hiding, or customizing the self-service password reset link on the sign-in page.

    - **Show self-service password reset** – Select this checkbox to display the self-service password link.
    - **Common URL** – Enter a password reset URL to use in place of the default Microsoft link.
    - **Account collection display text** – Enter link text to replace the Microsoft default "Can’t access your account" text.
    - **Password collection display text** – Enter link text to replace the Microsoft default "Forgot password" text.

        [![Screenshot of the company branding Self-service password reset. ](media/how-to-customize-branding-customers/company-branding-self-service-password-reset.png)](media/how-to-customize-branding-customers/company-branding-self-service-password-reset.png#lightbox)
2. Select **Next: Text** to continue customizing or **Review + save** to save your changes.

### To customize user attributes

Customize labels for attributes such as Given Name, Surname, City, and Postal Code, and other sign-up and sign-in text. Use Microsoft Graph or the **Text** tab in **Company Branding** to customize this text:

1. On the **Text** tab, select **Add Custom Text**.
2. Select any of the options:

    - Select **Attributes** to override the default values.
    - Select **Attribute collection** to add a new attribute option to collect during sign-up.
    - Select **Sign in** to add custom text for the sign-in page.
    - Select **Sign up** to add custom text for the sign-up page.
    - Select **Sign-in/up one time code (SISU OTC)** to add a custom title.

        [![Screenshot of the company branding text tab.](media/how-to-customize-branding-customers/custom-text.png)](media/how-to-customize-branding-customers/custom-text.png#lightbox)
3. Select **Next: Review** to review all your modifications. Then select **Save** if you'd like to save your changes or **Previous** if you want to continue customizing.

Important

Customize sign-up and sign-in strings through language customization in **User flows** or through **Company branding**. Both options modify the same JSON file, so the most recent change overrides the previous one.

## Customize the sign-out experience

The sign-out experience automatically matches your sign-in branding. If you haven't customized sign-in branding, sign-out pages use the tenant's default neutral branding.

## How to customize the tenant name

You can customize your tenant name in the Microsoft Entra admin center to replace the Microsoft banner logo in the neutral default sign-in experience. The new tenant name also appears in the verification email sent to the user.

[![Screenshot of the tenant name.](media/how-to-customize-branding-customers/tenant-name.png)](media/how-to-customize-branding-customers/tenant-name.png#lightbox)

To change the tenant name, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as at least an [Organizational Branding Administrator](../../identity/role-based-access-control/permissions-reference#organizational-branding-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the external tenant you created earlier from the **Directories + subscriptions** menu.
3. In the search bar, type and select **Tenant properties**.
4. Edit the **Name** field.

    ![Screenshot of editing the tenant name.](media/how-to-customize-branding-customers/tenant-name-edit.png)
5. Select **Save**.

## Customize your branding with the Microsoft Graph API

You can use the Microsoft Graph API to customize a few items programmatically. For example, you can use the API to upload a custom background image, change the color of the sign-in page, and add a custom logo. For more information, see the [update default branding](/en-us/graph/api/organizationalbranding-update) article.