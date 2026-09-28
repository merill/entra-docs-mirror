---
layout: Conceptual
title: Authentication Methods Activity - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-authentication-methods-activity
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Overview of the authentication methods that users register to sign in and reset passwords.
ms.topic: how-to
ms.date: 2025-10-22T00:00:00.0000000Z
ms.reviewer: dawoo
ms.custom: sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: cf2e7f7f-792d-3063-b672-f54f1e769cf3
document_version_independent_id: fca17480-6c8d-d067-1469-2771953de47e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-authentication-methods-activity.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-authentication-methods-activity
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-authentication-methods-activity.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 5759ca74-10d1-3ddb-002a-2312ebe25f12
---

# Authentication Methods Activity - Microsoft Entra ID | Microsoft Learn

The new authentication methods activity dashboard enables admins to monitor authentication method registration and usage across their organization. This reporting capability provides your organization with the means to understand what methods are being registered and how they're being used.

Note

For information about viewing or deleting personal data, see [Azure Data Subject Requests for the GDPR](/en-us/microsoft-365/compliance/gdpr-dsr-azure). For more information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## Permissions and licenses

Built-in and custom roles with the following permissions can access the Authentication Methods Activity blade and APIs:

- Microsoft.directory/auditLogs/allProperties/read
- Microsoft.directory/signInReports/allProperties/read

The following roles have the required permissions:

- Reports Reader
- Security Reader
- Global Reader
- Application Administrator
- Cloud Application Administrator
- Security Operator
- Security Administrator
- Global Administrator

A Microsoft Entra ID P1 or P2 license is required to access Usage and insights. Microsoft Entra multifactor authentication and self-service password reset (SSPR) licensing information can be found on the [Microsoft Entra pricing site](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## How it works

To access authentication method Usage and insights:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods** &gt; **Activity**.
3. There are two tabs in the report: **Registration** and **Usage**.

    ![Authentication Methods Activity overview](media/how-to-authentication-methods-usage-insights/registration-usage-tabs.png)

## Registration details

You can access the **Registration** tab to show the number of users capable of multifactor authentication, passwordless authentication, and self-service password reset.

Click any of the following options to pre-filter a list of user registration details:

- **Users capable of Azure multifactor authentication** shows the breakdown of users who are both:

    - Registered for a strong authentication method
    - Enabled by policy to use that method for MFA

    This number doesn't reflect users registered for MFA outside of Microsoft Entra ID.
- **Users capable of passwordless authentication** shows the breakdown of users who are registered to sign in without a password by using FIDO2, Windows Hello for Business, or passwordless Phone sign-in with the Microsoft Authenticator app.
- **Users capable of self-service password reset** shows the breakdown of users who can reset their passwords. Users can reset their password if they're both:

    - Registered for enough methods to satisfy their organization's policy for self-service password reset
    - Enabled to reset their password

    ![Screenshot of users who can register](media/how-to-authentication-methods-usage-insights/users-capable.png)

**Users registered by authentication method** shows how many users are registered for each authentication method. Click an authentication method to see who is registered for that method.

![Screenshot of Users Registered](media/how-to-authentication-methods-usage-insights/users-registered.png)

**Recent registration by authentication method** shows how many registrations succeeded and failed, sorted by authentication method. Click an authentication method to see recent registration events for that method.

![Screenshot of Recently Registered](media/how-to-authentication-methods-usage-insights/recently-registered.png)

## Usage details

The **Usage** report shows which authentication methods are used to sign-in and reset passwords.

![Screenshot of Usage page](media/how-to-authentication-methods-usage-insights/usage-page.png)

**Sign-ins by authentication requirement** shows the number of successful user interactive sign-ins that were required for single-factor versus multifactor authentication in Microsoft Entra ID. Sign-ins where MFA was enforced by a third-party MFA provider are not included.

![Screenshot of sign ins by authentication requirement](media/how-to-authentication-methods-usage-insights/sign-ins-protected.png)

**Sign-ins by authentication method** shows the number of user interactive sign-ins (success and failure) by authentication method used. It doesn't include sign-ins where the authentication requirement was satisfied by a claim in the token.

![Screenshot of sign ins by method](media/how-to-authentication-methods-usage-insights/sign-ins-by-method.png)

**Number of password resets and account unlocks** shows the number of successful password changes and password resets (self-service and by admin) over time.

![Screenshot of resets and unlocks](media/how-to-authentication-methods-usage-insights/password-changes.png)

**Password resets by authentication method** shows the number of successful and failed authentications during the password reset flow by authentication method.

![Screenshot of Resets by method](media/how-to-authentication-methods-usage-insights/resets-by-method.png)

## User registration details

Using the controls at the top of the list, you can search for a user and filter the list of users based on the columns shown. The report updates for most users in the tenant in 36 hours. It's possible for the reporting of a few users to fall out of that time range in rare cases. If that happens, please revisit the report after 24 hours.

Note

User accounts that were recently deleted, also known as [soft-deleted users](../../fundamentals/users-restore), are not listed in user registration details. Same for disabled users.

The registration details report shows the following information for each user:

- User principal name
- Name
- MFA Capable (Capable, Not Capable)
- Passwordless Capable (Capable, Not Capable)
- SSPR Registered (Registered, Not Registered)
- SSPR Enabled (Enabled, Not Enabled)
- SSPR Capable (Capable, Not Capable)
- Methods registered (Alternate Mobile Phone, Certificate-based authentication, Email, FIDO2 security key, Hardware OATH token, Microsoft Authenticator app, Microsoft Passwordless phone sign-in, Mobile phone, Office phone, Security questions, Software OATH token, Temporary Access Pass, Windows Hello for Business)
- Last Updated Time (The date and time when the report most recently updated. This value is not related the user's authentication method registration.)

    ![Screenshot of user registration details](media/how-to-authentication-methods-usage-insights/registration-details.png)

## Registration and reset events

**Registration and reset events** shows registration and reset events from the last 24 hours, last seven days, or last 30 days including:

- Date
- User name
- User
- Feature (Registration, Reset)
- Method used (App notification, App code, Phone Call, Office Call, Alternate Mobile Call, SMS, Email, Security questions)
- Status (Success, Failure)
- Reason for failure (explanation)

    ![Screenshot of registration and reset events](media/how-to-authentication-methods-usage-insights/registration-and-reset-logs.png)

## Limitations

- The data in the report is not updated in real-time and may reflect a latency of up to 36 hours. It's possible for the reporting of a few users to fall out of that time range in rare cases. In that case, recheck the report after 24 hours.
- The **PhoneAppNotification** or **PhoneAppOTP** methods that a user might have configured are not displayed in the dashboard on **Microsoft Entra authentication methods - Policies**.
- Bulk operations in the Microsoft Entra admin portal could time out and fail on very large tenants. This limitation is a known issue due to scaling limitations. For more information, see [Bulk operations](/en-us/entra/fundamentals/bulk-operations-service-limitations?WT.mc_id=Portal-Microsoft_AAD_IAM).