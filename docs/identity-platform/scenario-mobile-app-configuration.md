---
layout: Conceptual
title: Configure mobile apps that call web APIs - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-mobile-app-configuration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure your mobile app's code to call a web API
manager: pmwongera
ms.date: 2025-03-19T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: 454c976e-794a-3d75-c01f-ac79bccebf51
document_version_independent_id: 926807e8-c456-9273-74e3-0595daaebbb5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-mobile-app-configuration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-mobile-app-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-mobile-app-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: bc672739-da98-912e-f184-a8dcb70816a8
---

# Configure mobile apps that call web APIs - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

After you create your application, you'll learn how to configure the code by using the app registration parameters. Mobile applications present some extra complexities related to fitting into their creation framework.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). This account must have permissions to manage applications. Use any of the following roles needed to register the application:
    - Application Administrator
    - Application Developer
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID

## Add a platform redirect URI

To specify your app type to your app registration, follow these steps:

1. Under **Manage**, select **Authentication** &gt; **Add a platform** &gt; **iOS/macOS**.
2. Enter your bundle ID, and then select **Configure**. The redirect URI is computed for you.

If you prefer to manually configure the redirect URI, you can do so through the application manifest. Here's the recommended format for the manifest:

- **iOS**: `msauth.<BUNDLE_ID>://auth`
    - For example, enter `msauth.com.yourcompany.appName://auth`
- **Android**: `msauth://<PACKAGE_NAME>/<SIGNATURE_HASH>`
    - You can generate the Android signature hash by using the release key or debug key through the KeyTool command.

## Enable public client flow

If your app uses only username-password authentication, you don't need to register a redirect URI for your application. This flow does a round trip to the Microsoft identity platform. Your application won't be called back on any specific URI. But you should enable the public client flow.

To identify your app as a public client, follow these steps:

1. Under **Manage**, select **Authentication**.
2. Under **Advanced settings**, for **Allow public client flows**, select **Yes**.
3. Select **Save** to save your changes.

## Microsoft libraries supporting mobile apps

The following Microsoft libraries support mobile apps:

| Platform | Project onGitHub | Package | Gettingstarted | Sign in users | Access web APIs | Generally available (GA)*or*Public preview^1^ |
| --- | --- | --- | --- | --- | --- | --- |
| Android (Java) | [MSAL Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [MSAL](https://mvnrepository.com/artifact/com.microsoft.identity.client/msal) | [Quickstart](quickstart-mobile-app-android-sign-in) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Android (Kotlin) | [MSAL Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [MSAL](https://mvnrepository.com/artifact/com.microsoft.identity.client/msal) | — | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| iOS (Swift/Obj-C) | [MSAL for iOS and macOS](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [MSAL](https://cocoapods.org/pods/MSAL) | [Tutorial](tutorial-v2-ios) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |

^1^[Universal License Terms for Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) apply to libraries in *Public preview*.

## Instantiate the application

### Android

Mobile applications use the `PublicClientApplication` class. Here's how to instantiate it:

```Java
PublicClientApplication sampleApp = new PublicClientApplication(
                    this.getApplicationContext(),
                    R.raw.auth_config);
```

### iOS

Mobile applications on iOS need to instantiate the `MSALPublicClientApplication` class. To instantiate the class, use the following code.

```objc
NSError *msalError = nil;

MSALPublicClientApplicationConfig *config = [[MSALPublicClientApplicationConfig alloc] initWithClientId:@"<your-client-id-here>"];
MSALPublicClientApplication *application = [[MSALPublicClientApplication alloc] initWithConfiguration:config error:&msalError];
```

```swift
let config = MSALPublicClientApplicationConfig(clientId: "<your-client-id-here>")
if let application = try? MSALPublicClientApplication(configuration: config){ /* Use application */}
```

[Additional MSALPublicClientApplicationConfig properties](https://azuread.github.io/microsoft-authentication-library-for-objc/Classes/MSALPublicClientApplicationConfig.html#/Configuration%20options) can override the default authority, specify a redirect URI, or change the behavior of MSAL token caching.

### UWP

This section explains how to instantiate the application for UWP apps.

#### Instantiate the application

In UWP, the simplest way to instantiate the application is by using the following code. In this code, `ClientId` is the GUID of your registered app.

```csharp
var app = PublicClientApplicationBuilder.Create(clientId)
                                        .Build();
```

Additional `With<Parameter>` methods set the UI parent, override the default authority, specify a client name and version for telemetry, specify a redirect URI, and specify the HTTP factory to use. The HTTP factory might be used, for instance, to handle proxies and to specify telemetry and logging.

The following sections provide more information about instantiating the application.

##### Specify the parent UI, window, or activity

On Android, pass the parent activity before you do the interactive authentication. On iOS, when you use a broker, pass-in `ViewController`. In the same way on UWP, you might want to pass-in the parent window. You pass it in when you acquire the token. But when you're creating the app, you can also specify a callback as a delegate that returns `UIParent`.

```csharp
IPublicClientApplication application = PublicClientApplicationBuilder.Create(clientId)
  .ParentActivityOrWindowFunc(() => parentUi)
  .Build();
```

On Android, we recommend that you use [`CurrentActivityPlugin`](https://github.com/jamesmontemagno/CurrentActivityPlugin). The resulting `PublicClientApplication` builder code looks like this example:

```csharp
// Requires MSAL.NET 4.2 or above
var pca = PublicClientApplicationBuilder
  .Create("<your-client-id-here>")
  .WithParentActivityOrWindow(() => CrossCurrentActivity.Current)
  .Build();
```

##### Find more app-building parameters

For a list of all methods that are available on `PublicClientApplicationBuilder`, see the [Methods list](/en-us/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder#methods).

For a description of all options that are exposed in `PublicClientApplicationOptions`, see the [reference documentation](/en-us/dotnet/api/microsoft.identity.client.publicclientapplicationoptions).

## Tasks for MSAL for iOS and macOS

These tasks are necessary when you use MSAL for iOS and macOS:

- Implement the `openURL` callback
- [Enable keychain access groups](/en-us/entra/msal/objc/howto-v2-keychain-objc)
- [Customize browsers and WebViews](/en-us/entra/msal/objc/customize-webviews)

#### Tasks for UWP

On UWP, you can use corporate networks. The following sections explain the tasks that you should complete in the corporate scenario.

For more information, see [UWP-specific considerations with MSAL.NET](/en-us/entra/msal/dotnet/acquiring-tokens/desktop-mobile/uwp).

## Configure the application to use the broker

On Android and iOS, brokers enable:

- **Single sign-on (SSO)**: You can use SSO for devices that are registered with Microsoft Entra ID. When you use SSO, your users don't need to sign in to each application.
- **Device identification**: This setting enables conditional-access policies that are related to Microsoft Entra devices. The authentication process uses the device certificate that was created when the device was joined to the workplace.
- **Application identification verification**: When an application calls the broker, it passes its redirect URL. Then the broker verifies it.

### Enable the broker for MSAL for Android

For information about enabling a broker on Android, see [Brokered authentication on Android](msal-android-single-sign-on).

### Enable the broker for MSAL for iOS and macOS

Brokered authentication is enabled by default for Microsoft Entra scenarios in MSAL for iOS and macOS.

The following sections provide instructions to configure your application for brokered authentication support for iOS and macOS. In the two sets of instructions, some of the steps differ.

### Brokered authentication for MSAL for iOS and macOS

Brokered authentication is enabled by default for Microsoft Entra scenarios.

#### Step 1: Update AppDelegate to handle the callback

When MSAL for iOS and macOS calls the broker, the broker calls back to your application by using the `openURL` method. Because MSAL waits for the response from the broker, your application needs to cooperate to call back MSAL. Set up this capability by updating the `AppDelegate.m` file to override the method, as the following code examples show.

```objc
- (BOOL)application:(UIApplication *)app
            openURL:(NSURL *)url
            options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
{
    return [MSALPublicClientApplication handleMSALResponse:url
                                         sourceApplication:options[UIApplicationOpenURLOptionsSourceApplicationKey]];
}
```

```swift
    func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {

        guard let sourceApplication = options[UIApplication.OpenURLOptionsKey.sourceApplication] as? String else {
            return false
        }

        return MSALPublicClientApplication.handleMSALResponse(url, sourceApplication: sourceApplication)
    }
```

If you adopted `UISceneDelegate` on iOS 13 or later, then place the MSAL callback into the `scene:openURLContexts:` of `UISceneDelegate` instead. MSAL `handleMSALResponse:sourceApplication:` must be called only once for each URL.

For more information, see the [Apple documentation](https://developer.apple.com/documentation/uikit/uiscenedelegate/3238059-scene?language=objc).

#### Step 2: Register a URL scheme

MSAL for iOS and macOS uses URLs to invoke the broker and then return the broker response to your app. To finish the round trip, register a URL scheme for your app in the `Info.plist` file.

To register a scheme for your app:

1. Prefix your custom URL scheme with `msauth`.
2. Add your bundle identifier to the end of your scheme. Follow this pattern:

    `$"msauth.(BundleId)"`

    Here, `BundleId` uniquely identifies your device. For example, if `BundleId` is `yourcompany.xforms`, your URL scheme is `msauth.com.yourcompany.xforms`.

    This URL scheme will become part of the redirect URI that uniquely identifies your app when it receives the broker's response. Make sure that the redirect URI in the format `msauth.(BundleId)://auth` is registered for your application.

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>msauth.[BUNDLE_ID]</string>
            </array>
        </dict>
    </array>
    ```

#### Step 3: Add LSApplicationQueriesSchemes

Add `LSApplicationQueriesSchemes` to allow calls to the Microsoft Authenticator app, if it's installed.

Note

The `msauthv3` scheme is needed when your app is compiled by using Xcode 11 and later.

Here's an example of how to add `LSApplicationQueriesSchemes`:

```xml
<key>LSApplicationQueriesSchemes</key>
<array>
  <string>msauthv2</string>
  <string>msauthv3</string>
</array>
```