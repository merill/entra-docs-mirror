---
layout: Conceptual
title: Prepare your iOS/macOS app for native authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-prepare-ios-macos-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to add Microsoft Authentication Library (MSAL) native auth SDK framework to your iOS/macOS application.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2024-09-30T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 0d54f657-88f5-7d3c-cdc1-d5c2f2d6ff6e
document_version_independent_id: 0d54f657-88f5-7d3c-cdc1-d5c2f2d6ff6e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-prepare-ios-macos-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-prepare-ios-macos-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-prepare-ios-macos-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 2a2ee5e3-dfe3-d20d-90c5-f31c0c521d4f
---

# Prepare your iOS/macOS app for native authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to add Microsoft Authentication Library (MSAL) native authentication SDK framework to your iOS/macOS Swift app.

In this tutorial, you:

- Add the MSAL framework to an iOS/macOS app.
- Create SDK instance.

## Prerequisites

- [Xcode](https://developer.apple.com/xcode/resources/)
- If you haven't already, follow the instructions in [Sign in users in sample iOS (Swift) mobile app by using native authentication](../external-id/customers/how-to-run-native-authentication-sample-ios-app)and register an app in your external tenant. Make sure you complete the following steps:
    - Register an application.
    - Enable public client and native authentication flows.
    - Grant API permissions.
    - Create a user flow.
    - Associate the app with the user flow.
- iOS/macOS project

## Add the MSAL framework to an iOS/macOS app

1. Open your iOS/macOS project in Xcode.
2. Select **Add Package Dependencies...** from the **File** menu.
3. Enter `https://github.com/AzureAD/microsoft-authentication-library-for-objc` as the Package URL and choose **Add Package**.
4. Add a new keychain group to your project **Capabilities**. Use `com.microsoft.adalcache` on iOS and `com.microsoft.identity.universalstorage` on macOS.

For more information and other mechanisms to add MSAL to your project, see the [project Readme file](https://github.com/AzureAD/microsoft-authentication-library-for-objc?tab=readme-ov-file#installation).

## Create SDK instance

1. Import the MSAL library into your view controller by adding `import MSAL` at the top of your `ViewController` class.
2. Add a `nativeAuth` member variable to your `ViewController` class by adding the following code just before the `viewDidLoad()` function:

    ```swift
    var nativeAuth: MSALNativeAuthPublicClientApplication!
    ```
3. Next, add the following code to the `viewDidLoad()` function:

    ```swift
     do {
        nativeAuth = try MSALNativeAuthPublicClientApplication(
            clientId: "Enter_the_Application_Id_Here",
            tenantSubdomain: "Enter_the_Tenant_Subdomain_Here",
            challengeTypes: [.OOB]
        )
    
        print("Initialized Native Auth successfully.")
     } catch {
        print("Unable to initialize MSAL \(error)")
     }
    ```
4. Replace the following values with the values from the Microsoft Entra admin center:

    1. Find the `Enter_the_Application_Id_Here` value and replace it with the **Application (client) ID** of the app you registered earlier.
    2. Find the `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your Directory (tenant) subdomain, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).

        The challenge types are a list of values, which the app uses to notify Microsoft Entra about the authentication method that it supports.

        - For sign-up and sign-in flows with email one-time passcode, use `[.OOB]`.
        - For sign-up and sign-in flows with email and password, use `[.OOB, .password]`.
        - For self-service password reset (SSPR), use `[.OOB]`.

        Learn more [challenge types](concept-native-authentication-challenge-types).
5. To build, select the **Product** &gt; **Build** in your project’s toolbar.

### Optional: Logging configuration

MSAL provides a logging API that you can use to enable and configure logging. To see all debug output from MSAL add the following code at the start of the `viewDidLoad()` function:

```swift
MSALGlobalConfig.loggerConfig.logLevel = .verbose
MSALGlobalConfig.loggerConfig.setLogCallback { logLevel, message, containsPII in
   if !containsPII {
      print("MSAL: \(message ?? "")")
   }
}
```

This outputs all debug logs from MSAL, which can be helpful in diagnosing issues and learning how the native authentication flows work. To learn more about configuring log levels and best practices see [Logging in MSAL for iOS/macOS](/en-us/entra/msal/objc/logging-ios?tabs=swift).