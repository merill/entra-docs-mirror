---
layout: Conceptual
title: QR code authentication method in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-qr-code
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about using QR code authentication method in Microsoft Entra ID to help improve and secure sign-in events for frontline workers.
ms.topic: concept-article
ms.date: 2026-06-26T00:00:00.0000000Z
contributors: minatoruan
ms.reviewer: anjusingh
locale: en-us
document_id: a1dbddeb-acbc-7c9b-da81-c17016cadcd9
document_version_independent_id: a1dbddeb-acbc-7c9b-da81-c17016cadcd9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-authentication-qr-code.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-authentication-qr-code
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-authentication-qr-code.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 98f81a84-4fdb-a18c-e7de-4a90655dc237
---

# QR code authentication method in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

QR code authentication method enables frontline workers to sign in efficiently in apps on shared devices. Users can use a unique QR code provided to them and enter their PIN to sign in, eliminating the need to enter intricate usernames and passwords. Currently, QR code authentication is supported only on mobile devices that run iOS/iPadOS or Android.

Before you enable QR code authentication method, review the best practices for using security controls for work or home access for frontline workers. For more information, see [Best practices to protect frontline workers](/en-us/entra/identity-platform/security-best-practices-for-frontline-workers).

## What is QR code authentication?

QR code authentication is a simple authentication method primarily designed for frontline workers. It consists of a unique QR code and a numeric PIN. The QR code serves as an identifier and is unique to the user. It can be downloaded and printed by using the Microsoft Entra admin center, My Staff, or Microsoft Graph. For convenience, the QR code can be attached to a badge or any other wearable item.

Authentication Administrators provide a temporary PIN to users, who then change it during sign-in. Only the user knows the PIN. It's exclusively bound to the QR code only. It can't be used with other user identifiers, such as a username or phone number. QR code authentication is a single-factor method in which the PIN (something you know) is a credential.

## Benefits of QR code authentication

| Benefit | Description |
| --- | --- |
| Easier and faster sign-in | Frontline workers don't have to enter complex usernames or passwords to sign in multiple times into shared devices throughout their shift. |
| Inexpensive | Printing a QR code costs less than a hardware key, which can be cost prohibitive for organizations with temporary frontline workers. |

### PIN properties

The following policies are applied when an Authentication Policy Administrator creates or resets a PIN.

| Policy | Values |
| --- | --- |
| Allowed characters | Numbers (0-9) |
| Unallowed characters | - Characters (A-Z, a-z)- Symbols (- @ # $ % ^ & \* - \_ ! + = [ ] { } | \ : ' , . ? / ` ~ " ( ) ; &lt; &gt;)- Unicode characters- Blank space |
| PIN length | 8-20 digits |
| PIN complexity | Enforced to avoid repetition and common sequences. The following patterns are checked:- Don't contain 0123456789 or 9876543210.- Don't repeat a sequence of 2-3 digits in the PIN, like 121212, or 123123 or 342342.An **Invalid PIN** error appears if the PIN includes unallowed characters or is less than the minimum PIN length. |

## Best security practices to implement with QR code authentication

We recommend the following measures when you enable QR code authentication method as it's a single-factor authentication (something you know).

- QR code authentication is primarily for frontline workers (FLW) and not for information workers (IW). We recommend phishing-resistant authentication or MFA for IW.
- Don't enable QR code authentication for all the users in your tenant. Enable only for target users who will be using this auth method, for example, create a group for frontline workers and enable QR code auth only for them in Microsoft Entra Authentication Methods policies.
- Combine QR code authentication with Conditional Access policies as another security layer. We recommended policies such as compliant devices, access within network, allow for certain applications, and shared device mode.
- Enforce phishing-resistant authentication or MFA when users access resources from outside of the store or workplace network.
- Replace QR codes that are lost or stolen.
- Enforce [sign-in risk based Conditional Access policy](/en-us/entra/id-protection/concept-identity-protection-policies#sign-in-risk-based-conditional-access-policy) to block access.

## Enforce QR code sign-in with a custom authentication strength

To require QR code sign-in for a specific group of users, such as frontline workers, a specific resource, or both, create a custom Conditional Access authentication strength that includes **QR code** under **Single factor authentication**. Then use the custom authentication strength in a Conditional Access policy for the resources and users that need QR code sign-in. For steps, see [Create and manage custom Conditional Access authentication strengths](concept-authentication-strength-advanced-options#create-a-custom-authentication-strength).

## QR code configurations in the Authentication method policy

Authentication Policy Administrators can enable QR code in Authentication methods in the Microsoft Entra admin center. QR code authentication is disabled by default.

In the Authentication method policy for QR code, you can configure:

- PIN length: 8-20 digits.
- Lifetime of standard QR code: 1-395 days. Default is 365 days. An Authentication Policy Administrator can change the default value when they add a standard QR code for a user.

    For example, an admin can set the value to 30 days in the Authentication method policy. For every user in that tenant, the default expiration of a standard QR code is 30 days. An admin can change the default lifetime of the standard QR code for a specific user.

In this screenshot, the PIN length is set to the default of eight digits. The lifetime for the standard QR code is reduced to 200 days.

![Screenshot that shows QR code settings.](media/concept-authentication-qr-code/qr-code-settings.png)

## Functional details of QR code authentication method

When an Authentication Policy Administrator adds the QR code authentication method for a user, it generates a standard QR code and PIN. To create a temporary QR code, they need to edit the QR code authentication method.

A temporary QR code helps when a user forgets to bring their badge with standard QR code. It has a shorter lifetime, up to 12 hours. When a QR code authentication method is deleted for the user, they can't sign-in with their existing QR codes and PIN.

A PIN works with both standard and temporary QR codes because PIN is valid for the QR code authentication method. An Authentication Policy Administrator can provide a custom PIN or generate a PIN when they create a QR code authentication method. They can copy a temporary PIN only when they generate it. The PIN is then masked to prevent exposure.

The usability states for a standard QR code, a temporary QR code, and the PIN for a QR code authentication method aren't related to each other. For example, an active QR code authentication method can have a deleted or expired standard QR code, and an active temporary QR code. At any given point of time, there can be only a single active standard QR code and a single active temporary QR code.

The following table lists examples for combinations for the states for a standard QR code, a temporary QR code, and PIN. An active QR code and active PIN are required for successful authentication.

| Standard QR code | Temporary QR code | PIN for QR code authentication method |
| --- | --- | --- |
| Active | Doesn't exist | Temporary, or user updated |
| Active | Active | Temporary, or user updated |
| Deleted | Doesn't exist | Temporary, or user updated |
| Expired | Active | Temporary, or user updated |
| Expired | Expired | Temporary, or user updated |

For more information about how to manage QR codes, see [How to enable the QR code authentication method in Microsoft Entra ID](how-to-authentication-qr-code).

## User sign-in experience with QR code authentication

Users can sign in with a QR code by using the web sign-in experience or an optimized app sign-in experience.

### Mobile web sign-in experience

You can use Microsoft's web browser sign-in experience (login.microsoft.com) to authenticate users. Users can click **Sign in options** &gt; **Sign in to an organization** &gt; **Sign in with a QR code**.

![Screenshot that shows web sign-in experience.](media/concept-authentication-qr-code/sign-in-web.png)

### Mobile app sign-in experience

You can optimize sign-in for your apps by using Microsoft Authentication Library (MSAL) to add QR code as an option on the sign-in page. Then users can scan the QR code with two fewer clicks. This optimized sign-in experience is available in BlueFletch and Jamf app launchers.

For more information about how to optimize the sign-in experience or suppress camera consent prompt, see:

- [Set up optimized QR code authentication experience in Android app](../../identity-platform/android-qr-code-pin-authentication)
- [Set up optimized QR code authentication experience in iOS app](../../identity-platform/ios-qr-code-pin-authentication)

![Screenshot that shows Teams sign-in experience.](media/concept-authentication-qr-code/teams.png)

## Unsupported user scenarios in current release

- Self-service PIN reset for users
- Bulk provisioning of QR code and PIN
- QR code scan by barcode scanners
- QR code authentication doesn't work with desktop apps or browsers
- Custom tenant endpoint for sign in
- Configurable PIN protection policies that define account lockout threshold, duration, or PIN complexity

## Known limitation

If you enable QR code authentication for a user, they need to sign-in with an existing authentication method before they can sign in with a QR code for the first time, or they see an **Incorrect QR code** error.

For example:

- You enable QR code authentication for a user.
- The user needs to sign in with their password or another sign-in method.
- For subsequent sign-ins, they can sign in with a QR code.

The user needs to sign in with another method because the cached user authentication method policy isn't updated until the user is authenticated again.