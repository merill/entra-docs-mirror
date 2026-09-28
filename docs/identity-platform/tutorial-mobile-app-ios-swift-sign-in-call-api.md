---
layout: Conceptual
title: Sign in user and call a protected web API in iOS app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-mobile-app-ios-swift-sign-in-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: The tutorials provide a step-by-step guide on how to Sign in user and call a protected web API in iOS (Swift) app for authentication.
manager: pmwongera
ms.topic: tutorial
ms.date: 2024-05-09T00:00:00.0000000Z
ms.custom: 
zone_pivot_groups: entra-tenants
locale: en-us
document_id: a9183710-5ea8-a248-900f-e92f7ff57b02
document_version_independent_id: a9183710-5ea8-a248-900f-e92f7ff57b02
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-mobile-app-ios-swift-sign-in-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-mobile-app-ios-swift-sign-in-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-mobile-app-ios-swift-sign-in-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 1f67466f-3be3-125f-dd5b-0162958c968a
---

# Sign in user and call a protected web API in iOS app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

::: zone pivot="workforce"

This is the fourth tutorial in the tutorial series that guides you on signing in users and calling a protected web API using Microsoft Entra ID.

In this tutorial, you:

- Call a protected web API.

## Prerequisites

- [Tutorial: Sign in users in iOS (Swift) mobile app](tutorial-mobile-app-ios-swift-sign-in)

## Call API

Once you have a token, your app can use it in the HTTP header to make an authorized request to the Microsoft Graph:

| header key | value |
| --- | --- |
| Authorization | Bearer &lt;access-token&gt; |

Add the following code to the `ViewController` class:

```swift
    func getContentWithToken() {

        // Specify the Graph API endpoint
        let graphURI = getGraphEndpoint()
        let url = URL(string: graphURI)
        var request = URLRequest(url: url!)

        // Set the Authorization header for the request. We use Bearer tokens, so we specify Bearer + the token we got from the result
        request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")

        URLSession.shared.dataTask(with: request) { data, response, error in

            if let error = error {
                self.updateLogging(text: "Couldn't get graph result: \(error)")
                return
            }

            guard let result = try? JSONSerialization.jsonObject(with: data!, options: []) else {

                self.updateLogging(text: "Couldn't deserialize result JSON")
                return
            }

            self.updateLogging(text: "Result from Graph: \(result))")

            }.resume()
    }
```

See [Microsoft Graph API](https://graph.microsoft.com) to learn more about the Microsoft Graph API.

## Test your app

Build and deploy the app to a test device or simulator. You should be able to sign in and get tokens for Microsoft Entra ID or personal Microsoft accounts.

The first time a user signs into your app, they'll be prompted by Microsoft identity to consent to the permissions requested. While most users are capable of consenting, some Microsoft Entra tenants have disabled user consent, which requires admins to consent on behalf of all users. To support this scenario, register your app's scopes.

After you sign in, the app will display the data returned from the Microsoft Graph `/me` endpoint.

::: zone-end

::: zone pivot="external"

This is the fourth tutorial in the tutorial series that guides you on signing in users and calling a protected web API using Microsoft Entra External ID.

In this tutorial, you:

- Call a protected web API.

## Prerequisites

- [Tutorial: Sign in users in iOS (Swift) mobile app](tutorial-mobile-app-ios-swift-sign-in)
- An API registration that exposes at least one scope (delegated permissions) and one app role (application permission) such as *ToDoList.Read*. If you haven't already, follow the instructions for [call an API in a sample iOS mobile app](../external-id/customers/sample-native-authentication-ios-sample-app-call-web-api) to have a functional protected ASP.NET Core web API. Make sure you complete the following steps:

    - Register a web API application.
    - Configure API scopes.
    - Configure app roles.
    - Configure optional claims.
    - Clone or download sample web API.
    - Configure and run sample web API.

## Call API

To call a protected web API from your iOS app, use the following code:

```swift
    func getContentWithToken() {
        // Specify the API endpoint in _Configuration.swift_ file you created earlier
        guard let url = URL(string: Configuration.kProtectedAPIEndpoint) else {
            let errorMessage = "Invalid API url"
            print(errorMessage)
            updateLogging(text: errorMessage)
            return
        }
        var request = URLRequest(url: url)

        // Set the Authorization header for the request. We use Bearer tokens, so we specify Bearer + the token we got from the result
        request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")

        self.updateLogging(text: "Performing request...")

        URLSession.shared.dataTask(with: request) { data, response, error in

            if let error = error {
                self.updateLogging(text: "Couldn't get API result: \(error)")
                return
            }

            guard let httpResponse = response as? HTTPURLResponse,
                  (200...299).contains(httpResponse.statusCode)
            else {
                self.updateLogging(text: "Couldn't get API result: \(error)")
                return
            }

            guard let data = data, let result = try? JSONSerialization.jsonObject(with: data, options: []) else {
                self.updateLogging(text: "Couldn't deserialize result JSON")
                return
            }

            self.updateLogging(text: """
                                Accessed API successfully using access token.
                                HTTP response code: \(httpResponse.statusCode)
                                HTTP response body: \(result)
                                """)

            }.resume()
    }
```

The code specifies the API endpoint, ensuring its validity. Then, it constructs a request object, setting the authorization header with the access token obtained. After logging the initiation of the request, it performs the request asynchronously using `URLSession`.

Upon completion, it checks for any errors during the request. If an error occurs, it logs the corresponding message. Next, it verifies the success of the HTTP response, ensuring it falls within the range of 200 to 299 status codes. After, it deserializes the received JSON data. Finally, it updates the logging text, indicating successful access to the API along with relevant HTTP response details.

::: zone-end