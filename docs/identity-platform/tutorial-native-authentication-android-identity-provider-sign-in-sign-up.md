---
layout: Conceptual
title: Add federated identity provider sign-in and sign-up to an Android app using native authentication web flow - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-android-identity-provider-sign-in-sign-up
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to enable federated identity provider sign-in and sign-up in an Android app using Microsoft Entra native authentication with web-based authentication flow.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2026-04-10T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: 
locale: en-us
document_id: 473e799d-4f7a-66eb-e36d-7c213b8fc637
document_version_independent_id: 473e799d-4f7a-66eb-e36d-7c213b8fc637
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-android-identity-provider-sign-in-sign-up.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-android-identity-provider-sign-in-sign-up
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-android-identity-provider-sign-in-sign-up.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 95fe53f6-8159-3e63-80bc-96ee55dfbd3a
---

# Add federated identity provider sign-in and sign-up to an Android app using native authentication web flow - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to implement federated identity provider (IdP) authentication into your Android app using native authentication with web flow. Federated IdP authentication allows users to sign in or sign up using their existing accounts from providers like Apple, Facebook, Google and custom OIDC providers.

In this tutorial, you learn how to:

- Sign in a user using a federated identity provider via web flow
- Sign up a user using a federated identity provider via web flow

## Prerequisites

1. Complete the steps in [Tutorial: Prepare your Android mobile app for native authentication](tutorial-native-authentication-prepare-android-app).
2. Configure federated identity providers in your Microsoft Entra External ID tenant. Follow the steps in the Microsoft Entra admin center to add and configure your desired identity providers:

    - [Configure Apple as an identity provider](../external-id/customers/how-to-apple-federation-customers)
    - [Configure Facebook as an identity provider](../external-id/customers/how-to-facebook-federation-customers)
    - [Configure Google as an identity provider](../external-id/customers/how-to-google-federation-customers)
    - [Configure a custom OIDC provider](../external-id/customers/how-to-custom-oidc-federation-customers). Use the domain of the Issuer URI configured for custom OIDC as the `domain_hint`.
3. If you'd like to explore our federated IdP Sign in and Sign up implementation, take a look at our [sample Android application](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-android-sample/blob/main/app/src/main/java/com/azuresamples/msalnativeauthandroidkotlinsampleapp/IdPSignInSignUpWebFragment.kt) before getting started.

## Sign in a user with a federated identity provider

To sign in a user with a federated identity provider via web flow, you need to first identify the identity provider to register/authenticate with, and the corresponding `domain_hint`.

- Use the identity providers defined in the prerequisite configuration section.
- Use the `domain_hint`parameter to direct authentication to a specific identity provider. Choose one of the following values:
    - `"Apple"` for Apple
    - `"Facebook"` for Facebook
    - `"Google"` for Google

To sign in a user, you need to:

1. Create a user interface to sign in with a federated identity provider. This should identify a specific identity provider and its corresponding `domain_hint`.
2. Once `domain_hint` value is identified from the client app, call `INativeAuthPublicClientApplication.acquireToken` with `domain_hint` to trigger web authentication with Social IdP. Here's a code snippet example:

    Use the Prompt value as `Prompt.LOGIN` to force interactive authentication, even if user is signed in.

    ```kotlin
    private fun signInWithIdp(domainHint: String) {
        val acquireTokenParameters = AcquireTokenParameters.Builder()
            .startAuthorizationFromActivity(requireActivity())
            .withScopes(listOf("openid", "profile", "email"))
            .withDomainHint(domainHint)
            .withPrompt(Prompt.LOGIN)
            .withCallback(getAuthenticationCallback())
            .build()
    
        authClient.acquireToken(acquireTokenParameters)
    }
    ```
3. To handle the sign in results, you need to implement the `AuthenticationCallback`, example below:

    ```kotlin
    private fun getAuthenticationCallback(): AuthenticationCallback {
        return object : AuthenticationCallback {
    
            override fun onSuccess(authenticationResult: IAuthenticationResult) {
                Log.d(TAG, "Successfully authenticated with IdP")
    
                val account = authenticationResult.account
                val idToken = account.idToken
                val accessToken = authenticationResult.accessToken
    
                Toast.makeText(
                    requireContext(),
                    "Sign in successful!",
                    Toast.LENGTH_SHORT
                ).show()
            }
    
            override fun onError(exception: MsalException) {
                Log.e(TAG, "Authentication failed: ${exception.message}", exception)
    
                showErrorDialog(
                    "Sign in failed",
                    exception.message ?: "An error occurred during authentication"
                )
            }
    
            override fun onCancel() {
                Log.d(TAG, "User cancelled authentication")
    
                Toast.makeText(
                    requireContext(),
                    "Sign in cancelled",
                    Toast.LENGTH_SHORT
                ).show()
            }
        }
    }
    ```

    For error code and handling, refer to [Handle errors and exceptions in MSAL for Android](/en-us/entra/msal/android/handling-exceptions).
4. You can also retrieve the current cached account after successful authentication by using the `getCurrentAccount()` from `INativeAuthPublicClientApplication`, which returns an object, `accountResult`:

    ```kotlin
    val accountResult = iNativeAuthPublicClientApplication.getCurrentAccount()
    
    when (accountResult) {
        is GetAccountResult.AccountFound -> {
            accountResult.resultValue.getIdToken()
        }
    
        is GetAccountResult.NoAccountFound -> {
            Log.d(TAG, "No account found")
        }
    
        is GetAccountError -> {
            displayDialog(
                getString(R.string.msal_exception_title),
                accountResult.exception?.message ?: accountResult.errorMessage
            )
        }
    }
    ```

### Update configurations

1. Ensure your client JSON configuration file includes the `redirect_uri` parameter for handling web-based authentication flows:

    - [Microsoft Authentication Library (MSAL) configuration](/en-us/entra/msal/android/msal-configuration#redirect_uri)

    ```json
    {
        "client_id": "Enter_the_Application_Id_Here",
        "redirect_uri": "msauth://com.yourpackage.name/Enter_your_Signature_Hash_Here",
        "authorities": [
        {
            "type": "CIAM",
            "authority_url": "https://Enter_the_Tenant_Subdomain_Here.ciamlogin.com/Enter_the_Tenant_Subdomain_Here.onmicrosoft.com/"
        }
        ],
        ...
    }
    ```
2. Add or update the MSAL dependency to at least `8.1.0` in your app's `build.gradle` file if not already present:

    ```gradle
    dependencies {
        implementation 'com.microsoft.identity.client:msal:[8.1.0,)'
    }
    ```

## Sign up a user with a federated identity provider

To sign up a user with a federated identity provider, the process is almost the same as signing in, with a minor change to the Prompt value: use `Prompt.CREATE`.

```kotlin
private fun signUpWithIdp(domainHint: String) {
    val acquireTokenParameters = AcquireTokenParameters.Builder()
        .startAuthorizationFromActivity(requireActivity())
        .withScopes(listOf("openid", "profile", "email"))
        .withDomainHint(domainHint)
        .withPrompt(Prompt.CREATE)
        .withCallback(getAuthenticationCallback())
        .build()
    
    authClient.acquireToken(acquireTokenParameters)
}
```