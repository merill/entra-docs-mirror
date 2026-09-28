---
layout: Conceptual
title: Self-service password reset in Android app using native authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-android-self-service-password-reset
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to implement self-service password reset (SSPR) to my Android app using native authentication.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2024-02-23T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 0249ea42-e819-73da-7adb-7cc4059e8b5d
document_version_independent_id: 0249ea42-e819-73da-7adb-7cc4059e8b5d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-android-self-service-password-reset.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-android-self-service-password-reset
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-android-self-service-password-reset.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 58dd7d03-cafb-3e5c-5a25-b65d7ca86e22
---

# Self-service password reset in Android app using native authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to enable users to change or reset their password, with no administrator or help desk involvement.

In this tutorial, you:

- Add self-service password reset (SSPR) flow.
- Add the required user interface (UI) for SSPR to your app.
- Handle errors.

## Prerequisites

- Complete the steps in [Sign in users in a sample native Android mobile application](../external-id/customers/how-to-run-native-authentication-sample-android-app). This article shows you how to run a sample Android that you configure by using your tenant settings.
- [Enable self-service password reset](../external-id/customers/how-to-enable-password-reset-customers). This article enables you to enable the email one-time passcode authentication method for all users in your tenant, which is a requirement for SSPR.
- [Tutorial: Prepare your Android app for native authentication](tutorial-native-authentication-android-sign-up).

## Add self-service password reset flow

To add SSPR flow to your Android application, you need a password reset user interface:

- An input text field to collect user's email address (username).
- An input text field to collect one-time passcode.
- An input text field to collect new password.

When users forget their passwords, they need a form to input their usernames (email addresses) to start password reset flow. The user selects the **Forget Password** button or link.

### Start password reset flow

To handle the request when the user selects the **Forget Password** button or link, use the Android SDK's `resetPassword(parameters)` method as shown in the following code snippet:

```kotlin
 private fun forgetPassword() { 
     CoroutineScope(Dispatchers.Main).launch { 
         val parameter = NativeAuthResetPasswordParameters(username = email)
         val actionResult = authClient.resetPassword(parameter)

         when (resetPasswordResult) { 
             is ResetPasswordStartResult.CodeRequired -> { 
                 // The implementation of submitCode() please see below. 
                 submitCode(resetPasswordResult.nextState) 
             } 
             is ResetPasswordError -> {
                 // Handle errors
                 handleResetPasswordError(resetPasswordResult)
             }
         }
     } 
 } 
```

- `resetPassword(parameters)` method initiates password reset flow and an email one-time passcode is sent to the user's emails address for verification.
- The return result of `resetPassword(parameters)` is either `ResetPasswordStartResult.CodeRequired` or `ResetPasswordError`.
- If `resetPasswordResult is ResetPasswordStartResult.CodeRequired`, the app needs to collect the email one-time passcode from the user and submits it as shown in Submit email one-time passcode.
- If `resetPasswordResult is ResetPasswordError`, Android SDK provides utility methods to enable you to analyze the specific errors further: - `isUserNotFound()` - `isBrowserRequired()`
- These errors indicate that the previous operation was unsuccessful, and so a reference to a new state isn't available. Handle these errors as shown in Handle errors section.

### Submit email one-time passcode

Your app collects the email one-time passcode from the user. To submit the email one-time passcode, use the following code snippet:

```kotlin
private suspend fun submitCode(currentState: ResetPasswordCodeRequiredState) { 
    val code = binding.codeText.text.toString() 
    val submitCodeResult = currentState.submitCode(code) 

    when (submitCodeResult) { 
        is ResetPasswordSubmitCodeResult.PasswordRequired -> { 
            // Handle success
            resetPassword(submitCodeResult.nextState) 
        } 
         is SubmitCodeError -> {
             // Handle errors
             handleSubmitCodeError(actionResult)
         }
    } 
} 
```

- The return result of the `submitCode()` action is either `ResetPasswordSubmitCodeResult.PasswordRequired` or `SubmitCodeError`.
- If `submitCodeResult is ResetPasswordSubmitCodeResult.PasswordRequired` the app needs to collect a new password from the user and submit it as shown in Submit a new password.
- If the user doesn't receive the email one-time passcode in their email, the app can resend the email one-time passcode. Use the following code snippet to resend a new email one-time passcode:

    ```kotlin
    private fun resendCode() { 
         clearCode() 
    
         val currentState = ResetPasswordCodeRequiredState 
    
         CoroutineScope(Dispatchers.Main).launch { 
             val resendCodeResult = currentState.resendCode() 
    
             when (resendCodeResult) { 
                 is ResetPasswordResendCodeResult.Success -> { 
                     // Handle code resent success
                 } 
                 is ResendCodeError -> {
                      // Handle ResendCodeError errors
                  }
             } 
         } 
    } 
    ```

    - The return result of the `resendCode()` action is either `ResetPasswordResendCodeResult.Success` or `ResendCodeError`.
    - `ResendCodeError` is an unexpected error for SDK. This error indicates that the previous operation was unsuccessful, so a reference to a new state isn't available.
- If `submitCodeResult is SubmitCodeError`, Android SDK provides utility methods to enable you to analyze the specific errors further:

    - `isInvalidCode()`
    - `isBrowserRequired()`

    These errors indicate that the previous operation was unsuccessful, and so a reference to a new state isn't available. Handle these errors as shown in Handle errors section.

### Submit a new password

After you verify the user's email, you need to collect a new password from the user and submit it. The password that the app collects from the user need to meet [Microsoft Entra's password policies](/en-us/entra/identity/authentication/concept-password-ban-bad-combined-policy). Use the following code snippet:

```kotlin
private suspend fun resetPassword(currentState: ResetPasswordPasswordRequiredState) { 
    val password = binding.passwordText.text.toString() 

    val submitPasswordResult = currentState.submitPassword(password) 

    when (submitPasswordResult) { 
        is ResetPasswordResult.Complete -> { 
            // Handle reset password complete. 
        } 
        is ResetPasswordSubmitPasswordError -> {
            // Handle errors
            handleSubmitPasswordError(actionResult)
        }
    } 
} 
```

- The return result of the `submitPassword()` action is either `ResetPasswordResult.Complete` or `ResetPasswordSubmitPasswordError`.
- `ResetPasswordResult.Complete` indicates a successful password reset flow.
- If `submitPasswordResult is ResetPasswordSubmitPasswordError`, the SDK provides utility methods for further analyzing the specific type of error returned: - `isInvalidPassword()` - `isPasswordResetFailed()`

    These errors indicate that the previous operation was unsuccessful, and so a reference to a new state isn't available. Handle these errors as shown in Handle errors section.

## Auto sign in after password reset

After a successful password reset flow, you can automatically sign in your users without initiating a fresh sign-in flow.

The `ResetPasswordResult.Complete` returns `SignInContinuationState` object. The `SignInContinuationState` provides access to `signIn(parameters)` method.

To automatically sign in users after a password reset, use the following code snippet:

```kotlin
 private suspend fun resetPassword(currentState: ResetPasswordPasswordRequiredState) { 
     val submitPasswordResult = currentState.submitPassword(password) 
 
     when (submitPasswordResult) { 
         is ResetPasswordResult.Complete -> { 
             signInAfterPasswordReset(nextState = actionResult.nextState)
         } 
     } 
 } 
 
 private suspend fun signInAfterPasswordReset(nextState: SignInContinuationState) {
     val signInContinuationState = nextState

     val parameters = NativeAuthSignInContinuationParameters()
     val signInActionResult = signInContinuationState.signIn(parameters)

     when (actionResult) {
         is SignInResult.Complete -> {
             fetchTokens(accountState = actionResult.resultValue)
         }
         else {
             // Handle unexpected error
         }
     }
  }
 
 private suspend fun fetchTokens(accountState: AccountState) {
     val getAccessTokenParameters = NativeAuthGetAccessTokenParameters()
     val accessTokenResult = accountState.getAccessToken(getAccessTokenParameters)

     if (accessTokenResult is GetAccessTokenResult.Complete) {
         val accessToken =  accessTokenResult.resultValue.accessToken
         val idToken = accountState.getIdToken()
     }
 }
```

To retrieve ID token claims after sign-in, use the steps in [Read ID token claims](../external-id/customers/tutorial-native-authentication-android-sign-in-user-with-username-password#read-id-token-claims).

## Handle password reset errors

A few expected errors might occur. For example, the user might attempt to reset the password with a nonexistent email or provide a password that doesn't meet the password requirements.

When errors occur, give your users a hint to the errors.

These errors can happen at the start of password reset flow or at submit email one-time passcode or at submit password.

### Handle start password reset error

To handle error caused by start password reset, use the following code snippet:

```kotlin
private fun handleResetPasswordError(error: ResetPasswordError) {
    when {
        error.isUserNotFound() -> {
            // Display error
        }
        else -> {
            // Unexpected error
        }
    }
}
```

### Handle submit email one-time passcode error

To handle error caused by submitting email one-time passcode, use the following code snippet:

```kotlin
private fun handleSubmitCodeError(error: SubmitCodeError) {
    when {
        error.isInvalidCode() -> {
            // Display error
        }
        else -> {
            // Unexpected error
        }
    }
}
```

### Handle submit password error

To handle error caused by submitting password, use the following code snippet:

```kotlin
private fun handleSubmitPasswordError(error: ResetPasswordSubmitPasswordError) {
    when {
        error.isInvalidPassword() || error.isPasswordResetFailed()
        -> {
            // Display error
        }
        else -> {
            // Unexpected error
        }
    }
}
```