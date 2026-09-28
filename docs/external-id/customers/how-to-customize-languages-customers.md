---
layout: Conceptual
title: Customize the browser language - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-customize-languages-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about how to customize the browser language for your app's authentication experience to provide a personalized sign-in.
ms.topic: how-to
ms.date: 2026-04-24T00:00:00.0000000Z
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: 2bacf417-cb67-bbae-8bb3-18b229b11f25
document_version_independent_id: c41c44b8-795d-2332-43f3-32f8d49246df
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-customize-languages-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-customize-languages-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-customize-languages-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: bae80f04-b3bb-cd17-1c70-6c68bb0e3de1
---

# Customize the browser language - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Tip

This article applies to user flows in external tenants. For information about workforce tenants, see [Language customization in Microsoft Entra External ID](../user-flow-customize-language).

This article explains how to customize the browser language for your app's authentication experience. By personalizing the sign-in process based on browser language, you can deliver a tailored experience for your users and override default branding settings.

## Prerequisites

- If you haven't already created your own Microsoft Entra external tenant, create one now.
- [Register an application](/en-us/entra/identity-platform/quickstart-register-app).
- [Create a user flow](how-to-user-flow-sign-up-sign-in-customers).
- Review the file size requirements for each image you want to add. You might need to use a photo editor to create the right-sized images. The preferred image type for all images is PNG, but JPG is accepted.

## Add browser language under Company branding

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Organizational Branding Administrator](../../identity/role-based-access-control/permissions-reference#organizational-branding-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the external tenant you created earlier from the **Directories + subscriptions** menu.
3. Browse to **Company branding** &gt; **Browser language customizations** &gt; **Add browser language**.

    [![Screenshot of Company branding with Browser language customizations and the Add browser language action.](media/how-to-customize-languages-customers/company-branding-add-browser-language.png)](media/how-to-customize-languages-customers/company-branding-add-browser-language.png#lightbox)
4. On the **Basics** tab, under **Language specific UI Customization**, select the browser language you want to customize from the menu.

    [![Screenshot of the language selector on the Basics tab for browser language customization.](media/how-to-customize-languages-customers/language-selection.png)](media/how-to-customize-languages-customers/language-selection.png#lightbox)

The following languages are supported in the external tenant:

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

1. Customize the elements on the **Basics**, **Layout**, **Header**, **Footer**, **Sign-in form**, and **Text** tabs. For detailed instructions, see [Customize the branding and end-user experience](how-to-customize-branding-customers).
2. When you're finished, select the **Review** tab and go over all your language customizations. Then select **Add** to save your changes, or **Previous** to continue editing.

## Add language customization to a user flow

Language customization in the external tenant lets your user flow accommodate different languages to suit your customer's needs. You can use languages to modify the strings displayed to your customers as part of the attribute collection process during sign-up.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Organizational Branding Administrator](../../identity/role-based-access-control/permissions-reference#organizational-branding-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the external tenant you created earlier from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
4. Select the user flow that you want to enable for translations.
5. Select **Languages**.
6. On the **Languages** page for the user flow, select the language that you want to customize.
7. Expand **Sign up and sign in**.
8. Select **Download defaults** (or **Download overrides** if you have previously edited this language).

    [![Screenshot that shows how to add languages under a user flow.](media/how-to-customize-languages-customers/language-customization-flow.png)](media/how-to-customize-languages-customers/language-customization-flow.png#lightbox)

The downloaded file is in JSON format and includes both built-in and custom attributes, as well as other page-level and error strings:

```http
{"AttributeCollection_Description": "Wir benötigen nur ein paar weitere Informationen, um Ihr Konto einzurichten.","AttributeCollection_Title": "Details hinzufügen","Attribute_City": "Ort","Attribute_Country": "Land/Region","Attribute_DisplayName": "Anzeigename","Attribute_Email": "E-Mail-Adresse","Attribute_Generic_ConfirmationLabel": "{0} erneut eingeben","Attribute_GivenName": "Vorname","Attribute_JobTitle": "Position","Attribute_Password": "Kennwort","Attribute_Password_MismatchErrorString": "Kennwörter stimmen nicht überein.","Attribute_PostalCode": "Postleitzahl","Attribute_State": "Bundesland/Kanton","Attribute_StreetAddress": "Straße","Attribute_Surname": "Nachname","SignIn_Description": "Melden Sie sich an, um auf {0} zuzugreifen.","SignIn_Title": "Anmelden","SignUp_Description": "Registrieren Sie sich, um auf {0} zuzugreifen.","SignUp_Title": "Konto erstellen","SisuOtc_Title": "Code eingeben","Attribute_extension_a235ca9a0a7c4d33bd69e07bed81c8b1_Shoesize": "Shoe size"
}  
```

You can modify any or all of these attributes in the downloaded file. For example, you can modify the built-in attribute, **City** and the custom attribute, **Shoesize**:

```http
{"AttributeCollection_Description": "Wir benötigen nur ein paar weitere Informationen, um Ihr Konto einzurichten.","AttributeCollection_Title": "Details hinzufügen","Attribute_City": "Ort2","Attribute_Country": "Land/Region","Attribute_DisplayName": "Anzeigename","Attribute_Email": "E-Mail-Adresse","Attribute_Generic_ConfirmationLabel": "{0} erneut eingeben","Attribute_GivenName": "Vorname","Attribute_JobTitle": "Position","Attribute_Password": "Kennwort","Attribute_Password_MismatchErrorString": "Kennwörter stimmen nicht überein.","Attribute_PostalCode": "Postleitzahl","Attribute_State": "Bundesland/Kanton","Attribute_StreetAddress": "Straße","Attribute_Surname": "Nachname","SignIn_Description": "Melden Sie sich an, um auf {0} zuzugreifen.","SignIn_Title": "Anmelden","SignUp_Description": "Registrieren Sie sich, um auf {0} zuzugreifen.","SignUp_Title": "Konto erstellen","SisuOtc_Title": "Code eingeben","Attribute_extension_a235ca9a0a7c4d33bd69e07bed81c8b1_Shoesize": "Schuhgröße"
}  
```

1. After making the necessary changes, you can upload the new overrides file. The changes are saved to your user flow automatically. The override appears under the **Configured** tab.
2. To double-check your changes, select the language under the **Configured** tab and expand the **Sign up and sign in** option. You can view your customized language file by selecting **Download overrides**. To remove your customized override file, select **Remove overrides**.

[![Screenshot that shows how to remove or download the modified JSON file.](media/how-to-customize-languages-customers/remove-download-override-file.png)](media/how-to-customize-languages-customers/remove-download-override-file.png#lightbox)

1. Go to the sign-in page of your external tenant. Make sure you have the right locale and market in your URLs, for example: `ui_locales=de-DE` and `mkt=de-DE`. The updated attributes on the sign-up page appear as follows:

![Screenshot of the modified sign-up page attributes.](media/how-to-customize-languages-customers/customized-attributes.png)

Important

In the external tenant, we have two options to add custom text to the sign-up and sign-in experience. The function is available under each user flow during language customization and under [Company Branding](how-to-customize-branding-customers). Although we have two ways to customize strings (via Company branding and via User flows), both ways modify the same JSON file. The most recent change made either via User flows or via Company branding always overrides the previous one.

## Right-to-left language support

Languages that are read right-to-left, such as Arabic and Hebrew, are displayed in the opposite direction compared to languages that are read left-to-right. The external tenant supports right-to-left functionality and features for languages that work in a right-to-left environment for entering, and displaying data. Right-to-left readers can interact in a natural reading manner.

[![Screenshot showing the right-to-left language support.](media/how-to-customize-languages-customers/right-to-left-language-support.png)](media/how-to-customize-languages-customers/right-to-left-language-support.png#lightbox)

## Remove the browser language customization

When no longer needed, you can remove the language customization from your external tenant in the admin center or with the Microsoft Graph API.

### Remove the language customization in the admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Company branding** &gt; **Browser language customizations**
3. Select the language you want to delete and then select **Delete** and **OK**.

    [![Screenshot of the browser language customizations tab and the delete button.](media/how-to-customize-languages-customers/company-branding-delete-browser-language.png)](media/how-to-customize-languages-customers/company-branding-delete-browser-language.png#lightbox)

### Remove the language customization with the Microsoft Graph API

1. Sign in to the [MS Graph explorer](https://developer.microsoft.com/en-us/graph/graph-explorer) with your external tenant account: `https://developer.microsoft.com/en-us/graph/graph-explorer?tenant=<your-tenant-name.onmicrosoft.com>`.
2. Query the default branding object using the Microsoft Graph API: `https://graph.microsoft.com/v1.0/organization/<your-tenant-ID>/branding/localizations`. To confirm that you're signed in to your external tenant, verify the tenant name on the right side of the screen.
3. [Remove the localized branding object](/en-us/graph/api/organizationalbrandinglocalization-delete).

    [![Screenshot of MS Graph API with CIAM tenant logged in.](media/how-to-customize-branding-customers/msgraph-ciam-branding.png)](media/how-to-customize-branding-customers/msgraph-ciam-branding.png#lightbox)
4. Wait a few minutes for the changes to take effect.