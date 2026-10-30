---
layout: Conceptual
title: Customize the sign-in experience for your application with branding themes - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/how-to-customize-branding-themes-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn how to create branding themes and apply them to the sign-in experience for your application in Microsoft Entra ID.
ms.date: 2026-08-18T00:00:00.0000000Z
ms.reviewer: 
ms.topic: how-to
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 00de8e12-082f-ab38-0c5a-ce5b6df78cd4
document_version_independent_id: 00de8e12-082f-ab38-0c5a-ce5b6df78cd4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/how-to-customize-branding-themes-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/how-to-customize-branding-themes-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/how-to-customize-branding-themes-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ee6f6e73-3693-63c8-3acf-2eb8bae5072e
---

# Customize the sign-in experience for your application with branding themes - Microsoft Entra | Microsoft Learn

You can create unique authentication experiences for applications in your tenant. Each application can have its own theme that you can customize with a background image or color, favicon, layout, header, and footer. This customization overrides any configurations made to the default branding. If you don't make any changes to the elements, the default elements are displayed.

This article describes how you can create multiple branding themes for different applications in your tenant.

Important

For external tenants, branding themes is generally available. For Microsoft Entra ID tenants, branding themes is in PREVIEW. This information relates to a prerelease product that may be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

- For external tenants, there isn't a license requirement. For Microsoft Entra ID tenants, you must have an [Microsoft Entra ID P1 or P2 license](https://www.microsoft.com/security/business/microsoft-entra-pricing).
- Have at least the [Organizational Branding Administrator](../identity/role-based-access-control/permissions-reference#organizational-branding-administrator) role.
- Have at least the [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator) role for applications that you want to apply a theme to.
- A registered application in your tenant. If you haven't registered an application yet, see [Register an application](../identity-platform/quickstart-register-app).
- Review the file size requirements for each image you want to add. Use a photo editor if needed to create correctly sized and formatted images: PNG, JPG, or JPEG with image size 245x36px and maximum file size 10KB.

## Branding theme properties

When you create a branding theme, here are some of the properties you can customize.

[![Screenshot of the sign-in page, with each of the default branding elements highlighted.](media/how-to-customize-branding-themes-apps/sign-in-page-map.png)](media/how-to-customize-branding-themes-apps/sign-in-page-map.png#lightbox)

| Property | Description |
| --- | --- |
| Favicon | Small icon that appears on the left side of the browser tab. |
| Header | Space across the top of the sign-in page, behind the header log. |
| Header logo | Logo that appears in the upper-left corner of the sign-in page. |
| Background image | The entire space behind the sign-in box. |
| Page background color | The entire space behind the sign-in box. |
| Banner logo | Logo that appears at the top of the sign-in box |
| Sign-in page title | Larger text that appears below the banner logo. |
| Sign-in page description | Text to describe the sign-in page. |
| Username hint and text | The text that appears before a user enters their information. |
| Sign-in display message box | Text you can add below the username field. |
| Footer link: Privacy & Cookies | Link you can add to the lower-right corner for privacy information. |
| Footer: Terms of Use | Text in the lower-right corner of the page where you can add Terms of use information. |
| Footer | Space across the bottom of the page for privacy and Terms of Use information. |
| Template | The layout of the page and sign-in boxes. |

## How branding themes work

Branding themes build on neutral branding and default branding.

- **Branding theme** - Customizations of the default branding where you can have multiple themes.
- **Default branding (company branding)** - Customizations of the neutral branding for a tenant.
- **Neutral branding** - Initial branding for a tenant.

Here are some important things to know about how branding themes work.

- Branding themes can be applied to specific applications, while default branding applies tenant-wide.
- Default branding is used as fallback for any properties not defined in the branding theme.
- Neutral branding is used for any properties not defined in default branding.

## Limits and constraints

Here are some of the limits and constraints for branding themes.

- You can create up to 5 branding themes per tenant.
- The live preview capability previews style and layout changes and only shows the Sign in page. Live preview doesn't include any custom text overrides.
- You can't use the name **Default theme** for your branding theme name. This name is reserved.
- Custom text changes are currently limited to sign-in page only.
- If you don't update the banner logo property, the Microsoft logo is displayed instead of the tenant name (neutral branding).

## Create a new theme

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as [Organizational Branding Administrator](../identity/role-based-access-control/permissions-reference#organizational-branding-administrator) and [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Custom branding**.
3. On the **Company branding** page, select **Branding themes** and then select the **Themes** tab.

    [![Screenshot of the Company Branding page and the Themes tab.](media/how-to-customize-branding-themes-apps/create-new-theme.png)](media/how-to-customize-branding-themes-apps/create-new-theme.png#lightbox)
4. Select **Create new theme**.
5. On the **Basics** tab, enter a **Name** for your theme.

    [![Screenshot of the Create a theme page and the Basics tab to apply themes to applications.](media/how-to-customize-branding-themes-apps/add-application-to-theme.png)](media/how-to-customize-branding-themes-apps/add-application-to-theme.png#lightbox)
6. To select the applications that will use this theme, under **Apply theme to**, select **Add applications**. (Or you can add applications later.)
7. On the **Layout** tab, select the placement of web page elements on the sign-in page.

    - **Layout template** – Choose whether the sign-in pane is center-aligned on the page or right-aligned.
    - **Header** – To show an image in a page header, select the checkbox and browse for the image you want to display. Requirements: Transparent PNG, JPG, or JPEG with image size 245x36px and maximum file size 10KB.
    - **Footer** – To show a page footer that includes links to your published privacy and cookies and/or terms of use statements, select the appropriate checkbox, enter the link text, and add the URL for your content.

    [![Screenshot of the Create a theme page and the Layout tab to specify the sign-in experience.](media/how-to-customize-branding-themes-apps/layout-tab.png)](media/how-to-customize-branding-themes-apps/layout-tab.png#lightbox)
8. Select the **Preview** button to see your changes to the layout.

    [![Screenshot of the Preview button to preview a layout.](media/how-to-customize-branding-themes-apps/preview-button.png)](media/how-to-customize-branding-themes-apps/preview-button.png#lightbox)
9. On the **Styling** tab, modify any of the background elements.

    - **Background color** – The color that replaces the background image whenever the image can't be loaded, for example due to connection latency.
    - **Background image** – The large image that displays on the sign-in page. If you upload an image, it scales and crops to fill the browser window.
    - **Favicon** – The icon that displays in the web browser tab.
    - **Banner logo** – Displays on the sign-in page and in the user's access panel.
    - **Square logo (light theme)** – Represents user accounts in your tenant.
    - **Square logo (dark theme)** – If the light theme square logo displays poorly on dark backgrounds, you can upload a logo to be used in its place when dark backgrounds are used.
    - **Custom CSS** – Upload your own CSS file to replace default Microsoft styling with your own styling for: color, font, text size, position of elements, and displays for different devices and screen sizes. For more information, see [CSS template reference guide](reference-company-branding-css-template).

        Important

        To align with the [Microsoft Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative) and its focus on identity security and phishing resistance, Microsoft Entra ID is retiring support for custom CSS *layout and positioning properties* in company branding. After July 21, 2026, tenants created before January 6, 2026, that don't already use custom CSS can't configure custom CSS. Later, the properties will be deprecated globally and stop functioning. Eventually, custom CSS will be retired entirely. For the full list of deprecated properties and steps to update your CSS, see [CSS template reference guide](reference-company-branding-css-template#deprecation-of-custom-css-positioning-properties). For more information, see the blog post [Microsoft Entra ID enhances security of branded sign-ins](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/microsoft-entra-id-enhances-security-of-branded-sign-ins/4537471).

    [![Screenshot of the Create a theme page and the Styling tab settings.](media/how-to-customize-branding-themes-apps/styling-tab.png)](media/how-to-customize-branding-themes-apps/styling-tab.png#lightbox)
10. Select the **Preview** button to see your styling changes.

    [![Screenshot of the customized Sign in experience.](media/how-to-customize-branding-themes-apps/sign-in.png)](media/how-to-customize-branding-themes-apps/sign-in.png#lightbox)
11. On the **Custom text** tab, select the **Default** link for one of the pages, such as the **Sign-in** page.

    - **Sign-in** – The page where users enter their credentials to sign in.
    - **Sign-up** – The page where users create a new account.
    - **Attribute collection** – The page where users provide additional information during sign-up or profile editing.
    - **One-time code** – The page where users enter a one-time code sent to their email or phone for verification.

    [![Screenshot of the Create a theme page and the Custom text tab settings.](media/how-to-customize-branding-themes-apps/custom-text-tab.png)](media/how-to-customize-branding-themes-apps/custom-text-tab.png#lightbox)
12. Customize the text for the selected page and then select **Add**.

    Custom text set for a theme might impact localized UX as they will not be localized. To ensure full localization of all text, set custom text for each theme language.

    [![Screenshot of the Edit custom text page for the Sign-in page.](media/how-to-customize-branding-themes-apps/custom-text-edit.png)](media/how-to-customize-branding-themes-apps/custom-text-edit.png#lightbox)

    On the **Sign-in** page, you can customize the **Display message box** text. This text appears at the bottom of the Microsoft Entra ID sign-in page and in the Microsoft Entra ID Join experience on Windows. Use this text to convey instructions or tips. Anyone can see your sign-in page, so don't put sensitive info here. It has a maximum of 1024 characters. Use the following syntax to format text including bold, italics, underline, or clickable link:

    - Bold: `**text**` or `__text__`
    - Italics: `*text*` or `_text_`
    - Underline: `++text++`
    - Hyperlink: `[text](link)`
13. On the **Review** tab, review your settings.
14. Select **Create** to create the theme.

## Apply a theme to applications

In this section, you apply a theme to applications in your tenant.

1. On the **Branding Themes** page, select the **Themes** tab.
2. Select a theme you created to open the overview.
3. Under **Basics**, select the pencil edit icon.

    [![Screenshot of the Overview tab of the edit theme page.](media/how-to-customize-branding-themes-apps/edit-theme-overview.png)](media/how-to-customize-branding-themes-apps/edit-theme-overview.png#lightbox)
4. Under **Apply theme to**, select **Edit** to edit the list of applications.

    [![Screenshot of the Edit Basics page to edit the list of applications.](media/how-to-customize-branding-themes-apps/edit-basics.png)](media/how-to-customize-branding-themes-apps/edit-basics.png#lightbox)
5. Search for or browse to your application. Select the check box, and then choose **Select**.

    [![Screenshot of the Add applications page to select applications.](media/how-to-customize-branding-themes-apps/select-application.png)](media/how-to-customize-branding-themes-apps/select-application.png#lightbox)

## Edit a theme

In this section, you edit a theme.

1. On the **Branding Themes** page, select the **Themes** tab.
2. Select a theme you created to open the overview.
3. Select the pencil edit icon of the parts you want to edit.

## Add a language to a theme

In this section, you add a language to a theme.

1. On the **Branding Themes** page, select the **Themes** tab.
2. Select a theme you created to open the overview.
3. On the **Languages** tab, select **Add a language** to customize the language of the theme.

    The steps for customizing the language are similar to customizing branding theme.

    [![Screenshot of the Languages tab to add a language.](media/how-to-customize-branding-themes-apps/languages-tab.png)](media/how-to-customize-branding-themes-apps/languages-tab.png#lightbox)
4. On the **Basics** tab, select a language.

    [![Screenshot of the Add a language page and Basics tab to select a language.](media/how-to-customize-branding-themes-apps/language-basics-tab.png)](media/how-to-customize-branding-themes-apps/language-basics-tab.png#lightbox)

    The following languages are supported:

    - Arabic (Saudi Arabia)
    - Basque (Basque)
    - Bulgarian (Bulgaria)
    - Catalan (Catalan)
    - Chinese (China)
    - Chinese (Hong Kong SAR)
    - Croatian (Croatia)
    - Czech (Czechia)
    - Danish (Denmark)
    - Dutch (Netherlands)
    - English (United States)
    - Estonian (Estonia)
    - Finnish (Finland)
    - French (France)
    - Galician (Galician)
    - German (Germany)
    - Greek (Greece)
    - Hebrew (Israel)
    - Hungarian (Hungary)
    - Italian (Italy)
    - Japanese (Japan)
    - Kazakh (Kazakhstan)
    - Korean (Korea)
    - Latvian (Latvia)
    - Lithuanian (Lithuania)
    - Norwegian Bokmål (Norway)
    - Polish (Poland)
    - Portuguese (Brazil)
    - Portuguese (Portugal)
    - Romanian (Romania)
    - Russian (Russia)
    - Serbian (Latin, Serbia)
    - Slovak (Slovakia)
    - Slovenian (Slovenia)
    - Spanish (Spain)
    - Swedish (Sweden)
    - Thai (Thailand)
    - Turkish (Türkiye)
    - Ukrainian (Ukraine)
5. Customize the elements on the **Layout**, **Styling**, and **Custom text** tabs.
6. On the **Review** tab, select **Add** to add the language.