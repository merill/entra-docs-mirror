---
layout: Conceptual
title: Set up QR Code and PIN Authentication in iOS/macOS App - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/ios-qr-code-pin-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure your iOS app to use QR code and PIN authentication using the Microsoft Authentication Library for iOS and macOS.
manager: pmwongera
ms.subservice: 
ms.topic: concept-article
ms.date: 2025-07-24T00:00:00.0000000Z
ms.reviewer: akgoel
locale: en-us
document_id: e6130470-e58f-0ba7-e580-a660fc73accf
document_version_independent_id: e6130470-e58f-0ba7-e580-a660fc73accf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/ios-qr-code-pin-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/ios-qr-code-pin-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/ios-qr-code-pin-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 6765cac6-7132-f36e-6b98-9dec0a476f8d
---

# Set up QR Code and PIN Authentication in iOS/macOS App - Microsoft identity platform | Microsoft Learn

QR code authentication method enables frontline workers to sign in quickly and easily in apps on shared device. Users are able to use unique QR code provided by their admins and enter their PIN to sign in, eliminating the need to enter usernames and passwords.

You can use QR code web sign-in experience available at *login.microsoft.com*. This user entry point doesn't require any developer changes. Users select **Sign in options** &gt; **Sign in to an organization** &gt; **Sign in with a QR code**. You can optimize QR code sign-in experience by providing the entry point at your sign in page, eliminating two user clicks. To take advantage of QR code authentication method, app developers and [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference) work together:

- App developers integrate QR code authentication's optimized entry point in their app using the Microsoft Authentication Library (MSAL) for iOS and macOS.
- Authentication Policy Administrator configures the [authentication method](/en-us/entra/identity/authentication/how-to-authentication-qr-code) in Microsoft Entra ID.

## Configure your app to use QR code authentication

To configure your app to use QR code authentication, you can call the `getDeviceInformationWithParameters` API in MSAL to receive the `MSALDeviceInformation` object. In this object, a new flag is available to reflect the admin configured QR code authentication in the single sign-on (SSO) extension configuration. The following code snippet shows how to retrieve the preferred authentication method:

```objectivec

@property (nonatomic, readonly) MSALPreferredAuthMethod configuredPreferredAuthMethod; 

```

`MSALPreferredAuthMethod` is an enumeration that describes the different authentication methods available. The `configuredPreferredAuthMethod` property allows you to retrieve the preferred authentication method for the application. Currently, QR code is private enum value of 1. When released to general availability (GA), it's `MSALPreferredAuthMethodQRPIN`.

`MSALInteractiveTokenParameters` also define a new, optional parameter of type `MSALPreferredAuthMethod: preferredAuthMethod`. When this parameter is set for QR code authentication, the resulting interactive sign-in UI takes the user directly to the QR code authentication entry page. The following code snippet shows how to configure your app to use QR code authentication:

```objectivec
MSALWebviewParameters *webParameters = [[MSALWebviewParameters alloc] initWithAuthPresentationViewController:viewController]; 

MSALInteractiveTokenParameters *interactiveParams = [[MSALInteractiveTokenParameters alloc] initWithScopes:scopes webviewParameters:webParameters]; 

interactiveParams.preferredAuthMethod = 1; //Currently need to use the private enum value 

[application acquireTokenWithParameters:interactiveParams completionBlock:^(MSALResult *result, NSError *error) { 

    // When token acquisition completes 

}]; 

```

This code snippet configures and acquires a token using the MSAL in an iOS app, focusing on QR code authentication. It initializes `MSALWebviewParameters` with a view controller for the authentication web view and creates `MSALInteractiveTokenParameters` with the required scopes and web parameters. The preferred authentication method is set to QR code authentication.

Finally, it calls `acquireTokenWithParameters` on the `MultipleAccountPublicClientApplication` instance, using the configured parameters and a completion block to handle the result. This setup ensures the authentication flow uses the QR code authentication method for secure and convenient user authentication.

It's advised to call the `getDeviceInformationWithParameters` API in MSAL to find out if the admin has configured QR code authentication method. If it has, an app can update its UI to indicate that QR code authentication method is available as a sign-in option.

## Suppress camera consent prompt

By default, QR code authentication prompts users for camera permission every time they need to use the camera to scan a QR code.

[![Screenshot of a how to allow camera access on iOS.](media/ios-qr-code-pin-authentication/allow-camera.png)](media/ios-qr-code-pin-authentication/allow-camera.png#lightbox)

Administrators can suppress this behavior and skip the request for camera permission. To configure the request, set the following SSO extension configuration:

- **Key**: suppress\_camera\_consent
- **Type**: Integer
- **Value**: 1 or 0. This value is set to 0 by default.

The location is the same as where you can configure preferred\_auth\_method. For more information about SSO extension configuration, see [More configuration options for Microsoft Enterprise SSO plug-in for Apple devices](/en-us/entra/identity-platform/apple-sso-plugin#more-configuration-options).

Note

The camera consent prompt shows one time because of operating system requirements.