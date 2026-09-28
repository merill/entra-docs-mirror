---
layout: Conceptual
title: Add SMS one-time passcode MFA to an Android app using native authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-android-sms-one-time-passcode-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to add multifactor authentication (MFA) with SMS one-time passcodes to an Android app using Microsoft Entra native authentication.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2026-01-27T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: fe252349-7b2e-436e-2835-a39c763248a0
document_version_independent_id: fe252349-7b2e-436e-2835-a39c763248a0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-android-sms-one-time-passcode-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-android-sms-one-time-passcode-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-android-sms-one-time-passcode-sign-in.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e4ab3d61-81e9-d6cf-3402-253b6ffeb2a3
---

# Add SMS one-time passcode MFA to an Android app using native authentication - Microsoft identity platform | Microsoft Learn

This tutorial shows you how to add multifactor authentication (MFA) with SMS one-time passcode (OTP) to your Android app using native authentication. MFA adds an extra layer of security by requiring a second verification step during sign-in. We'll also demonstrate how to enhance security during authentication and enforce MFA by using [authentication context](/en-us/entra/identity/conditional-access/concept-conditional-access-cloud-apps#authentication-context).

In this tutorial, you learn how to:

- Sign in a user with SMS one-time passcode MFA
- Specify an authentication context during sign-in to enforce MFA
- Handle sign-in with SMS one-time passcode MFA errors

## Prerequisites

1. Complete the steps in [Tutorial: Add sign-in and sign-out in Android app by using native authentication](tutorial-native-authentication-android-sign-in-sign-out).
2. Enable SMS as an MFA method in your tenant: follow the steps in [Enable SMS as an MFA method](../identity/authentication/howto-authentication-sms-signin#enable-the-sms-based-authentication-method).
3. If you'd like to explore our Sign-in with MFA using SMS implementation, take a look at our [Code sample](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-android-sample) before getting started.

## Add MFA capabilities to the client configuration file

Note

Currently there's a known issue using the SMS one time passcode with the authority format: `<tenantSubdomain>.ciamlogin.com/<tenantSubdomain>.onmicrosoft.com` because of that the following format should be used: `<tenantSubdomain>.ciamlogin.com/<tenantID>`

To support MFA, update the Android client configuration to include the required MFA capabilities.

```json
{
    "client_id": "Enter_the_Application_Id_Here",
    "authorities": [
    {
        "type": "CIAM",
        "authority_url": "https://Enter_the_Tenant_Subdomain_Here.ciamlogin.com/Enter_the_Tenant_Id_Here/"
    }
    ],
    "challenge_types": ["oob", "password"],
    "capabilities": ["mfa_required"],
    "logging": {
    "pii_enabled": false,
    "log_level": "INFO",
    "logcat_enabled": true
    }
}
```

## Sign in a user with SMS one-time passcode MFA

To sign in a user with SMS one-time passcode multifactor authentication (MFA), after collecting first factor, you need to send an SMS containing a one-time passcode for the user to verify their phone number. When the user enters a valid one-time passcode, the app signs them in.

To sign in a user with SMS one-time passcode MFA, you need to:

1. Create a user interface (UI) to:

    - Advise the user that MFA is required to sign in (optional).
    - Collect an SMS one-time passcode from the user to fulfill second authenticator factor.
    - Resend one-time passcode (recommended).
2. Handle `MFARequired` sign in result:

    ```kotlin
    is SignInResult.MFARequired -> {
        // Handle "mfa required" result 
        val awaitingMFAState = actionResult.nextState
    
        // Select the authentication method from authMethods, either programmatically or through the UI, and assign it to authMethod.
        val authMethod = actionResult.authMethods.first {it.challengeChannel.uppercase() == "SMS"} 
        val requestChallengeResult = awaitingMFAState.requestChallenge(authMethod)
    
        // Handle "mfa verification required" result 
        if (requestChallengeResult is MFARequiredResult.VerificationRequired) {
            // Next Step: submitChallenge using nextState
        } else {
            // Handle unexpected result as well as errors
        }
    }
    ```

    When signing in, if MFA is necessary, the system returns `SignInResult.MFARequired`. At this point, you can advise the user that MFA is required to proceed with the authentication, or you can call the `requestChallenge(authMethod)` method to send the one-time passcode. In most common scenario `requestChallenge(authMethod)`, returns a result `MFARequiredResult.VerificationRequired`, which indicates that the SDK expects the app to submit SMS one-time passcode sent to the user's phone.
3. Handle `submitChallenge()` result:

    ```kotlin
    val mfaRequiredState = requestChallengeResult.nextState
    val submitChallengeResult = mfaRequiredState.submitChallenge(code)
    
    when (submitChallengeResult) {
        is SignInResult.Complete -> {
            // Handle sign in success               
        }
        is SubmitChallengeError -> {
            // Handle "mfa submit challenge" error
        }
        else -> {
            // Handle unexpected result
        }
    }
    ```

    The `MFARequiredResult.VerificationRequired` object contains a new state reference, which you can retrieve through `requestChallengeResult.nextState`. The new state gives you access to the `submitChallenge()` method that you can use to submit the MFA challenge. In most common scenario, the `submitChallenge()` returns a result, `SignInResult.Complete`, which indicates that the user has been authenticated successfully.

## Use authentication context during sign-in

To learn how to use authentication context during sign-in, see [authentication context during sign-in](tutorial-native-authentication-android-email-one-time-passcode-sign-in#use-authentication-context-during-sign-in) is how you can use authentication context during sign-in.

## Handle sign-in with SMS one-time passcode MFA errors

To handle errors that occur during MFA, implement error handling logic for both the challenge request and challenge submission:

1. Handle errors in the `requestChallenge` method:

    ```kotlin
    if (requestChallengeResult is MFARequiredResult.Error) {
        if (requestChallengeResult.isBrowserRequired()) {
            showResultText("Browser is required")
        } else {
            showResultText("Unexpected error while requesting challenge: ${requestChallengeResult.errorMessage}")
        }
    }
    ```
2. Handle errors in the `submitChallenge` method:

    ```kotlin
    if (result is SignInError) {
        if (result.isInvalidChallenge()) {
            // Inform the user that the submitted code was incorrect and ask for a new code
            // Optionally, allow resubmission using newState.submitChallenge(newCode, authMethod)
        } else {
            showResultText("Unexpected error occurred: ${result.errorMessage}")
        }
    }
    ```