---
layout: Conceptual
title: Sign in users in an Android app by using Microsoft identity platform - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-mobile-app-android-prepare-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Set up an Android app project that signs in users into customer facing app by in an external tenant or employees in a workforce tenant
manager: pmwongera
ms.topic: tutorial
ms.date: 2025-09-30T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: f551b62d-67f9-d23f-3b8a-dde502487fdb
document_version_independent_id: f551b62d-67f9-d23f-3b8a-dde502487fdb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-mobile-app-android-prepare-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-mobile-app-android-prepare-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-mobile-app-android-prepare-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: da091667-6bd3-6aab-5ec9-599a2c790013
---

# Sign in users in an Android app by using Microsoft identity platform - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial you how to add Microsoft Authentication Library (MSAL) for Android to your Android app. MSAL enables Android applications to authenticate users with Microsoft Entra.

In this tutorial you'll;

- Add MSAL dependency
- Add configuration
- Create MSAL SDK instance

## Prerequisites

# [Workforce tenant](#tab/workforce-tenant)
- A workforce tenant. You can use your [Default Directory](quickstart-create-new-tenant) or set up a new tenant.
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- An Android project. If you don't have an Android project, create it.

# [External tenant](#tab/external-tenant)
- An external tenant. To create one, choose from the following methods:
    - Use the [Microsoft Entra External ID extension](https://aka.ms/ciamvscode/samples/marketplace) to set up an external tenant directly in Visual Studio Code. *(Recommended)*
    - [Create a new external tenant](../external-id/customers/how-to-create-external-tenant-portal) in the Microsoft Entra admin center.
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in any organizational directory and personal Microsoft accounts*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID

---

## Add a redirect URI

You must configure specific redirect URIs in your app registration to ensure compatibility with the downloaded code sample. These URIs are essential for redirecting users back to the app after they successfully sign in.

# [Workforce tenant](#tab/workforce-tenant)
1. Under **Manage**, select **Authentication** &gt; **Add a platform** &gt; **Android**.
2. Enter your project's Package Name based on the sample type you downloaded above.

    - Java sample - `com.azuresamples.msalandroidapp`
    - Kotlin sample - `com.azuresamples.msalandroidkotlinapp`
3. In the **Signature hash** section of the **Configure your Android app** pane, select **Generating a development Signature Hash.** and copy the KeyTool command to your command line.

    - KeyTool.exe is installed as part of the Java Development Kit (JDK). You must also install the OpenSSL tool to execute the KeyTool command. For more information, see [Android documentation on generating a key](https://developer.android.com/studio/publish/app-signing#generate-key) for more information.
4. Enter the **Signature hash** generated by KeyTool.
5. Select **Configure** and save the **MSAL Configuration** that appears in the **Android configuration** pane so you can enter it when you configure your app later.
6. Select **Done**.

# [External tenant](#tab/external-tenant)
To specify your app type to your app registration, follow these steps:

1. Under **Manage**, select **Authentication**.
2. On the **Platform configurations** page, select **Add a platform**, and then select **Android** option.
3. Enter your project's Package Name. If you downloaded the [sample code](https://github.com/Azure-Samples/ms-identity-ciam-browser-delegated-android-sample), this value is `com.azuresamples.msaldelegatedandroidkotlinsampleapp`.
4. In the **Signature hash** section of the **Configure your Android app** pane, select **Generating a development Signature Hash. This will change for each development environment.** Copy and run the KeyTool command for your operating system in your Terminal.
5. Enter the **Signature hash** generated by KeyTool.
6. Select **Configure**.
7. Copy the **MSAL Configuration** from the **Android configuration** pane and save it for later app configuration.
8. Select **Done**.

### Enable public client flow

To identify your app as a public client, follow these steps:

1. Under **Manage**, select **Authentication**.
2. Under **Advanced settings**, for **Allow public client flows**, select **Yes**.
3. Select **Save** to save your changes.

---

## Add MSAL dependency and relevant libraries to your project

To add MSAL dependencies in your Android project, follow these steps:

1. Open your project in Android Studio or create a new project.
2. Open your application's `build.gradle` and add the following dependencies:

    ```gradle
    allprojects {
    repositories {
        //Needed for com.microsoft.device.display:display-mask library
        maven {
            url 'https://pkgs.dev.azure.com/MicrosoftDeviceSDK/DuoSDK-Public/_packaging/Duo-SDK-Feed/maven/v1'
            name 'Duo-SDK-Feed'
        }
        mavenCentral()
        google()
        }
    }
    //...
    
    dependencies { 
        implementation 'com.microsoft.identity.client:msal:5.+'
        //...
    }
    ```

    In the `build.gradle` configuration, repositories are defined for project dependencies. It includes a Maven repository URL for the `com.microsoft.device.display:display-mask` library from Azure DevOps. Additionally, it utilizes Maven Central and Google repositories. The dependencies section specifies the implementation of the MSAL version 5 and potentially other dependencies.
3. In Android Studio, select **File** &gt; **Sync Project with Gradle Files**.

## Add configuration

You pass the required tenant identifiers, such as the application (client) ID, to the MSAL SDK through a JSON configuration setting.

Use these steps to create configuration file:

# [Workforce tenant configuration](#tab/workforce-tenant)
1. In Android Studio's project pane, navigate to **app\src\main\res**.
2. Right-click **res** and choose **New** &gt; **Directory**. Enter `raw` as the new directory name and select **OK**.
3. In **app** &gt; **src** &gt; **main** &gt; **res** &gt; **raw**, create a new JSON file called `auth_config_single_account.json` and paste the MSAL Configuration that you saved earlier.

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
      "broker_redirect_uri_registered": true,
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

    As this tutorial only demonstrates how to configure an app in Single Account mode, see [single vs. multiple account mode](single-multi-account) and [configuring your app](msal-configuration) for more information
4. We recommend using 'WEBVIEW'. In case you want to configure "authorization\_user\_agent" as 'BROWSER' in your app, you need make the following updates. a) Update auth\_config\_single\_account.json with "authorization\_user\_agent": "Browser". b) Update AndroidManifest.xml. In the app go to **app** &gt; **src** &gt; **main** &gt; **AndroidManifest.xml**, add the `BrowserTabActivity` activity as a child of the `<application>` element. This entry allows Microsoft Entra ID to call back to your application after it completes the authentication:

    ```xml
    <!--Intent filter to capture System Browser or Authenticator calling back to our app after sign-in-->
    <activity
        android:name="com.microsoft.identity.client.BrowserTabActivity"
        android:exported="true">
        <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="msauth"
                android:host="Enter_the_Package_Name"
                android:path="/Enter_the_Signature_Hash" />
        </intent-filter>
    </activity>
    ```

    - Use the **Package name** to replace `android:host=.` value. It should look like `com.azuresamples.msalandroidapp`.
    - Use the **Signature Hash** to replace `android:path=` value. Ensure that there's a leading `/` at the beginning of your Signature Hash. It should look like `/aB1cD2eF3gH4+iJ5kL6-mN7oP8q=`.

    You can find these values in the Authentication blade of your app registration as well.

# [External tenant configuration](#tab/external-tenant)
1. In Android Studio's project pane, navigate to *app\src\main\res*.
2. Right-click **res** and select **New** &gt; **Directory**. Enter `raw` as the new directory name and select **OK**.
3. In *app\src\main\res\raw*, create a new JSON file called `auth_config_ciam_auth.json`.
4. In the `auth_config_ciam_auth.json` file, add the following MSAL configurations:

    ```json
    {
      "client_id" : "Enter_the_Application_Id_Here",
      "authorization_user_agent" : "DEFAULT",
      "redirect_uri" : "Enter_the_Redirect_Uri_Here",
      "account_mode" : "SINGLE",
      "authorities" : [
        {
          "type": "CIAM",
          "authority_url": "https://Enter_the_Tenant_Subdomain_Here.ciamlogin.com/Enter_the_Tenant_Subdomain_Here.onmicrosoft.com/"
        }
      ]
    }
    ```

    The JSON configuration file specifies various settings for an Android application. It includes the client ID, authorization user agent, redirect URI, and account mode. Additionally, it defines an authority for authentication, specifying the type and authority URL.

    Replace the following placeholders with your tenant values that you obtained from the Microsoft Entra admin center:

    - `Enter_the_Application_Id_Here` and replace it with the **Application (client) ID** of the app you registered earlier.
    - `Enter_the_Redirect_Uri_Here` and replace it with the value of *redirect\_uri* in the Microsoft Authentication Library (MSAL) configuration file you downloaded earlier when you added the platform redirect URL.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't know your tenant subdomain, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
5. Open */app/src/main/AndroidManifest.xml* file.
6. In *AndroidManifest.xml*, add the following data specification to an intent filter:

    ```xml
    <data
        android:host="ENTER_YOUR_PROJECT_PACKAGE_NAME_HERE"
        android:path="/ENTER_YOUR_SIGNATURE_HASH_HERE"
        android:scheme="msauth" />
    ```

    Find the placeholder:

    - `ENTER_YOUR_PROJECT_PACKAGE_NAME_HERE` and replace it with your Android's project package name.
    - `ENTER_YOUR_SIGNATURE_HASH_HERE` and replace it with the Signature Hash that you generated earlier when you added the platform redirect URL.

### Use custom URL domain (Optional)

Use a custom domain to fully brand the authentication URL. From a user perspective, users remain on your domain during the authentication process, rather than being redirected to *ciamlogin.com* domain name.

Use the following steps to use a custom domain:

1. Use the steps in [Enable custom URL domains for apps in external tenants](../external-id/customers/how-to-custom-url-domain) to enable custom URL domain for your external tenant.
2. Open *auth\_config\_ciam\_auth.json* file:

    1. Update the value of the `authority_url` property to *https://Enter\_the\_Custom\_Domain\_Here/Enter\_the\_Tenant\_ID\_Here*. Replace `Enter_the_Custom_Domain_Here` with your custom URL domain and `Enter_the_Tenant_ID_Here` with your tenant ID. If you don't have your tenant ID, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
    2. Add `knownAuthorities` property with a value *[Enter\_the\_Custom\_Domain\_Here]*.

After you make the changes to your *auth\_config\_ciam\_auth.json* file, if your custom URL domain is *login.contoso.com*, and your tenant ID is *aaaabbbb-0000-cccc-1111-dddd2222eeee*, then your file should look similar to the following snippet:

```json
{
    "client_id" : "Enter_the_Application_Id_Here",
    "authorization_user_agent" : "DEFAULT",
    "redirect_uri" : "Enter_the_Redirect_Uri_Here",
    "account_mode" : "SINGLE",
    "authorities" : [
    {
        "type": "CIAM",
        "authority_url": "https://login.contoso.com/aaaabbbb-0000-cccc-1111-dddd2222eeee",
        "knownAuthorities": ["login.contoso.com"]
    }
    ]
}
```

---

## Create MSAL SDK instance

To initialize MSAL SDK instance, use the following code:

# [Workforce tenant configuration](#tab/workforce-tenant)
```java
PublicClientApplication.createSingleAccountPublicClientApplication(
    getContext(),
    R.raw.auth_config_single_account,
    new IPublicClientApplication.ISingleAccountApplicationCreatedListener() {
        @Override
        public void onCreated(ISingleAccountPublicClientApplication application) {
            // Initialize the single account application instance
            mSingleAccountApp = application;
            loadAccount();
        }

        @Override
        public void onError(MsalException exception) {
            // Handle any errors that occur during initialization
            displayError(exception);
        }
    }
);
```

This code creates a single account public client application using the configuration file auth\_config\_single\_account.json. When the application is successfully created, it assigns the instance to `mSingleAccountApp` and calls the `loadAccount()` method. If an error occurs during the creation, it handles the error by calling the displayError(exception) method.

# [External tenant configuration](#tab/external-tenant)
```kotlin
private suspend fun initClient(): ISingleAccountPublicClientApplication = withContext(Dispatchers.IO) {
    return@withContext PublicClientApplication.createSingleAccountPublicClientApplication(
        this@MainActivity,
        R.raw.auth_config_ciam_auth
    )
}
```

The code initializes a single account public client application asynchronously. It uses the provided authentication configuration file and runs on the I/O dispatcher.

---

Make sure you include the import statements. Android Studio should include the import statements for you automatically.