---
layout: Conceptual
title: Call an API in Android app by using native authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-android-sign-in-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to acquire multiple access tokens and call an API in Android app by using native authentication.
manager: dougeby
ms.subservice: external
ms.topic: tutorial
ms.date: 2024-07-07T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: c3423de5-f11f-b096-7abd-594265150351
document_version_independent_id: c3423de5-f11f-b096-7abd-594265150351
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-android-sign-in-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-android-sign-in-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-android-sign-in-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b51d188e-e41e-8c94-94e8-a29e01b438b3
---

# Call an API in Android app by using native authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to acquire an access token and call an API in your Android mobile app. Microsoft Authentication Library (MSAL) native authentication SDK for Android allows you to acquire multiple access tokens with a single sign-in. This capability allows you to acquire one or more access tokens without requiring a user to reauthenticate.

In this tutorial, you:

- Acquire one or multiple access tokens.
- Call an API

## Prerequisites

- Complete the steps in [Tutorial: Add sign-in in Android app by using native authentication](tutorial-native-authentication-android-sign-in-sign-out). This tutorial shows you how to sign in users in your Android app by using native authentication.

## Acquire an access token

Once the user signs in, you acquire an access token by specifying the scopes for which the access token is valid.

MSAL native authentication SDK supports multiple access tokens, so you can specify multiple sets of scopes, then request access token for each set of scopes:

1. Declare and set values for a set of API scopes by using the following code snippet:

    ```kotlin
    companion object {
        // Set values for respective API scopes for their web API resources here, for example: ["api://<Resource_App_ID>/ToDoList.Read", "api://<Resource_App_ID>/ToDoList.ReadWrite"]
        // A list of scope for API 1
        private val scopesForAPI1 = listOf<String>()
        // A list of scope for API 2
        private val scopesForAPI2 = listOf<String>()
    }
    ```
2. Signs in user by using the following code snippet:

    ```kotlin
    CoroutineScope(Dispatchers.Main).launch {
        val parameters = NativeAuthSignInParameters(username = email)
        parameters.password = password
        val actionResult: SignInResult = authClient.signIn(parameters)
    
        if (actionResult is SignInResult.Complete) -> {
            // Perform operations after successful sign-in
        } else if (actionResult is SignInError) {
            // Handle sign-in errors
        }
    }
    ```
3. Acquire one or multiple access tokens by using the following code snippet:

    ```kotlin
    CoroutineScope(Dispatchers.Main).launch {
        val accountResult = authClient.getCurrentAccount()
        when (accountResult) {
            is GetAccountResult.AccountFound -> {
                try {
                    // Access token for API 1
                    val accessTokenOne = getAccessToken(accountResult.resultValue, scopesForAPI1)
                    // Access token for API 2
                    val accessTokenTwo = getAccessToken(accountResult.resultValue, scopesForAPI2)
                    // Proceed to make a call to an API
                } catch (e: Exception) {
                    // Handle Exception
                }
            }
            is GetAccountResult.NoAccountFound -> {
                // Handle etAccountResult.NoAccountFound
            }
            is GetAccountError -> {
                // Handle GetAccountError 
            }
        }
    }   
    
    ```

    Define the `getAccessToken()` function as shown in the following code:

    ```kotlin
    private suspend fun getAccessToken(accountState: AccountState, scopes: List<String>): String {
        val parameters = NativeAuthGetAccessTokenParameters()
        parameters.scopes = scopes
        val accessTokenState = accountState.getAccessToken(parameters)
    
        return if (accessTokenState is GetAccessTokenResult.Complete) {
            accessTokenState.resultValue.accessToken
        } else {
            throw Exception("Failed to get access token")
        }
    }
    ```

## Call an API

To make an API call, use the access token you acquired in Acquire an access token and an API URL:

1. Declare and set values for the API URLs by using the following code snippet:

    ```kotlin
    companion object {
        // Set values for respective API scopes for web API resources here, for example: ["api://<Resource_App_ID>/ToDoList.Read", "api://<Resource_App_ID>/ToDoList.ReadWrite"]
        // A list of scope for API 1
        private val scopesForAPI1 = listOf<String>()
        // A list of scope for API 2
        private val scopesForAPI2 = listOf<String>()
        // Set the URL of first web API resource here
        private const val WEB_API_URL_1 = "Enter_URL_Of_First_Web_API" 
        // Set the URL of second web API resource here
        private const val WEB_API_URL_2 = "Enter_URL_Of_Second_Web_API" 
    }
    ```

    Replace the:

    - `Enter_URL_Of_First_Web_API` placeholder with the full URL value of your first API.
    - `Enter_URL_Of_Second_Web_API` placeholder with the full URL value of your second API.
2. Use the following code snippets to call an API:

    ```kotlin
    // After you acquire an access token, use it to call an API
    
    val firstApiResponse = useAccessToken(WEB_API_URL_1, accessTokenOne)
    val secondApiResponse = useAccessToken(WEB_API_URL_2, accessTokenTwo)
    
    private suspend fun useAccessToken(WEB_API_URL: String, accessToken: String): Response {
        return withContext(Dispatchers.IO) {
            ApiClient.performGetApiRequest(WEB_API_URL, accessToken)
        }
    }
    ```

    Define the `performGetApiRequest()` function as shown in the following code:

    ```kotlin
    object ApiClient {
        private val client = OkHttpClient()
    
        fun performGetApiRequest(WEB_API_URL: String, accessToken: String): Response {    
            val requestBuilder = Request.Builder()
                    .url(WEB_API_URL)
                    .addHeader("Authorization", "Bearer $accessToken")
                    .get()
    
            val request = requestBuilder.build()
    
            client.newCall(request).execute().use { response -> return response }
        }
    }
    ```

## Configure custom claims provider

If you want to add claims from an external system into the token that is issued to your app, use a [custom claims provider](custom-claims-provider-overview). A custom claims provider is made up of a custom authentication extension that calls an external REST API to fetch claims from external systems.

Follow the steps in [Configure a custom claim provider](/en-us/entra/identity-platform/custom-extension-tokenissuancestart-configuration?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json) to add claims from an external system into your security tokens.