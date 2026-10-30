---
layout: Conceptual
title: Add company branding to your organization's sign-in page - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/how-to-customize-branding
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: pmwongera
description: Instructions about how to add your organization's custom branding to the Microsoft Entra sign-in experience.
ms.topic: how-to
ms.date: 2026-08-18T00:00:00.0000000Z
ms.reviewer: mkokkalera
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 72f2e675-436d-dcd4-fa27-49408b201158
document_version_independent_id: 4d821732-fc10-f4a6-3c7d-77bce75299d7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/how-to-customize-branding.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/how-to-customize-branding
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/how-to-customize-branding.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b00caaf5-5e0e-1599-a278-d6234c94ecf3
---

# Add company branding to your organization's sign-in page - Microsoft Entra | Microsoft Learn

When users authenticate into your corporate intranet or web-based applications, Microsoft Entra ID provides the identity and access management (IAM) service. You can add company branding that applies to all these experiences to create a consistent sign-in experience for your users.

The default sign-in experience is the global look and feel that applies across all sign-ins to your tenant. Before you customize any settings, the default Microsoft branding appears in your sign-in pages. You can customize this default experience with a custom background image or color, favicon, layout, header, and footer. You can also upload a custom CSS file.

## Prerequisites

Adding custom branding requires one of the following licenses:

- [Microsoft Entra ID P1 or P2](https://www.microsoft.com/security/business/microsoft-entra-pricing)
- [Microsoft 365 Business Standard](https://www.microsoft.com/microsoft-365/business)
- [SharePoint (Plan 1)](https://www.microsoft.com/microsoft-365/sharepoint/compare-sharepoint-plans)

Microsoft Entra ID P1 or P2 editions are available for customers in China using the worldwide instance of Microsoft Entra ID. Microsoft Entra ID P1 or P2 editions aren't currently supported in the Azure service operated by 21Vianet in China.

The **Organizational Branding Administrator** role is the minimum role required to customize company branding.

## Before you begin

**All branding elements are optional. Default settings will remain, if left unchanged.** For example, if you specify a banner logo but no background image, the sign-in page shows your logo with a default background image from the destination site such as Microsoft 365. Additionally, sign-in page branding doesn't carry over to personal Microsoft accounts. If your users or guests authenticate using a personal Microsoft account, the sign-in page doesn't reflect the branding of your organization.

**Images have different image and file size requirements.** We recommend you review the company branding process in the Microsoft Entra admin center to gather the image requirements you need. You might need to use a photo editor to create the right size images. The preferred image type for all images is PNG, but JPG is accepted.

**External URLs aren't supported in the sign-in experience.** For example, if you add an external URL for your internal help desk to the footer, that URL is displayed explicitly but isn't clickable. Users must copy the URL and navigate to it directly.

**The Azure Active Directory B2C (Azure AD B2C) company branding options are different.** Azure AD B2C branding is currently limited to background image, banner logo, and background color customization. For more information, see [Customize the UI](/en-us/azure/active-directory-b2c/customize-ui?pivots=b2c-user-flow#configure-company-branding) in the Azure AD B2C documentation.

Important

Effective May 1, 2025, Azure Active Directory B2C (Azure AD B2C) is no longer available for new customers to purchase. To learn more, see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

**Use Microsoft Graph with Microsoft Entra company branding.** Company branding can be viewed and managed using Microsoft Graph on the `/beta` endpoint and the `organizationalBranding` resource type. For more information, see the [organizational branding API documentation](/en-us/graph/api/resources/organizationalbranding?view=graph-rest-beta&amp;preserve-view=true).

The branding elements are called out in the following example. Text descriptions are provided following the image.

[![Screenshot of the sign-in page, with each of the company branding elements highlighted.](media/how-to-customize-branding/sign-in-page-map.png)](media/how-to-customize-branding/sign-in-page-map-expanded.png#lightbox)

1. **Favicon**: Small icon that appears on the left side of the browser tab.
2. **Header**: Space across the top of the sign-in page, behind the header logo.
3. **Header logo**: Logo that appears in the upper-left corner of the sign-in page.
4. **Background image**: The entire space behind the sign-in box.
5. **Page background color**: The entire space behind the sign-in box.
6. **Banner logo**: Logo that appears at the top of the sign-in box
7. **Sign-in page title**: Larger text that appears below the banner logo.
8. **Sign-in page description**: Text to describe the sign-in page.
9. **Username hint and text**: The text that appears before a user enters their information.
10. **Self-service password reset**: A link you can add below the sign-in page text for password resets.
11. **Sign-in page text**: Text you can add below the username field.
12. **Footer link: Privacy & Cookies**: Link you can add to the lower-right corner for privacy information.
13. **Footer: Terms of Use**: Text in the lower-right corner of the page where you can add Terms of use information.
14. **Footer**: Space across the bottom of the page for privacy and Terms of Use information.
15. **Template**: The layout of the page and sign-in boxes.

## How to navigate the company branding process

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Organizational Branding Administrator](../identity/role-based-access-control/permissions-reference#organizational-branding-administrator).
2. Browse to **Entra ID** &gt; **Custom Branding**.

    - If you currently have a customized sign-in experience, the **Edit** button is available.

    [![Screenshot of Custom branding landing page with Company branding highlighted in the side menu and Configure button.](media/how-to-customize-branding/customize-branding-getting-started.png)](media/how-to-customize-branding/customize-branding-getting-started.png#lightbox)

The sign-in experience process is grouped into sections. At the end of each section, select the **Review + create** button to review what you selected and submit your changes or the **Next** button to move to the next section.

![Screenshot of Review + create and Next: Layout buttons from the bottom of the configure custom branding page.](media/how-to-customize-branding/customize-branding-buttons.png)

### Basics

- **Favicon**: Select a PNG or JPG of your logo that appears in the web browser tab.

    - Image size: 32x32 px
    - Max file size: 5 KB

    ![Screenshot of sample favicons in a web browser.](media/how-to-customize-branding/favicon-example.png)
- **Background image**: Select a PNG or JPG to display as the main image on your sign-in page. This image scales and crops according to the window size, but the sign-in prompt might partially block it.

    - Image size: 1920x1080 px
    - Max file size: 300 KB
- **Page background color**: If the background image isn't able to load because of a slower connection, your selected background color appears instead.

### Layout

- **Visual Templates**: Customize the layout of your sign-in page using templates or a custom CSS file.

    - Choose one of two **Templates**: Full-screen or partial-screen background. The full-screen background could obscure your background image, so choose the partial-screen background if your background image is important.
    - The details of the **Header** and **Footer** options are set on the next two sections of the process.

    ![Screenshot of the Layout tab for customizing branding.](media/how-to-customize-branding/layout-visual-templates.png)
- **Custom CSS**: Upload a custom CSS file to replace the Microsoft default style of the page.

    - [Download the CSS template](https://download.microsoft.com/download/7/2/7/727f287a-125d-4368-a673-a785907ac5ab/custom-styles-template-013023.css).
    - View the [CSS template reference guide](reference-company-branding-css-template).

    Important

    Tenants created after January 5, 2026, don't have custom CSS available for company branding in Microsoft Entra ID. After July 21, 2026, tenants created before January 6, 2026, that don't already use custom CSS can't configure custom CSS.

    To align with the [Microsoft Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative) and its focus on identity security and phishing resistance, Microsoft Entra ID is retiring support for custom CSS *layout and positioning properties* (such as `position`, `margin`, `transform`, and `overflow`). Later, the properties will be deprecated globally and stop functioning. Eventually, custom CSS will be retired entirely. If your custom CSS uses these properties, remove them from your configuration. For the full list of deprecated properties and steps to update your CSS, see [CSS template reference guide](reference-company-branding-css-template#deprecation-of-custom-css-positioning-properties). For more information, see the blog post [Microsoft Entra ID enhances security of branded sign-ins](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/microsoft-entra-id-enhances-security-of-branded-sign-ins/4537471).

### Header

If you haven't enabled the header, go to the **Layout** section and select **Show header**. Once enabled, select a PNG or JPG to display in the header of the sign-in page.

- Image size: 245x36 px
- Max file size: 10 KB

![Screenshot of the message indicating that the header needs to be enabled.](media/how-to-customize-branding/disabled-header-message.png)

### Footer

If you haven't enabled the footer, go to the **Layout** section and select **Show footer**. Once enabled, adjust the following settings.

- **Show 'Privacy & Cookies'**: This option is selected by default and displays the [Microsoft 'Privacy & Cookies'](https://privacy.microsoft.com/privacystatement) link.

    - Uncheck this option to hide the default Microsoft link.
    - Optionally provide your own **Display text** and **URL**. The text and links don't have to be related to privacy and cookies.
    - Custom URLs are displayed as text and aren't clickable.
- **Show 'Terms of Use'**: This option is also selected by default and displays the [Microsoft 'Terms of Use'](https://www.microsoft.com/servicesagreement/) link.

    - Uncheck this option to hide the default Microsoft link. Optionally provide your own **Display text** and **URL**.
    - The text and links don't have to be related to your terms of use.

        Important

        The default Microsoft 'Terms of Use' link isn't the same as the Conditional Access Terms of Use. Seeing the terms here doesn't mean you accepted those terms and conditions.

    ![Screenshot of customizing branding on the Footer section.](media/how-to-customize-branding/customize-branding-footer.png)

### Sign-in form

- **Banner logo**: Select a PNG or JPG image file of a banner-sized logo (short and wide) to appear on the sign-in pages.

    - Image size: 245x36 px
    - Max file size: 50 KB
- **Square logo (light theme)**: Select a square PNG or JPG image file of your logo to be used in browsers that are using a light color theme. This logo is used to represent your organization on the Microsoft Entra web interface and in Windows.

    - Image size: 240x240 px
    - Max file size: 50 KB
- **Square logo (dark theme)**: Select a square PNG or JPG image file of your logo to be used in browsers that are using a dark color theme. This logo is used to represent your organization on the Microsoft Entra web interface and in Windows. If your logo looks good on light and dark backgrounds, there's no need to add a dark theme logo.

    - Image size: 240x240 px
    - Max file size: 50 KB
- **Username hint text**: Enter hint text for the username input field on the sign-in page. If guests use the same sign-in page, we don't recommend using hint text here.
- **Sign-in page text**: Enter text that appears on the bottom of the sign-in page. You can use this text to communicate additional information, such as the phone number to your help desk or a legal statement. This page is public, so don't provide sensitive information here. This text must be Unicode and can't exceed 1,024 characters.

    To begin a new paragraph, press the Enter key twice. You can also change text formatting to include bold, italics, an underline, or clickable link. Use the following syntax to add formatting to text:

    - Hyperlink: `[text](link)`
    - Bold: `**text**` or `__text__`
    - Italics: `*text*` or `_text_`
    - Underline: `++text++`

    Important

    Hyperlinks that are added to the sign-in page text render as text in native environments, such as desktop and mobile applications.
- **Self-service password reset**:

    - Show self-service password reset (SSPR): Select the checkbox to turn on SSPR.
    - Common URL: Enter the destination URL for where your users reset their passwords. This URL appears on the username and password collection screens as text and isn't clickable.
    - Username collection display text: Replace the default text with your own custom username collection text.
    - Password collection display text: Replace the default text with your own custom password collection text.

### Review

All of the available options appear in one list so you can review everything you customized or left at the default setting. When you're done, select the **Create** button.

Once your default sign-in experience is created, select the **Edit** button to make any changes. You can't delete a default sign-in experience after it's created, but you can remove all custom settings.

The time it takes for changes to appear in the sign-in experience vary based on the tenant's geographical location.

## Customize the sign-in experience by browser language

You can create a personalized sign-in experience for users who sign in using a specific browser language by customizing the branding elements for that browser language. This customization overrides any configurations made to the default branding. If you don't make any changes to the elements, the default elements are displayed.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Organizational Branding Administrator](../identity/role-based-access-control/permissions-reference#organizational-branding-administrator).
2. Browse to **Entra ID** &gt; **Custom Branding**.
3. Select **Add browser language**.

The process for customizing the experience is the same as the default sign-in experience process, except you must select a language from the dropdown list in the **Basics** section. We recommend adding custom text in the same areas as your default sign-in experience.

Microsoft Entra ID supports right-to-left functionality for languages such as Arabic and Hebrew that are read right-to-left. The layout adjusts automatically, based on the user's browser settings.

![Screenshot of the sign-in experience in Hebrew, demonstrating the right-to-left layout.](media/how-to-customize-branding/right-to-left-language-example.png)

## User experience

There are some scenarios for you to consider when you customize the sign-in pages for your organization's tenant-specific applications.

### Default background image

The default background image behind the sign-in box is changing later this year. The change is only to the image, requires no action, and doesn't affect any functionality. We know that the default background image is often used for training and documentation to demonstrate the sign-in experience. Providing the updated image allows you to update your documentation so you can demonstrate the exact sign-in experience that your users will see. For details on the upcoming change, see [Microsoft Entra releases and announcements](whats-new).

[![Screenshot of the current background on the left and the new image on the right.](media/how-to-customize-branding/background-image-update.png)](media/how-to-customize-branding/background-image-update-expanded.png#lightbox)

The current background image is on the left and the new background image is on the right.

### Software as a Service (SaaS) and multitenant applications

For Microsoft, Software as a Service (SaaS), and multitenant applications such as https://myapps.microsoft.com, or https://outlook.com, the customized sign-in page appears only after the user types their **Email** or **Phone number** and selects the **Next** button.

### Home Realm Discovery

Some Microsoft applications support [Home Realm Discovery](../identity/enterprise-apps/home-realm-discovery-policy) for authentication. In these scenarios, when a customer signs in to a Microsoft Entra common sign-in page, Microsoft Entra ID can use the customer's user name to determine where they should sign in.

For customers who access applications from a custom URL, the `whr` query string parameter, or a domain variable, can be used to apply company branding at the initial sign-in screen, not just after adding the email or phone number. For example, `whr=contoso.com` would appear in the custom URL for the app. With the Home Realm Discover and domain parameter included, the company branding appears immediately in the first sign-in step. Other domain hints can be included.

In the following examples, replace the contoso.com with your own tenant name, or verified domain name:

- For Microsoft Outlook `https://outlook.com/contoso.com`
- For SharePoint in Microsoft 365 `https://contoso.sharepoint.com`
- For My Apps portal `https://myapps.microsoft.com/?whr=contoso.com`
- Self-service password reset `https://passwordreset.microsoftonline.com/?whr=contoso.com`

### B2B scenarios

For B2B collaboration end-users who perform cross-tenant sign-ins, their home tenant branding appears, even if there isn't custom branding specified.

In the following example, the company branding for Woodgrove Groceries appears on the left, with the Woodgrove logo, fonts, and custom text. The example on the right displays the default branding for the user's home tenant. The default branding displays the Microsoft logo, fonts, and text.

![Screenshot of comparison of the branded sign-in experience and the default sign-in experience.](media/how-to-customize-branding/b2b-comparison.png)