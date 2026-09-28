---
layout: Conceptual
title: Call an API in iOS/macOS app by using native authentication - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-native-authentication-ios-sign-in-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to acquire multiple access tokens and call an API in iOS/macOS app by using native authentication.
manager: pmwongera
ms.subservice: external
ms.topic: tutorial
ms.date: 2024-08-12T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 97dbc16b-9b78-c597-5ed1-1b66a58850ec
document_version_independent_id: 97dbc16b-9b78-c597-5ed1-1b66a58850ec
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-native-authentication-ios-sign-in-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-native-authentication-ios-sign-in-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-native-authentication-ios-sign-in-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 172d3bbb-ee4d-7ed9-71d1-2a9d5c05444d
---

# Call an API in iOS/macOS app by using native authentication - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial, you learn how to acquire an access token and call an API in your iOS/macOS app. Microsoft Authentication Library (MSAL) native authentication SDK for iOS/macOS allows you to acquire multiple access tokens with a single sign-in. This capability allows you to acquire one or more access tokens without requiring a user to reauthenticate.

In this tutorial, you:

- Acquire one or multiple access tokens.
- Call an API

## Prerequisites

- Complete the steps in [Sign in users and call an API in sample iOS mobile app by using native authentication](quickstart-native-authentication-ios-call-api).
- Complete the steps in [Tutorial: Add sign-in and sign-out in iOS/macOS app by using native authentication](tutorial-native-authentication-ios-macos-sign-in-sign-out). This tutorial shows you how to sign in users in your iOS/macOS app by using native authentication.

## Acquire one or multiple access tokens

MSAL native authentication SDK can store multiple access tokens. After signing in, you can obtain an access token by using the `getAccessToken(parameters:)` function and specifying the scopes for the new access token you wish to grant.

1. Declare and set values for a set of API scopes by using the following code snippet:

    ```swift
    let protectedAPIUrl1: String? = nil
    let protectedAPIUrl2: String? = nil 
    let protectedAPIScopes1: [String] = []
    let protectedAPIScopes2: [String] = []
    
    var accessTokenAPI1: String?
    var accessTokenAPI2: String?
    ```

    - Initialize `protectedAPIUrl1` with the URL of your first web API.
    - Initialize `protectedAPIUrl2` with the URL of your second web API.
    - Define `protectedAPIScopes1` with scopes for your first API, like `["api://<Resource_App_ID>/ToDoList.Read", "api://<Resource_App_ID>/ToDoList.ReadWrite"]`.
    - Define `protectedAPIScopes2` with scopes for your second API, similar to `protectedAPIScopes1`.
    - Declare the optional string variables `accessTokenAPI1` and `accessTokenAPI2`.
2. Signs in user by using the following code snippet:

    ```swift
    @IBAction func signInPressed(_: Any) {
        guard let email = emailTextField.text, let password = passwordTextField.text else {
            resultTextView.text = "Email or password not set"
            return
        }
    
        print("Signing in with email \(email) and password")
    
        showResultText("Signing in...")
        let parameters = MSALNativeAuthSignInParameters(username: email)
        parameters.password = password
        nativeAuth.signIn(parameters: parameters, delegate: self)
    }
    ```

    The `signInPressed` method handles the sign-in button press. It checks if the email and password fields are filled. If either is empty, it shows "Email or password not set." If both fields are filled, it logs the email, displays "Signing in...", and initiates the sign-in using the `signIn` method from `nativeAuth` with the provided email and password. The SDK retrieves a token valid for the default OIDC scopes (openid, offline\_access, profile) because no scopes are specified.
3. Acquire one or multiple access tokens by using the following code snippet:

    ```swift
    @IBAction func protectedApi1Pressed(_: Any) {
        guard let url = protectedAPIUrl1, !protectedAPIScopes1.isEmpty else {
            showResultText("API 1 not configured.")
            return
        }
    
        if let accessToken = accessTokenAPI1 {
            accessProtectedAPI(apiUrl: url, accessToken: accessToken)
        } else {
            let parameters = MSALNativeAuthGetAccessTokenParameters()
            parameters.scopes = protectedAPIScopes1
            accountResult?.getAccessToken(parameters: parameters, delegate: self)
            let message = "Retrieving access token to use with API 1..."
            showResultText(message)
            print(message)
        }
    }
    
    @IBAction func protectedApi2Pressed(_: Any) {
        guard let url = protectedAPIUrl2, !protectedAPIScopes2.isEmpty else {
            showResultText("API 2 not configured.")
            return
        }
    
        if let accessToken = accessTokenAPI2 {
            accessProtectedAPI(apiUrl: url, accessToken: accessToken)
        } else {
            let parameters = MSALNativeAuthGetAccessTokenParameters()
            parameters.scopes = protectedAPIScopes2
            accountResult?.getAccessToken(parameters: parameters, delegate: self)
            let message = "Retrieving access token to use with API 2..."
            showResultText(message)
            print(message)
        }
    }
    ```

    The `protectedApi1Pressed` and `protectedApi2Pressed` methods manage the process of acquiring access tokens for two distinct sets of scopes. They first ensure that each API's URL and scopes are properly configured. If an access token for the API is already available, it directly accesses the API. Otherwise, it requests an access token and informs the user about the ongoing token retrieval process.

    To assign an access token to `protectedAPIScopes1` and `protectedAPIScopes2`, use the following snippet:

    ```swift
    func onAccessTokenRetrieveCompleted(result: MSALNativeAuthTokenResult) {
        print("Access Token: \(result.accessToken)")
    
        if protectedAPIScopes1.allSatisfy(result.scopes.contains),
           let url = protectedAPIUrl1
        {
            accessTokenAPI1 = result.accessToken
            accessProtectedAPI(apiUrl: url, accessToken: result.accessToken)
        }
    
        if protectedAPIScopes2.allSatisfy(result.scopes.contains(_:)),
           let url = protectedAPIUrl2
        {
            accessTokenAPI2 = result.accessToken
            accessProtectedAPI(apiUrl: url, accessToken: result.accessToken)
        }
    
        showResultText("Signed in." + "\n\n" + "Scopes:\n\(result.scopes)" + "\n\n" + "Access Token:\n\(result.accessToken)")
        updateUI()
    }
    
    func onAccessTokenRetrieveError(error: MSAL.RetrieveAccessTokenError) {
        showResultText("Error retrieving access token: \(error.errorDescription ?? "No error description")")
    }
    ```

    The `onAccessTokenRetrieveCompleted` method prints the access token to the console. It then checks if `protectedAPIScopes1` are included in the result's scopes and if `protectedAPIUrl1` is available; if so, it sets `accessTokenAPI1` and calls `accessProtectedAPI` with the URL and token. It performs a similar check for `protectedAPIScopes2` and `protectedAPIUrl2`, updating `accessTokenAPI2` and making the API call if conditions are met. Finally, the method displays a message with the signed-in status, scopes, and access token, and updates the UI.

    The `onAccessTokenRetrieveError` method displays an error message with the description of the access token retrieval error or a default message if no description is provided.

## Call an API

Use the following code snippets to call an API:

```swift
func accessProtectedAPI(apiUrl: String, accessToken: String) {
    guard let url = URL(string: apiUrl) else {
        let errorMessage = "Invalid API url"
        print(errorMessage)
        DispatchQueue.main.async {
            self.showResultText(errorMessage)
        }
        return
    }
    
    var request = URLRequest(url: url)
    request.httpMethod = "GET"
    request.setValue("Bearer \(accessToken)", forHTTPHeaderField: "Authorization")
    
    let task = URLSession.shared.dataTask(with: request) { data, response, error in
        if let error = error {
            print("Error found when accessing API: \(error.localizedDescription)")
            DispatchQueue.main.async {
                self.showResultText(error.localizedDescription)
            }
            return
        }
        
        guard let httpResponse = response as? HTTPURLResponse, (200...299).contains(httpResponse.statusCode)
        else {
            DispatchQueue.main.async {
                self.showResultText("Unsuccessful response found when accessing the API")
            }
            return
        }
        
        guard let data = data, let result = try? JSONSerialization.jsonObject(with: data, options: []) else {
            DispatchQueue.main.async {
                self.showResultText("Couldn't deserialize result JSON")
            }
            return
        }
        
        DispatchQueue.main.async {
            self.showResultText("""
                            Accessed API successfully using access token.
                            HTTP response code: \(httpResponse.statusCode)
                            HTTP response body: \(result)
                            """)
        }
    }
    
    task.resume()
}
```

The `accessProtectedAPI` method sends a GET request to the specified API endpoint using the provided access token. It configures the request with the token in the Authorization header. When it receives a successful response (HTTP status code 200-299), it deserializes the JSON data and updates the UI with the HTTP status code and response body. If an error occurs during the request or response handling, it displays the error message in the UI. This method allows access to either API 1 or API 2, depending on the URL and access token provided.