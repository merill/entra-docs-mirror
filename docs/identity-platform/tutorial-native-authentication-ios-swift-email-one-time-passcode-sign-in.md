---
layout: Conceptual
title: Add email one-time passcode MFA to your iOS/macOS app by using native authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-ios-swift-email-one-time-passcode-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to add email one-time passcode (OTP) multifactor authentication (MFA) to an iOS or macOS app by using native authentication and enforce MFA with authentication context.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2026-01-27T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: de229adc-360c-b589-b4be-ebba2d642c5e
document_version_independent_id: de229adc-360c-b589-b4be-ebba2d642c5e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-ios-swift-email-one-time-passcode-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-ios-swift-email-one-time-passcode-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-ios-swift-email-one-time-passcode-sign-in.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e5a790f9-16f6-46d2-a166-09ff2b338722
---

# Add email one-time passcode MFA to your iOS/macOS app by using native authentication - Microsoft identity platform | Microsoft Learn

This tutorial demonstrates how to implement multifactor authentication (MFA) into your iOS/macOS app using the native authentication. MFA adds an extra layer of security to your app by requiring users to provide an extra verification step during sign-in. We support email and SMS one-time passcode MFA. We'll also demonstrate how to enhance security during authentication and enforce MFA by using [authentication context](/en-us/entra/identity/conditional-access/concept-conditional-access-cloud-apps#authentication-context).

In this tutorial, you learn how to:

- Sign in a user with email one-time passcode MFA
- Specify the authentication context during user sign-in to enforce MFA.

## Prerequisites

1. Complete the steps in [Tutorial: Add sign-in and sign-out in iOS/macOS app by using native authentication](tutorial-native-authentication-ios-macos-sign-in-sign-out).
2. To enable MFA for your customers, follow the steps in [Add MFA to an app](../external-id/customers/how-to-multifactor-authentication-customers). Currently, native authentication supports email one-time passcode as a second factor for MFA, which is available only when the primary authentication method is email with password.
3. If you'd like to explore our Sign-in with MFA using Email OTP implementation, take a look at our [Code sample](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-ios-sample) before getting started.

## Enable MFA capabilities in the native authentication client

Enable multifactor authentication by configuring the capabilities parameter when you initialize `MSALNativeAuthPublicClientApplication`.

```swift
let config = try MSALNativeAuthPublicClientApplicationConfig(
    clientId: Configuration.clientId,
    tenantSubdomain: Configuration.tenantSubdomain,
    challengeTypes: [.OOB, .password]
)
config.capabilities = [.mfaRequired]
nativeAuth = try MSALNativeAuthPublicClientApplication(nativeAuthConfiguration: config)
```

## Sign in a user with email one-time passcode MFA

To sign in a user with email one-time passcode MFA, after collecting email and password, you need to send an email containing a one-time passcode for the user to verify their email. When the user enters a valid one-time passcode, the app signs them in.

To sign in a user with email one-time passcode MFA, you need to:

1. Create a user interface (UI) to:

    - Advise the user that MFA is required to sign in (optional).
    - Display to the user the possible `authMethods` and have them select the one with email (optional).
    - Collect an email one-time passcode from the user to fulfill second authenticator factor.
    - Resend one-time passcode (recommended).
2. Implement the `onSignInAwaitingMFA` method as part of the `SignInStartDelegate` protocol:

    ```swift
     extension ViewController: SignInStartDelegate {
    
         // previous code omitted
    
         func onSignInAwaitingMFA(authMethods: [MSALAuthMethod], newState: AwaitingMFAState) {
             // inform the user that MFA is required
             let alert = UIAlertController(
                 title: "MFA required", 
                 message: "Do you want to proceed with MFA?", 
                 preferredStyle: .alert
             )
    
             alert.addAction(UIAlertAction(title: "OK", style: .default, handler: { _ in
                 // You can select the first authMethod which has a challengeChannel of type email
                 // Or use "actionResult.authMethods" to let the user pick the authentication method to use.
                 var authMethod = actionResult.authMethods.first { $0.channelTargetType.isEmailType }     
                 self.authMethod = authMethod
                 newState.requestChallenge(authMethod: authMethod, delegate: self)
             }))
    
             alert.addAction(UIAlertAction(title: "Cancel", style: .cancel, handler: { _ in
                 self.resultTextView.text = "Second factor authentication required"
             }))
    
             present(alert, animated: true)
         }
     }
    ```

    The `signIn(username:password:delegate)` results in a call to delegate methods. The `onSignInAwaitingMFA(authMethods:newState)` method handles the scenario where MFA is required. You present an alert to the user, asking if they want to proceed with MFA. If the user chooses **OK** you request the MFA challenge by calling `newState.requestChallenge(authMethod: authMethod delegate: self)`. The `newState.requestChallenge(authMethod: authMethod, delegate: self)` method sends the one-time passcode to the user's email address.

    If you prefer not to inform the user about the necessity for MFA, you can bypass the user interaction by directly invoking `newState.requestChallenge(authMethod: authMethod, delegate: self)`. The `requestChallenge(authMethod: delegate)` requires the authMethod to be specified where the email should be sent and accepts a delegate parameter. You must implement the required methods in the `MFARequestChallengeDelegate` protocol.
3. Implement the `MFARequestChallengeDelegate` protocol:

    ```swift
    extension ViewController: MFARequestChallengeDelegate {
    
        func onMFARequestChallengeError(error: MFARequestChallengeError, newState: MFARequiredState?) {
            resultTextView.text = "Error requesting MFA challenge: \(error.errorDescription ?? "no description")"
        }
    
        func onMFARequestChallengeVerificationRequired(
            newState: MFARequiredState,
            sentTo: String,
            channelTargetType: MSALNativeAuthChannelType,
            codeLength: Int
        ) {
            let code = retrieveCodeFromUser()
            newState.submitChallenge(challenge: code, delegate: self)
        }
    }
    ```

    In the most common scenario, you receive a call to `onMFARequestChallengeVerificationRequired(newState:sentTo:channelTargetType:codeLength)` to indicate that a code has been sent to verify the user's email address. Once you collect the one-time passcode from the user, you can call the `submitChallenge` calls like this`newState.submitChallenge(challenge: code, delegate: self)`. The `submitChallenge` accepts a delegate parameter and you must implement the required methods in the `MFASubmitChallengeDelegate` protocol.
4. Implement the `MFASubmitChallengeDelegate` protocol:

    ```swift
    extension MultiFactorAuthenticationViewController: MFASubmitChallengeDelegate {
    
        func onMFASubmitChallengeError(error: MFASubmitChallengeError, newState: MFARequiredState?) {
            resultTextView.text = "Error submitting MFA challenge: \(error.errorDescription ?? "no description")"
            newState.submitChallenge(challenge: "newCode", delegate: self)
        }
    
        func onSignInCompleted(result: MSALNativeAuthUserAccountResult) {
            print("Signed in as: \(result.account.username ?? "unknown user")")
        }
    }
    ```

    The `MFASubmitChallengeDelegate` protocol enables you to handle MFA code submission and verification. It provides methods to manage errors, such as invalid codes through `onMFASubmitChallengeError`, allowing resubmission. When the MFA is successful, `onSignInCompleted` finalizes the sign-in process. Implementing this delegate ensures smooth MFA handling during authentication.

## Use authentication context during sign-in

Before specifying the authentication context during sign-in, ensure that you configure the conditional access policy on the Microsoft Entra admin center by completing the steps listed in [Configure authentication contexts](/en-us/entra/identity/conditional-access/concept-conditional-access-cloud-apps#configure-authentication-contexts). After configuring the authentication context, you can specify this request claim during sign-in by using the following code snippet:

```swift
@IBAction func signInPressed(_: Any) {
    let parameters = MSALNativeAuthSignInParameters(username: email)
    parameters.password = password
    // before calling the signIn method, we need to specify the authentication context as request claim
    var error: NSError? = nil
    let authenticationContextClaim = "{\"access_token\":{\"acrs\":{\"essential\":true,\"value\":\"<authentication context id>\"}}}"
    params.claimsRequest = MSALClaimsRequest(jsonString: authenticationContextClaim, error: &error)
    // now we can call the signIn method
    nativeAuth.signIn(parameters: parameters, delegate: self)
}
```

At this point the MFA flow should be initiated, and the method "onSignInAwaitingMFA(newState)" will be invoked.

## Handle sign-in with email one-time passcode MFA errors

To handle errors that occur during MFA, you need to implement the following methods:

1. To handle errors in the `requestChallenge` method, use the following code snippet

    ```swift
    func onMFARequestChallengeError(error: MFARequestChallengeError, newState: MFARequiredState?) {
        if error.isBrowserRequired {
            showResultText("Browser is required")
        } else {
            showResultText("Unexpected error while requesting challenge: \(error.errorDescription ?? "No error description")")
        }
    }
    ```

    The `onMFARequestChallengeError` function handles errors that occur during an MFA request challenge.
2. To handle errors in the `submitChallenge(challenge)` method, use the following code snippet

    ```swift
    func onMFASubmitChallengeError(error: MFASubmitChallengeError, newState: MFARequiredState?) {
        if error.isInvalidChallenge {
            // Inform the user that the submitted code was incorrect and ask for a new code to be supplied
            let userSuppliedCode = retrieveNewCode()
            newState.submitChallenge(challenge: userSuppliedCode, delegate: self)
        } else {
            showResultText("Unexpected error occurred: \(error.errorDescription ?? "No error description")")
        }
    }
    ```

    The `onMFASubmitChallengeError` function handles errors that occur during the submission of an MFA challenge. In case the challenge submitted is invalid, you can use the `newState` parameter to submit a new challenge.