---
layout: Conceptual
title: Sign in user automatically after sign-up in iOS/macOS app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-ios-macos-sign-in-user-after-sign-up
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to automatically sign-in a user after sign-up in an iOS/macOS app by using native authentication.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2024-09-02T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 59cd78e1-92e5-cb9e-ba79-758c65dd0533
document_version_independent_id: 59cd78e1-92e5-cb9e-ba79-758c65dd0533
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-ios-macos-sign-in-user-after-sign-up.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-ios-macos-sign-in-user-after-sign-up
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-ios-macos-sign-in-user-after-sign-up.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 2a2cc633-1b13-8e4f-c948-95e32fe5b9ad
---

# Sign in user automatically after sign-up in iOS/macOS app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to sign in user automatically after sign-up in an iOS/macOS app by using native authentication.

In this tutorial, you:

- Sign in after sign-up.
- Handle errors.

## Prerequisites

- If you’re on iOS, follow the steps in [Sign in users in sample iOS (Swift) mobile app by using native authentication](../external-id/customers/how-to-run-native-authentication-sample-ios-app). If you’re using macOS, follow the steps in [Sign in users in sample macOS (Swift) app by using native authentication](../external-id/customers/how-to-run-native-authentication-sample-macos-app). These articles show you how to run sample apps that you configure using your tenant settings.
- [Tutorial: Add sign-up in an iOS/macOS app using native authentication](tutorial-native-authentication-ios-macos-sign-up). The steps in this tutorial should work whether you sign up with email and password or email one-time passcode.

## Sign in after sign-up

The `Sign in after sign up` is an enhancement functionality of the sign in user flows, which has the effect of automatically signing in after successfully signing up. The SDK provides developers the ability to sign in a user after signing up, without having to supply the username, or to verify the email address through a one-time passcode.

To sign in a user after successful sign-up use the `signIn(delegate)` method from the new state `SignInAfterSignUpState` returned in the `onSignUpCompleted(newState)`:

```swift
extension ViewController: SignUpVerifyCodeDelegate {
    func onSignUpVerifyCodeError(error: MSAL.VerifyCodeError, newState: MSAL.SignUpCodeRequiredState?) {
        resultTextView.text = "Error verifying code: \(error.errorDescription ?? "no description")"
    }

    func onSignUpCompleted(newState: SignInAfterSignUpState) {
        resultTextView.text = "Signed up successfully!"
        let parameters = MSALNativeAuthSignInAfterSignUpParameters()
        newState.signIn(parameters: parameters, delegate: self)
    }
}
```

The `signIn(parameters:delegate)` accepts a `MSALNativeAuthSignInAfterSignUpParameters` instance and a delegate parameter and we must implement the required methods in the `SignInAfterSignUpDelegate` protocol.

In the most common scenario, we receive a call to `onSignInCompleted(result)` indicating that the user has signed in. The result can be used to retrieve the `access token`.

```swift
extension ViewController: SignInAfterSignUpDelegate {
    func onSignInAfterSignUpError(error: SignInAfterSignUpError) {
        resultTextView.text = "Error signing in after sign up"
    }

    func onSignInCompleted(result: MSAL.MSALNativeAuthUserAccountResult) {
        // User successfully signed in
        let parameters = MSALNativeAuthGetAccessTokenParameters()
        result.getAccessToken(parameters: parameters, delegate: self)
    }
}
```

The `getAccessToken(parameters:delegate)` accepts a `MSALNativeAuthGetAccessTokenParameters` instance and a delegate parameter and we must implement the required methods in the `CredentialsDelegate` protocol.

In the most common scenario, we receive a call to `onAccessTokenRetrieveCompleted(result)` indicating that the user obtained an `access token`.

```swift
extension ViewController: CredentialsDelegate {
    func onAccessTokenRetrieveError(error: MSAL.RetrieveAccessTokenError) {
        resultTextView.text = "Error retrieving access token"
    }

    func onAccessTokenRetrieveCompleted(result: MSALNativeAuthTokenResult) {
        resultTextView.text = "Signed in. Access Token: \(result.accessToken)"
    }
}

```

## Configure custom claims provider

If you want to add claims from an external system into the token that is issued to your app, use a [custom claims provider](custom-claims-provider-overview). A custom claims provider is made up of a custom authentication extension that calls an external REST API to fetch claims from external systems.

Follow the steps in [Configure a custom claim provider](/en-us/entra/identity-platform/custom-extension-tokenissuancestart-configuration?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) to add claims from an external system into your security tokens.