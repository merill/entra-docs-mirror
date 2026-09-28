---
layout: Conceptual
title: Native authentication SDK attribute builder - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/concept-native-authentication-user-attribute-builder
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to use native authentication Android and iOS SDK attribute builders to prepare built-in and custom attributes.
manager: dougeby
ms.subservice: external
ms.topic: concept-article
ms.date: 2024-08-01T00:00:00.0000000Z
locale: en-us
document_id: a217838d-71b2-3bf0-9cde-f402f834f479
document_version_independent_id: a217838d-71b2-3bf0-9cde-f402f834f479
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/concept-native-authentication-user-attribute-builder.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/concept-native-authentication-user-attribute-builder
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/concept-native-authentication-user-attribute-builder.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 758b9e7c-2e0a-029f-a2cf-60bb616a00ee
---

# Native authentication SDK attribute builder - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In native authentication, the information you collect from the user during sign-up is configured in the user flow in the Microsoft Entra admin center. The name of the user attribute as it appears in the Microsoft Entra admin center is different from the variable name that you use when you reference it in your app.

Fortunately, the native authentication SDK enables you to build the user attributes and assign values to them before you use them in the SDKs `signUp()` method.

## Build user attributes

# [Android (Kotlin)](#tab/android-kotlin)
To build user attributes in the Android SDK:

- Use the utility class `UserAttribute.Builder` that the SDK provides. The `UserAttributes.Builder` class contains methods whose parameter is the value that you collect from the user.
- Identify the user attributes that you want to build, then use the following code snippet to build them:

    ```kotlin
        //build the user attributes, both built-in and custom attributes
        val userAttributes = UserAttributes.Builder()
            .country(country)
            .city(city)
            .displayName(displayName)
            .givenName(givenName)
            .jobTitle(jobTitle)
            .postalCode(postalCode)
            .state(state)
            .streetAddress(streetAddress)
            .surname(surname)
            .build() 
    
        CoroutineScope(Dispatchers.Main).launch {
            //use the userAttributes variable in your signUp method 
            val actionResult = authAuthClientInstance.signUp(
                username = emailAddress,
                attributes = userAttributes
            )
        }  
    ```
- To build [custom attributes](/en-us/entra/external-id/customers/concept-user-attributes#custom-user-attributes), use `UserAttribute.Builder` class `customAttribute()` method. The method accepts the custom attribute's programmable name, and the value of the attribute:

    ```kotlin
       val userAttributes = UserAttributes.Builder()
           .customAttribute("extension_2588abcdwhtfeehjjeeqwertc_loyaltyNumber", loyaltyNumber)
           .build() 
    
       CoroutineScope(Dispatchers.Main).launch {
           //use the userAttributes variable in your signUp method 
           val actionResult = authAuthClientInstance.signUp(
               username = emailAddress,
               attributes = userAttributes
           )
       }  
    ```

# [iOS/macOS (Swift)](#tab/ios-macos-swift)
To build user attributes in the iOS/macOS MSAL SDK:

- Identify the user attributes that you want to build, then create a dictionary variable, where:

    - the `key` is the programmable name of the user attribute, as a string. The programmable name can be for built-in or custom attribute.
    - the `value` in the value of the user attribute that you collect from the user.
- Identify the user attributes that you want to build, then use the following code snippet to build them:

    ```swift
       let attributes = [
           "country": "United States",
           "city": "Redmond",
           "displayName": displayName,
           "givenName": givenName,
           "jobTitle": jobTitle,
           "postalCode": postalCode,
           "state": state,
           "streetAddress": streetAddress,
           "surname": surname
       ]
    
       authAuthClientInstance.signUp(username: email, attributes: attributes, delegate: self)
    ```
- To build [custom attributes](/en-us/entra/external-id/customers/concept-user-attributes#custom-user-attributes), use `UserAttribute.Builder` class `customAttribute()` method. The method accepts the custom attribute's programmable name, and the value of the attribute:

    ```swift
            let attributes = [
                "country": "United States",
                "extension_2588abcdwhtfeehjjeeqwertc_loyaltyNumber", loyaltyNumber
            ]
    
            authAuthClientInstance.signUp(username: email, attributes: attributes, delegate: self)
    ```

---

To learn more about the programmable names of user profile attributes, see the [User profile attributes](/en-us/entra/external-id/customers/concept-user-attributes) article.