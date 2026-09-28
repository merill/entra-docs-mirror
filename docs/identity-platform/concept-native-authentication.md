---
layout: Conceptual
title: Native authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/concept-native-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to set up native authentication in Microsoft Entra External ID. Customize the user interface for mobile and desktop apps, and provide a seamless sign-in experience.
manager: dougeby
ms.subservice: external
ms.topic: concept-article
ms.date: 2026-06-22T00:00:00.0000000Z
locale: en-us
document_id: 82b9a249-1fd3-f098-b2bf-9ca0a0f7c3fe
document_version_independent_id: 82b9a249-1fd3-f098-b2bf-9ca0a0f7c3fe
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/concept-native-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/concept-native-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/concept-native-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 512d2d52-7152-fe30-f8bd-cccc6c99140e
---

# Native authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Microsoft Entra’s native authentication allows you to have full control over the design of your mobile and desktop application sign-in experience. Unlike browser-based solutions, native authentication allows you to create visually appealing, pixel-perfect authentication screens that seamlessly blend into your app's interface. With this approach, you can fully customize the user interface, including design elements, logo placement, and layout, ensuring a consistent and branded look.

The standard app sign-in process, which relies on browser-delegated authentication, often results in a disruptive transition during authentication. Users are temporarily redirected to a system browser for authentication, only to be brought back to the app once the sign-in is complete.

While browser-delegated authentication offers benefits such as reduced attack vectors and support for single sign-on (SSO), it offers limited UI customization options.

## When to use native authentication

When it comes to implementing authentication for mobile and desktop apps on External ID, you have two options:

- Microsoft-hosted browser-delegated authentication.
- Fully custom SDK based native authentication.

The approach you choose depends on your app's specific requirements. While each app has unique authentication needs, there are some common considerations to keep in mind. Whether you choose native authentication or browser-delegated authentication, Microsoft Entra External ID supports both of them.

For a side-by-side comparison of the two approaches, including feature availability, supported languages and frameworks, user experience, customization, and security trade-offs, see [Choose an authentication approach](/en-us/entra/external-id/customers/concept-choose-authentication-approach).

## How to enable native authentication

First, review the guidelines on [when to use native authentication](/en-us/entra/external-id/customers/concept-native-authentication#when-to-use-native-authentication). Then, have an internal discussion with your application's business owner, designer, and development team to determine if native authentication is necessary.

If your team determines that native authentication is necessary for your application, follow these steps to enable native authentication in the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **App registrations** and select the app registration for which you want to enable public client and native authentication flows.
3. Under **Manage**, select **Authentication**.
4. On the **Redirect URI configuration**tab, allow public client flows:
    1. For **Enable the following mobile and desktop flows** select **Yes**.
    2. For **Enable native authentication**, select **Yes**.
5. Select the **Save** button.

## Update your configuration code

After enabling the native authentication APIs in the admin center, you still need to update your application's configuration code to support native authentication flows for Android or iOS/macOS. To do so, you need to add the challenge type field to your configuration. Challenge types are a list of values that the app uses to notify Microsoft Entra about the authentication method it supports. You can find more information about native authentication challenge types in [Native authentication challenge types](/en-us/entra/external-id/customers/concept-native-authentication-challenge-types). If the configuration isn't updated to integrate native authentication components, the native authentication SDKs and APIs aren't usable.

## Security considerations for native authentication

Native authentication gives your development team full control over the authentication experience. With this control comes the responsibility to follow security best practices in your app's implementation, such as secure token handling and transport security (HTTPS).

## Single sign-on (SSO)

Native authentication supports single sign-on (SSO) for embedded web views. This allows users to sign in once through the native app's UI and then access web resources hosted in an embedded web view (for example, `WKWebView` on iOS or `WebView` on Android) without encountering a second login prompt.

The app achieves this by retrieving an access token using the Native Auth SDK or the [native authentication API](reference-native-authentication-api) and injecting it into the web view's HTTP request via the `Authorization` header. The web resource validates the token and establishes a session, providing a seamless transition from the native experience to web content.

For implementation steps, see [Implement single sign-on from native apps to embedded web views](how-to-native-authentication-webview-sso).

Note

Cross-app SSO through system browsers isn't supported with native authentication.

## How to use native authentication

You can build apps that use native authentication by using our native authentication APIs or the Microsoft Authentication Library (MSAL) SDK for Android, iOS, macOS, and web applications. Whenever possible, we recommend using MSAL to add native authentication to your apps.

For more information on native authentication samples and tutorials, see the following table:

| Language/Platform | Quickstart | Build and integrate guide |
| --- | --- | --- |
| Android (Kotlin) | • [Sign in users](/en-us/entra/external-id/customers/how-to-run-native-authentication-sample-android-app) | • [Sign in users](/en-us/entra/external-id/customers/tutorial-native-authentication-prepare-android-app) |
| iOS (Swift) | • [Sign in users](/en-us/entra/external-id/customers/how-to-run-native-authentication-sample-ios-app) | • [Sign in users](/en-us/entra/external-id/customers/tutorial-native-authentication-prepare-ios-macos-app) |
| macOS (Swift) | • [Sign in users](/en-us/entra/external-id/customers/how-to-run-native-authentication-sample-macos-app) | • [Sign in users](/en-us/entra/external-id/customers/tutorial-native-authentication-prepare-ios-macos-app) |
| React (Next.js) | • [Quickstart](quickstart-native-authentication-single-page-app-sdk-sign-in) | • [Tutorials](tutorial-native-authentication-single-page-app-react-sdk-sign-up) |
| Angular | • [Quickstart](quickstart-native-authentication-single-page-app-sdk-sign-in) | • [Tutorials](tutorial-native-authentication-single-page-app-angular-sign-up) |

If you're planning to create an app on a framework currently not supported by MSAL, you can use our authentication API. For more information, see [Native authentication API reference](reference-native-authentication-api).