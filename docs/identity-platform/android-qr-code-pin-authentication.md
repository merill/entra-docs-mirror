---
layout: Conceptual
title: Set up QR Code and PIN Authentication in Android App - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/android-qr-code-pin-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure your Android app to use QR code and PIN authentication using the Microsoft Authentication Library for Android.
manager: pmwongera
ms.subservice: 
ms.topic: concept-article
ms.date: 2025-02-05T00:00:00.0000000Z
ms.reviewer: akgoel
locale: en-us
document_id: e33439d8-1f27-a0b9-4a33-69d311aad29d
document_version_independent_id: e33439d8-1f27-a0b9-4a33-69d311aad29d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/android-qr-code-pin-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/android-qr-code-pin-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/android-qr-code-pin-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: 84b89776-09e6-d2fd-b10f-41f0f3edc10c
---

# Set up QR Code and PIN Authentication in Android App - Microsoft identity platform | Microsoft Learn

QR code authentication method enables frontline workers to sign in quickly and easily in apps on shared device. Users are able to use unique QR code provided by their admins and enter their PIN to sign in, eliminating the need to enter usernames and passwords.

You can use QR code web sign-in experience available at *login.microsoft.com*. This user entry point doesn't require any developer changes. Users select **Sign in options** &gt; **Sign in to an organization** &gt; **Sign in with a QR code**. You can optimize QR code sign-in experience by providing the entry point at your sign in page, eliminating two user clicks. To take advantage of QR code authentication method, app developers and [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference) work together:

- App developers integrate QR code authentication's optimized entry point in their app using the Microsoft Authentication Library for Android (MSAL).
- Authentication Policy Administrator configures the [authentication method](/en-us/entra/identity/authentication/how-to-authentication-qr-code) in Microsoft Entra ID.

## Configure your app to use QR code authentication

To configure your app to use QR code authentication, you need to set the `PreferredAuthMethod` to QR in the `AcquireTokenParameters` object. The following code snippet shows how to configure your app to use QR code authentication:

```java
final AcquireTokenParameters acquireTokenParameters = 
    new AcquireTokenParameters.Builder()
    .startAuthorizationFromActivity(activity)
    .withLoginHint(requestOptions.getLoginHint())
     .forAccount(requestOptions.getAccount())
     .withPrompt(requestOptions.getPrompt())
     .withPreferredAuthMethod(PreferredAuthMethod.QR)
     .withCallback(getAuthenticationCallback(callback))
     .build(); 
```

The `PreferredAuthMethod` is set to `PreferredAuthMethod.QR`, which specifies that the QR code authentication method should be used. This method allows users to authenticate by scanning a QR code and entering their pin.

Once you have configured the `AcquireTokenParameters` object, you can call the `acquireToken` method to start the authentication process. The following code snippet shows how to acquire a token using the `AcquireTokenParameters` object:

```java
// Create the MultipleAccountPublicClientApplication instance with the given configuration
final MultipleAccountPublicClientApplication mpca = new MultipleAccountPublicClientApplication(config);

// Pass the acquireTokenParameters object to the acquireToken function
mpca.acquireToken(acquireTokenParameters);

```

This initiates the token acquisition process using the specified parameters, including the preferred QR code authentication method.

## Get preferred authentication method

The QR code authentication method is configured by the Authentication Policy Administrator through an [app configuration policy for managed Android Enterprise devices](/en-us/mem/intune/apps/app-configuration-policies-use-android) on the Microsoft Authenticator App, setting `preferred_auth_method` equal to `qrpin`.

![Screenshot showing how to configure QR code authentication.](media/common/configure-qr-code-auth.png)

You can get the preferred authentication method for the current account by calling the `getPreferredAuthMethod` method on the `mpca` object. The following code snippet shows how to get the preferred authentication method for the current account:

```java
mpca.getPreferredAuthConfiguration()
```

The `getPreferredAuthConfiguration` method requires the Microsoft Authenticator app to be installed on the device. If the Microsoft Authenticator app isn't installed, the method returns `None`.

## Suppress camera consent prompt

By default, QR code and PIN authentication prompts users for camera permission every time they need to use the camera to scan a QR code. However, administrators can suppress this behavior and skip requesting camera permission.

![Screenshot showing Android QR code and PIN authentication prompt.](media/common/android-qr-pin-prompt.png)

This is configured by the Authentication Policy Administrator through an [app configuration policy for managed Android Enterprise devices](/en-us/mem/intune/apps/app-configuration-policies-use-android) on the Microsoft Authenticator App, setting `sdm_suppress_camera_consent` equal to `true`, similar to how the `preferred_auth_method` is configured.

When this setting is enabled:

- The app won't show the camera consent prompt if camera permissions are already granted at the OS level.
- Users will have a smoother authentication experience without repeated permission requests.
- The QR code scanning flow will be more streamlined for managed devices.

This configuration is useful in enterprise environments where devices are managed and camera permissions can be preconfigured by IT administrators.