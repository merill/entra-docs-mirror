---
layout: Conceptual
title: Enable self-service password reset - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-enable-password-reset-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to enable self-service password reset so your customers can reset their own passwords without admin assistance.
ms.topic: how-to
ms.date: 2025-09-16T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: 8af59c6b-3d0d-3e29-26ad-b75b4c9af68c
document_version_independent_id: 38739490-80a0-f5c6-e9cd-2083923c662e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-enable-password-reset-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-enable-password-reset-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-enable-password-reset-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 36f8fe56-2373-6535-9b0e-9da8c1dcb311
---

# Enable self-service password reset - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Self-service password reset (SSPR) in Microsoft Entra External ID gives customers the ability to change or reset their password, with no administrator or help desk involvement. If a customer's account is locked or they forget their password, they can follow prompts to unblock themselves and get back to work.

## How the password reset process works

Self-service password reset (SSPR) supports two authentication methods: email one-time passcode (Email OTP) and SMS. When SSPR is enabled, users who forget their password can verify their identity using either Email OTP or SMS. With one-time passcode authentication, a passcode is sent by email or SMS. After entering the passcode, the user is prompted to create a new password.

The process works as follows:

1. From the app, the user selects **Sign in**.
2. On the sign-in page, they enter their email address and choose **Next**.
3. If the user forgot their password, they select **Forgot password?**.
4. The user is prompted to choose how to verify their identity. They can select a one-time passcode sent to their email or phone, based on the methods they registered.
5. A one-time passcode is sent to the email address they entered on the first page or to their registered phone number.
6. The user enters the passcode to continue.
7. After successfully verifying their identity, the user is prompted to create a new password.

## Prerequisites

- If you haven't already created your own external tenant, create one now.
- Have at least the [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) role.
- If you haven't already created a User flow, [create one](how-to-user-flow-sign-up-sign-in-customers) now.

## Enable self-service password reset for customers

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the external tenant you created earlier from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
4. From the list of **User flows**, select the user flow you want to enable SSPR.
5. Make sure that the sign-up user flow registers **Email with password** as an authentication method under **Identity providers**.

    ![Screenshot that shows how to enable email authentication.](media/how-to-enable-password-reset-customers/email-authentication-method.png)

### Enable authentication method for password reset

To enable self-service password reset, configure the authentication method for all users or for a specific group in your tenant. Choose one of the following tabs to see the steps for each method.

# [Email OTP](#tab/emailotp)
The following steps show how to enable **Email OTP** as an authentication method for self-service password reset.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com). If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu and switch to your external tenant from the **Directories + subscriptions** menu.
2. Browse to **Entra ID** &gt; **Authentication methods**.
3. Under **Policies** &gt; **Method** select **Email OTP**.

    ![Screenshot that shows authentication methods.](media/how-to-enable-password-reset-customers/authentication-methods.png)
4. Under **Enable and Target**, turn on Email OTP.
5. Under **Include**, choose **All users** or **Select groups** to specify who can use this method.

    ![Screenshot of enabling OTP.](media/how-to-enable-password-reset-customers/enable-otp.png)
6. Select **Save**.

# [SMS](#tab/sms)
To use SMS for self-service password reset, users need to register their phone number as a multifactor authentication (MFA) method. There are two ways to do this:

- MFA registration happens automatically when an admin sets up a Conditional Access policy that requires [MFA](/en-us/entra/identity/conditional-access/policy-all-users-mfa-strength).
- Admins can manually add their phone number under [Authentication methods](/en-us/entra/identity/authentication/howto-mfa-userdevicesettings#add-or-change-authentication-methods-for-a-user).

The following steps show how to enable **SMS** as an authentication method for self-service password reset.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com). If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu and switch to your external tenant from the **Directories + subscriptions** menu.
2. Browse to **Entra ID** &gt; **Authentication methods**.
3. Under **Policies** &gt; **Method** select **SMS**.

    ![Screenshot that shows authentication methods including SMS.](media/how-to-enable-password-reset-customers/authentication-methods-sms.png)
4. Under **Enable and Target**, turn on SMS.
5. Under **Include**, choose **All users** or **Select groups** to specify who can use this method.

    ![Screenshot of enabling SMS.](media/how-to-enable-password-reset-customers/enable-sms.png)

Note

Self-service password reset with Phone SMS includes built-in integration with the Phone Reputation platform to detect telephony fraud in real time. Each request returns an *Allow*, *Block*, or *Challenge* decision to help protect users. SMS-based password reset is part of an add-on feature with [tiered pricing](/en-us/entra/external-id/customers/concept-multifactor-authentication-customers#sms-pricing-tiers-by-countryregion) based on location or region. Charges per SMS include fraud protection services.

1. Select **I Acknowledge** to accept the SMS terms of use.
2. Select **Save**.

---

### Enable the password reset link (optional)

You can hide, show, or customize the self-service password reset link on the sign-in page.

1. In the search bar, type and select **Company Branding**.
2. Under **Default sign-in** select **Edit**.
3. On the **Sign-in form** tab, scroll to the **Self-service password reset** section and select **Show self-service password reset**.

    ![Screenshot of the company branding Self-service password reset.](media/how-to-customize-branding-customers/company-branding-self-service-password-reset.png)
4. Select **Review + save** and **Save** on the **Review** tab.

For more details, check out the [Customize the neutral branding in your external tenant](how-to-customize-branding-customers#to-customize-self-service-password-reset) article.

## Test self-service password reset

To go through the self-service password reset flow:

1. Open your application, and select **Sign-in**.
2. In the sign-in page, enter your **Email address** and select **Next**.

    ![Screenshot that shows the sign-in page.](media/how-to-enable-password-reset-customers/sign-in.png)
3. Select the **Forgot password?** link.

    ![Screenshot that shows the forgot password link.](media/how-to-enable-password-reset-customers/forgot-password.png)
4. If SMS is available for self-service password reset, you can choose to receive a one-time passcode by email or phone. Enter the passcode sent to your email address or phone number.
5. Once you're authenticated, you're prompted to enter a new password. Provide a **New password**, and **Confirm password**, then select **Reset password** to sign in to your application.

    ![Screenshot that shows the update password screen.](media/how-to-enable-password-reset-customers/update-password.png)