---
layout: Conceptual
title: Voice call authentication method - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-phone-options
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about using the voice call authentication method in Microsoft Entra ID to help improve and secure sign-in events
ms.topic: concept-article
ms.date: 2025-10-26T00:00:00.0000000Z
ms.reviewer: jupetter
ms.custom: sfi-image-nochange
locale: en-us
document_id: cd8e9708-dae9-55bb-4bcf-b2bad768b695
document_version_independent_id: e78950ad-e28a-a3be-b526-c77bfba7e82c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-authentication-phone-options.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-authentication-phone-options
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-authentication-phone-options.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
2PlusCloud:
- Azure
- M365
- Power
__autotagging_hash:
- CCB353B9D563C7288C34DF373AA0D41C0ED927AD7505FE2A8FA6D69E35A70B67
platformId: b02658f6-3301-f494-3801-a9444f4169bd
---

# Voice call authentication method - Microsoft Entra ID | Microsoft Learn

Microsoft recommends users move away from using text messages or voice calls for multifactor authentication. Modern authentication methods like [Microsoft Authenticator](concept-authentication-authenticator-app) are a recommended alternative. For more information, see [It's Time to Hang Up on Phone Transports for Authentication](https://aka.ms/hangup). Users can still verify themselves using a mobile phone or office phone as secondary form of authentication used for multifactor authentication or self-service password reset (SSPR).

You can [configure and enable users for SMS-based authentication](howto-authentication-sms-signin) for direct authentication using text message. Text messages are convenient for Frontline workers. With text messages, users don't need to know a username and password to access applications and services. The user instead enters their registered mobile phone number, receives a text message with a verification code, and enters that in the sign-in interface.

Note

Phone call verification isn't available for Microsoft Entra tenants with trial subscriptions. For example, if you sign up for a trial license Microsoft Enterprise Mobility and Security (EMS), phone call verification isn't available. Phone numbers must be provided in the format *+CountryCode PhoneNumber*, for example, *+1 4251234567*. There must be a space between the country/region code and the phone number.

## Mobile phone verification

For Microsoft Entra multifactor authentication or SSPR, users can choose to receive a text message with a verification code to enter in the sign-in interface, or receive a phone call.

If users don't want their mobile phone number to be visible in the directory but want to use it for password reset, administrators shouldn't populate the phone number in the directory. Instead, users should populate their **Authentication Phone** at [My Sign-Ins](https://aka.ms/setupsecurityinfo). Administrators can see this information in the user's profile, but it's not published elsewhere.

![Screenshot of the Microsoft Entra admin center that shows authentication methods with a phone number populated](media/concept-authentication-methods/user-authentication-methods.png)

Note

Phone extensions are supported only for office phones.

Microsoft doesn't guarantee consistent text message or voice-based Microsoft Entra multifactor authentication prompt delivery by the same number. In the interest of our users, we may add or remove short codes at any time as we make route adjustments to improve text message deliverability. Microsoft doesn't support short codes for countries/regions besides the United States and Canada.

Note

We apply delivery method optimizations such that tenants with a free or trial subscription may receive a text message or voice call.

### Text message verification

With text message verification during SSPR or Microsoft Entra multifactor authentication, a text message is sent to the mobile phone number containing a verification code. To complete the sign-in process, the verification code provided is entered into the sign-in interface.

Text messages can be sent over channels such as Short Message Service (SMS), Rich Communication Services (RCS), or WhatsApp.

Android users can enable RCS on their devices. RCS offers encryption and other improvements over SMS. For Android, MFA text messages may be sent over RCS rather than SMS. The MFA text message is similar to SMS, but RCS messages have more Microsoft branding and a verified checkmark so users know they can trust the message.

![Screenshot of Microsoft branding in RCS messages.](media/concept-authentication-methods/brand.png)

Some users may receive their verification codes in WhatsApp. Like RCS, these messages are similar to SMS, but have more Microsoft branding and a verified checkmark. The first time a user receives a verification code in WhatsApp, they're notified by SMS text message of the changed behavior.

Only users that have WhatsApp receive verification codes through this channel. To check if a user has WhatsApp, we silently try to deliver them a message in the app by using the phone number they registered for text message verification.

If users don't have any internet connectivity or they uninstall WhatsApp, they receive SMS verification codes. The phone number associated with Microsoft's WhatsApp Business Agent is: *+1 (217) 302 1989*.

![Screenshot of confirmation.](media/concept-authentication-methods/code.png)

### Phone call verification

With phone call verification during SSPR or Microsoft Entra multifactor authentication, an automated voice call is made to the phone number registered by the user. To complete the sign-in process, the user is prompted to press # on their keypad.

The calling number that a user receives the voice call from differs for each country. See [phone call settings](howto-mfa-mfasettings#phone-call-settings) to view all possible voice call numbers.

Note

SSPR can only be completed with a primary phone method or an office phone method. Alternate phone methods are only available for MFA.

## Office phone verification

With office phone call verification during SSPR or Microsoft Entra multifactor authentication, an automated voice call is made to the phone number registered by the user. To complete the sign-in process, the user is prompted to press # on their keypad.

## Troubleshooting phone options

If you have problems with phone authentication for Microsoft Entra ID, review the following troubleshooting steps:

- "You've hit our limit on verification calls" or "You've hit our limit on text verification codes" error messages during sign-in

    - Microsoft may limit repeated authentication attempts that are performed by the same user or organization in a short period of time. This limitation doesn't apply to Microsoft Authenticator or verification codes. If you have hit these limits, you can use the Authenticator App, verification code or try to sign in again in a few minutes.
- "Sorry, we're having trouble verifying your account" error message during sign-in

    - Microsoft may limit or block voice or text message authentication attempts that are performed by the same user, phone number, or organization due to high number of voice or text message authentication attempts. If you experience this error, you can try another method, such as Authenticator or verification code, or reach out to your admin for support.
- Blocked caller ID on a single device.

    - Review any blocked numbers configured on the device.
- Wrong phone number or incorrect country/region code, or confusion between personal phone number versus work phone number.

    - Troubleshoot the user object and configured authentication methods. Make sure that the correct phone numbers are registered.
- Wrong PIN entered.

    - Confirm the user has used the correct PIN as registered for their account (MFA Server users only).
- Call forwarded to voicemail.

    - Ensure that the user has their phone turned on and that service is available in their area, or use alternate method.
- User is blocked

    - Have a Microsoft Entra administrator unblock the user in the Microsoft Entra admin center.
- Text messaging platforms like SMS, RCS, or WhatsApp aren't subscribed on the device.

    - Have the user change methods or activate a text messaging platform on the device.
- Faulty telecom providers, such as when no phone input is detected, missing DTMF tones issues, blocked caller ID on multiple devices, or blocked text messages across multiple devices.

    - Microsoft uses multiple telecom providers to route phone calls and text messages for authentication. If you see any of these issues, have a user attempt to use the method at least five times within 5 minutes and have that user's information available when contacting Microsoft support.
- Poor signal quality.

    - Have the user attempt to log in using a wi-fi connection by installing the Authenticator app.
    - Or use a text message instead of phone (voice) authentication.
- Phone number is blocked and unable to be used for Voice MFA

    - There are a few country codes blocked for voice MFA unless your Microsoft Entra administrator has opted in for those country codes. Have your Microsoft Entra administrator opt-in to receive MFA for those country codes.
    - Or, use Microsoft Authenticator instead of voice authentication.