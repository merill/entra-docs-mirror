---
layout: Conceptual
title: SMS-based user sign-in for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-authentication-sms-signin
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to configure and enable users to sign-in to Microsoft Entra ID using SMS
ms.topic: how-to
ms.date: 2026-03-04T00:00:00.0000000Z
ms.reviewer: anjusingh
ms.custom: sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: b7e90747-a144-01b7-8066-31b31e4eb6aa
document_version_independent_id: 4855c2d8-d647-1ca0-fe5f-670495df5042
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-authentication-sms-signin.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-authentication-sms-signin
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-authentication-sms-signin.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0cd46e47-e0dc-beb8-f75b-a494d3b5ee91
---

# SMS-based user sign-in for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

To simplify and secure sign-in to applications and services, Microsoft Entra ID provides SMS-based authentication. This method lets users such as frontline workers sign in using only a registered phone number and a one-time passcode (OTP) sent via SMS, without needing a username or password.

## Move to modern, phishing-resistant authentication

Important

Microsoft recommends phishing-resistant authentication methods for improved security. Consider migrating users to one of the following methods:

- [Passkeys (FIDO2)](concept-authentication-passkeys-fido2)
- [Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/hello-overview)
- [Certificate-based authentication](concept-certificate-based-authentication)

Microsoft Entra SMS-based authentication allows users to sign in using only a registered phone number and a one-time passcode (OTP) sent via SMS, no username or password required. This is different from Microsoft Entra SMS multifactor authentication, which typically requires a username, password, and SMS as an MFA method. This authentication method is primarily designed to simplify sign-in experience of frontline workers and not recommended for Information workers (IW).

Microsoft Entra also has an alternative approach for frontline-workers called [QR code authentication](concept-authentication-qr-code) that organizations may want to consider for frontline shared device scenarios.

The rest of this article shows you how to enable SMS-based authentication as a first factor for select users or groups in Microsoft Entra ID. For a list of apps that support using SMS-based sign-in, see [App support for SMS-based authentication](how-to-authentication-sms-supported-apps).

## Before you begin

Here are some important points before you start:

- You should enable SMS authentication *only* for frontline workers.
- If you enable SMS authentication, make sure you follow best practices for using security controls for work or home access for frontline workers. For more information, see [Best practices to protect frontline workers](/en-us/entra/identity-platform/security-best-practices-for-frontline-workers).
- If you enable SMS authentication for frontline workers, we suggest you move to using QR code authentication. For more information, see [Authentication methods in Microsoft Entra ID - QR code authentication method](/en-us/entra/identity/authentication/concept-authentication-qr-code).

To simplify and secure sign-in to applications and services, Microsoft Entra ID provides multiple authentication options. SMS-based authentication lets users such as frontline workers enter an SMS code as a first factor for sign in. Users don't need to provide, or even know, their user name and password.

After their account is created by an identity administrator, they can enter their phone number at the sign-in prompt. They receive an SMS authentication code that they can provide to complete the sign-in. This authentication method simplifies access to applications and services, especially for Frontline workers.

## Prerequisites

To complete this article, you need the following resources and privileges:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription.
    - If needed, [create a Microsoft Entra tenant](../../fundamentals/sign-up-organization) or [associate an Azure subscription with your account](../../fundamentals/how-subscriptions-associated-directory).
- You need at least the [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator) role in your Microsoft Entra tenant to enable SMS-based authentication.
- Each user that's enabled in the SMS authentication method policy must be licensed, even if they don't use it. Each enabled user must have one of the following licenses for Microsoft Entra ID, EMS, or Microsoft 365:
    - [Microsoft 365 F1 or F3](https://www.microsoft.com/licensing/news/m365-firstline-workers)
    - [Microsoft Entra ID P1 or P2](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing)
    - [Enterprise Mobility + Security (EMS) E3 or E5](https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing) or [Microsoft 365 E3 or E5](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans)
    - [Office 365 F3](https://www.microsoft.com/microsoft-365/business/office-365-f3?activetab=pivot%3aoverviewtab)

## Known issues

Here are some known issues:

- SMS-based authentication isn't currently compatible with Microsoft Entra multifactor authentication.
- Except for Teams, SMS-based authentication isn't compatible with native Office applications.
- SMS-based authentication isn't supported for B2B accounts.
- Federated users won't authenticate in the home tenant. They only authenticate in the cloud.
- If a user's default sign-in method is a text or call to your phone number, then the SMS code or voice call is sent automatically during multifactor authentication. As of June 2021, some apps will ask users to choose **Text** or **Call** first. This option prevents sending too many security codes for different apps. If the default sign-in method is the Microsoft Authenticator app ([which we highly recommend](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/it-s-time-to-hang-up-on-phone-transports-for-authentication/ba-p/1751752)), then the app notification is sent automatically.
- [Cross-tenant synchronization](/en-us/entra/identity/app-provisioning/known-issues?pivots=cross-tenant-synchronization) does not support users with SMS sign-in enabled.

## Enable the SMS-based authentication method

There are three main steps to enable and use SMS-based authentication in your organization:

- Enable the authentication method policy.
- Select users or groups that can use the SMS-based authentication method.
- Assign a phone number for each user account.
    - This phone number can be assigned in the Microsoft Entra admin center (which is shown in this article), and in *My Staff* or *My Account*.

First, let's enable SMS-based authentication for your Microsoft Entra tenant.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods** &gt; **Policies**.
3. From the list of available authentication methods, select **SMS**.

    ![Screenshot that shows how to select the SMS authentication method.](media/howto-authentication-sms-signin/authentication-methods-policy.png)
4. Select **Enable** and select **Target users**. You can choose to enable SMS-based authentication for *All users* or groups.

    Note

    To configure SMS-based authentication for first-factor (that is, to allow users to sign in with this method), check the **Use for sign-in** checkbox. Leaving this unchecked makes SMS-based authentication available for multifactor authentication and Self-Service Password Reset only.

    ![Enable SMS authentication in the authentication method policy window](media/howto-authentication-sms-signin/enable-sms-authentication-method.png)

## Assign the authentication method to users and groups

With SMS-based authentication enabled in your Microsoft Entra tenant, now select some users or groups to be allowed to use this authentication method.

1. In the SMS authentication policy window, set **Target** to *Select users*.
2. Choose to **Add All users or groups**, then select a test user or group, such as *Contoso User* or *Contoso SMS Users*.
3. When you've selected your users or groups, choose **Select**, then **Save** the updated authentication method policy.

Each user that's enabled in SMS authentication method policy must be licensed, even if they don't use it. Make sure you have the appropriate licenses for the users you enable in the authentication method policy, especially when you enable the feature for large groups of users.

## Set a phone number for user accounts

Users are now enabled for SMS-based authentication, but their phone number must be associated with the user profile in Microsoft Entra ID before they can sign-in. The user can [set this phone number themselves](https://support.microsoft.com/account-billing/set-up-sms-sign-in-as-a-phone-verification-method-0aa5b3b3-a716-4ff2-b0d6-31d2bcfbac42) in *My Account*, or you can assign the phone number using the Microsoft Entra admin center. Phone numbers can be set by those with at least the [Authentication Administrator](../role-based-access-control/permissions-reference#authentication-administrator) role.

When a phone number is set for SMS-based sign-in, it's also then available for use with [Microsoft Entra multifactor authentication](tutorial-enable-azure-mfa) and [self-service password reset](tutorial-enable-sspr).

1. Search for and select **Microsoft Entra ID**.
2. From the navigation menu on the left-hand side of the Microsoft Entra window, select **Users**.
3. Select the user you enabled for SMS-based authentication in the previous section, such as *Contoso User*, then select **Authentication methods**.
4. Select **+ Add authentication method**, then in the *Choose method* drop-down menu, choose **Phone number**.

    Enter the user's phone number, including the country code, such as *+1 xxxxxxxxx*. The Microsoft Entra admin center validates the phone number is in the correct format.

    Then, from the *Phone type* drop-down menu, select *Mobile*, *Alternate mobile*, or *Other* as needed.

    ![Set a phone number for a user in the Microsoft Entra admin center to use with SMS-based authentication](media/howto-authentication-sms-signin/set-user-phone-number.png)

    The phone number must be unique in your tenant. If you try to use the same phone number for multiple users, an error message is shown.
5. To apply the phone number to a user's account, select **Add**.

When successfully provisioned, a check mark appears for *SMS Sign-in enabled*.

## Test SMS-based sign-in

To test the user account that's now enabled for SMS-based sign-in, complete the following steps:

1. Open a new InPrivate or Incognito web browser window to https://www.office.com
2. In the top right-hand corner, select **Sign in**.
3. At the sign-in prompt, enter the phone number associated with the user in the previous section, then select **Next**.

    ![Enter a phone number at the sign-in prompt for the test user](media/howto-authentication-sms-signin/sign-in-with-phone-number.png)
4. An SMS message is sent to the phone number provided. To complete the sign-in process, enter the 6-digit code provided in the SMS message at the sign-in prompt.

    ![Enter the SMS confirmation code sent to the user's phone number](media/howto-authentication-sms-signin/sign-in-with-phone-number-confirmation-code.png)
5. The user is now signed in without the need to provide a username or password.

## Troubleshoot SMS-based sign-in

You can use the following scenarios and troubleshooting steps if you have problems with enabling and using SMS-based sign-in. For a list of apps that support using SMS-based sign-in, see [App support for SMS-based authentication](how-to-authentication-sms-supported-apps).

### Phone number already set for a user account

If a user has already registered for Microsoft Entra multifactor authentication or self-service password reset (SSPR), they already have a phone number associated with their account. This phone number isn't automatically available for use with SMS-based sign-in.

For more information on the end-user experience, see [SMS sign-in user experience for phone number](https://support.microsoft.com/account-billing/set-up-sms-sign-in-as-a-phone-verification-method-0aa5b3b3-a716-4ff2-b0d6-31d2bcfbac42).

### Error when trying to set a phone number on a user's account

If you receive an error when you try to set a phone number for a user account in the Microsoft Entra admin center, review the following troubleshooting steps:

1. Make sure that you're enabled for the SMS-based sign-in.
2. Confirm that the user account is enabled in the **SMS** authentication method policy.
3. Make sure you set the phone number with the proper formatting, as validated in the Microsoft Entra admin center (such as *+1 4251234567*).
4. Make sure that the phone number isn't used elsewhere in your tenant.
5. Check there's no voice number set on the account. If a voice number is set, delete and try to the phone number again.