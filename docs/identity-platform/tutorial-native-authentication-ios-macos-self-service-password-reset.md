---
layout: Conceptual
title: Self-service password reset - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-ios-macos-self-service-password-reset
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to implement self-service password reset (SSPR) to my iOS/macOS app using native authentication.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2024-08-19T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 0bfa01af-1f4c-a84f-a699-9cf2de9e1553
document_version_independent_id: 0bfa01af-1f4c-a84f-a699-9cf2de9e1553
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-ios-macos-self-service-password-reset.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-ios-macos-self-service-password-reset
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-ios-macos-self-service-password-reset.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: f877faa6-7dc4-c757-1920-89e1550ab86c
---

# Self-service password reset - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to give users the ability to change or reset their password, with no administrator or help desk involvement.

In this tutorial, you:

- Add self-service password reset.
- Handle errors.

## Prerequisites

- [Enable self-service password reset](../external-id/customers/how-to-enable-password-reset-customers)

## Reset password

To reset the password of an existing user, we need to validate the email address using a one-time-passcode (OTP).

1. To validate the email, we call the `resetPassword(parameters:delegate)` method from the SDK instance using the following code snippet:

    ```swift
    let parameters = MSALNativeAuthResetPasswordParameters(username: email)
    nativeAuth.resetPassword(parameters: parameters, delegate: self)
    ```
2. To implement the `ResetPasswordStartDelegate` protocol as an extension to our class, use the following code snippet:

    ```swift
    extension ViewController: ResetPasswordStartDelegate {
        func onResetPasswordCodeRequired(
            newState: MSAL.ResetPasswordCodeRequiredState,
            sentTo: String,
            channelTargetType: MSALNativeAuthChannelType,
            codeLength: Int
        ) {
            resultTextView.text = "Verification code sent to \(sentTo)"
        }
    
        func onResetPasswordStartError(error: MSAL.ResetPasswordStartError) {
            resultTextView.text = "Error verifying code: \(error.errorDescription ?? "no description")"
        }
    }
    ```

    The call to `resetPassword(parameters:delegate)` results in a call to either `onResetPasswordCodeRequired()` or `onResetPasswordStartError()` delegate methods.

    In the most common scenario `onResetPasswordCodeRequired(newState:sentTo:channelTargetType:codeLength)` will be called to indicate that a code has been sent to verify the user's email address. Along with some details of where the code has been sent, and how many digits it contains, this delegate method also has a `newState` parameter of type `ResetPasswordCodeRequiredState`, which gives us access to two new methods:

    - `submitCode(code:delegate)`
    - `resendCode(delegate)`

    To submit the code that the user supplied us with, use:

    ```swift
    newState.submitCode(code: userSuppliedCode, delegate: self)
    ```
3. To verify the submitted code, start by implementing the `ResetPasswordVerifyCodeDelegate` protocol as an extension to your class using the following code snippet:

    ```swift
    extension ViewController: ResetPasswordVerifyCodeDelegate {
    
        func onResetPasswordVerifyCodeError(
            error: MSAL.VerifyCodeError,
            newState: MSAL.ResetPasswordCodeRequiredState?
        ) {
            resultTextView.text = "Error verifying code: \(error.errorDescription ?? "no description")"
        }
    
        func onPasswordRequired(newState: MSAL.ResetPasswordRequiredState) {
            // use newState instance to submit the new password
        }
    }
    ```

    In the most common scenario, we receive a call to `onPasswordRequired(newState)` indicating that we can provide the new password using the `newState` instance.

    ```swift
    newState.submitPassword(password: newPassword, delegate: self)
    ```
4. To implement the `ResetPasswordRequiredDelegate` protocol as an extension to our class, use the following code snippet:

    ```swift
    extension ViewController: ResetPasswordRequiredDelegate {
    
        func onResetPasswordRequiredError(
            error: MSAL.PasswordRequiredError,
            newState: MSAL.ResetPasswordRequiredState?
        ) {
            resultTextView.text = "Error submitting new password: \(error.errorDescription ?? "no description")"
        }
    
        func onResetPasswordCompleted(newState: SignInAfterResetPasswordState) {
            resultTextView.text = "Password reset completed"
        }
    }
    ```

    In the most common scenario, we receive a call to `onResetPasswordCompleted(newState)` indicating that the password reset flow has completed.

## Handle errors

In our earlier implementation of `ResetPasswordStartDelegate` protocol, we displayed the error when we handled the `onResetPasswordStartError(error)` delegate function.

We can enhance the user experience by handling the specific error type as follows:

```swift
func onResetPasswordStartError(error: MSAL.ResetPasswordStartError) {
    if error.isInvalidUsername {
        resultTextView.text = "Invalid username"
    } else if error.isUserNotFound {
        resultTextView.text = "User not found"
    } else if error.isUserDoesNotHavePassword {
        resultTextView.text = "User is not registered with a password"
    } else {
        resultTextView.text = "Error during reset password flow in: \(error.errorDescription ?? "no description")"
    }
}
```

### Handle errors with states

Some errors include a reference to a new state. For example, if the user enters an incorrect email verification code, the error handler includes a reference to a `ResetPasswordCodeRequiredState` that can be used to submit a new verification code.

In our previous implementation of `ResetPasswordVerifyCodeDelegate` protocol, we simply displayed the error when we handled the `onResetPasswordError(error:newState)` delegate function.

We can improve the user experience by asking the user to enter the correct code and resubmitting it as follows:

```swift
func onResetPasswordVerifyCodeError(
    error: MSAL.VerifyCodeError,
    newState: MSAL.ResetPasswordCodeRequiredState?
) {
    if error.isInvalidCode {
        // Inform the user that the submitted code was incorrect and ask for a new code to be supplied.
        // Request a new code calling `newState.resendCode(delegate)`
        let userSuppliedCode = retrieveNewCode(newState)
        newState?.submitCode(code: userSuppliedCode, delegate: self)
    } else {
        resultTextView.text = "Error verifying code: \(error.errorDescription ?? "no description")"
    }
}
```

Another example where the error handler includes a reference to a new state is when the user enters an invalid password. In this case, the error handler includes a reference to a `ResetPasswordRequiredState` that can be used to submit a new password. Here's an example:

```swift
func onResetPasswordRequiredError(
    error: MSAL.PasswordRequiredError,
    newState: MSAL.ResetPasswordRequiredState?
) {
    if error.isInvalidPassword {
        // Inform the user that the submitted password was invalid and ask for a new password to be supplied.
        let newPassword = retrieveNewPassword()
        newState?.submitPassword(password: newPassword, delegate: self)
    } else {
        resultTextView.text = "Error submitting password: \(error.errorDescription ?? "no description")"
    }
}
```

### Sign in after password reset

The SDK provides developers the ability to sign in a user after resetting their password without having to supply the username, or to verify the email address through a one-time passcode.

To sign in a user after successful password reset use the `signIn(parameters:delegate)` method from the new state `SignInAfterResetPasswordState` returned in the `onResetPasswordCompleted(newState)` function:

```swift
extension ViewController: ResetPasswordRequiredDelegate {

    func onResetPasswordRequiredError(
        error: MSAL.PasswordRequiredError,
        newState: MSAL.ResetPasswordRequiredState?
    ) {
        resultTextView.text = "Error submitting new password: \(error.errorDescription ?? "no description")"
    }

    func onResetPasswordCompleted() {
        resultTextView.text = "Password reset completed"
        let parameters = MSALNativeAuthSignInAfterResetPasswordParameters()
        newState.signIn(parameters: parameters, delegate: self)
    }
}
```

The `signIn(parameters:delegate)` accepts a delegate parameter and we must implement the required methods in the `SignInAfterResetPasswordDelegate` protocol.

In the most common scenario, we receive a call to `onSignInCompleted(result)` indicating that the user has signed in. The result can be used to retrieve the `access token`.

```swift
extension ViewController: SignInAfterSignUpDelegate {
    func onSignInAfterSignUpError(error: SignInAfterSignUpError) {
        resultTextView.text = "Error signing in after password reset"
    }

    func onSignInCompleted(result: MSAL.MSALNativeAuthUserAccountResult) {
        // User successfully signed in
        let parameters = MSALNativeAuthGetAccessTokenParameters()
        result.getAccessToken(parameters: parameters, delegate: self)
    }
}
```

The `getAccessToken(parameters:delegate)` accepts a delegate parameter and we must implement the required methods in the `CredentialsDelegate` protocol.

In the most common scenario, we receive a call to `onAccessTokenRetrieveCompleted(result)` indicating that the user obtained an `access token`.

```swift
extension ViewController: CredentialsDelegate {
    func onAccessTokenRetrieveError(error: MSAL.RetrieveAccessTokenError) {
        resultTextView.text = "Error retrieving access token"
    }

    func onAccessTokenRetrieveCompleted(result: MSALNativeAuthTokenResult) {
        resultTextView.text = "Signed in. Access Token: \(result.accessToken)"
    }
}

```