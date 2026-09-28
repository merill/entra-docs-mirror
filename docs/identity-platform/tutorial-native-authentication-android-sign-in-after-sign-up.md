---
layout: Conceptual
title: Sign in user automatically after sign-up in Android by using native authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-android-sign-in-after-sign-up
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to automatically sign-in a user after sign-up in an Android app by using native authentication.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2024-03-20T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: f5aed2e4-e0e6-cf51-7887-0d8231e305c1
document_version_independent_id: f5aed2e4-e0e6-cf51-7887-0d8231e305c1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-android-sign-in-after-sign-up.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-android-sign-in-after-sign-up
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-android-sign-in-after-sign-up.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 98e56e14-e347-b237-4de1-a92e1c9b4175
---

# Sign in user automatically after sign-up in Android by using native authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to sign in user automatically after sign-up in an Android app by using native authentication.

In this tutorial, you:

- Sign in after sign-up.
- Handle errors.

## Prerequisites

- Complete the steps [Sign in users in a sample native Android mobile application](../external-id/customers/how-to-run-native-authentication-sample-android-app). This article shows you how to run a sample Android that you configure by using your tenant settings.
- [Tutorial: Add sign-up in an Android mobile app using native authentication](tutorial-native-authentication-android-sign-up). The steps in this tutorial should work whether you sign up with email and password or email one-time passcode.

## Sign in after sign-up

After a successful sign-up flow, you can automatically sign in your users without initiating a fresh sign-in flow.

The `SignUpResult.Complete` returns `SignInContinuationState` object. The `SignInContinuationState` object provides access to `signIn(parameters)` method.

To sign up a user with email and password, then automatically sign them in, use the following code snippet:

```kotlin
CoroutineScope(Dispatchers.Main).launch {
    val parameters = NativeAuthSignUpParameters(username = email)
    parameters.password = password
    val actionResult: SignUpResult = authClient.signUp(parameters)

    if (SignUpActionResult is SignUpResult.CodeRequired) { 
        val nextState = signUpActionResult.nextState 
        val submitCodeActionResult = nextState.submitCode( 
            code = code 
        ) 
        if (submitCodeActionResult is SignUpResult.Complete) {
            // Handle sign up success 
            val signInContinuationState = actionResult.nextState 

            val parameters = NativeAuthSignInContinuationParameters()
            val signInActionResult = signInContinuationState.signIn(parameters)

            if (signInActionResult is SignInResult.Complete) { 
                // Handle sign in success
                val accountState = signInActionResult.resultValue

                val getAccessTokenParameters = NativeAuthGetAccessTokenParameters()
                val accessTokenResult = accountState.getAccessToken(getAccessTokenParameters)

                if (accessTokenResult is GetAccessTokenResult.Complete) {
                    val accessToken = accessTokenResult.resultValue.accessToken
                    val idToken = accountState.getIdToken()
                }
            } 
        } 
    } 
}
```

To retrieve ID token claims after sign-in, use the steps in [Read ID token claims](../external-id/customers/tutorial-native-authentication-android-sign-in-user-with-username-password#read-id-token-claims).

## Handle sign-in errors

The `SignInContinuationState.signIn(parameters)` method returns `SignInResult.Complete` after a successful sign-in. It can also return an error.

To handle errors in `SignInContinuationState.signIn(parameters)`, use the following code snippet:

```kotlin
val parameters = NativeAuthSignInContinuationParameters()
val signInActionResult = signInContinuationState.signIn(parameters)

when (signInActionResult) {
    is SignInResult.Complete -> {
        // Handle sign in success
         displayAccount(accountState = actionResult.resultValue)
    }
    is SignInContinuationError -> {
        // Handle unexpected error
    }
    else -> {
        // Handle unexpected error
    }
}

private fun displayAccount(accountState: AccountState) {
    CoroutineScope(Dispatchers.Main).launch {
        val getAccessTokenParameters = NativeAuthGetAccessTokenParameters()
        val accessTokenResult = accountState.getAccessToken(getAccessTokenParameters)
        if (accessTokenResult is GetAccessTokenResult.Complete) {
            val accessToken = accessTokenResult.resultValue.accessToken
            val idToken = accountState.getIdToken()
        }
    }
}
```