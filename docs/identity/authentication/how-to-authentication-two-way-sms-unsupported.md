---
layout: Conceptual
title: Two-way SMS no longer supported - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-authentication-two-way-sms-unsupported
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Explains how to enable another method for users who still use two-way SMS.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: dawoo
locale: en-us
document_id: d9ca6a61-ba3e-12da-9251-2e969bc33e5c
document_version_independent_id: 017f8369-6136-6425-adad-891715223ba1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-authentication-two-way-sms-unsupported.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-authentication-two-way-sms-unsupported
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-authentication-two-way-sms-unsupported.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: 45d43e96-56ae-63a7-d384-18e953fc4052
---

# Two-way SMS no longer supported - Microsoft Entra ID | Microsoft Learn

Two-way SMS for Azure Multi-Factor Authentication Server was originally deprecated in 2018, and no longer supported after February 24, 2021, except for organizations that received a support extension until August 2, 2021. Administrators should enable another method for users who still use two-way SMS.

Email notifications and Service Health notifications (portal toasts) were sent to affected admins on December 8, 2020 and January 28, 2021. The alerts went to the Owner, Co-Owner, Admin, and Service Admin RBAC roles tied to the subscriptions. If you've already completed the following steps, no action is necessary.

## Required actions

1. Enable the mobile app for your users, if you haven't done so already. For more information, see [Enable mobile app authentication with MFA Server](howto-mfaserver-deploy-mobileapp).
2. Notify your end users to visit your MFA Server [User portal](howto-mfaserver-deploy-userportal) to activate the mobile app. The [Microsoft Authenticator app](https://www.microsoft.com/en-us/account/authenticator) is the recommended verification option since it's more secure than two-way SMS. For more information, see [It's Time to Hang Up on Phone Transports for Authentication](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/it-s-time-to-hang-up-on-phone-transports-for-authentication/ba-p/1751752).
3. Change the user settings from two-way text message to mobile app as the default method.

## FAQ

### What if I don't change the default method from two-way SMS to the mobile app?

Two-way SMS fails after February 24, 2021. Users will see an error when they try to sign in and pass MFA.

### How do I change the user settings from two-way text message to mobile app?

You should change the user settings by following these steps:

1. In MFA Server, filter the user list for two-way text message.
2. Select all users.
3. Open the Edit Users dialog.
4. Change users from Text message to Mobile app.

    ![Screenshot of End Users](media/how-to-authentication-two-way-sms-unsupported/end-users.png)

### Do my users need to take any action? If yes, how?

Yes. Your end users need to visit your specific MFA Server User portal to activate the mobile app, if they haven't done so already. After you've done Step 3, any users that didn't visit the User Portal to set up the mobile app will start failing sign in until they visit the User portal to re-register.

### What if my users can't install the mobile app? What other options do they have?

The alternative to two-way SMS or the mobile app is a phone call. However, the Microsoft Authenticator app is the recommended verification method.

### Will one-way SMS be deprecated as well?

No, just two-way SMS is being deprecated. For MFA Server, one-way SMS works for a subset of scenarios:

- AD FS Adapter
- IIS Authentication (requires User Portal and configuration)
- RADIUS (requires that RADIUS clients support access challenge and that PAP protocol is used)

There are limitations to when one-way SMS can be used that make the mobile app a better alternative because it doesn’t require the verification code prompt. If you still want to use one-way SMS in some scenarios, then you could leave these checked, but change the **Company Settings** section, **General** tab **User Defaults Text Message** to **One-Way** instead of **Two-Way**. Lastly, if you use Directory Synchronization that defaults to SMS, you’d need to change it to One-Way instead of Two-Way.

### How can I check which users are still using two-way SMS?

To list these users, start **MFA Server**, select the **Users** section, click **Filter User List**, and filter for **Text Message Two-Way**.

### How do we hide two-way SMS as an option in the MFA portal to prevent users from selecting it in the future?

In MFA Server User portal, click **Settings**, you can clear **Text Message** so that it's not available. The same is true in the **AD FS** section if you're using AD FS for user enrollment.