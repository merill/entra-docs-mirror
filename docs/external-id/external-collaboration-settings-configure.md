---
layout: Conceptual
title: Configure external collaboration - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/external-collaboration-settings-configure
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to configure external collaboration settings in Microsoft Entra External ID. Control guest user access, specify who can invite guests, and manage domain restrictions for B2B collaboration.
ms.topic: how-to
ms.date: 2026-04-24T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
ms.custom: has-azure-ad-ps-ref, sfi-ga-blocked
locale: en-us
document_id: 4aa45818-3e2a-f952-2a60-86fe930d416c
document_version_independent_id: 02f84110-9385-e158-b847-303cd31d888f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/external-collaboration-settings-configure.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/external-collaboration-settings-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/external-collaboration-settings-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 0a2d53b2-9b2a-6e4e-fd9f-203e1156dfb0
---

# Configure external collaboration - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

External collaboration settings let you specify what roles in your organization can invite external users for B2B collaboration. These settings also include options for [allowing or blocking specific domains](allow-deny-list), and options for restricting what external guest users can see in your Microsoft Entra directory. The following options are available:

- **Determine guest user access**: Microsoft Entra External ID allows you to restrict what external guest users can see in your Microsoft Entra directory. For example, you can limit guest users' view of group memberships, or allow guests to view only their own profile information.
- **Specify who can invite guests**: By default, all users in your organization, including B2B collaboration guest users, can invite external users to B2B collaboration. If you want to limit the ability to send invitations, you can turn invitations on or off for everyone, or limit invitations to certain roles.
- **Enable guest self-service sign-up via user flows**: For applications you build, you can create user flows that allow a user to sign up for an app and create a new guest account. You can enable the feature in your external collaboration settings, and then [add a self-service sign-up user flow to your app](self-service-sign-up-user-flow).
- **Allow or block domains**: You can use collaboration restrictions to allow or deny invitations to the domains you specify. For details, see [Allow or block domains](allow-deny-list).

For B2B collaboration with other Microsoft Entra organizations, you should also review your [cross-tenant access settings](cross-tenant-access-settings-b2b-collaboration) to ensure your inbound and outbound B2B collaboration and scope access to specific users, groups, and applications.

Note

Microsoft began rolling out an update to the guest user sign-in experience for B2B collaboration in July 2025, and the rollout completed by the end of 2025. With this update, guest users are redirected to their own organization's sign-in page to provide credentials. Guest users see the branding and URL endpoint of their home tenant. Following successful authentication in their own organization, guest users are returned to your organization to complete sign-in. In the following example, the company branding for Woodgrove Groceries appears on the left. The example on the right displays the custom branding for the user's home tenant.

![Screenshot showing guest user login flow.](media/external-collaboration-settings-configure/guest-login-flow.png)

## Configure settings in the portal

In the Microsoft Entra admin center, you need a role that can update external collaboration settings, such as Global Administrator or External Identity Provider Administrator. When using Microsoft Graph, lesser-privileged roles might be available for individual settings. See Configure settings with Microsoft Graph later in this article.

### To configure guest user access

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **External collaboration settings**.
3. Under **Guest user access**, choose the level of access you want guest users to have:

    ![Screenshot showing Guest user access settings.](media/external-collaboration-settings-configure/guest-user-access.png)

    - **Guest users have the same access as members (most inclusive)**: This option gives guests the same access to Microsoft Entra resources and directory data as member users.
    - **Guest users have limited access to properties and memberships of directory objects**: (Default) This setting blocks guests from certain directory tasks, like enumerating users, groups, or other directory resources. Guests can see membership of all non-hidden groups. [Learn more about default guest permissions](../fundamentals/users-default-permissions#member-and-guest-users).
    - **Guest user access is restricted to properties and memberships of their own directory objects (most restrictive)**: With this setting, guests can access only their own profiles. Guests aren't allowed to see other users' profiles, groups, or group memberships.

### To configure guest invite settings

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **External collaboration settings**.
3. Under **Guest invite settings**, choose the appropriate settings:

    ![Screenshot showing Guest invite settings.](media/external-collaboration-settings-configure/guest-invite-settings.png)

    - **Anyone in the organization can invite guest users including guests and non-admins (most inclusive)**: To allow guests in the organization to invite other guests including users who aren't members of an organization, select this radio button.
    - **Member users and users assigned to specific admin roles can invite guest users including guests with member permissions**: To allow member users and users who have specific administrator roles to invite guests, select this radio button.
    - **Only users assigned to specific admin roles can invite guest users**: To allow only those users with [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator) or [Guest Inviter](../identity/role-based-access-control/permissions-reference#guest-inviter) roles to invite guests, select this radio button.
    - **No one in the organization can invite guest users including admins (most restrictive)**: To deny everyone in the organization from inviting guests, select this radio button.

### To configure guest self-service sign-up

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **External collaboration settings**.
3. Under **Enable guest self-service sign up via user flows**, select **Yes** if you want to be able to create user flows that let users sign up for apps. For more information about this setting, see [Add a self-service sign-up user flow to an app](self-service-sign-up-user-flow).

    ![Screenshot showing Self-service sign up via user flows setting.](media/external-collaboration-settings-configure/self-service-sign-up-setting.png)

### To configure external user leave settings

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **External collaboration settings**.
3. Under **External user leave settings**, you can control whether external users can remove themselves from your organization.

    - **Yes**: Users can leave the organization themselves without approval from your admin or privacy contact.
    - **No**: Users can't leave your organization themselves. They see a message guiding them to contact your admin or privacy contact to request removal from your organization.

    Important

    You can configure **External user leave settings** only if you have [added your privacy information](../fundamentals/properties-area) to your Microsoft Entra tenant. Otherwise, this setting will be unavailable.

    ![Screenshot showing External user leave settings in the portal.](media/external-collaboration-settings-configure/external-user-leave-settings.png)

### To configure collaboration restrictions (allow or block domains)

Important

Microsoft recommends that you use roles with the fewest permissions. This practice helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios or when you can't use an existing role.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **External collaboration settings**.
3. Under **Collaboration restrictions**, you can choose whether to allow or deny invitations to the domains you specify and enter specific domain names in the text boxes. For multiple domains, enter each domain on a new line. For more information, see [Allow or block invitations to B2B users from specific organizations](allow-deny-list).

    ![Screenshot showing Collaboration restrictions settings.](media/external-collaboration-settings-configure/collaboration-restrictions.png)

## Configure settings with Microsoft Graph

External collaboration settings can be configured by using the Microsoft Graph API:

- For **Guest user access restrictions** and **Guest invite restrictions**, use the [authorizationPolicy](/en-us/graph/api/resources/authorizationpolicy?view=graph-rest-1.0&amp;preserve-view=true) resource type.
- For the **Enable guest self-service sign up via user flows** setting, use the [authenticationFlowsPolicy](/en-us/graph/api/resources/authenticationflowspolicy?view=graph-rest-1.0&amp;preserve-view=true) resource type.
- For **External user leave settings**, use the [externalidentitiespolicy](/en-us/graph/api/resources/externalidentitiespolicy?view=graph-rest-1.0&amp;preserve-view=true) resource type.
- For email one-time passcode settings (now on the **All identity providers** page in the Microsoft Entra admin center), use the [emailAuthenticationMethodConfiguration](/en-us/graph/api/resources/emailAuthenticationMethodConfiguration?view=graph-rest-1.0&amp;preserve-view=true) resource type.

## Assign the Guest Inviter role to a user

With the [Guest Inviter](../identity/role-based-access-control/permissions-reference#guest-inviter) role, you can give individual users the ability to invite guests without assigning them a higher privilege administrator role. Users with the Guest Inviter role are able to invite guests even when the option **Only users assigned to specific admin roles can invite guest users** is selected (under **Guest invite settings**).

Here's an example that shows how to use Microsoft Graph PowerShell to add a user to the `Guest Inviter` role:

```powershell

Import-Module Microsoft.Graph.Identity.DirectoryManagement

$roleName = "Guest Inviter"
$role = Get-MgDirectoryRole | where {$_.DisplayName -eq $roleName}
$userId = <User Id/User Principal Name>

$DirObject = @{
  "@odata.id" = "https://graph.microsoft.com/v1.0/directoryObjects/$userId"
  }

New-MgDirectoryRoleMemberByRef -DirectoryRoleId $role.Id -BodyParameter $DirObject

```

## Sign-in logs for B2B users

When a B2B user signs into a resource tenant to collaborate, a sign-in log is generated in both the home tenant and the resource tenant. These logs include information such as the application being used, email addresses, tenant name, and tenant ID for both the home tenant and the resource tenant.