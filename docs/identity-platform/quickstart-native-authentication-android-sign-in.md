---
layout: Conceptual
title: Sign in users in Android mobile app by using native authentication. - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-native-authentication-android-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure a sample Android (Kotlin) sample app to sign in customer users by using Microsoft Entra's native authentication.
manager: pmwongera
ms.subservice: external
ms.topic: how-to
ms.date: 2025-11-17T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 5d5907ef-efd6-f3ce-b852-9b3dd1fb0fe7
document_version_independent_id: 5d5907ef-efd6-f3ce-b852-9b3dd1fb0fe7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-native-authentication-android-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-native-authentication-android-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-native-authentication-android-sign-in.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 27537b80-046e-07f1-cc6b-234f46ac2310
---

# Sign in users in Android mobile app by using native authentication. - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this quickstart you learn how to run an Android sample application that demonstrates sign-up, sign in, sign out, and password reset scenarios using Microsoft Entra's [native authentication](concept-native-authentication).

## Prerequisites

- An Azure account with an active subscription. If you don't already have one, [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- This Azure account must have permissions to manage applications. Any of the following Microsoft Entra roles include the required permissions:

    - Application Administrator
    - Application Developer
- An external tenant. If you don't have one, [create a new external tenant](../external-id/customers/how-to-create-external-tenant-portal) in the Microsoft Entra admin center.
- If you haven't already done so, [Register an application in the Microsoft Entra admin center](quickstart-register-app). Make sure to:

    - Record the **Application (client) ID** and **Directory (tenant) ID** for later use.
    - [Grant admin consent](quickstart-register-app#grant-admin-consent-external-tenants-only) to the application.
- If you haven't already done so, [Create a user flow in the Microsoft Entra admin center](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers)
- [Associate your app registration with the user flow](/en-us/entra/external-id/customers/how-to-user-flow-add-application)
- [Android Studio](https://developer.android.com/studio).

## Enable public client and native authentication flows

To specify that this app is a public client and can use native authentication, enable public client and native authentication flows:

1. From the app registrations page, select the app registration for which you want to enable public client and native authentication flows.
2. Under **Manage**, select **Authentication**.
3. Under **Advanced settings**, allow public client flows:
    1. For **Enable the following mobile and desktop flows** select **Yes**.
    2. For **Enable native authentication**, select **Yes**.
4. Select **Save** button.

## Clone sample Android mobile application

1. Open Terminal and navigate to a directory where you want to keep the code.
2. Clone the application from GitHub by running the following command:

    ```bash
    git clone https://github.com/Azure-Samples/ms-identity-ciam-native-auth-android-sample 
    ```

## Configure the sample Android mobile application

1. In Android Studio, open the project that you cloned.
2. Open *app/src/main/res/raw/native\_auth\_sample\_app\_config.json* file.
3. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the **Application (client) ID** of the app you registered earlier.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't know your tenant subdomain, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).

You've now configured the app and it's ready to run.

## Run and test the sample Android mobile application

To build and run your app, follow these steps:

1. In the toolbar, select your app from the run configurations menu.
2. In the target device menu, select the device that you want to run your app on.

    If you don't have any devices configured, you need to either create an Android Virtual Device to use the Android Emulator or connect a physical Android device.
3. Select the **Run** button. The app opens the **Email & OTP** screen.

    [![Screenshot of user prompt to enter email in Android application.](media/native-authentication/android/android-email-otp.png)](media/native-authentication/android/android-email-otp-expanded.png#lightbox)
4. Enter a valid email address and select then **Sign up** button. The app opens the submit code screen and you receive an OTP code in the email address.

    [![Screenshot of user prompt to enter one-time passcode in Android application.](media/native-authentication/android/android-submit-code.png)](media/native-authentication/android/android-submit-code-expanded.png#lightbox)
5. Enter the OTP code that you receive in the email inbox and select **Next**. If the sign-up is successful, the app signs you in automatically. If you don't receive the OTP code in your email inbox, you can resend it after a while by selecting **Resend Passcode**.
6. To sign out, select the **Sign out** button.

### Other scenarios that this sample supports

This sample app also supports the following authentication flows:

- **Email + password** covers sign-in or sign-up flows with an email with password.
- **Email + password sign-up with user attributes** covers sign-up with email and password, and submitting user attributes.
- **Password reset** covers self-service password reset (SSPR).
- **Access Protected API** covers call a protected API after the user successfully signs up or signs in and acquires an access token.
- **Fallback to web browser** covers the use the browser-based authentication as a fallback mechanism when the user can't complete authentication through native authentication for whatever reason.

## Test email with password flow

In this section, you test email with password flow, with its variants such as, email with password sign-up with user attributes and SSPR:

1. Use the steps in [create a user flow](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers) to create a new user flow, but this time select **Email with password** as your authentication method. You need to configure **Country/Region** and **City** as the user attributes. Alternatively, you can modify the existing user flow to use **Email with password** (Select **External Identities** &gt; **User flows** &gt; **SignInSignUpSample** &gt; **Identity providers** &gt; **Email with password** &gt; **Save**).
2. Use the steps in [associate the application with the new user flow](../external-id/customers/how-to-user-flow-add-application) to add an app to your new user flow.
3. Run the sample app, then select the ellipsis menu (**...**) to open more options.
4. Select the scenario you want to test, such as **Email + password** or **Email + password sign-up with user attributes** or **Password reset**, then follow the prompts. To test **Password reset**, you need to first sign up a user, and [enable email one-time passcode](../external-id/customers/how-to-enable-password-reset-customers) for all users in your tenant.

## Test call a protected API flow

Use the steps in [Call a protected web API in a sample Android mobile app by using native authentication](quickstart-native-authentication-android-call-api) to call a protected web API from a sample Android mobile app.

## Enable sign-in with an alias or username

You can allow users who sign in with an email address and password to also sign in with a username and password. The username also called an alternate sign-in identifier, can be a customer ID, account number, or another identifier that you choose to use as a username.

You can assign usernames to the user account manually via the Microsoft Entra admin center or automate it in your app via the Microsoft Graph API.

Use the steps in [Sign in with an alias or username](../external-id/customers/how-to-sign-in-alias) article to allow your users to sign-in using a username in your application:

1. [Enable username in sign-in](../external-id/customers/how-to-sign-in-alias#enable-username-in-sign-in-identifier-policy).
2. [Create users with username in the admin center](../external-id/customers/how-to-sign-in-alias#create-and-update-users-with-username) or [update existing users to by adding a username](../external-id/customers/how-to-sign-in-alias#create-and-update-users-with-username). Alternatively, you can also [automate user creation and updating in your app by using the Microsoft Graph API](../external-id/customers/how-to-sign-in-alias#create-and-update-users-with-username).