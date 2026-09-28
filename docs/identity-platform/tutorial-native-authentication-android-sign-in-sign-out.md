---
layout: Conceptual
title: Add sign-in in Android app by using native authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-android-sign-in-sign-out
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to add sign-in and sign-out with email one-time passcode or username and password in Android app by using native authentication.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2025-11-17T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: dd4631dd-89eb-49ab-0c1c-58676496a417
document_version_independent_id: dd4631dd-89eb-49ab-0c1c-58676496a417
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-android-sign-in-sign-out.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-android-sign-in-sign-out
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-android-sign-in-sign-out.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: fc67d95c-b61a-1f5b-de71-4de71eb4da44
---

# Add sign-in in Android app by using native authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to sign-in and sign-out a user with email one-time passcode or username and password in your Android mobile app by using native authentication.

In this tutorial, you:

- Sign in a user using email one-time passcode or username (email) and password.
- Sign out a user.
- Handle sign-in error

## Prerequisites

- Complete the steps in [Tutorial: Prepare your Android app for native authentication](tutorial-native-authentication-android-sign-up). This tutorial shows you how to prepare your Android project or app for native authentication.

## Sign in a user

To sign in a user using the one-time passcode, collect the email and send an email containing a one-time passcode for the user to verify their email. When the user enters a valid one-time passcode, the app signs them in.

To sign in a user using username (email) and password, collect the email and password from the user. If the username and password are valid, the app signs in the user.

If the **Username** built-in user attribute is enabled in your tenant's sign-up user flow, the `username` parameter in sign-in accepts either the user's email address or their username (alias). No separate sign-in logic is needed to support alias-based sign-in.

To sign in a user, you need to:

1. Create a user interface (UI) to:

    - Collect an email from the user. Add validation to your inputs to make sure the user enters a valid emails address.
    - Collect a password if you sign in with username (email) and password.
    - Collect an email one-time passcode from the user if you sign in with email one-time passcode.
    - Resend one-time passcode (recommended) if you sign in with email one-time passcode.
2. In your UI, add a button, whose select event starts a sign-in as shown in the following code snippet:

    ```kotlin
     CoroutineScope(Dispatchers.Main).launch {
         val parameters = NativeAuthSignInParameters(username = email)
         // Assign 'password' param if you sign in with username (email) and password
         // parameters.password = password
         val actionResult: SignInResult = authClient.signIn(parameters)
    
         if (actionResult is SignInResult.CodeRequired) {
             val nextState = actionResult.nextState
             val submitCodeActionResult = nextState.submitCode(
                 code = code
             )
             if (submitCodeActionResult is SignInResult.Complete) {
                 // Handle sign in success
                 val accountState = submitCodeActionResult.resultValue
    
                 val getAccessTokenParameters = NativeAuthGetAccessTokenParameters()
                 val accessTokenResult = accountState.getAccessToken(getAccessTokenParameters)
    
                 if (accessTokenResult is GetAccessTokenResult.Complete) {
                     val accessToken = accessTokenResult.resultValue.accessToken
                     val idToken = accountState.getIdToken()
                 }
             }
         }
     }
    ```

    If the user isn't required to submit a passcode, such as where a user signs in with email and password, use the following code snippet:

    ```kotlin
    CoroutineScope(Dispatchers.Main).launch {
        val parameters = NativeAuthSignInParameters(username = email)
        parameters.password = password
        val actionResult: SignInResult = authClient.signIn(parameters)
    
        if (actionResult is SignInResult.Complete) -> {
            // Handle sign in success
            val accountState = actionResult.resultValue
    
            val getAccessTokenParameters = NativeAuthGetAccessTokenParameters()
            val accessTokenResult = accountState.getAccessToken(getAccessTokenParameters)
    
            if (accessTokenResult is GetAccessTokenResult.Complete) {
                val accessToken = accessTokenResult.resultValue.accessToken
                val idToken = accountState.getIdToken()
            }
        }
    }
    ```

    - To start the sign-in flow, use the SDK's `signIn(parameters)` method.
    - An instance of the `NativeAuthSignInParameters` class, containing the `username` that is the email address you collect from the user.
    - If the sign-in method is username (email) and password, the method's parameter, `password` is then password you collect from the user.
    - In most common scenario, the `signIn(parameters)` returns a result, `SignInResult.CodeRequired`, which indicates that the SDK expects the app to submit the email one-time passcode sent to the user's emails address.
    - The `SignInResult.CodeRequired` object contains a new state reference, which we can retrieve through `actionResult.nextState`.
    - The new state gives us access to two new methods:
        - `submitCode()` submits the email one-time passcode that the app collects from the user.
        - `resendCode()` resends the email one-time passcode if the user doesn't receive the code.

### Handle sign-in errors

During sign-in, not all actions succeed. For instance, the user might attempt to sign in with an email address that doesn't exist or submit an invalid code.

#### Handle sign-in start errors

To handle errors in the `signIn(parameters)` method, use the following code snippet:

```Kotlin
 val parameters = NativeAuthSignInParameters(username = email)
 // Assign 'password' param if you sign in with username (email) and password
 // parameters.password = password
val actionResult: SignInResult = authClient.signIn(parameters)

if (actionResult is SignInResult.CodeRequired) {
    // Next step: submit code
} else if (actionResult is SignInError) {
    // Handle sign in errors
    when {
         actionResult.isUserNotFound() -> {
             // Handle "user not found" error
         }
         actionResult.isAuthNotSupported() -> {
             // Handle "authentication type not support" error
         }
         actionResult.isInvalidCredentials() -> {
             // Handle specific errors
         }
         else -> {
             // Handle other errors
         }
     }
}
```

- `SignInError` indicates an unsuccessful action result returned by `signIn(parameters)`, so the action result doesn't include a reference to the new state.
- If `actionResult is SignUpError`, the Android SDK provides utility methods to enable you to analyze the specific errors further:
    - The method `isUserNotFound()` checks whether the user signs in with a username (email address) that doesn't exist.
    - The method `isBrowserRequired()` checks the need for a browser (web fallback), to complete authentication flow. This scenario happens when native authentication isn't sufficient to complete the authentication flow. For examples, an admin configures email and password as the authentication method, but the app fails to send *password* as a challenge type or simply doesn't support it. Use the steps in [Support web fallback in Android app](tutorial-native-authentication-android-support-web-fallback) to handle scenario when it happens.
    - The method `isAuthNotSupported()` checks whether the app sends a challenge type that Microsoft Entra doesn't support, that's a challenge type value other than *oob* and *password*. Learn more about [challenge types](concept-native-authentication-challenge-types).
    - For username (email) and password sign-in, the method `isInvalidCredentials()` checks whether the combination of username and password is incorrect.

#### Handle submit code errors

To handle errors in `submitCode()` method, use the following code snippet:

```Kotlin
val submitCodeActionResult = nextState.submitCode(
    code = code
)
if (submitCodeActionResult is SignInResult.Complete) {
    // Sign in flow complete, handle success state.
} else if (submitCodeActionResult is SubmitCodeError && submitCodeActionResult.isInvalidCode()) {
    // Handle "invalid code" error
}
```

- The `SubmitCodeError` error indicates an unsuccessful action result returned by `submitCode()` and so the action result doesn't include a reference to the new state.
- The `isInvalidCode()` checks for the specific error. In this case, the previous state reference must be used to reperform the action.

To retrieve the new email one-time passcode, use the following code snippet:

```kotlin
val submitCodeActionResult = nextState.submitCode(
    code = code
)
if (submitCodeActionResult is SignInError && submitCodeActionResult.isInvalidCode) {
    // Inform the user that the submitted code was incorrect or invalid, then ask them to input a new email one-time passcode
    val newCode = retrieveNewCode()
    nextState.submitCode(
        code = newCode
    )
}
```

You've completed all the necessary steps to successfully sign in a user on your app. Build and run your application. If all good, you should be able to provide an email, receive a code on the email, and use that to successfully sign in user.

## Read ID token claims

Once your app acquires an ID token, you can retrieve the claims associated with the current account. To do so, use the following code snippet.

```kotlin
val preferredUsername = accountState.getClaims()?.get("preferred_username")
val city = accountState.getClaims()?.get("City")
val givenName = accountState.getClaims()?.get("given_name")
//custom attribute
val loyaltyNumber = accountState.getClaims()?.get("loyaltyNumber")
```

The key you use to access the claim value is the name that you specify when you add the user attribute as a token claim.

To learn how to add built-in and custom attributes to as token claims in the [Add user attributes to token claims](../external-id/customers/how-to-add-attributes-to-token) article.

## Sign out a user

To sign out a user, you need to remove the account currently stored in the cache.

1. Create your custom user interface (UI) that includes:

    - A sign-out button that user select to send a sign-out request.
2. To sign out a user, use the following code:

    ```kotlin
    private fun performSignOut(accountState: AccountState) {
         CoroutineScope(Dispatchers.Main).launch {
             val accountResult = authClient.getCurrentAccount()
             if (accountResult is GetAccountResult.AccountFound) {
                 val signOutResult = accountResult.resultValue.signOut()
                 if (signOutResult is SignOutResult.Complete) {
                     // Show sign out successful UI
                 }
             }
         }
     }
    ```

### Handle sign-out errors

Sign out should be error-free. If any errors occur, inspect the error result using the following code snippet:

```kotlin
val actionResult = accountResult.signOut()
if (actionResult is SignOutResult.Complete) {
    // Show sign out successful UI
} else {
    // Handle errors
}
```

Make sure you include the import statements. Android Studio should include the import statements for you automatically.

You have completed all the necessary steps to successfully sign out a user on your app. Build and run your application. If all good, you should be able to select sign out button to successfully sign out.

## Configure custom claims provider

If you want to add claims from an external system into the token that is issued to your app, use a [custom claims provider](custom-claims-provider-overview). A custom claims provider is made up of a custom authentication extension that calls an external REST API to fetch claims from external systems.

Follow the steps in [Configure a custom claim provider](/en-us/entra/identity-platform/custom-extension-tokenissuancestart-configuration?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) to add claims from an external system into your security tokens.

## Enable sign-in with an alias or username

You can allow users who sign in with an email address and password to also sign in with a username and password. The username also called an alternate sign-in identifier, can be a customer ID, account number, or another identifier that you choose to use as a username.

You can assign usernames to the user account manually via the Microsoft Entra admin center or automate it in your app via the Microsoft Graph API.

Use the steps in [Sign in with an alias or username](../external-id/customers/how-to-sign-in-alias) article to allow your users to sign-in using a username in your application:

1. [Enable username in sign-in](../external-id/customers/how-to-sign-in-alias#enable-username-in-sign-in-identifier-policy).
2. [Create users with username in the admin center](../external-id/customers/how-to-sign-in-alias#create-and-update-users-with-username) or [update existing users to by adding a username](../external-id/customers/how-to-sign-in-alias#create-and-update-users-with-username). Alternatively, you can also [automate user creation and updating in your app by using the Microsoft Graph API](../external-id/customers/how-to-sign-in-alias#create-and-update-users-with-username).