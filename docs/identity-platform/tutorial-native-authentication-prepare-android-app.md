---
layout: Conceptual
title: Prepare your Android mobile app for native authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-prepare-android-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to add Microsoft Authentication Library (MSAL) native auth SDK framework to your Android app.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2024-05-30T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 59c6d851-db8d-e537-3ecf-36eb7b857a63
document_version_independent_id: 59c6d851-db8d-e537-3ecf-36eb7b857a63
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-prepare-android-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-prepare-android-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-prepare-android-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 48605599-30c3-cfa6-23fc-cbc4a9169510
---

# Prepare your Android mobile app for native authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to add Microsoft Authentication Library (MSAL) native authentication SDK to an Android mobile app.

In this tutorial, you:

- Add MSAL dependencies.
- Create a configuration file.
- Create MSAL SDK instance.

## Prerequisites

- If you haven't already, follow the instructions in [Sign in users in sample Android (Kotlin) mobile app by using native authentication](../external-id/customers/how-to-run-native-authentication-sample-android-app)and register an app in your external tenant. Make sure you complete the following steps:
    - Register an application.
    - Enable public client and native authentication flows.
    - Grant API permissions.
    - Create a user flow.
    - Associate the app with the user flow.
- An Android project. If you don't have an Android project, create it.

## Add MSAL dependencies

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
        implementation 'com.microsoft.identity.client:msal:6.+'
        //...
    }
    ```
3. In Android Studio, select **File** &gt; **Sync Project with Gradle Files**.

## Create a configuration file

You pass the required tenant identifiers, such as the application (client) ID, to the MSAL SDK through a JSON configuration setting.

Use these steps to create configuration file:

1. In Android Studio's project pane, navigate to *app\src\main\res*.
2. Right-click **res** and select **New** &gt; **Directory**. Enter `raw` as the new directory name and select **OK**.
3. In *app\src\main\res\raw*, create a new JSON file called `auth_config_native_auth.json`.
4. In the `auth_config_native_auth.json` file, add the following MSAL configurations:

    ```json
    { 
      "client_id": "Enter_the_Application_Id_Here", 
      "authorities": [ 
        { 
          "type": "CIAM", 
          "authority_url": "https://Enter_the_Tenant_Subdomain_Here.ciamlogin.com/Enter_the_Tenant_Subdomain_Here.onmicrosoft.com/" 
        } 
      ], 
      "challenge_types": ["oob"], 
      "logging": { 
        "pii_enabled": false, 
        "log_level": "INFO", 
        "logcat_enabled": true 
      } 
    } 
     //...
    ```
5. Replace the following placeholders with your tenant values that you obtained from the Microsoft Entra admin center:

    - Replace the `Enter_the_Application_Id_Here` placeholder with the application (client) ID of the app you registered earlier.
    - Replace the `Enter_the_Tenant_Subdomain_Here` with the directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-customer-tenant-portal#get-the-customer-tenant-details).

    The challenge types are a list of values, which the app uses to notify Microsoft Entra about the authentication method that it supports.

    - For sign-up and sign-in flows with email one-time passcode, use `["oob"]`.
    - For sign-up and sign-in flows with email and password, use `["oob","password"]`.
    - For self-service password reset (SSPR), use `["oob"]`.

    Learn more [challenge types](concept-native-authentication-challenge-types).

### Optional: Logging configuration

Turn on logging at app creation by creating a logging callback, so the SDK can output logs.

```kotlin
import com.microsoft.identity.client.Logger

fun initialize(context: Context) {
        Logger.getInstance().setExternalLogger { tag, logLevel, message, containsPII ->
            Logs.append("$tag $logLevel $message")
        }
    }
```

To configure the logger, you need to add a section in the configuration file, `auth_config_native_auth.json`:

```json
    //...
   { 
     "logging": { 
       "pii_enabled": false, 
       "log_level": "INFO", 
       "logcat_enabled": true 
     } 
   } 
    //...
```

1. **logcat\_enabled**: Enables the logging functionality of the library.
2. **pii\_enabled**: Specifies whether messages containing personal data, or organizational data are logged. When set to false, logs won't contain personal data. When set to true, the logs might contain personal data.
3. **log\_level**: Use it to decide which level of logging to enable. Android supports the following log levels:
    1. ERROR
    2. WARNING
    3. INFO
    4. VERBOSE

For more information on MSAL logging, see [Logging in MSAL for Android](/en-us/entra/identity-platform/msal-logging-android).

## Create native authentication MSAL SDK instance

In the `onCreate()` method, create an MSAL instance so the app can perform authentication with your tenant through native authentication. The `createNativeAuthPublicClientApplication()` method returns an instance called `authClient`. Pass the JSON configuration file that you created earlier as a parameter.

```kotlin
    //...
    authClient = PublicClientApplication.createNativeAuthPublicClientApplication( 
        this, 
        R.raw.auth_config_native_auth 
    )
    //...
```

Your code should look something similar to the following snippet:

```kotlin
    class MainActivity : AppCompatActivity() { 
        private lateinit var authClient: INativeAuthPublicClientApplication 
 
        override fun onCreate(savedInstanceState: Bundle?) { 
            super.onCreate(savedInstanceState) 
            setContentView(R.layout.activity_main) 
 
            authClient = PublicClientApplication.createNativeAuthPublicClientApplication( 
                this, 
                R.raw.auth_config_native_auth 
            ) 
            getAccountState() 
        } 
 
        private fun getAccountState() {
            CoroutineScope(Dispatchers.Main).launch {
                val accountResult = authClient.getCurrentAccount()
                when (accountResult) {
                    is GetAccountResult.AccountFound -> {
                        displaySignedInState(accountResult.resultValue)
                    }
                    is GetAccountResult.NoAccountFound -> {
                        displaySignedOutState()
                    }
                }
            }
        } 
 
        private fun displaySignedInState(accountResult: AccountState) { 
            val accountName = accountResult.getAccount().username 
            val textView: TextView = findViewById(R.id.accountText) 
            textView.text = "Cached account found: $accountName" 
        } 
 
        private fun displaySignedOutState() { 
            val textView: TextView = findViewById(R.id.accountText) 
            textView.text = "No cached account found" 
        } 
    } 
```

- Retrieve the cached account by using the `getCurrentAccount()`, which returns an object, `accountResult`.
- If an account is found in persistence, use `GetAccountResult.AccountFound` to display a signed-in state.
- Otherwise, use `GetAccountResult.NoAccountFound` to display a signed-out state.

Make sure you include the import statements. Android Studio should include the import statements for you automatically.