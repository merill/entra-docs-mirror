---
layout: Conceptual
title: Troubleshoot SAML-based single sign-on - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/troubleshoot-saml-based-sso
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Troubleshoot issues with a Microsoft Entra app configured for SAML-based single sign-on.
ms.topic: troubleshooting
ms.date: 2023-09-07T00:00:00.0000000Z
ms.reviewer: alamaral
ms.custom: enterprise-apps
locale: en-us
document_id: 7bb246ca-4158-7508-0be1-4fac4507c461
document_version_independent_id: 628dc172-db91-fb8d-0d53-d5313b280116
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/troubleshoot-saml-based-sso.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/troubleshoot-saml-based-sso
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/troubleshoot-saml-based-sso.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7bfd52b4-67ed-2f7b-5421-a7f615676bb1
---

# Troubleshoot SAML-based single sign-on - Microsoft Entra ID | Microsoft Learn

If you encounter a problem when configuring an application, verify you followed all the steps in the tutorial for the application. In the application’s configuration, you have inline documentation on how to configure the application. Also, you can access the [List of tutorials on how to integrate SaaS apps with Microsoft Entra ID](../saas-apps/tutorial-list) for a detail step-by-step guidance.

## Can’t add another instance of the application

To add a second instance of an application, you need to be able to:

- Configure a unique identifier for the second instance. You aren't able to configure the same identifier used for the first instance.
- Configure a different certificate than the one used for the first instance.

If the application doesn’t support any of the listed options, you aren't able to configure a second instance.

## Can’t add the Identifier or the Reply URL

If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns preconfigured for the application.

To know the patterns preconfigured for the application:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator). Go to step 4 if you're already in the application configuration pane in Microsoft Entra ID.
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select the application you want to configure single sign-on.
4. Once the application loads, select the **Single sign-on** from the application’s left-hand navigation menu.
5. Select **SAML-based Sign-on** from the **Mode** dropdown.
6. Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**
7. There are three ways to know the supported patterns for the application.
    - In the textbox, you see the supported pattern as a placeholder, for example: `https://contoso.com`.
    - if the pattern isn't supported, you see a red exclamation mark when you try to enter the value in the textbox. If you hover your mouse over the red exclamation mark, you see the supported patterns.
    - In the tutorial for the application, you can also get information about the supported patterns. Under the **Configure Microsoft Entra single sign-on** section. Go to the step for configured the values under the **Domain and URLs** section.

If the values don’t match with the patterns preconfigured in Microsoft Entra ID, you can work with the application vendor to get values that match the pattern preconfigured in Microsoft Entra ID. If the application is multi-tenant, a single identifier is allowed when the principal object isn't the primary instance of the app.

## Where do I set the EntityID (User Identifier) format

You won’t be able to select the EntityID (User Identifier) format that Microsoft Entra ID sends to the application in the response after user authentication.

Microsoft Entra ID selects the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest. For more information visit the article [Single sign-on SAML protocol](../../identity-platform/single-sign-on-saml-protocol#authnrequest) under the section NameIDPolicy,

## Can’t find the Microsoft Entra metadata to complete the configuration with the application

To download the application metadata or certificate from Microsoft Entra ID, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select the application you configure for single sign-on.
4. Once the application loads, select **Single sign-on** from the application’s left-hand navigation menu.
5. Go to **SAML Signing Certificate** section, then select **Download** column value. Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.

Microsoft Entra doesn’t provide a URL to get the metadata. The metadata can only be retrieved as an XML file.

## Customize SAML claims sent to an application

To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Microsoft Entra ID](../../identity-platform/saml-claims-customization) for more information.