---
layout: Conceptual
title: Self-service password reset reports - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-sspr-reporting
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Reporting on Microsoft Entra self-service password reset events
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: tilarso
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 53a138ee-fab3-0542-f8f7-084c7ee7514c
document_version_independent_id: 0ef5a7e6-8e8b-f005-2be9-de0e5ea45efe
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-sspr-reporting.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-sspr-reporting
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-sspr-reporting.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d7ffb4f3-ff52-fb15-2bb3-0a5823e46dae
---

# Self-service password reset reports - Microsoft Entra ID | Microsoft Learn

After deployment, many organizations want to know how or if self-service password reset (SSPR) is really being used. The reporting feature that Microsoft Entra ID provides helps you answer questions by using prebuilt reports. If you're appropriately licensed, you can also create custom queries.

![Screenshot of audit log for SSPR reporting.](media/howto-sspr-reporting/sspr-reporting.png)

The following questions can be answered by the reports that exist in the [Microsoft Entra admin center](https://entra.microsoft.com):

Note

You must opt in for this data to be gathered on behalf of your organization. To opt in, you must visit the **Reporting** tab or the audit logs at least once. Until then, data isn't collected for your organization.

- What changes were made to the SSPR policy?
- How many people have registered for password reset?
- Who has registered for password reset?
- What data are people registering?
- How many people reset their passwords in the last seven days?
- What are the most common methods that users or admins use to reset their passwords?
- What are common problems users or admins face when attempting to use password reset?
- What admins are resetting their own passwords frequently?
- Is there any suspicious activity going on with password reset?

## How to view password management reports

Use the following the steps to find the password reset and password reset registration events:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **Audit Logs** from the **Users** blade. This shows you all of the audit events that occurred against all the users in your directory. You can filter this view to see all the password-related events.
4. From the **Filter** menu at the top of the pane, select the **Service** drop-down list, and change it to the **Self-service Password Management** service type.
5. Optionally, further filter the list by choosing the specific **Activity** you're interested in.

### Combined registration

[Combined registration](concept-registration-mfa-sspr-combined) security information registration and management events can be found in the audit logs under **Security** &gt; **Authentication Methods**.

## Description of the report columns

The following list explains each of the report columns in detail:

- **User**: The user who attempted a password reset registration operation.
- **Role**: The role of the user in the directory.
- **Date and Time**: The date and time of the attempt.
- **Data Registered**: The authentication data that the user provided during password reset registration.

## Description of the report values

The following table describes the different values that are you can set for each column:

| Column | Permitted values and their meanings |
| --- | --- |
| Data registered | **Alternate email**: The user used an alternate email or authentication email to authenticate.<br>**Office phone**: The user used an office phone to authenticate.<br><br>**Mobile phone**: The user used a mobile phone or authentication phone to authenticate.<br><br>**Security questions**: The user used security questions to authenticate.<br><br>**Any combination of the previous methods, for example, alternate email + mobile phone**: Occurs when a two-gate policy is specified and shows which two methods the user used to authentication their password reset request. |

## Self-Service Password Management activity types

The following activity types appear in the **Self-Service Password Management** audit event category:

- Self-service password reset policy changes: Indicates any changes to the SSPR policy, including old value and new value.
- Blocked from self-service password reset: Indicates that a user tried to reset a password, use a specific gate, or validate a phone number more than five total times in 24 hours.
- Change password (self-service): Indicates that a user performed a voluntary, or forced (due to expiry) password change.
- Reset password (by admin): Indicates that an administrator performed a password reset on behalf of a user.
- Reset password (self-service): Indicates that a user successfully reset their password from [Microsoft Entra password reset](https://passwordreset.microsoftonline.com).
- Self-service password reset flow activity progress: Indicates each specific step a user proceeds through, such as passing a specific password reset authentication gate, as part of the password reset process.
- Unlock user account (self-service): Indicates that a user successfully unlocked their Active Directory account without resetting their password from [Microsoft Entra password reset](https://passwordreset.microsoftonline.com) by using the Active Directory feature of account unlock without reset.
- User registered for self-service password reset: Indicates that a user has registered all the required information to be able to reset their password in accordance with the currently specified tenant password reset policy.

### Activity type: Self-service password reset policy changes

The following list explains this activity in detail:

- **Activity description**: Indicates that an administrator updated settings in the SSPR policy.
- **Activity actor**: The display name and user principal name (UPN) of the administrator who made the changes.
- **Activity target**: Updated properties in the SSPR policy.
- **Activity statuses**:
    - *Success*: Indicates that a user successfully changed a setting in the SSPR policy.
    - *Failure*: Indicates that a user failed to change a setting in the SSPR policy.
- **Activity status failure reason**:
    - Permission failure?

### Activity type: Blocked from self-service password reset

The following list explains this activity in detail:

- **Activity description**: Indicates that a user tried to reset a password, use a specific gate, or validate a phone number more than five total times in 24 hours.
- **Activity actor**: The user who was throttled from performing additional reset operations. The user can be an end user or an administrator.
- **Activity target**: The user who was throttled from performing additional reset operations. The user can be an end user or an administrator.
- **Activity status**:
    - *Success*: Indicates that a user was throttled from performing any additional resets, attempting any additional authentication methods, or validating any additional phone numbers for the next 24 hours.
- **Activity status failure reason**: Not applicable.

### Activity type: Change password (self-service)

The following list explains this activity in detail:

- **Activity description**: Indicates that a user performed a voluntary, or forced (due to expiry) password change.
- **Activity actor**: The user who changed their password. The user can be an end user or an administrator.
- **Activity target**: The user who changed their password. The user can be an end user or an administrator.
- **Activity statuses**:
    - *Success*: Indicates that a user successfully changed their password.
    - *Failure*: Indicates that a user failed to change their password. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred.
- **Activity status failure reason**:
    - *FuzzyPolicyViolationInvalidPassword*: The user selected a password that was automatically banned because the Microsoft Banned Password Detection capabilities found it to be too common or especially weak.

### Activity type: Reset password (by admin)

The following list explains this activity in detail:

- **Activity description**: Indicates that an administrator performed a password reset on behalf of a user.
- **Activity actor**: The administrator who performed the password reset on behalf of another end user or administrator. Must be a password administrator, user administrator, or helpdesk administrator.
- **Activity target**: The user whose password was reset. The user can be an end user or a different administrator.
- **Activity statuses**:
    - *Success*: Indicates that an admin successfully reset a user's password.
    - *Failure*: Indicates that an admin failed to change a user's password. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred.
- **Activity additional details OnPremisesAgent**:
    - *None*: Indicates cloud-only reset.
    - *Microsoft Entra Connect*: Indicates password was reset on-premises via Microsoft Entra Connect writeback agent.
    - *CloudSync*: Indicates password was reset on-premises via Microsoft Entra CloudSync writeback agent.

### Activity type: Reset password (self-service)

The following list explains this activity in detail:

- **Activity description**: Indicates that a user successfully reset their password from [Microsoft Entra password reset](https://passwordreset.microsoftonline.com).
- **Activity actor**: The user who reset their password. The user can be an end user or an administrator.
- **Activity target**: The user who reset their password. The user can be an end user or an administrator.
- **Activity statuses**:
    - *Success*: Indicates that a user successfully reset their own password.
    - *Failure*: Indicates that a user failed to reset their own password. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred.
- **Activity status failure reason**:
    - *FuzzyPolicyViolationInvalidPassword*: The admin selected a password that was automatically banned because the Microsoft Banned Password Detection capabilities found it to be too common or especially weak.

### Activity type: Self-service password reset flow activity progress

The following list explains this activity in detail:

- **Activity description**: Indicates each specific step a user proceeds through (such as passing a specific password reset authentication gate) as part of the password reset process.
- **Activity actor**: The user who performed part of the password reset flow. The user can be an end user or an administrator.
- **Activity target**: The user who performed part of the password reset flow. The user can be an end user or an administrator.
- **Activity statuses**:
    - *Success*: Indicates that a user successfully completed a specific step of the password reset flow.
    - *Failure*: Indicates that a specific step of the password reset flow failed. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred.
- **Activity status reasons**: See the following table for all the permissible reset activity status reasons.

### Activity type: Unlock a user account (self-service)

The following list explains this activity in detail:

- **Activity description**: Indicates that a user successfully unlocked their Active Directory account without resetting their password from [Microsoft Entra password reset](https://passwordreset.microsoftonline.com) by using the Active Directory feature of account unlock without reset.
- **Activity actor**: The user who unlocked their account without resetting their password. The user can be an end user or an administrator.
- **Activity target**: The user who unlocked their account without resetting their password. The user can be an end user or an administrator.
- **Allowed activity statuses**:
    - *Success*: Indicates that a user successfully unlocked their own account.
    - *Failure*: Indicates that a user failed to unlock their account. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred.

### Activity type: User registered for self-service password reset

The following list explains this activity in detail:

- **Activity description**: Indicates that a user has registered all the required information to be able to reset their password in accordance with the currently specified tenant password reset policy.
- **Activity actor**: The user who registered for password reset. The user can be an end user or an administrator.
- **Activity target**: The user who registered for password reset. The user can be an end user or an administrator.
- **Allowed activity statuses**:
    - *Success*: Indicates that a user successfully registered for password reset in accordance with the current policy.
    - *Failure*: Indicates that a user failed to register for password reset. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred.

        Note

        Failure doesn't mean a user is unable to reset their own password. It means that they didn't finish the registration process. If there's unverified data on their account that's correct, such as a phone number that's not validated, even though they haven't verified this phone number, they can still use it to reset their password.