---
layout: Conceptual
title: Add federated identity provider sign-in and sign-up to an iOS app using native authentication web flow - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-ios-macos-identity-provider-sign-in-sign-up
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to enable federated identity provider sign-in and sign-up in an iOS app using Microsoft Entra native authentication with web-based authentication flow.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2026-04-10T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: ac2fe3ea-9a24-bf5c-0ff9-531736079dc4
document_version_independent_id: ac2fe3ea-9a24-bf5c-0ff9-531736079dc4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-ios-macos-identity-provider-sign-in-sign-up.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-ios-macos-identity-provider-sign-in-sign-up
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-ios-macos-identity-provider-sign-in-sign-up.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8f86abd7-9efc-2d74-0254-1b5f6e489dc7
---

# Add federated identity provider sign-in and sign-up to an iOS app using native authentication web flow - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to implement federated identity provider (IdP) authentication into your iOS app using native authentication with web flow. Federated IdP authentication allows users to sign in or sign up using their existing accounts from providers like Apple, Facebook, Google and custom OIDC providers.

In this tutorial, you learn how to:

- Sign in a user using a federated identity provider via web flow
- Sign up a user using a federated identity provider via web flow

## Prerequisites

1. Complete the steps in [Tutorial: Prepare your iOS/macOS app for native authentication](tutorial-native-authentication-prepare-ios-macos-app).
2. Configure federated identity providers in your Microsoft Entra External ID tenant. Follow the steps in the Microsoft Entra admin center to add and configure your desired identity providers:

    - [Configure Apple as an identity provider](../external-id/customers/how-to-apple-federation-customers)
    - [Configure Facebook as an identity provider](../external-id/customers/how-to-facebook-federation-customers)
    - [Configure Google as an identity provider](../external-id/customers/how-to-google-federation-customers)
    - [Configure a custom OIDC provider](../external-id/customers/how-to-custom-oidc-federation-customers). Use the domain of the Issuer URI configured for custom OIDC as the `domain_hint`.
3. Ensure your app supports web fallback [Tutorial: Support web fallback](tutorial-native-authentication-ios-macos-support-web-fallback).
4. Add/update the Microsoft Authentication Library (MSAL) dependency to at least `2.6.0`.
5. If you'd like to explore our federated IdP Sign in and Sign up implementation, take a look at our [sample iOS application](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-ios-sample/blob/main/NativeAuthSampleApp/WebFallbackViewController.swift) before getting started.

## Sign in a user with a federated identity provider

To sign in a user with a federated identity provider via web flow, you need to first identify the identity provider to authenticate with, and the corresponding `domain_hint`.

- Use the identity providers defined in the prerequisite configuration section.
- Use the `domain_hint` parameter to direct authentication to a specific identity provider. Choose one of the following values:

    - `"Apple"` for Apple
    - `"Facebook"` for Facebook
    - `"Google"` for Google

To sign in a user, you need to:

1. Create a user interface that lets the user sign in with a federated identity provider. This interface should identify a specific identity provider and its corresponding `domain_hint`.
2. Once `domain_hint` value is identified from the client app, create `MSALInteractiveTokenParameters`, set `domain_hint` and call `acquireToken(with: parameters)` method of `MSALNativeAuthPublicClientApplication` to trigger web authentication with Social IdP like below.

    Use the Prompt type value as `.login` to force interactive authentication, even if user is signed in.

    ```swift
    let parameters = MSALInteractiveTokenParameters(scopes: ["User.Read"], webviewParameters: webviewParams)
    parameters.promptType = .login
    parameters.domainHint = domainHint
    
    nativeAuth.acquireToken(with: parameters) { [weak self] (result: MSALResult?, error: Error?) in
        guard let self = self else { return }
    
        if let error = error {
            self.showResultText("Error acquiring token: \(error)")
            return
        }
    
        self.msalAccount = result?.account
    
        guard let msalAccount = self.msalAccount else {
            self.showResultText("Could not acquire token: No result or account returned")
            return
        }
    
        self.updateUI()
    }
    ```
3. You can also retrieve the current cached account after successful authentication by using the `getNativeAuthUserAccount()` from `MSALNativeAuthPublicClientApplication`:

    ```swift
        if let account = nativeAuth.getNativeAuthUserAccount() {
            ...
        }
    ```

## Sign up a user with a federated identity provider

To sign up a user with a federated identity provider, the process is almost the same as signing in, with a minor change to the Prompt value: use `.create`.

```swift
    let parameters = MSALInteractiveTokenParameters(scopes: ["User.Read"], webviewParameters: webviewParams)
    parameters.promptType = .create
    parameters.domainHint = domainHint

    nativeAuth.acquireToken(with: parameters) { [weak self] (result: MSALResult?, error: Error?) in
        ...
    }
```