---
layout: Conceptual
title: Native authentication challenge types - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/concept-native-authentication-challenge-types
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how apps that use native authentication notify native authentication API about the authentication flows that they support.
manager: dougeby
ms.subservice: external
ms.topic: concept-article
ms.date: 2026-02-27T00:00:00.0000000Z
locale: en-us
document_id: 96f43c9a-6adc-fe0d-02ef-180f440aaa71
document_version_independent_id: 96f43c9a-6adc-fe0d-02ef-180f440aaa71
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/concept-native-authentication-challenge-types.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/concept-native-authentication-challenge-types
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/concept-native-authentication-challenge-types.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 76327a0f-4f03-4314-fe83-4bea55bad4d7
---

# Native authentication challenge types - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Native authentication supports two authentication flows:

- Email with one-time passcode (OTP)
- Email and password with support for self-service password reset (SSPR)

A client app that uses native authentication to sign in users can use either authentication flow. To make successful calls to the native authentication API, the app must declare which authentication flows and capabilities it supports. The native authentication API enables client apps to advertise their supported challenge types and capabilities using predefined values.

## Challenge types

Challenge types are predefined values that client apps include in their requests to declare which authentication flows they support to the native authentication API.

The following table contains the supported challenge type values:

| Challenge type | Description |
| --- | --- |
| *password* | This challenge type indicates that the app supports collecting a password credential from the user. |
| *oob* | This challenge type indicates that the application supports using one-time password or passcode (OTP) codes sent to the user using a secondary channel. Currently, the API supports only email and SMS OTP. |
| *redirect* | This challenge type indicates that the application supports falling back to the browser-delegated authentication, also known as web fallback. All native authentication compliant apps must support this capability. This requirement means that in every call the app makes to the native authentication API, it must include this challenge type. If the client app fails to include this challenge type, the request fails. |

New values are added when native authentication supports new authentication methods.

## Challenge type values for native authentication flows

The following table summarizes the challenge type values an app should use for various authentication flows:

| - | Sign-up flow | Sign-in flow | SSPR |
| --- | --- | --- | --- |
| **Email with password** | *oob*, *password*, and *redirect* | *oob*, *password*, and *redirect* | *oob* and *redirect* |
| **Email OTP** | *oob* and *redirect* | *oob* and *redirect* | Not applicable |

**Important notes:**

- Apps that use the [native authentication API](reference-native-authentication-api) directly must include the *redirect* challenge type when declaring their supported challenge types.
- Apps that use native authentication SDKs (Android, iOS, or JavaScript) don't need to include the *redirect* challenge type as the SDK automatically includes it.

## Capabilities

In addition to challenge types, client apps can specify a list of *capabilities*. While `challenge_type` defines which authentication methods the app supports, `capabilities` indicate which additional flows the client app can handle and what UI experiences it can provide to users.

Native authentication API supports the following capabilities:

- `mfa_required`: Indicates that the client app can handle multifactor authentication (MFA) flows inline, including calling the `/introspect`, `/challenge`, and `/token` endpoints in sequence and displaying the appropriate UI for users to complete MFA challenges when required. Advertise this capability if your app integrates inline MFA scenarios such as risk-based MFA driven by Conditional Access authentication context (for example, third-party account takeover protection integrations that use a Web Application Firewall in front of native authentication endpoints). If the app doesn't advertise `mfa_required` and MFA is required, the native authentication API initiates a [web fallback](concept-native-authentication-web-fallback).
- `registration_required`: The client can handle strong authentication registration: it can call the registration APIs and show UI to guide users through registering strong authentication methods.

## Behavior for unsupported challenge types and capabilities

The following table summarizes the behavior when either the native authentication API or the client app doesn't support a given challenge type or capability:

| Scenario | Behavior |
| --- | --- |
| **Client app includes unsupported challenge type** | Native authentication API returns an error and treats the request as invalid. |
| **Client app includes unsupported capability** | Native authentication API returns an error and treats the request as invalid. |
| **Client app fails to include a required challenge type** | The app doesn't support a challenge type configured by the administrator. Native authentication API initiates a [web fallback](concept-native-authentication-web-fallback). |
| **Client app fails to include a required capability** | The app functions normally if MFA or strong authentication registration is not required. If these capabilities are required but not supported, native authentication API initiates a [web fallback](concept-native-authentication-web-fallback) to complete the authentication flow. |