---
layout: Conceptual
title: Language customization in Microsoft Entra user flows - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/user-flow-customize-language
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about customizing the language experience in your user flows in Microsoft Entra External ID.
ms.topic: how-to
ms.date: 2026-04-24T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
locale: en-us
document_id: 10f2db68-698d-91be-1c8b-a14cad2c3c09
document_version_independent_id: 06a184eb-f4bd-6d75-ae52-ba73b310f903
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/user-flow-customize-language.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/user-flow-customize-language
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/user-flow-customize-language.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: ae12ef69-8896-0d09-98e3-1a726c905cb4
---

# Language customization in Microsoft Entra user flows - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Tip

This article applies to B2B collaboration user flows in workforce tenants. For information about external tenants, see [Customize the language of the authentication experience](customers/how-to-customize-languages-customers).

Language customization in Microsoft Entra External ID allows your user flow to accommodate different languages to suit your users' needs. Microsoft provides translations for 36 languages. In this article, you learn how to customize attribute names on the [attribute collection page](self-service-sign-up-user-flow#select-the-layout-of-the-attribute-collection-form), even if your experience is provided in only a single language.

## How language customization works

By default, language customization is enabled for users signing up to ensure a consistent sign-up experience. You can use languages to modify the strings displayed to users as part of the attribute collection process during sign-up. If you're using [custom user attributes](user-flow-add-custom-attributes), you need to provide your own translations.

## Customize your strings

Language customization enables you to customize any string in your user flow.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [External ID User Flow Administrator](../identity/role-based-access-control/permissions-reference#external-id-user-flow-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
3. Select the user flow that you want to enable for translations.
4. Select **Languages**.
5. On the **Languages** page for the user flow, select the language that you want to customize.
6. Expand the **Attribute collection page**.
7. Select **Download defaults** (or **Download overrides** if you previously edited this language).

These steps give you a JSON file that you can use to start editing your strings.

[![Screenshot of a user flow language page showing the Download defaults option for the Attribute collection page.](media/user-flow-customize-language/language-customization-download-defaults.png)](media/user-flow-customize-language/language-customization-download-defaults.png#lightbox)

### Change any string on the page

1. Open the JSON file downloaded from previous instructions in a JSON editor.
2. Find the element that you want to change. You can find `StringId` for the string you're looking for, or look for the `Value` attribute that you want to change.
3. Update the `Value` attribute with what you want displayed.
4. For every string that you want to change, change `Override` to `true`. If the `Override` value isn't changed to `true`, the entry is ignored.
5. Save the file and upload your changes.

![Screenshot of the language customization workflow showing where to upload an override JSON file.](media/user-flow-customize-language/language-customization-upload-override.png)

### Change extension attributes

If you want to change the string for a custom user attribute, or you want to add one to the JSON, it's in the following format:

```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": true,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```

Replace `<ExtensionAttribute>` with the name of your custom user attribute.

Replace `<ExtensionAttributeValue>` with the new string to be displayed.

### Provide a list of values by using LocalizedCollections

If you want to provide a set list of values for responses, you need to create a `LocalizedCollections` attribute. `LocalizedCollections` is an array of `Name` and `Value` pairs. The items are displayed in the order listed. To add `LocalizedCollections`, use the following format:

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType",
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": true,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```

- `ElementId` is the user attribute that this `LocalizedCollections` attribute is a response to.
- `Name` is the value shown to the user.
- `Value` is what is returned in the claim when this option is selected.

### Upload your changes

1. After you complete the changes to your JSON file, go back to your tenant.
2. Select **User flows** and select the user flow that you want to enable for translations.
3. Select **Languages**.
4. Select the language that you want to translate to.
5. Select **Attribute collection page**.
6. Select the folder icon, and select the JSON file to upload.
7. The changes are saved to your user flow automatically. You can find the override under the **Configured** tab.
8. To remove or download your customized override file, select the language and expand the **Attribute collection page**.

![Screenshot of configured language overrides with options to download or remove the override JSON file.](media/user-flow-customize-language/language-customization-remove-download-overrides.png)

## Additional information

### Page UI customization labels as overrides

When you enable language customization, your previous edits for labels using page UI customization are persisted in a JSON file for English (en). You can continue to change your labels and other strings by uploading language resources in language customization.

### Up-to-date translations

Microsoft is committed to providing the most up-to-date translations for your use. Microsoft continuously improves translations and keeps them in compliance for you. Microsoft identifies bugs and global terminology changes, and makes updates that work seamlessly in your user flow.

### Support for right-to-left languages

Microsoft currently doesn't provide support for right-to-left languages, but you can use custom locales and CSS to change how strings are displayed. If you need this feature, vote for it on [Azure Feedback](https://feedback.azure.com/d365community/idea/10a7e89c-c325-ec11-b6e6-000d3a4f0789).

### Social identity provider translations

Microsoft provides the `ui_locales` OIDC parameter to social logins. But some social identity providers, including Facebook and Google, don't honor them.

### Browser behavior

Chrome and Firefox both request their set language. If the language is supported, it displays instead of the default. Microsoft Edge currently doesn't request a language and uses the default language.

## Supported languages

Microsoft Entra External ID includes support for the following languages. User flow languages are provided by Microsoft Entra External ID. The multifactor authentication notification languages are provided by [Microsoft Entra multifactor authentication](../identity/authentication/concept-mfa-howitworks).

| Language | Language code | User flows | MFA notifications |
| --- | --- | --- | --- |
| Arabic | ar | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Bulgarian | bg | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Bangla | bn | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![X indicating no.](media/user-flow-customize-language/no.png) |
| Catalan | ca | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Czech | cs | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Danish | da | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| German | de | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Greek | el | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| English | en | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Spanish | es | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Estonian | et | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Basque | eu | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Finnish | fi | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| French | fr | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Galician | gl | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Gujarati | gu | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![X indicating no.](media/user-flow-customize-language/no.png) |
| Hebrew | he | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Hindi | hi | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Croatian | hr | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Hungarian | hu | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Indonesian | id | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Italian | it | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Japanese | ja | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Kazakh | kk | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Kannada | kn | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![X indicating no.](media/user-flow-customize-language/no.png) |
| Korean | ko | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Lithuanian | lt | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Latvian | lv | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Malayalam | ml | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![X indicating no.](media/user-flow-customize-language/no.png) |
| Marathi | mr | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![X indicating no.](media/user-flow-customize-language/no.png) |
| Malay | ms | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Norwegian Bokmal | nb | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![X indicating no.](media/user-flow-customize-language/no.png) |
| Dutch | nl | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Norwegian | no | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Punjabi | pa | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![X indicating no.](media/user-flow-customize-language/no.png) |
| Polish | pl | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Portuguese - Brazil | pt-br | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Portuguese - Portugal | pt-pt | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Romanian | ro | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Russian | ru | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Slovak | sk | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Slovenian | sl | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Serbian - Cyrillic | sr-cryl-cs | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Serbian - Latin | sr-latn-cs | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Swedish | sv | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Tamil | ta | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![X indicating no.](media/user-flow-customize-language/no.png) |
| Telugu | te | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![X indicating no.](media/user-flow-customize-language/no.png) |
| Thai | th | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Turkish | tr | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Ukrainian | uk | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Vietnamese | vi | ![X indicating no.](media/user-flow-customize-language/no.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Chinese - Simplified | zh-hans | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |
| Chinese - Traditional | zh-hant | ![Green check mark.](media/user-flow-customize-language/yes.png) | ![Green check mark.](media/user-flow-customize-language/yes.png) |