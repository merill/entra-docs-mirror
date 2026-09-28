---
layout: Conceptual
title: An app page shows an error message after the user signs in - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/application-sign-in-problem-application-error
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: How to resolve issues with Microsoft Entra sign-in when the app returns an error message.
ms.topic: troubleshooting
ms.date: 2025-04-29T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.collection: M365-identity-device-management
ms.custom: enterprise-apps
locale: en-us
document_id: 5dd7955a-11da-73ac-7489-eedd966ff490
document_version_independent_id: 944ed9a5-c04f-487e-5298-0950296d4167
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/application-sign-in-problem-application-error.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/application-sign-in-problem-application-error
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/application-sign-in-problem-application-error.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d32d1bb9-cf2f-cb05-417d-2cecf97d88a0
---

# An app page shows an error message after the user signs in - Microsoft Entra ID | Microsoft Learn

In this scenario, Microsoft Entra ID signs the user in. But the application displays an error message and doesn't let the user finish the sign-in flow. The problem is that the app didn't accept the response that Microsoft Entra ID issued.

There are several possible reasons why the app didn't accept the response from Microsoft Entra ID. If there's an error message or code displayed, use the following resources to diagnose the error:

- [Microsoft Entra authentication and authorization error codes](../../identity-platform/reference-error-codes)
- [Troubleshooting consent prompt errors](application-sign-in-unexpected-user-consent-error)

If the error message doesn't clearly identify what's missing from the response, try the following steps:

- If the app is in the Microsoft Entra gallery, verify that you followed the steps in [How to debug SAML-based single sign-on to applications in Microsoft Entra ID](debug-saml-sso-issues).
- Use a tool like [Fiddler](https://www.telerik.com/fiddler) to capture the SAML request, response, and token.
- Send the SAML response to the app vendor and ask them what's missing.

## Attributes are missing from the SAML response

To add an attribute in the Microsoft Entra configuration that is sent in the Microsoft Entra response, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Enter the name of the existing application in the search box, and then select the application that you want to configure for single sign-on.
4. After the app loads, select **Single sign-on** in the navigation pane.
5. In the **User Attributes** section, select **View and edit all other user attributes**. Here you can change which attributes to send to the app in the SAML token when users sign in.

    To add an attribute:

    1. Select **Add attribute**. Enter the **Name**, and select the **Value** from the drop-down list.
    2. Select **Save**. You see the new attribute in the table.
6. Save the configuration.

    The next time that the user signs in to the app, Microsoft Entra ID will send the new attribute in the SAML response.

## The app can't identify the user

Signing in to the app fails because the SAML response is missing an attribute such as a role. Or it fails because the app expects a different format or value for the **NameID** (User Identifier) attribute.

If you're using [Microsoft Entra ID automated user provisioning](../app-provisioning/user-provisioning) to create, maintain, and remove users in the app, verify that the user is provisioned to the SaaS app. For more information, see [No users are being provisioned to a Microsoft Entra Gallery application](../app-provisioning/application-provisioning-config-problem-no-users-provisioned).

### Add an attribute to the Microsoft Entra app configuration

To change the User Identifier value, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select the app that you want to configure for SSO.
4. After the app loads, select **Single sign-on** in the navigation pane.
5. Under **User attributes**, select the unique identifier for the user from the **User Identifier** drop-down list.

### Change the NameID format

If the application expects another format for the **NameID** (User Identifier) attribute, see the [Edit nameID](../../identity-platform/saml-claims-customization#edit-nameid) section to change the NameID format.

Microsoft Entra ID selects the format for the **NameID** attribute (User Identifier) based on the value selected or the format that's requested by the app in the SAML AuthRequest. For more information, see the "NameIDPolicy" section of [Single sign-on SAML protocol](../../identity-platform/single-sign-on-saml-protocol#nameidpolicy).

## The app expects a different signature method for the SAML response

To change which parts of the SAML token are digitally signed by Microsoft Entra ID, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select the application that you want to configure for single sign-on.
4. After the application loads, select **Single sign-on** in the navigation pane.
5. Under **SAML Signing Certificate**, select **Show advanced certificate signing settings**.
6. Select the **Signing Option** that the app expects from among these options:

    - **Sign SAML response**
    - **Sign SAML response and assertion**
    - **Sign SAML assertion**

    The next time that the user signs in to the app, Microsoft Entra ID will sign the part of the SAML response that you selected.

## The app expects the SHA-1 signing algorithm

By default, Microsoft Entra ID signs the SAML token by using the most-secure algorithm. We recommend that you don't change the signing algorithm to *SHA-1* unless the app requires SHA-1.

To change the signing algorithm, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select the app that you want to configure for single sign-on.
4. After the app loads, select **Single sign-on** from the navigation pane on the left side of the app.
5. Under **SAML Signing Certificate**, select **Show advanced certificate signing settings**.
6. Select **SHA-1** as the **Signing Algorithm**.

    The next time that the user signs in to the app, Microsoft Entra ID will sign the SAML token by using the SHA-1 algorithm.