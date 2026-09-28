---
layout: Conceptual
title: Enable per-user multifactor authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-mfa-userstates
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to enable per-user Microsoft Entra multifactor authentication by changing the user state
ms.topic: how-to
ms.date: 2025-07-13T00:00:00.0000000Z
ms.reviewer: lvandenende
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
locale: en-us
document_id: 4cb129d2-9594-bf0c-5946-982f0ed0d888
document_version_independent_id: 6522b038-6853-3552-55c8-f174cf56573d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-mfa-userstates.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-mfa-userstates
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-mfa-userstates.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 198c8f9e-c2cd-cd84-9b4b-4618e1b35313
---

# Enable per-user multifactor authentication - Microsoft Entra ID | Microsoft Learn

To secure user sign-in events in Microsoft Entra ID, you can require Microsoft Entra multifactor authentication (MFA). The best way to protect users with Microsoft Entra MFA is to create a Conditional Access policy. Conditional Access is a Microsoft Entra ID P1 or P2 feature that lets you apply rules to require MFA as needed in certain scenarios. To get started using Conditional Access, see [Tutorial: Secure user sign-in events with Microsoft Entra multifactor authentication](tutorial-enable-azure-mfa).

For Microsoft Entra ID Free tenants without Conditional Access, you can [use security defaults to protect users](../../fundamentals/security-defaults). Users are prompted for MFA as needed, but you can't define your own rules to control the behavior.

If needed, you can instead enable each account for per-user Microsoft Entra MFA. When you enable users individually, they perform MFA each time they sign in. You can enable exceptions, such as when they sign in from trusted IP addresses, or when the **remember MFA on trusted devices** feature is turned on.

Changing user states isn't recommended unless your Microsoft Entra ID licenses don't include Conditional Access and you don't want to use security defaults. For more information on the different ways to enable MFA, see [Features and licenses for Microsoft Entra multifactor authentication](concept-mfa-licensing).

Important

This article details how to view and change the status for per-user Microsoft Entra multifactor authentication. If you use Conditional Access or security defaults, you don't review or enable user accounts using these steps.

Enabling Microsoft Entra multifactor authentication through a Conditional Access policy doesn't change the state of the user. Don't be alarmed if users appear disabled. Conditional Access doesn't change the state.

**Don't enable or enforce per-user Microsoft Entra multifactor authentication if you use Conditional Access policies.**

## Microsoft Entra multifactor authentication user states

A user's state reflects whether an Authentication Administrator enrolled them in per-user Microsoft Entra multifactor authentication. User accounts in Microsoft Entra multifactor authentication have the following three distinct states:

| State | Description | Legacy authentication affected | Browser apps affected | Modern authentication affected |
| --- | --- | --- | --- | --- |
| Disabled | The default state for a user not enrolled in per-user Microsoft Entra multifactor authentication. | No | No | No |
| Enabled | The user is enrolled in per-user Microsoft Entra multifactor authentication, but can still use their password for legacy authentication. If the user has no registered MFA authentication methods, they receive a prompt to register the next time they sign in using modern authentication (such as when they sign in on a web browser). | No. Legacy authentication continues to work until the registration process is completed. | Yes. After the session expires, Microsoft Entra multifactor authentication registration is required. | Yes. After the access token expires, Microsoft Entra multifactor authentication registration is required. |
| Enforced | The user is enrolled per-user in Microsoft Entra multifactor authentication. If the user has no registered authentication methods, they receive a prompt to register the next time they sign in using modern authentication (such as when they sign in on a web browser). Users who complete registration while they're *Enabled* are automatically moved to the *Enforced* state. | Yes. Apps require app passwords. | Yes. Microsoft Entra multifactor authentication is required at sign-in. | Yes. Microsoft Entra multifactor authentication is required at sign-in. |

All users start out *Disabled*. When you enroll users in per-user Microsoft Entra multifactor authentication, their state changes to *Enabled*. When enabled users sign in and complete the registration process, their state changes to *Enforced*. Administrators may move users between states, including from *Enforced* to *Enabled* or *Disabled*.

Note

If per-user MFA is re-enabled on a user and the user doesn't re-register, their MFA state doesn't transition from *Enabled* to *Enforced* in MFA management UI. The administrator must move the user directly to *Enforced*.

## View the status for a user

The per-user MFA administration experience in the Microsoft Entra admin center is recently improved. To view and manage user states, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Identity** &gt; **Users** &gt; **All users**.
3. Click **Per-user MFA**.
4. Select a user account, and select **User MFA settings**.
5. After you make any changes, select **Save**.

    ![Screenshot that shows an example of MFA settings for a user.](media/howto-mfa-userstates/user-states.png)

    If you try to sort thousands of users, the result might gracefully return **There are no users to display**. Try to enter more specific search criteria to narrow the search, or apply specific **Status** or **View** filters.

    ![Screenshot that shows an example of how to filter a large user sort.](media/howto-mfa-userstates/sort.png)

## Change the status for a user

To change the per-user Microsoft Entra multifactor authentication state for a user, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Identity** &gt; **Users** &gt; **All users**.
3. Click **Per-user MFA**.
4. Select a user account, and select **Enable MFA**. ![Screenshot that shows how to enable a user for Microsoft Entra multifactor authentication.](media/howto-mfa-userstates/new-enable.png)

    Tip

    *Enabled* users are automatically switched to *Enforced* when they register for Microsoft Entra multifactor authentication. Don't manually change the user state to *Enforced* unless the user is already registered or if it is acceptable for the user to experience interruption in connections to legacy authentication protocols.
5. Confirm your selection in the pop-up window that opens.

After you enable users, notify them by email. Tell the users that a prompt is displayed to ask them to register the next time they sign in. If your organization uses applications that don't run in a browser or support modern authentication, you can create application passwords. For more information, see [Enforce Microsoft Entra multifactor authentication with legacy applications using app passwords](howto-mfa-app-passwords).

## Use Microsoft Graph to manage per-user MFA

You can manage per-user MFA settings by using the Microsoft Graph REST API Beta. You can use the [authentication resource type](/en-us/graph/api/resources/authentication) to expose authentication method states for users.

To manage per-user MFA, use the perUserMfaState property within users/id/authentication/requirements. For more information, see [strongAuthenticationRequirements resource type](/en-us/graph/api/resources/strongauthenticationrequirements).

### View per-user MFA state

To retrieve the per-user multifactor authentication state for a user:

```http
GET /users/{id | userPrincipalName}/authentication/requirements
```

For example:

```http
GET https://graph.microsoft.com/beta/users/071cc716-8147-4397-a5ba-b2105951cc0b/authentication/requirements
```

If the user is enabled for per-user MFA, the response is:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "perUserMfaState": "enforced"
}
```

For more information, see [Get authentication method states](/en-us/graph/api/authentication-get).

### Change MFA state for a user

To change multifactor authentication state for a user, use the user's strongAuthenticationRequirements. For example:

```http
PATCH https://graph.microsoft.com/beta/users/071cc716-8147-4397-a5ba-b2105951cc0b/authentication/requirements
Content-Type: application/json

{
  "perUserMfaState": "disabled"
}
```

If successful, the response is:

```http
HTTP/1.1 204 No Content
```

For more information, see [Update authentication method states](/en-us/graph/api/authentication-update).