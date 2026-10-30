---
layout: Conceptual
title: Prepare your iOS (Swift) app for authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-mobile-app-ios-swift-prepare-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: The tutorials provide a step-by-step guide on how to prepare your iOS (Swift) app for authentication.
manager: pmwongera
ms.topic: tutorial
ms.date: 2024-06-27T00:00:00.0000000Z
ms.custom: 
zone_pivot_groups: entra-tenants
locale: en-us
document_id: 1ae69a36-3293-235c-f629-3483bb2026fa
document_version_independent_id: 1ae69a36-3293-235c-f629-3483bb2026fa
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-mobile-app-ios-swift-prepare-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-mobile-app-ios-swift-prepare-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-mobile-app-ios-swift-prepare-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
platformId: 4c6a0398-065e-3378-95b2-72717d3ce226
---

# Prepare your iOS (Swift) app for authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

::: zone pivot="workforce"

This is the second tutorial in the tutorial series that demonstrates how to add Microsoft Authentication Library (MSAL) for iOS and macOS to your iOS Swift app.

Before you begin, use the **Choose a tenant type** selector at the top of this page to select tenant type. Microsoft Entra ID provides two tenant configurations, [workforce](../external-id/tenant-configurations#workforce-tenants) and [external](../external-id/tenant-configurations#external-tenants). A workforce tenant configuration is for your employees, internal apps, and other organizational resources. An external tenant is for your customer-facing apps.

In this tutorial, you:

- Add the MSAL framework to an iOS (Swift) app.
- Create SDK instance.
- Configure Xcode project settings.

## Prerequisites

- Register a new client web app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in any organizational directory and personal Microsoft accounts*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- [Xcode](https://developer.apple.com/xcode/resources/).
- iOS (Swift) project.

## Add a platform redirect URL

To specify your app type to your app registration, follow these steps:

1. Under **Manage**, select **Authentication** &gt; **Add a platform** &gt; **iOS/macOS**.
2. Enter your project's Bundle ID. If downloaded the code sample, the Bundle ID is `com.microsoft.identitysample.MSALiOS`. If you're creating your own project, select your project in Xcode and open the **General** tab. The bundle identifier appears in the **Identity** section.
3. Select **Configure** and save the **MSAL Configuration** that appears in the **MSAL configuration** page so you can enter it when you configure your app later.
4. Select **Done**.

## Add the MSAL framework to an iOS (Swift) app

Choose one of the following ways to install the MSAL library in your app:

### CocoaPods

1. If you're using [CocoaPods](https://cocoapods.org/), install `MSAL` by first creating an empty file called *podfile* in the same folder as your project's *.xcodeproj* file. Add the following to *podfile*:

    ```
    use_frameworks!
    
    target '<your-target-here>' do
       pod 'MSAL'
    end
    ```
2. Replace `<your-target-here>` with the name of your project.
3. In a terminal window, navigate to the folder that contains the *podfile* you created and run `pod install` to install the MSAL library.
4. Close Xcode and open `<your project name>.xcworkspace` to reload the project in Xcode.

### Carthage

If you're using [Carthage](https://github.com/Carthage/Carthage), install `MSAL` by adding it to your *Cartfile*:

```
github "AzureAD/microsoft-authentication-library-for-objc" "master"
```

From a terminal window, in the same directory as the updated *Cartfile*, run the following command to have Carthage update the dependencies in your project.

iOS:

```bash
carthage update --platform iOS
```

macOS:

```bash
carthage update --platform macOS
```

### Manually

You can also use Git Submodule, or check out the latest release to use as a framework in your application.

## Add the app registration

Next, we add your app registration to your code.

First, add the following import statement to the top of the *ViewController.swift* file and either *AppDelegate.swift* or *SceneDelegate.swift*:

```swift
import MSAL
```

Next, add the following code to *ViewController.swift* before to `viewDidLoad()`:

```swift
// Update the below to your client ID. The below is for running the demo only
let kClientID = "Your_Application_Id_Here"
let kGraphEndpoint = "https://graph.microsoft.com/" // the Microsoft Graph endpoint
let kAuthority = "https://login.microsoftonline.com/common" // this authority allows a personal Microsoft account and a work or school account in any organization's Azure AD tenant to sign in

let kScopes: [String] = ["user.read"] // request permission to read the profile of the signed-in user

var accessToken = String()
var applicationContext : MSALPublicClientApplication?
var webViewParameters : MSALWebviewParameters?
var currentAccount: MSALAccount?
```

The only value you modify is the value assigned to `kClientID` to be your [Application ID](developer-glossary#application-client-id). This value is part of the MSAL Configuration data that you saved during the step at the beginning of this tutorial to register the application.

## Create SDK instance

To create MSAL instance in your project, follow these steps:

To the `ViewController` class, add the `initMSAL` method:

```swift
    func initMSAL() throws {

        guard let authorityURL = URL(string: kAuthority) else {
            self.updateLogging(text: "Unable to create authority URL")
            return
        }

        let authority = try MSALAADAuthority(url: authorityURL)

        let msalConfiguration = MSALPublicClientApplicationConfig(clientId: kClientID, redirectUri: nil, authority: authority)
        self.applicationContext = try MSALPublicClientApplication(configuration: msalConfiguration)
        self.initWebViewParams()
    }
```

Still in the `ViewController` class and after the `initMSAL` method, add the `initWebViewParams` method:

### iOS code:

```swift
func initWebViewParams() {
        self.webViewParameters = MSALWebviewParameters(authPresentationViewController: self)
    }
```

### macOS code:

```swift
func initWebViewParams() {
        self.webViewParameters = MSALWebviewParameters()
    }
```

## Configure Xcode project settings

Add a new keychain group to your project **Signing & Capabilities**. The keychain group should be `com.microsoft.adalcache` on iOS and `com.microsoft.identity.universalstorage` on macOS.

![Xcode UI displaying how the keychain group should be set up.](media/guidedsetup-ios-introduction/ios-intro-keychain-share.png)

### For iOS only, configure URL schemes

In this step, you'll register `CFBundleURLSchemes` so that the user can be redirected back to the app after sign in. By the way, `LSApplicationQueriesSchemes` also allows your app to make use of Microsoft Authenticator.

In Xcode, open *Info.plist* as a source code file, and add the following inside of the `<dict>` section. Replace `[BUNDLE_ID]` with the value you previously used. If you downloaded the code, the bundle identifier is `com.microsoft.identitysample.MSALiOS`. If you're creating your own project, select your project in Xcode and open the **General** tab. The bundle identifier appears in the **Identity** section.

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
<key>LSApplicationQueriesSchemes</key>
<array>
    <string>msauthv2</string>
    <string>msauthv3</string>
</array>
```

### For macOS only, configure App Sandbox

1. Go to your Xcode Project Settings &gt; **Capabilities tab** &gt; **App Sandbox**
2. Select **Outgoing Connections (Client)** checkbox.

::: zone-end

::: zone pivot="external"

This is the second tutorial in the tutorial series that demonstrates how to add Microsoft Authentication Library (MSAL) for iOS and macOS to your iOS Swift app.

Before you begin, use the **Choose a tenant type** selector at the top of this page to select tenant type. Microsoft Entra ID provides two tenant configurations, [workforce](../external-id/tenant-configurations#workforce-tenants) and [external](../external-id/tenant-configurations#external-tenants). A workforce tenant configuration is for your employees, internal apps, and other organizational resources. An external tenant is for your customer-facing apps.

In this tutorial, you;

- Add the MSAL framework to an iOS (Swift) app.
- Create SDK instance.

## Prerequisites

- Register a new client web app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in any organizational directory and personal Microsoft accounts*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- [Xcode](https://developer.apple.com/xcode/resources/).
- iOS (Swift) project.

## Add a platform redirect URL

To specify your app type to your app registration, follow these steps:

1. Under **Manage**, select **Authentication** &gt; **Add a platform** &gt; **iOS/macOS**.
2. Enter your project's Bundle ID. If downloaded the code sample, the Bundle ID is `com.microsoft.identitysample.MSALiOS`. If you're creating your own project, select your project in Xcode and open the **General** tab. The bundle identifier appears in the **Identity** section.
3. Select **Configure** and save the **MSAL Configuration** that appears in the **MSAL configuration** page so you can enter it when you configure your app later.
4. Select **Done**.

## Enable public client flow

To identify your app as a public client, follow these steps:

1. Under **Manage**, select **Authentication**.
2. Under **Advanced settings**, for **Allow public client flows**, select **Yes**.
3. Select **Save** to save your changes.

## Add the MSAL framework to an iOS (Swift) app

The MSAL authentication SDK is used for integrating authentication into your apps using standard OAuth2 and OpenID Connect. It allows you to sign in users or apps with Microsoft identities. To add MSAL to your iOS (Swift) project, follow these steps:

1. Open your iOS project in Xcode.
2. Select **Add Package Dependencies...** from the **File** menu.
3. Enter `https://github.com/AzureAD/microsoft-authentication-library-for-objc` as the Package URL and choose **Add Package**

### Update the Bundle Identifier

In Apple ecosystem, a Bundle Identifier is a unique identifier for an application. To update the Bundle Identifier in your project, follow these steps:

1. Open the project settings. In the **Identity** section, enter the **Bundle Identifier**.
2. Right-click **Info.plist** and select **Open As** &gt; **Source Code**.
3. Under the dict root node, replace `Enter_the_bundle_Id_Here` with the ***Bundle Id*** that you used in the portal. Notice the `msauth.` prefix in the string.

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
       <dict>
          <key>CFBundleURLSchemes</key>
          <array>
             <string>msauth.Enter_the_Bundle_Id_Here</string>
          </array>
       </dict>
    </array>
    ```

## Create SDK instance

To create MSAL instance in your project, follow these steps:

1. Import the MSAL library into your view controller by adding `import MSAL` at the top of your `ViewController` class.
2. Add an `applicationContext` member variable to your ViewController class by adding the following code just before the `viewDidLoad()` function:

    ```swift
    var applicationContext : MSALPublicClientApplication?
    var webViewParameters : MSALWebviewParameters?
    ```

    The code declares two variables: `applicationContext`, which stores an instance of `MSALPublicClientApplication`, and `webViewParameters`, which stores an instance of `MSALWebviewParameters`. `MSALPublicClientApplication` is a class provided by the MSAL for handling public client applications. The `MSALWebviewParameters` is a class provided by MSAL that defines parameters for configuring the web view used during the authentication process.
3. Add the following code to the view `viewDidLoad()` function:

    ```swift
     do {
            try self.initMSAL()
        } catch let error {
            self.updateLogging(text: "Unable to create Application Context \(error)")
        }
    ```

    The code attempts to initialize MSAL, handling any errors that occur during the process. If an error occurs, it updates the logging with the details of the error.
4. Add the following code that creates `initMSAL()` function, which initializes MSAL:

    ```swift
        func initMSAL() throws {
    
        guard let authorityURL = URL(string: Configuration.kAuthority) else {
            self.updateLogging(text: "Unable to create authority URL")
            return
        }
    
        let authority = try MSALCIAMAuthority(url: authorityURL)
    
        let msalConfiguration = MSALPublicClientApplicationConfig(clientId: Configuration.kClientID,
                                                                  redirectUri: Configuration.kRedirectUri,
                                                                  authority: authority)
        self.applicationContext = try MSALPublicClientApplication(configuration: msalConfiguration)
    }
    ```

    This code initializes the MSAL for iOS. It first attempts to create a URL for the authority using the provided *Configuration.kAuthority* string. If successful, it creates an MSAL authority object based on that URL. Then, it configures the `MSALPublicClientApplication` with the given client ID, redirect URI, and authority. If all configurations are set up correctly, it initializes the application context with the configured `MSALPublicClientApplication`. If any errors occur during the process, it throws an error.
5. Create *Configuration.swift* file and add the following configurations:

    ```swift
    import Foundation
    
    @objcMembers
    class Configuration {
        static let kTenantSubdomain = "Enter_the_Tenant_Subdomain_Here"
    
        // Update the below to your client ID you received in the portal.
        static let kClientID = "Enter_the_Application_Id_Here"
        static let kRedirectUri = "Enter_the_Redirect_URI_Here"
        static let kProtectedAPIEndpoint = "Enter_the_Protected_API_Full_URL_Here"
        static let kScopes = ["Enter_the_Protected_API_Scopes_Here"]
    
        static let kAuthority = "https://\(kTenantSubdomain).ciamlogin.com"
    
    }
    ```

    This Swift configuration code defines a class named `Configuration` and is marked with `@objcMembers`. It includes static constants for various configuration parameters related to an authentication setup. These parameters include the *tenant subdomain*, *client ID*, *redirect URI*, *protected API endpoint*, and *scopes*. These configuration constants should be updated with appropriate values specific to the application's setup.

    Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the **Application (client) ID** of the app you registered earlier.
    - `Enter_the_Redirect_URI_Here` and replace it with the value of *kRedirectUri* in the MSAL configuration file you downloaded earlier when you added the platform redirect URL.
    - `Enter_the_Protected_API_Scopes_Here` and replace it with the scopes recorded earlier. If you haven't recorded any scopes, you can leave this scope list empty.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't know your tenant subdomain, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).

### Use custom URL domain (Optional)

Use a custom domain to fully brand the authentication URL. From a user perspective, users remain on your domain during the authentication process, rather than being redirected to *ciamlogin.com* domain name.

Use the following steps to use a custom domain:

1. Use the steps in [Enable custom URL domains for apps in external tenants](../external-id/customers/how-to-custom-url-domain) to enable custom URL domain for your external tenant.
2. Open *Configuration.swift* file:

    1. Update the value of the `kAuthority` property to *https://Enter\_the\_Custom\_Domain\_Here/Enter\_the\_Tenant\_ID\_Here*. Replace `Enter_the_Custom_Domain_Here` with your custom URL domain and `Enter_the_Tenant_ID_Here` with your tenant ID. If you don't have your tenant ID, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).

After you make the changes to your *Configuration.swift* file, if your custom URL domain is *login.contoso.com*, and your tenant ID is *aaaabbbb-0000-cccc-1111-dddd2222eeee*, then your file should look similar to the following snippet:

```swift
    import Foundation

    @objcMembers
    class Configuration {
        static let kTenantSubdomain = "login.contoso.com"
        
        // Update the below to your client ID you received in the portal.
        static let kClientID = "Enter_the_Application_Id_Here"
        static let kRedirectUri = "Enter_the_Redirect_URI_Here"
        static let kProtectedAPIEndpoint = "Enter_the_Protected_API_Full_URL_Here"
        static let kScopes = ["Enter_the_Protected_API_Scopes_Here"]
        
        static let kAuthority = "https://\(kTenantSubdomain)/aaaabbbb-0000-cccc-1111-dddd2222eeee"
    
    }
```

## Next steps

::: zone-end