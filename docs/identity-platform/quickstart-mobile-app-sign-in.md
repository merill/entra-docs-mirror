---
layout: Conceptual
title: Quickstart - Sign in users in a sample mobile app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-mobile-app-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Quickstart for configuring a sample mobile app to sign in employees or customers with Microsoft identity platform.
manager: pmwongera
ms.topic: quickstart
ms.date: 2024-10-30T00:00:00.0000000Z
zone_pivot_groups: entra-tenants
locale: en-us
document_id: e9a999e1-15cf-c681-c3a5-67ecc761fbb6
document_version_independent_id: e9a999e1-15cf-c681-c3a5-67ecc761fbb6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-mobile-app-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-mobile-app-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-mobile-app-sign-in.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 86a21906-9fd9-ab3c-2ac7-aab2a78509e9
---

# Quickstart - Sign in users in a sample mobile app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Before you begin, use the **Choose a tenant type** selector at the top of this page to select tenant type. Microsoft Entra ID provides two tenant configurations, [workforce](../external-id/tenant-configurations#workforce-tenants) and [external](../external-id/tenant-configurations#external-tenants). A workforce tenant configuration is for your employees, internal apps, and other organizational resources. An external tenant is for your customer-facing apps.

::: zone pivot="workforce"

# [Android](#tab/android-workforce)
In this quickstart, you download and run a code sample that demonstrates how an Android application can sign in users and get an access token to call the Microsoft Graph API.

Applications must be represented by an app object in Microsoft Entra ID so that the Microsoft identity platform can provide tokens to your application.

# [iOS/macOS](#tab/ios-macos-workforce)
In this quickstart, you download and run a code sample that demonstrates how a native iOS or macOS application can sign in users and get an access token to call the Microsoft Graph API.

The quickstart applies to both iOS and macOS apps. Some steps are needed only for iOS apps and will be indicated as such.

---

## Prerequisites

- An Azure account with an active subscription. If you don't already have one, [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- This Azure account must have permissions to manage applications. Any of the following Microsoft Entra roles include the required permissions:
    - Application Administrator
    - Application Developer
- A workforce tenant. You can use your Default Directory or [set up a new tenant](quickstart-create-new-tenant).

# [Android](#tab/android-workforce)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in any organizational directory and personal Microsoft accounts*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Android Studio
- Android 16+

# [iOS/macOS](#tab/ios-macos-workforce)
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- XCode 10+
- iOS 10+
- macOS 10.12+

---

## Add a redirect URI

You must configure specific redirect URIs in your app registration to ensure compatibility with the downloaded code sample. These URIs are essential for redirecting users back to the app after they successfully sign in.

# [Android](#tab/android-workforce)
1. Under **Manage**, select **Authentication** &gt; **Add a platform** &gt; **Android**.
2. Enter your project's Package Name based on the sample type you downloaded above.

    - Java sample - `com.azuresamples.msalandroidapp`
    - Kotlin sample - `com.azuresamples.msalandroidkotlinapp`
3. In the **Signature hash** section of the **Configure your Android app** pane, select **Generating a development Signature Hash.** and copy the KeyTool command to your command line.

    - KeyTool.exe is installed as part of the Java Development Kit (JDK). You must also install the OpenSSL tool to execute the KeyTool command. For more information, see [Android documentation on generating a key](https://developer.android.com/studio/publish/app-signing#generate-key) for more information.
4. Enter the **Signature hash** generated by KeyTool.
5. Select **Configure** and save the **MSAL Configuration** that appears in the **Android configuration** pane so you can enter it when you configure your app later.
6. Select **Done**.

# [iOS/macOS](#tab/ios-macos-workforce)
1. Under **Manage**, select **Authentication** &gt; **Add Platform** &gt; **iOS**.
2. Enter the **Bundle Identifier** for your application. The bundle identifier is a unique string that uniquely identifies your application, for example `com.<yourname>.identitysample.MSALMacOS`. Make a note of the value you use. Note that the iOS configuration is also applicable to macOS applications.
3. Select **Configure** and save the **MSAL Configuration** details for later in this quickstart.
4. Select **Done**.

---

## Download the sample app

# [Android](#tab/android-workforce)
- Java: [Download the code](https://github.com/Azure-Samples/ms-identity-android-java/archive/master.zip).
- Kotlin: [Download the code](https://github.com/Azure-Samples/ms-identity-android-kotlin/archive/master.zip).

# [iOS/macOS](#tab/ios-macos-workforce)
Download the sample project

- [Download the code sample for iOS](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip)
- [Download the code sample for macOS](https://github.com/Azure-Samples/active-directory-macOS-swift-native-v2/archive/master.zip)

### Install dependencies

1. Extract the zip file.
2. In a terminal window, navigate to the folder with the downloaded code sample and run `pod install` to install the latest MSAL library.

---

## Configure the sample application

# [Android](#tab/android-workforce)
1. In Android Studio's project pane, navigate to **app\src\main\res**.
2. Right-click **res** and choose **New** &gt; **Directory**. Enter `raw` as the new directory name and select **OK**.
3. In **app** &gt; **src** &gt; **main** &gt; **res** &gt; **raw**, go to JSON file called `auth_config_single_account.json` and paste the MSAL Configuration that you saved earlier.

    Below the redirect URI, paste:

    ```json
      "account_mode" : "SINGLE",
    ```

    Your config file should resemble this example:

    ```json
    {
      "client_id": "00001111-aaaa-bbbb-3333-cccc4444",
      "authorization_user_agent": "WEBVIEW",
      "redirect_uri": "msauth://com.azuresamples.msalandroidapp/00001111%cccc4444%3D",
      "broker_redirect_uri_registered": false,
      "account_mode": "SINGLE",
      "authorities": [
        {
          "type": "AAD",
          "audience": {
            "type": "AzureADandPersonalMicrosoftAccount",
            "tenant_id": "common"
          }
        }
      ]
    }
    ```
4. Open */app/src/main/AndroidManifest.xml* file.
5. Find the placeholder:

    - `enter_the_signature_hash` and replace it with the **Signature Hash** that you generated earlier when you added the platform redirect URL.

    As this tutorial only demonstrates how to configure an app in Single Account mode, see [single vs. multiple account mode](single-multi-account) and [configuring your app](msal-configuration) for more information

## Run the sample app

Select your emulator, or physical device, from Android Studio's **available devices** dropdown and run the app.

The sample app starts on the **Single Account Mode** screen. A default scope, **user.read**, is provided by default, which is used when reading your own profile data during the Microsoft Graph API call. The URL for the Microsoft Graph API call is provided by default. You can change both of these if you wish.

![Screenshot of the MSAL sample app showing single and multiple account usage.](media/quickstart-v2-android/quickstart-sample-app.png)

Use the app menu to change between single and multiple account modes.

In single account mode, sign in using a work or home account:

1. Select **Get graph data interactively** to prompt the user for their credentials. You'll see the output from the call to the Microsoft Graph API in the bottom of the screen.
2. Once signed in, select **Get graph data silently** to make a call to the Microsoft Graph API without prompting the user for credentials again. You'll see the output from the call to the Microsoft Graph API in the bottom of the screen.

In multiple account mode, you can repeat the same steps. Additionally, you can remove the signed-in account, which also removes the cached tokens for that account.

# [iOS/macOS](#tab/ios-macos-workforce)
If you selected Option 1 above, you can skip these steps.

1. Open the project in XCode.
2. Edit **ViewController.swift** and replace the line starting with 'let kClientID' with the following code snippet. Remember to update the value for `kClientID` with the clientID that you saved when you registered your app earlier in this quickstart:

    ```swift
    let kClientID = "Enter_the_Application_Id_Here"
    ```
3. If you're building an app for [Microsoft Entra national clouds](/en-us/graph/deployments#app-registration-and-token-service-root-endpoints), replace the line starting with 'let kGraphEndpoint' and 'let kAuthority' with correct endpoints. For global access, use default values:

    ```swift
    let kGraphEndpoint = "https://graph.microsoft.com/"
    let kAuthority = "https://login.microsoftonline.com/common"
    ```
4. Other endpoints are documented [here](/en-us/graph/deployments#app-registration-and-token-service-root-endpoints). For example, to run the quickstart with Microsoft Entra Germany, use following:

    ```swift
    let kGraphEndpoint = "https://graph.microsoft.de/"
    let kAuthority = "https://login.microsoftonline.de/common"
    ```
5. Open the project settings. In the **Identity** section, enter the **Bundle Identifier**.
6. Right-click **Info.plist** and select **Open As** &gt; **Source Code**.
7. Under the dict root node, replace `Enter_the_bundle_Id_Here` with the ***Bundle Id*** that you used in the portal. Notice the `msauth.` prefix in the string.

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
8. Build and run the app!

---

## How the sample works

# [Android](#tab/android-workforce)
![Diagram showing how the sample app generated by this quickstart works.](media/quickstart-v2-android/android-intro.svg)

The code is organized into fragments that show how to write a single and multiple accounts MSAL app. The code files are organized as follows:

| File | Demonstrates |
| --- | --- |
| MainActivity | Manages the UI |
| MSGraphRequestWrapper | Calls the Microsoft Graph API using the token provided by MSAL |
| MultipleAccountModeFragment | Initializes a multi-account application, loads a user account, and gets a token to call the Microsoft Graph API |
| SingleAccountModeFragment | Initializes a single-account application, loads a user account, and gets a token to call the Microsoft Graph API |
| res/auth\_config\_multiple\_account.json | The multiple account configuration file |
| res/auth\_config\_single\_account.json | The single account configuration file |
| Gradle Scripts/build.grade (Module:app) | The MSAL library dependencies are added here |

We'll now look at these files in more detail and call out the MSAL-specific code in each.

# [iOS/macOS](#tab/ios-macos-workforce)
![Diagram showing how the sample app generated by this quickstart works.](media/quickstart-v2-ios/ios-intro.svg)

---

::: zone-end

::: zone pivot="external"

The quickstart guides you in configuring sample Android, .NET MAUI Android, and iOS/macOS apps to sign in users by registering applications, setting up redirect URLs, updating configurations, and testing the app.

## Prerequisites

- An Azure account with an active subscription. If you don't already have one, [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- This Azure account must have permissions to manage applications. Any of the following Microsoft Entra roles include the required permissions:
    - Application Administrator
    - Application Developer
- An external tenant. To create one, choose from the following methods:
    - Use the [Microsoft Entra External ID extension](https://aka.ms/ciamvscode/samples/marketplace) to set up an external tenant directly in Visual Studio Code. *(Recommended)*
    - [Create a new external tenant](../external-id/customers/how-to-create-external-tenant-portal) in the Microsoft Entra admin center.
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID

# [Android](#tab/android-external)
- [Android Studio](https://developer.android.com/studio).

# [Android(.NET MAUI)](#tab/android-netmaui-external)
- A user flow. For more information, refer to [create self-service sign-up user flows for apps in external tenants](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers). This user flow can be used for multiple applications.
- [Add your application to the user flow](/en-us/entra/external-id/customers/how-to-user-flow-add-application).
- [.NET 7.0 SDK](https://dotnet.microsoft.com/download/dotnet/7.0)
- [Visual Studio 2022](https://aka.ms/vsdownloads)with the MAUI workload installed:
    - [Instructions for Windows](/en-us/dotnet/maui/get-started/installation?tabs=vswin)
    - [Instructions for macOS](/en-us/dotnet/maui/get-started/installation?tabs=vsmac)

# [iOS/macOS](#tab/ios-macos-external)
- [Xcode](https://developer.apple.com/xcode/resources/).

---

## Add a platform redirect URL

You must configure specific redirect URIs in your app registration to ensure compatibility with the downloaded code sample. These URIs are essential for redirecting users back to the app after they successfully sign in.

# [Android](#tab/android-external)
To specify your app type to your app registration, follow these steps:

1. Under **Manage**, select **Authentication**.
2. On the **Platform configurations** page, select **Add a platform**, and then select **Android** option.
3. Enter your project's Package Name. If you downloaded the [sample code](https://github.com/Azure-Samples/ms-identity-ciam-browser-delegated-android-sample), this value is `com.azuresamples.msaldelegatedandroidkotlinsampleapp`.
4. In the **Signature hash** section of the **Configure your Android app** pane, select **Generating a development Signature Hash. This will change for each development environment.** Copy and run the KeyTool command for your operating system in your Terminal.
5. Enter the **Signature hash** generated by KeyTool.
6. Select **Configure**.
7. Copy the **MSAL Configuration** from the **Android configuration** pane and save it for later app configuration.
8. Select **Done**.

## Enable public client flow

To identify your app as a public client, follow these steps:

1. Under **Manage**, select **Authentication**.
2. Under **Advanced settings**, for **Allow public client flows**, select **Yes**.
3. Select **Save** to save your changes.

# [Android(.NET MAUI)](#tab/android-netmaui-external)
To specify your app type to your app registration, follow these steps:

1. Under **Manage**, select **Authentication**.
2. On the **Platform configurations** page, select **Add a platform**, and then select **Mobile and Desktop applications** option.
3. For the **Redirect URIs** enter `msal{client_id}://auth`. Ensure that the `{client_id}` matches the value of your app registration. Select **Configure**.
4. Select **Save** to save the changes.

# [iOS/macOS](#tab/ios-macos-external)
To specify your app type to your app registration, follow these steps:

1. Under **Manage**, select **Authentication**.
2. On the **Platform configurations** page, select **Add a platform**, and then select **iOS / macOS** option.
3. Enter your project's Bundle ID. If you downloaded the [sample code](https://github.com/Azure-Samples/ms-identity-ciam-browser-delegated-ios-sample.git), this value is `com.microsoft.identitysample.ciam.MSALiOS`.
4. Select **Configure** and save the **MSAL Configuration** that appears in the **iOS / macOS configuration** pane so you can enter it when you configure your app later.
5. Select **Done**.

## Enable public client flow

To identify your app as a public client, follow these steps:

1. Under **Manage**, select **Authentication**.
2. Under **Advanced settings**, for **Allow public client flows**, select **Yes**.
3. Select **Save** to save your changes.

---

## Clone sample application

# [Android](#tab/android-external)
To obtain the sample application, you can either clone it from GitHub or [download it as a .zip file](https://github.com/Azure-Samples/ms-identity-ciam-browser-delegated-android-sample/archive/refs/heads/main.zip).

- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-browser-delegated-android-sample
    ```

# [Android(.NET MAUI)](#tab/android-netmaui-external)
To get the .NET MAUI Android application sample code, [download the .zip file](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/archive/refs/heads/main.zip) or clone the sample .NET MAUI Android application from GitHub by running the following command:

```bash
git clone https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial.git
```

# [iOS/macOS](#tab/ios-macos-external)
To obtain the sample application, you can either clone it from GitHub or download it as a .zip file.

- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-browser-delegated-ios-sample.git
    ```

---

## Configure the sample application

# [Android](#tab/android-external)
To enable authentication and access to Microsoft Graph resources, configure the sample by following these steps:

1. In Android Studio, open the project that you cloned.
2. Open */app/src/main/res/raw/auth\_config\_ciam.json* file.
3. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the **Application (client) ID** of the app you registered earlier.
    - `Enter_the_Redirect_Uri_Here` and replace it with the value of *redirect\_uri* in the Microsoft Authentication Library (MSAL) configuration file you downloaded earlier when you added the platform redirect URL.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't know your tenant subdomain, learn how to [read your tenant details](../external-id/customers/how-to-create-customer-tenant-portal#get-the-customer-tenant-details).
4. Open */app/src/main/AndroidManifest.xml* file.
5. Find the placeholder:

    - `ENTER_YOUR_SIGNATURE_HASH_HERE` and replace it with the **Signature Hash** that you generated earlier when you added the platform redirect URL.
6. Open */app/src/main/java/com/azuresamples/msaldelegatedandroidkotlinsampleapp/MainActivity.kt* file.
7. Find property named `scopes` and set the scopes recorded in [Grant admin consent](quickstart-register-app#grant-admin-consent-external-tenants-only). If you haven't recorded any scopes, you can leave this scope list empty.

    ```kotlin
    private const val scopes = "" // Developers should set the respective scopes of their Microsoft Graph resources here. For example, private const val scopes = "api://{clientId}/{ToDoList.Read} api://{clientId}/{ToDoList.ReadWrite}"
    ```

You've configured the app and it's ready to run.

# [Android(.NET MAUI)](#tab/android-netmaui-external)
1. In Visual Studio, open *ms-identity-ciam-dotnet-tutorial-main/1-Authentication/2-sign-in-maui/appsettings.json* file.
2. Find the placeholder:
    1. `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
    2. `Enter_the_Application_Id_Here` and replace it with the **Application (client) ID** of the app you registered earlier.
3. In Visual Studio, open *ms-identity-ciam-dotnet-tutorial-main/1-Authentication/2-sign-in-maui/Platforms/Android/AndroidManifest.xml* file.
4. Find the placeholder:
    1. `Enter_the_Application_Id_Here` and replace it with the **Application (client) ID** of the app you registered earlier.

# [iOS/macOS](#tab/ios-macos-external)
To enable authentication and access to Microsoft Graph resources, configure the sample by following these steps:

1. In Xcode, open the project that you cloned.
2. Open */MSALiOS/Configuration.swift* file.
3. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the **Application (client) ID** of the app you registered earlier.
    - `Enter_the_Redirect_URI_Here` and replace it with the value of *kRedirectUri* in the Microsoft Authentication Library (MSAL) configuration file you downloaded earlier when you added the platform redirect URL.
    - `Enter_the_Protected_API_Scopes_Here` and replace it with the scopes recorded in [Grant admin consent](quickstart-register-app#grant-admin-consent-external-tenants-only). If you haven't recorded any scopes, you can leave this scope list empty.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't know your tenant subdomain, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).

You've configured the app and it's ready to run.

---

## Run and test the sample app

# [Android](#tab/android-external)
To build and run your app, follow these steps:

1. In the toolbar, select your app from the run configurations menu.
2. In the target device menu, select the device that you want to run your app on.

    If you don't have any devices configured, you need to either create an Android Virtual Device to use the Android Emulator or connect a physical Android device.
3. Select the **Run** button.
4. Select **Acquire Token Interactively** to request an access token.
5. If you select **API - Perform GET** to call a protected ASP.NET Core web API, you will get an error.

For more information about calling a protected web API, see our next steps

# [Android(.NET MAUI)](#tab/android-netmaui-external)
.NET MAUI apps are designed to run on multiple operating systems and devices. You'll need to select which target you want to test and debug your app with.

Set the **Debug Target** in the Visual Studio toolbar to the device you want to debug and test with. The following steps demonstrate setting the **Debug Target** to *Android*:

1. Select **Debug Target** drop-down.
2. Select **Android Emulators**.
3. Select emulator device.

Run the app by pressing *F5* or select the *play button* at the top of Visual Studio.

1. You can now test the sample .NET MAUI Android app. After you run the app, the Android app window appears in an emulator:

    ![Screenshot of the sign-in button in the Android application.](media/how-to-mobile-app-maui-sample-sign-in/maui-android-sign-in.jpg)
2. On the Android window that appears, select the **Sign In** button. A browser window opens, and you're prompted to sign in.

    ![Screenshot of user prompt to enter credential in Android application.](media/how-to-mobile-app-maui-sample-sign-in/maui-android-sign-in-prompt.jpg)

    During the sign in process, you're prompted to grant various permissions (to allow the application to access your data). Upon successful sign in and consent, the application screen displays the main page.

    ![Screenshot of the main page in the Android application after signing in.](media/how-to-mobile-app-maui-sample-sign-in/maui-android-after-sign-in.png)

# [iOS/macOS](#tab/ios-macos-external)
To build and run your app, follow these steps:

1. To build and run your code, select **Run** from the **Product** menu in Xcode. After a successful build, Xcode will launch the sample app in the Simulator.
2. Select **Acquire Token Interactively** to request an access token.
3. If you select **API - Perform GET** to call a protected ASP.NET Core web API, you will get an error.

For more information about calling a protected web API, see our Next steps

---

## Next steps

# [Android](#tab/android-external)
- [Sign in users and call a protected web API in sample Android (Kotlin) app](../external-id/customers/sample-mobile-app-android-kotlin-sign-in-call-api).

# [Android(.NET MAUI)](#tab/android-netmaui-external)
- [Customize the default branding](../external-id/customers/how-to-customize-branding-customers).
- [Configure sign-in with Google](../external-id/customers/how-to-google-federation-customers).

# [iOS/macOS](#tab/ios-macos-external)
- [Sign in users and call a protected web API in sample iOS (Swift) app](../external-id/customers/sample-mobile-app-ios-swift-sign-in-call-api).

---

::: zone-end