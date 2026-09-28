---
layout: HowTo
title: Manage authentication methods for Microsoft Entra multifactor authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-mfa-userdevicesettings
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how you can configure Microsoft Entra user settings for Microsoft Entra multifactor authentication
ms.reviewer: jupetter
ms.date: 2025-02-27T00:00:00.0000000Z
ms.topic: how-to
ms.custom:
- ge-structured-content-pilot
- sfi-image-nochange
locale: en-us
document_id: 51eadd8e-b820-be21-9cb3-b52f334fb94d
document_version_independent_id: fe358aa5-5bb6-b8f0-8ab7-ef181dc8af42
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-mfa-userdevicesettings.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: HowTo
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-mfa-userdevicesettings
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-mfa-userdevicesettings.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: af29b3b5-1b07-ae8c-2e73-652f13f65bf8
---

# Manage authentication methods for Microsoft Entra multifactor authentication - Microsoft Entra ID | Microsoft Learn

Users in Microsoft Entra ID have two distinct sets of contact information:

- Public profile contact information, which is managed in the user profile and visible to members of your organization. For users synced from on-premises Active Directory, this information is managed in on-premises Windows Server Active Directory Domain Services.
- Authentication methods, which are always kept private and only used for authentication, including multifactor authentication. Administrators can manage these methods in a user's authentication method blade and users can manage their methods in Security Info page of MyAccount.

When managing Microsoft Entra multifactor authentication methods for your users, Authentication administrators can:

- Add authentication methods for a specific user, including phone numbers used for MFA.
- Reset a user's password.
- Require a user to re-register for MFA.
- Revoke sessions.
- Delete a user's existing app passwords

Note

The screenshots in this topic show how to manage user authentication methods by using an updated experience in the Microsoft Entra admin center. There's also a legacy experience, and admins can toggle between the two using a banner in the admin center. The modern experience has full parity with the legacy experience, and it manages modern methods like Temporary Access Pass, passkeys, and other settings. The legacy experience in the Microsoft Entra admin center retired on Sept. 30, 2025. There's no action required by organizations before the retirement.

## Prerequisites

Microsoft Entra multifactor authentication, which is enabled by default.

## Add or change authentication methods for a user

You can add or change authentication methods for a user by using the Microsoft Entra admin center or Microsoft Graph PowerShell. In the Microsoft Entra admin center, the legacy method for managing user authentication methods retires after Sept. 30, 2025.

Note

For security reasons, public user contact information fields shouldn't be used to perform MFA. Instead, users should populate their authentication method numbers to be used for MFA.

![Screenshot of how to add authentication methods from the Microsoft Entra admin center.](media/howto-mfa-userdevicesettings/add-authentication-method-detail.png)

To add or change authentication methods for a user in the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Administrator](../role-based-access-control/permissions-reference#authentication-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Choose the user for whom you wish to add or change an authentication method and select **Authentication methods**.
4. At the top of the window, select **+ Add authentication method**.
    - Select a method (phone number or email). Email may be used for self-password reset but not authentication. When adding a phone number, select a phone type and enter phone number with valid format (such as `+1 4255551234`).
    - Select **Add**.

Users can add or edit their own authentication methods in [My Sign Ins | Security info](https://mysignins.microsoft.com/security-info). For example, to change the phone number, select **Phone number** and tap **Change**.

### Manage methods using PowerShell

Install the Microsoft.Graph.Identity.Signins PowerShell module using the following commands.

```powershell
Install-module Microsoft.Graph.Identity.Signins
Connect-MgGraph -Scopes "User.Read.all","UserAuthenticationMethod.Read.All","UserAuthenticationMethod.ReadWrite.All"
Select-MgProfile -Name beta
```

List phone based authentication methods for a specific user.

```powershell
Get-MgUserAuthenticationPhoneMethod -UserId balas@contoso.com
```

Create a mobile phone authentication method for a specific user.

```powershell
New-MgUserAuthenticationPhoneMethod -UserId balas@contoso.com -phoneType "mobile" -phoneNumber "+1 7748933135"
```

Remove a specific phone method for a user

```powershell
Remove-MgUserAuthenticationPhoneMethod -UserId balas@contoso.com -PhoneAuthenticationMethodId 00aa00aa-bb11-cc22-dd33-44ee44ee44ee
```

Authentication methods can also be managed using Microsoft Graph APIs. For more information, see [Authentication and authorization basics](/en-us/graph/auth/auth-concepts).

## Manage user authentication options

[Authentication Administrators](../role-based-access-control/permissions-reference#authentication-administrator) can require other users to reset their password, re-register for MFA, or revoke the user's sessions. Users can't update their own user object. To change or reset their own security methods, users can go to [Security info](https://aka.ms/security-info), or go to [self-service password reset](https://aka.ms/sspr) to reset their password. To manage other user's settings, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Administrator](../role-based-access-control/permissions-reference#authentication-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Choose the user you wish to perform an action on and select **Authentication methods**. At the top of the window, then choose one of the following options for the user:

    - **Reset password** resets the user's password and assigns a temporary password that must be changed on the next sign-in.
    - **Require re-register MFA** deactivates the user's hardware OATH tokens and deletes the following authentication methods from this user: phone numbers, Microsoft Authenticator apps and software OATH tokens. If needed, the user is requested to set up a new MFA authentication method the next time they sign in.
    - **Revoke sessions** invalidates a user's refresh tokens, forcing reauthentication across active sessions and applications.

## Delete users' existing app passwords

For users that have defined app passwords, administrators can also choose to delete these passwords, causing legacy authentication to fail in those applications. These actions may be necessary if you need to provide assistance to a user, or need to reset their authentication methods. Non-browser apps that were associated with these app passwords stop working until a new app password is created.

To delete a user's app passwords, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Administrator](../role-based-access-control/permissions-reference#authentication-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **Multifactor authentication**. You may need to scroll to the right to see this menu option. Select the example screenshot below to see the full window and menu location: [![Screenshot of select multifactor authentication from the Users window in Microsoft Entra ID.](media/howto-mfa-userstates/selectmfa-cropped.png)](media/howto-mfa-userstates/selectmfa.png#lightbox)
4. Check the box next to the user or users that you wish to manage. A list of quick step options appears on the right.
5. Select **Manage user settings**, then check the box for **Delete all existing app passwords generated by the selected users**, as shown in the following example: ![Screenshot of delete all existing app passwords.](media/howto-mfa-userdevicesettings/deleteapppasswords.png)
6. Select **save**, then **close**.