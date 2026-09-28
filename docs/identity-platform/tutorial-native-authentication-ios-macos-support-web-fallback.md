---
layout: Conceptual
title: Support web fallback - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-ios-macos-support-web-fallback
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to implement web fallback in an iOS/macOS application by using native authentication to ensure stability in authentication flow.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2024-09-02T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 5bcc4b08-a598-3a67-64a5-6f707ff522e6
document_version_independent_id: 5bcc4b08-a598-3a67-64a5-6f707ff522e6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-ios-macos-support-web-fallback.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-ios-macos-support-web-fallback
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-ios-macos-support-web-fallback.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7d4d7684-9223-4c86-9a77-4c75c463f7a9
---

# Support web fallback - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to acquire a token through a browser where native authentication isn't sufficient to complete the user flow.

In this tutorial, you:

- Check BrowserRequired error.
- Handle BrowserRequired error.

## Prerequisites

- If you’re using iOS, follow the steps in [Sign in users in a sample native iOS mobile application](quickstart-native-authentication-ios-sign-in).
- If you’re using macOS, follow the steps in [Sign in users in sample macOS (Swift) app by using native authentication](quickstart-native-authentication-macos-sign-in).

## Browser required

`BrowserRequired` is a fallback mechanism for various scenarios where native authentication isn't sufficient to complete the user flow.

To ensure stability of your application and avoid interruption of the authentication flow, it's highly recommended to use the SDK's `acquireToken()` method to continue the flow in the browser.

When we initialize the SDK, we need to specify which challenge types our application can support. Here are the list of challenge types that the SDK accepts:

- OOB (out of band): add this challenge type when your iOS/macOS application can handle a one-time-passcode, in this case an email code.
- Password: add this challenge type when your application is able to handle password based authentication.

When Microsoft Entra requires capabilities that the client can't provide the `BrowserRequired` error will be returned. For example, suppose we initialize the SDK instance specifying only the challenge type OOB, but in Microsoft Entra admin center, the application is configured with an **Email with password** user flow. When we call the **signUp(username)** method from the SDK instance, we get a `BrowserRequired` error, because Microsoft Entra requires different challenge type (password in this case) than the one configured in the SDK.

Insufficient challenge type is only one example of when `BrowserRequired` can occur. `BrowserRequired` is a general fallback mechanism that can happen in various scenarios.

## Sample flow

In the following code snippet you can see how you can specify the challenge types during the SDK instance initialization:

```swift
nativeAuth = try MSALNativeAuthPublicClientApplication(
    clientId: "<client id>",
    tenantSubdomain: "<tenant subdomain>",
    challengeTypes: [.OOB]
)
```

In this case we're specifying only the challenge type OOB. Suppose that in the Microsoft Entra admin center, the application is configured with an **Email with password** user flow.

```swift
let parameters = MSALNativeAuthSignUpParameters(username: email)
nativeAuth.signUp(parameters: parameters, delegate: self)

func onSignUpStartError(error: MSAL.SignUpStartError) {
    if error.isBrowserRequired {
        // handle browser required error
    }
}
```

When we call the `signUp(parameters:delegate)` method from the SDK instance, we get a `BrowserRequired` error, because Microsoft Entra requires a different challenge type (password in this case) than the one configured in the SDK.

## Handle BrowserRequired error

To handle this kind of error, we need to launch a browser and let the user perform the authentication flow there. This can be done by calling `acquireToken()` method. In order to use this method, a few additional configurations need to be done:

- [Configure URL schemes in our Xcode project](tutorial-mobile-app-ios-swift-prepare-app?pivots=workforce#for-ios-only-configure-url-schemes)
- [Configure the redirect URI in Microsoft Entra admin center](tutorial-mobile-app-ios-swift-prepare-tenant#add-a-platform-redirect-url)

Now we can get a token and an account interactively. Here's an example of how to do it:

```swift
func onSignUpStartError(error: MSAL.SignUpStartError) {
    if error.isBrowserRequired {
        let webviewParams = MSALWebviewParameters(authPresentationViewController: self)
        let parameters = MSALInteractiveTokenParameters(scopes: ["User.Read"], webviewParameters: webviewParams)

        nativeAuth.acquireToken(with: parameters) { (result: MSALResult?, error: Error?) in
            // result will contain account and tokens retrieved in the browser
        }
    }
}
```

The tokens and account that are returned are identical to the ones that would be retrieved through a native auth flow.