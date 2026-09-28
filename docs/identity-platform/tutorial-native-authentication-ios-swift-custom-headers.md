---
layout: Conceptual
title: Add custom headers to native authentication network requests in iOS (Swift) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-ios-swift-custom-headers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to attach custom x-* headers to native authentication network requests in an iOS (Swift) app to integrate fraud-detection SDKs with Microsoft Entra External ID.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.custom: msecd-doc-authoring-105
ms.date: 2026-04-29T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 44a0db35-4893-9fb1-ab2c-a3cb4df9277a
document_version_independent_id: 44a0db35-4893-9fb1-ab2c-a3cb4df9277a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-ios-swift-custom-headers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-ios-swift-custom-headers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-ios-swift-custom-headers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 1caa0cf5-88ec-150e-6da9-b903137f243f
---

# Add custom headers to native authentication network requests in iOS (Swift) - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to attach custom `x-*` headers to native authentication network requests in your iOS (Swift) app using the `MSALNativeAuthRequestInterceptor` protocol, enabling integration with third-party fraud and bot-detection SDKs.

In this tutorial, you:

- Understand the header naming rules enforced by MSAL.
- Implement the `MSALNativeAuthRequestInterceptor` protocol.
- Register the interceptor with your app configuration.

## Prerequisites

- An iOS (Swift) app that uses MSAL native authentication. If you don't have one, complete [Tutorial: Prepare your iOS/macOS mobile app for native authentication](tutorial-native-authentication-prepare-ios-macos-app).
- Your app is initialized with an `MSALNativeAuthPublicClientApplication` instance. The steps in this tutorial show you how to update your existing app initialization code to register the interceptor.

## Understand header naming rules

MSAL applies the following rules when evaluating the headers you provide:

- Headers **must** start with `x-` (case-insensitive). Headers that don't start with `x-` are ignored.
- Headers that start with any of the following reserved prefixes are ignored:
    - `x-client-`
    - `x-ms-`
    - `x-broker-`
    - `x-app-`
- MSAL adds headers that pass both rules to the network request. If a header you provide has the same name as one of MSAL's own internal headers, your value takes precedence.

Use these rules to verify your vendor-required header names before implementing the interceptor.

## Implement the request interceptor

The `MSALNativeAuthRequestInterceptor` protocol declares a single method that MSAL calls before it sends each network request. Your implementation receives the request URL and a completion block, and then calls the completion block with a dictionary of headers to add, or `nil` if no headers are needed for that request.

Make your view controller (or another class in your app) conform to `MSALNativeAuthRequestInterceptor`:

```swift
extension EmailAndPasswordViewController: MSALNativeAuthRequestInterceptor {

    func addAdditionalHeaderFields(
        _ requestUrl: URL?,
        completionBlock: @escaping MSALNativeAuthRequestInterceptorAddHeaderCompletionBlock
    ) {
        // Scope headers to specific endpoints only.
        if requestUrl?.absoluteString.contains("oauth2/v2.0/initiate") == true {
            completionBlock([
                "value_1": "customer_header_1",          // Ignored: doesn't start with "x-"
                "x-client-header": "customer_header_2",  // Ignored: starts with reserved prefix "x-client-"
                "X-my-custom-header": "my data"          // Added to the network request.
            ])
            return
        }

        // Return nil for all other requests to avoid over-sending signals.
        completionBlock(nil)
    }
}
```

The method receives the full URL of the outgoing request in `requestUrl`. Use this to scope your headers to the specific endpoints your fraud or bot-detection vendor requires. For example, sign-in or sign-up initiation endpoints. Sending headers to unrelated endpoints can degrade signal quality and increase false positives.

Note

Always call `completionBlock` exactly once per invocation. Pass `nil` if no extra headers are needed for that request.

## Register the interceptor

After implementing the protocol, assign your interceptor to the `requestInterceptor` property on your `MSALNativeAuthPublicClientApplicationConfig` instance before creating the `MSALNativeAuthPublicClientApplication`:

```swift
do {
    let config = try MSALNativeAuthPublicClientApplicationConfig(
        clientId: Configuration.clientId,
        tenantSubdomain: Configuration.tenantSubdomain,
        challengeTypes: [.OOB, .password]
    )

    config.requestInterceptor = self

    nativeAuth = try MSALNativeAuthPublicClientApplication(nativeAuthConfiguration: config)
} catch {
    print("Unable to initialize MSAL \(error)")
}
```

## Verify headers are applied

To confirm that your headers reach the intended endpoints, inspect the outgoing network traffic using a network proxy tool such as Fiddler or Charles Proxy. Check that:

- Headers starting with `x-` and without reserved prefixes appear in the request.
- Headers with reserved prefixes (`x-client-`, `x-ms-`, `x-broker-`, `x-app-`) don't appear in the request.
- Headers are sent only to the endpoints you scoped them to.

Note

Logging inside the interceptor callback won't show you the final request headers. The callback is invoked before MSAL evaluates and applies the naming rules, so it reflects only the headers you provide, not what is ultimately sent.