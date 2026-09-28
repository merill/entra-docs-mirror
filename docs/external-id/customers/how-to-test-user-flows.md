---
layout: Conceptual
title: Test a user flow - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-test-user-flows
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to use the Run user flow feature to test your sign-up and sign-in user flow for your consumer and business customer apps.
ms.topic: how-to
ms.date: 2025-01-22T00:00:00.0000000Z
ms.custom: it-pro, sfi-ropc-nochange, sfi-image-nochange
locale: en-us
document_id: fda34826-2505-b707-c422-2f7500e1023d
document_version_independent_id: fda34826-2505-b707-c422-2f7500e1023d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-test-user-flows.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-test-user-flows
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-test-user-flows.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: b8ae29a8-3918-6cc8-4948-9b252a4f505c
---

# Test a user flow - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

The **Run user flow** feature allows you to test your user flows by simulating a user’s sign-up or sign-in experience with your application. You can use this feature to verify that your user flow is working as expected. To use this feature, you select the user flow associated with your application, run the user flow, and enter the requested sign-up or sign-in information.

This feature obtains most of the values it needs to run from the application registration. You can select the application you want to test and specify the browser language for the user interface, but you can generally leave the other fields at their default values.

Note

This feature doesn't support SAML apps. However, you can still test the end-user experience by running your SAML app.

## Prerequisites

- A **Microsoft Entra external tenant**: You can set up a [free trial](https://aka.ms/ciam-free-trial?wt.mc_id=ciamcustomertenantfreetrial_linkclick_content_cnl), or you can create a new external tenant in Microsoft Entra ID.
- A [sign-up and sign-in user flow](how-to-user-flow-sign-up-sign-in-customers).
- Your application, which is [registered with Microsoft Entra](/en-us/entra/identity-platform/quickstart-register-app), has a Redirect URI specified, and is [associated with your user flow](how-to-user-flow-add-application).

## To test your user flow

Follow these steps to use the **Run user flow** feature to test your user flow.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
3. Select your user flow from the list. At least one application with a redirect URI must be associated with this user flow (see the Prerequisites).

    Note

    If the application you want to test hasn't been added to the user flow yet, you can add it now. After adding the application, there may be a short delay before it becomes available for testing with the **Run user flow** feature.
4. Select the **Run user flow** button.

    ![Screenshot showing the Run user flow button.](media/how-to-test-user-flows/run-user-flow-button.png)
5. In the **Run user flow** pane, most of the fields are populated with values from the application registration, so you can leave the default values. For details about each field, refer to the table below.

    ![Screenshot showing the Run user flow pane.](media/how-to-test-user-flows/run-user-flow-pane.png)

    | Field | Description |
    | --- | --- |
    | **Open Id Configuration URL** | This value is retrieved from the application registration. It's the publicly accessible URL that was assigned to your application when you registered it with Microsoft Entra ID. This URL points to the OpenID configuration document used by client applications to find authentication URLs and public signing keys. The format is: `https://{tenant}.ciamlogin.com/{tenant}.onmicrosoft.com/v2.0/.well-known/openid-configuration?appid=00001111-aaaa-2222-bbbb-3333cccc4444` |
    | **Application** | This menu lists the applications that are associated with this user flow. At least one application is required. If there are multiple applications, select the one you want to test. |
    | **Reply URL** / **Redirect URI** | This value is retrieved from the application registration, and is required for the Run user flow feature to work. Keep the current setting, which is the reply URL or redirect URI (depending on the protocol) that is configured for your application. [Learn more](/en-us/entra/identity-platform/quickstart-register-app#add-a-redirect-uri) |
    | **Resource** | This value is retrieved from the application registration for a protected web API and applies to access tokens. The **Resource** is the globally unique **Application ID URI** that was assigned to the API when it was exposed during app registration ([learn more](../../identity-platform/quickstart-configure-app-expose-web-apis)). The access token must contain both the **Resource** and **Scopes** values to allow secure access to the web API. |
    | **Scopes** | This value is retrieved from the application registration for a protected web API and applies to access tokens. The **Scopes** are the permissions needed by an application to access the data and functionality in the API. These values are defined when you expose the API during app registration ([learn more](../../identity-platform/quickstart-configure-app-expose-web-apis)). The access token must contain both the **Resource** and **Scopes** values to allow secure access to the web API. |
    | **Response type** | The **Response type** specifies the type of information to be returned in the token issued by the authorization endpoint. The values that are available for **Response type** are based on how the implicit grant and hybrid flows settings are configured in the application registration. If ID tokens are specified (for implicit and hybrid flows), then **id token** is available in this list. If only access tokens are specified (or no tokens are specified), **code** is the only option available. |
    | **Proof Key for Code Exchange** | The authorization code flow with Proof Key for Code Exchange (PKCE) is recommended for single-page applications (SPAs). With PKCE, an authorization code is delivered instead of a token to the specified reply URL of the application. To test the PKCE flow, select the **Specify code challenge** check box. Then you can use the autogenerated **Code Verifier**, **Code Challenge method**, and **Code Challenge** values to test the user flow experience. Or you can use the values expected by your application during development so the application can redeem the authorization code for a token. [Learn more](../../identity-platform/v2-oauth2-auth-code-flow) |
    | **Localization** | To test a specific language, select the **Specify ui locales** option and use **Select target language** menu to choose the language. [Learn more](how-to-customize-languages-customers) |
    | **Run user flow endpoint** | This URL runs the user flow with the selected options. You can use this URL or select the **Run user flow** button. |
6. Select the **Run user flow** button, or copy the **Run user flow endpoint** URL into a new browser window.
7. The sign-in page opens, allowing you to test the user experience.