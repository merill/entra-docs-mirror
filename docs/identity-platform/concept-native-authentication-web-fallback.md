---
layout: Conceptual
title: Native authentication web fallback - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/concept-native-authentication-web-fallback
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how you can use web fallback to improve the resilience of your customer apps that use native authentication.
manager: dougeby
ms.subservice: external
ms.topic: concept-article
ms.date: 2025-08-08T00:00:00.0000000Z
locale: en-us
document_id: b90c1737-f4e4-678c-5d39-48787d3d9b8a
document_version_independent_id: b90c1737-f4e4-678c-5d39-48787d3d9b8a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/concept-native-authentication-web-fallback.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/concept-native-authentication-web-fallback
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/concept-native-authentication-web-fallback.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: ad613520-1214-69f0-18d3-51891905be7c
---

# Native authentication web fallback - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Web fallback allows a client app that uses native authentication to use browser-delegated authentication as a fallback mechanism to improve resilience. This scenario happens when native authentication isn't sufficient to complete the authentication flow. For example, if the authorization server requires capabilities that the client can't provide.

All client apps that use native authentications needs to support web fallback.

## Web fallback flow

This flow shows how web fallback can happen:

- The client app collects initial information from the user and starts the authentication flow by making a request to Microsoft Entra.
- Microsoft Entra returns a success or error response. A success response indicates the client app can continue making requests Microsoft Entra. An error response can indicate the client can continue to prompt the user for more information and continue to make requests to Microsoft Entra. The error response can also indicate the client needs to use browser-delegated authentication.
- If the error response indicates the client needs to use browser-delegated authentication, the client continues the authentication flow in the browser.

### Example scenario

Let's look at an example when it's possible for Microsoft Entra to indicate that the client needs to use browser-delegated authentication:

- In the Microsoft Entra admin center, an administrator configures an app to use email with password authentication method.
- This configuration means Microsoft Entra requires the client app to have the ability to collect an email (username) and password from user. The client app communicates this ability to Microsoft Entra by sending *password* challenge type. Learn more about challenge types in [Native authentication challenge types](concept-native-authentication-challenge-types) article.
- The client app should also validate the email by submitting a one-time passcode that the server sends to the user's email. The client app communicates this ability to Microsoft Entra by sending *oob* challenge type. Learn more about challenge types in [Native authentication challenge types](concept-native-authentication-challenge-types) article
- If the client app doesn't send both *oob* and *password* challenge types, Microsoft Entra interprets it as the client app's inability to fulfill the set requirement. In this case, Microsoft Entra returns an error that indicates the client needs to use browser-delegated authentication.

## Support web fallback

If Microsoft Entra's response indicates that the client app needs to fall back to the browser-delegated authentication, we recommend you use a [Microsoft-built and supported authentication library](reference-v2-libraries).

Learn how to support web fallback in the following apps when you use native authentication:

- [Android apps](/en-us/entra/external-id/customers/tutorial-native-authentication-android-support-web-fallback).
- [iOS/macOS apps](/en-us/entra/external-id/customers/tutorial-native-authentication-ios-macos-support-web-fallback).
- [Single-page apps](tutorial-native-authentication-single-page-app-javascript-sdk-web-fallback).