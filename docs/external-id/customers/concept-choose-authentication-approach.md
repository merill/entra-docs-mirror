---
layout: Conceptual
title: Choose an authentication approach - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/concept-choose-authentication-approach
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Compare browser-delegated and native authentication in Microsoft Entra External ID and choose the right approach for your customer-facing app.
ai-usage: ai-assisted
ms.topic: concept-article
ms.date: 2026-04-16T00:00:00.0000000Z
locale: en-us
document_id: 5f5d53c5-c4f6-c3ae-683c-1ff67284213e
document_version_independent_id: 5f5d53c5-c4f6-c3ae-683c-1ff67284213e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/concept-choose-authentication-approach.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/concept-choose-authentication-approach
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/concept-choose-authentication-approach.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: a3290c41-db73-af3a-cbf2-a07b17177110
---

# Choose an authentication approach - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Browser-delegated authentication and native authentication are two sign-in approaches in Microsoft Entra External ID that define how your customer-facing app handles the authentication experience. Both approaches are fully supported, but they differ in user experience, development effort, and security model. Understanding these differences helps you choose the approach that best fits your app.

With **browser-delegated authentication**, your app redirects users to a Microsoft-hosted sign-in page in a system browser or embedded web view. Microsoft Entra handles the entire authentication flow, and your app receives tokens after sign-in completes. This approach requires minimal code and offers built-in branding customization.

With **native authentication**, you build the sign-in UI experience directly into your app by using the Microsoft Authentication Library (MSAL) SDK or the native authentication API. Users never leave your app. You control every aspect of the UI, but your team is responsible for building and maintaining the authentication experience.

## When to use browser-delegated authentication

Browser-delegated authentication is the better fit when:

- Your app can accommodate a browser redirect during sign-in without disrupting the user experience.
- You prefer lower implementation and maintenance effort. Microsoft manages security updates and new features automatically.
- You want to support the broadest range of platforms and languages with less code.

For specific feature availability, see the feature comparison.

## When to use native authentication

Native authentication is the better fit when:

- You need full control over the sign-in UI so it blends seamlessly into your app.
- A browser redirect would disrupt the user experience for your target platform.
- Your organization operates both the app and the authorization server, and your users perceive them as a single entity.
- Your development team can take on the additional implementation effort and ongoing maintenance.

For specific feature availability, see the feature comparison.

## Feature comparison

The following table shows which features are available in each approach.

| Feature | Browser-delegated authentication | Native authentication |
| --- | --- | --- |
| Sign up and sign in with email one-time passcode (OTP) | ✔️ | ✔️ |
| Sign up and sign in with email and password | ✔️ | ✔️ |
| Sign in with email and password can use username (alias) and password | ✔️ | ✔️ |
| Self-service password reset (SSPR) | ✔️ | ✔️ |
| Custom claims provider | ✔️ | ✔️ |
| Multifactor authentication with email one-time passcode (OTP) | ✔️ | ✔️ |
| Multifactor authentication with SMS one-time passcode (OTP) | ✔️ | ✔️ |
| Social identity provider sign-in (Apple, Facebook, and Google)^1^ | ✔️ | ✔️ |
| Single sign-on (SSO)^2^ | ✔️ | ✔️ |

^1^ Even with native authentication, social sign-in still uses a browser window for the identity provider step.

^2^ Native authentication supports SSO for embedded web views only. Cross-app SSO through system browsers isn't available with native authentication.

## Supported languages and frameworks

The following languages and frameworks are supported for each approach.

| Approach | Supported languages and frameworks |
| --- | --- |
| Browser-delegated authentication | - ASP.NET Core<br>- Android (Kotlin, Java)<br>- iOS/macOS (Swift, Objective-C)<br>- JavaScript<br>- React<br>- Angular<br>- Node.js<br>- Python<br>- Java |
| Native authentication | - Android (Kotlin, Java)<br>- iOS/macOS (Swift, Objective-C)<br>- Web (JavaScript, React, Angular)<br><br> For other languages and platforms, you can use the [native authentication API](/en-us/entra/identity-platform/reference-native-authentication-api). |

## Security considerations

Browser-delegated authentication is the more secure option. Microsoft manages the sign-in surface, which reduces your app's exposure to phishing and credential-harvesting attacks.

With native authentication, your development team shares security responsibility with Microsoft Entra. Your team must follow security best practices for handling user credentials. Before you choose native authentication, discuss the security implications with your app's business owner and development team.