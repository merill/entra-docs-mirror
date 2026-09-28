---
layout: Conceptual
title: Support passwordless authentication with FIDO2 keys in apps you develop - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/support-fido2-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: This deployment guide explains how to support passwordless authentication with FIDO2 security keys in the applications you develop
ms.date: 2021-01-29T00:00:00.0000000Z
ms.reviewer: 
ms.topic: reference
locale: en-us
document_id: 6f22cc9c-eabe-842d-1606-9725ddd69d73
document_version_independent_id: b0bcebe2-07f0-2bd9-3e26-eb5553d9838a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/support-fido2-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/support-fido2-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/support-fido2-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bb0e6133-c8dc-2a14-a0a7-1aebac8e1548
---

# Support passwordless authentication with FIDO2 keys in apps you develop - Microsoft identity platform | Microsoft Learn

These configurations and best practices will help you avoid common scenarios that block [FIDO2 passwordless authentication](../identity/authentication/concept-authentication-passkeys-fido2) from being available to users of your applications.

## General best practices

### Domain hints

Don't use a domain hint to bypass [home-realm discovery](../identity/enterprise-apps/configure-authentication-for-federated-users-portal). This feature is meant to make sign-ins more streamlined, but the federated identity provider may not support passwordless authentication.

### Requiring specific credentials

If you are using SAML, do not specify that a password is required [using the RequestedAuthnContext element](single-sign-on-saml-protocol#requestedauthncontext).

The RequestedAuthnContext element is optional, so to resolve this issue you can remove it from your SAML authentication requests. This is a general best practice, as using this element can also prevent other authentication options like multifactor authentication from working correctly.

### Using the most recently used authentication method

The sign-in method that was most recently used by a user will be presented to them first. This may cause confusion when users believe they must use the first option presented. However, they can choose another option by selecting "Other ways to sign in" as shown below.

![Image of the user authentication experience highlighting the button that allows the user to change the authentication method.](media/support-fido2-authentication/most-recently-used-method.png)

## Platform-specific best practices

### Windows

The recommended options for implementing authentication are, in order:

- .NET desktop applications that are using the Microsoft Authentication Library (MSAL) should use the Windows Authentication Manager (WAM). This integration and its benefits are [documented on GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/wiki/wam).
- Use [WebView2](/en-us/microsoft-edge/webview2/) to support FIDO2 in an embedded browser.
- Use the system browser. The MSAL libraries for desktop platforms use this method by default. You can consult our page on FIDO2 browser compatibility to ensure the browser you use supports FIDO2 authentication.

### Android

FIDO2 is supported for Android apps that use MSAL with [BROWSER as the authorization user agent](/en-us/entra/msal/android/msal-configuration#authorization_user_agent) or broker integration. Broker is shipped in Microsoft Authenticator, Company Portal, or Link to Windows app on Android.

If you aren't using MSAL, you should still use the system web browser for authentication. Features such as SSO and Conditional Access rely on a shared web surface provided by the system web browser.

### iOS and macOS

FIDO2 is supported for iOS apps that use MSAL with either ASWebAuthenticationSession or broker integration. Broker is shipped in Microsoft Authenticator on iOS, and Microsoft Intune Company Portal on macOS.

Make sure that your network proxy doesn't block the associated domain validation by Apple. FIDO2 authentication requires Apple's associated domain validation to succeed, which requires certain Apple domains to be excluded from network proxies. For more information, see [Use Apple products on enterprise networks](https://support.apple.com/HT210060).

If you aren't using MSAL, you should still use the system web browser for authentication. Features such as SSO and Conditional Access rely on a shared web surface provided by the system web browser. For more information, see [Authenticating a User Through a Web Service | Apple Developer Documentation](https://developer.apple.com/documentation/authenticationservices/authenticating_a_user_through_a_web_service).

### Web and single-page apps

The availability of FIDO2 passwordless authentication for applications that run in a web browser will depend on the combination of browser and platform. You can consult our [FIDO2 compatibility matrix](../identity/authentication/fido2-compatibility) to check if the combination your users will encounter is supported.