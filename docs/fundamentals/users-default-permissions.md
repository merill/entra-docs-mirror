---
layout: Conceptual
title: Default user permissions - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/users-default-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Compare the default user permissions available in Microsoft Entra ID and learn how to restrict access.
ms.topic: concept-article
ms.date: 2026-06-18T00:00:00.0000000Z
ms.reviewer: vincesm
ms.custom: sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: 510faed7-b79d-b8ec-f32f-e64d8773a30c
document_version_independent_id: 522e7e2e-ea93-5249-5e6f-5c984f1b6277
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/users-default-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/users-default-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/users-default-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 4d489c83-a429-1cae-f363-0705fb00d1e2
---

# Default user permissions - Microsoft Entra | Microsoft Learn

## Overview

In Microsoft Entra ID, all users are granted a set of default permissions. A user's access consists of the type of user, their [role assignments](how-subscriptions-associated-directory), and their ownership of individual objects.

This article describes those default permissions and compares the member and guest user defaults. The default user permissions can be changed only in user settings in Microsoft Entra ID.

## Member and guest users

The set of default permissions depends on whether the user is a native member of the tenant (member user) or is brought over from another directory, such as a business-to-business (B2B) collaboration guest (guest user). For more information about adding guest users, see [What is Microsoft Entra B2B collaboration?](../external-id/what-is-b2b). Here are the capabilities of the default permissions:

- *Member users* can register applications, manage their own profile photo and mobile phone number, change their own password, and invite B2B guests. These users can also read all directory information (with a few exceptions).
- *Guest users* have restricted directory permissions. They can manage their own profile, change their own password, and retrieve some information about other users, groups, and apps. However, they can't read all directory information.

    For example, guest users can't enumerate the list of all users, groups, and other directory objects. Guests can be added to administrator roles, which grant them full read and write permissions. Guests can also invite other guests when [Guest invite settings](../external-id/external-collaboration-settings-configure#to-configure-guest-invite-settings) allow it.

Note

As Intune employs its own RBAC system to manage access to device management features, restricted guest users will be able to access the Intune portal with the appropriate permissions.

## Compare member and guest default permissions

| **Area** | **Member user permissions** | **Default guest user permissions** | **Restricted guest user permissions** |
| --- | --- | --- | --- |
| Users and contacts | - Enumerate the list of all users and contacts<br>- Read all public properties of users and contacts<br>- Invite guests<br>- Change their own password<br>- Manage their own mobile phone number<br>- Manage their own photo<br>- Invalidate their own refresh tokens | - Read their own properties<br>- Read display name, email, sign-in name, photo, user principal name, and user type properties of other users and contacts<br>- Invite other guests if allowed by Guest invite settings<br>- Change their own password<br>- Search for another user by object ID (if allowed)<br>- Read manager and direct report information of other users | - Read their own properties<br>- Invite other guests if allowed by Guest invite settings<br>- Change their own password<br>- Manage their own mobile phone number |
| Groups | - Create security groups<br>- Create Microsoft 365 groups<br>- Enumerate the list of all groups<br>- Read all properties of groups<br>- Read nonhidden group membership<br>- Read hidden Microsoft 365 group membership for joined groups<br>- Manage properties, ownership, and membership of groups that the user owns<br>- Add guests to owned groups<br>- Manage group membership settings<br>- Delete owned groups<br>- Restore owned Microsoft 365 groups | - Read properties of nonhidden groups, including active and eligible membership and ownership (even nonjoined groups)<br>- Read hidden Microsoft 365 group membership for joined groups<br>- Search for groups by display name or object ID (if allowed) | - Read object ID for joined groups<br>- Read membership and ownership of joined groups in some Microsoft 365 apps (if allowed) |
| Applications | - Register (create) new applications<br>- Enumerate the list of all applications<br>- Read properties of registered and enterprise applications<br>- Manage application properties, assignments, and credentials for owned applications<br>- Create or delete application passwords for users<br>- Delete owned applications<br>- Restore owned applications<br>- List permissions granted to applications | - Read properties of registered and enterprise applications<br>- List permissions granted to applications | - Read properties of registered and enterprise applications<br>- List permissions granted to applications |
| Agents | - Enumerate the list of all blueprints, blueprint principals, and agent identities<br>- Read properties of blueprints, blueprint principals, and agent identities<br>- Manage properties, assignments, and credentials for owned blueprints, blueprint principals, and agent identities<br>- Delete owned blueprints, blueprint principals, and agent identities<br>- Delete and update sponsors of blueprints, blueprint principals, and agent identities when listed as a sponsor<br>- List permissions granted to blueprint principals and agent identities<br>- Create blueprint principals and agent identities when owner of the blueprint<br>- Create agent identities when owner of the blueprint principal | None | None |
| Devices | - Enumerate the list of all devices<br>- Read all properties of devices<br>- Manage all properties of owned devices | No permissions | No permissions |
| Organization | - Read all company information<br>- Read all domains<br>- Read configuration of certificate-based authentication<br>- Read all partner contracts<br>- Read multitenant organization basic details and active tenants<br>- Read tenant-wide directory settings (the directorySetting and groupSetting objects in Microsoft Graph) when the calling app has been granted the Directory.Read.All or Directory.ReadWrite.All delegated permission | - Read company display name<br>- Read all domains<br>- Read configuration of certificate-based authentication | - Read company display name<br>- Read all domains |
| Roles and scopes | - Read all administrative roles and memberships<br>- Read all properties and membership of administrative units | No permissions | No permissions |
| Subscriptions | - Read all licensing subscriptions<br>- Enable service plan memberships | No permissions | No permissions |
| Policies | - Read all properties of policies<br>- Manage all properties of owned policies | No permissions | No permissions |
| Terms of use | Read terms of use a user has accepted. | Read terms of use a user has accepted. | Read terms of use a user has accepted. |

Note

Some read permissions listed for member users—including reading tenant-wide directory settings—are accessible through Microsoft Graph only when the calling app has been granted an appropriate delegated permission, such as Directory.Read.All. Both the user's role and the app's delegated permission must allow the operation.

## Restrict member users' default permissions

It's possible to add restrictions to users' default permissions.

You can restrict default permissions for member users in the following ways:

Caution

The **Restrict access to Microsoft Entra administration portal** setting limits access to a set of commonly visited admin center pages. It is **not a security measure**. For more information on the setting, see the following table.

| Permission | Setting explanation |
| --- | --- |
| **Register applications** | Setting this option to **No** prevents users from creating application registrations. You can then grant the ability back to specific individuals, by adding them to the application developer role. |
| **Allow users to connect work or school account with LinkedIn** | Setting this option to **No** prevents users from connecting their work or school account with their LinkedIn account. For more information, see [LinkedIn account connections data sharing and consent](../identity/users/linkedin-user-consent). |
| **Create security groups** | Setting this option to **No** prevents users from creating security groups. Those users assigned at least the User Administrator role can still create security groups. To learn how, see [Microsoft Entra cmdlets for configuring group settings](../identity/users/groups-settings-cmdlets). |
| **Create Microsoft 365 groups** | Setting this option to **No** prevents users from creating Microsoft 365 groups. Setting this option to **Some** allows a set of users to create Microsoft 365 groups. Anyone assigned at least the [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator) role can still create Microsoft 365 groups. To learn how, see [Microsoft Entra cmdlets for configuring group settings](../identity/users/groups-settings-cmdlets). |
| **Restrict access to Microsoft Entra administration portal** | **What does this switch do?**Setting this option to **No** allows non-administrators to sign in to the Microsoft Entra admin center. Setting this option to **Yes** adds a layer of friction to casual browsing. This setting restricts non-administrators from loading a set of frequently visited pages in the Microsoft Entra admin center and Azure portal, including home, tenant overview, and the users list. Non-administrators who own groups will be unable to use the Microsoft Entra admin center or Azure portal to manage these resources. Most pages in the admin center remain reachable if the user has a direct (deep) link. <br>**What does it not do?** It **does not block** programmatic access to Microsoft Entra data via PowerShell, Microsoft Graph API, or other tools like Visual Studio. It **does not apply** to users with an administrative role, including custom roles.It **does not prevent** all access to the admin center. Many areas are still reachable through alternate paths. <br><br>**When should I use this switch?**Use this setting if you want to add a layer of friction that discourages non-admin users from casually opening the Microsoft Entra admin center. It might help reduce nonessential exploration, but it does not prevent users from accessing or managing their resources through other means. <br><br>**When should I not use this switch?**Do not rely on this setting as a security control. For stronger enforcement, use a Conditional Access policy targeting the Windows Azure Service Management API [Windows Azure Service Management API](../identity/conditional-access/concept-conditional-access-cloud-apps#windows-azure-service-management-api) to block non-admin access to Azure management endpoints.<br><br>**How do I grant only a specific non-administrator users the ability to use the Microsoft Entra administration portal?** Set the switch to **Yes**, then assign those users a role such as **Global Reader** or another role that grants appropriate permissions. <br><br>**Want to restrict access more effectively?**Use Conditional Access to target the Windows Azure Service Management API. This provides broader control over access to all Azure-based management experiences, including the Microsoft Entra admin center. |
| **Restrict non-admin users from creating tenants** | Users can create tenants in the Microsoft Entra ID and Microsoft Entra administration portal under Manage tenant. The creation of a tenant is recorded in the Audit log as category DirectoryManagement and activity Create Company. By default, the user who creates a Microsoft Entra tenant is automatically assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role. The newly created tenant doesn't inherit any settings or configurations. <br>**What does this switch do?** Setting this option to **Yes** restricts creation of Microsoft Entra tenants to anyone assigned at least the [Tenant Creator](../identity/role-based-access-control/permissions-reference#tenant-creator) role. Setting this option to **No** allows nonadmin users to create Microsoft Entra tenants. Tenant create continues to be recorded in the Audit log. <br><br>**How do I grant only a specific non-administrator users the ability to create new tenants?** Set this option to Yes, then assign them the [Tenant Creator](../identity/role-based-access-control/permissions-reference#tenant-creator) role. |
| **Restrict users from recovering the BitLocker key(s) for their owned devices** | This setting can be found in the Microsoft Entra admin center in the Device Settings. Setting this option to **Yes** restricts users from being able to self-service recover BitLocker key(s) for their owned devices. Users must contact their organization's helpdesk to retrieve their BitLocker keys. Setting this option to **No** allows users to recover their BitLocker keys. |
| **Read other users** | This setting is available in Microsoft Graph and PowerShell only. Setting this flag to `$false` prevents all nonadmins from reading user information from the directory. This flag might prevent reading user information in other Microsoft services like Microsoft Teams.<br>This setting is meant for special circumstances, so setting the flag to `$false` isn't recommended. To configure this setting, update the [authorizationPolicy](/en-us/graph/api/authorizationpolicy-update?tabs=http#request-3) using Microsoft Graph by setting the [AllowedToReadOtherUsers](/en-us/graph/api/resources/defaultuserrolepermissions#json-representation) property. |

The **Restrict non-admin users from creating tenants** option is shown in the following screenshot.

[![Screenshot showing the option to Restrict nonadmins from creating tenants.](media/user-default-permissions/tenant-creation-restriction.png)](media/user-default-permissions/tenant-creation-restriction.png#lightbox)

## Restrict guest users' default permissions

You can restrict default permissions for guest users in the following ways.

Note

The **Guest user access restrictions** setting replaced the **Guest users permissions are limited** setting. For guidance on using this feature, see [Restrict guest access permissions in Microsoft Entra ID](../identity/users/users-restrict-guest-permissions).

| Permission | Setting explanation |
| --- | --- |
| **Guest user access restrictions** | Setting this option to **Guest users have the same access as members** grants all member user permissions to guest users by default.<br>Setting this option to **Guest user access is restricted to properties and memberships of their own directory objects** restricts guest access to only their own user profile by default. Access to other users is no longer allowed, even when they're searching by user principal name, object ID, or display name. Access to group information, including groups memberships, is also no longer allowed.<br><br>This setting doesn't prevent access to joined groups in some Microsoft 365 services like Microsoft Teams. To learn more, see [Microsoft Teams guest access](/en-us/MicrosoftTeams/guest-access).<br><br>Guest users can still be added to administrator roles regardless of this permission setting. |
| **Guests can invite** | Setting this option to **Yes** allows guests to invite other guests. To learn more, see [Configure external collaboration settings](../external-id/external-collaboration-settings-configure). |

## Object ownership

### Application registration owner permissions

When a user registers an application, they're automatically added as an owner for the application. As an owner, they can manage the metadata of the application, such as the name and permissions that the app requests. They can also manage the tenant-specific configuration of the application, such as the single sign-on (SSO) configuration and user assignments.

An owner can also add or remove other owners. Unlike those users assigned at least the Application Administrator role, owners can manage only the applications that they own.

### Enterprise application owner permissions

When a user adds a new enterprise application, they're automatically added as an owner. As an owner, they can manage the tenant-specific configuration of the application, such as the SSO configuration, provisioning, and user assignments.

An owner can also add or remove other owners. Unlike those users assigned at least the Application Administrator role, owners can manage only the applications that they own.

### Group owner permissions

When a user creates a group, they're automatically added as an owner for that group. As an owner, they can manage properties of the group (such as the name) and manage group membership.

An owner can also add or remove other owners. Unlike those users assigned at least the [Groups Administrator](../identity/role-based-access-control/permissions-reference#groups-administrator) role, owners can manage only the groups that they own and they can add or remove group members only if the group's membership type is **Assigned**.

To assign a group owner, see [Managing owners for a group](how-to-manage-groups).

To use Privileged Access Management (PIM) to make a group eligible for a role assignment, see [Use Microsoft Entra groups to manage role assignments](../identity/role-based-access-control/groups-concept).

### Ownership permissions

The following tables describe the specific permissions in Microsoft Entra ID that member users have over objects they own. Users have these permissions only on objects that they own.

#### Owned application registrations

Users can perform the following actions on owned application registrations:

| **Action** | **Description** |
| --- | --- |
| microsoft.directory/applications/audience/update | Update the `applications.audience` property in Microsoft Entra ID. |
| microsoft.directory/applications/authentication/update | Update the `applications.authentication` property in Microsoft Entra ID. |
| microsoft.directory/applications/basic/update | Update basic properties on applications in Microsoft Entra ID. |
| microsoft.directory/applications/credentials/update | Update the `applications.credentials` property in Microsoft Entra ID. |
| microsoft.directory/applications/delete | Delete applications in Microsoft Entra ID. |
| microsoft.directory/applications/owners/update | Update the `applications.owners` property in Microsoft Entra ID. |
| microsoft.directory/applications/permissions/update | Update the `applications.permissions` property in Microsoft Entra ID. |
| microsoft.directory/applications/policies/update | Update the `applications.policies` property in Microsoft Entra ID. |
| microsoft.directory/applications/restore | Restore applications in Microsoft Entra ID. |

#### Owned enterprise applications

Users can perform the following actions on owned enterprise applications. An enterprise application consists of a service principal, one or more application policies, and sometimes an application object in the same tenant as the service principal.

| **Action** | **Description** |
| --- | --- |
| microsoft.directory/auditLogs/allProperties/read | Read all properties (including privileged properties) on audit logs in Microsoft Entra ID. |
| microsoft.directory/policies/basic/update | Update basic properties on policies in Microsoft Entra ID. |
| microsoft.directory/policies/delete | Delete policies in Microsoft Entra ID. |
| microsoft.directory/policies/owners/update | Update the `policies.owners` property in Microsoft Entra ID. |
| microsoft.directory/servicePrincipals/appRoleAssignedTo/update | Update the `servicePrincipals.appRoleAssignedTo` property in Microsoft Entra ID. |
| microsoft.directory/servicePrincipals/appRoleAssignments/update | Update the `users.appRoleAssignments` property in Microsoft Entra ID. |
| microsoft.directory/servicePrincipals/audience/update | Update the `servicePrincipals.audience` property in Microsoft Entra ID. |
| microsoft.directory/servicePrincipals/authentication/update | Update the `servicePrincipals.authentication` property in Microsoft Entra ID. |
| microsoft.directory/servicePrincipals/basic/update | Update basic properties on service principals in Microsoft Entra ID. |
| microsoft.directory/servicePrincipals/credentials/update | Update the `servicePrincipals.credentials` property in Microsoft Entra ID. |
| microsoft.directory/servicePrincipals/delete | Delete service principals in Microsoft Entra ID. |
| microsoft.directory/servicePrincipals/owners/update | Update the `servicePrincipals.owners` property in Microsoft Entra ID. |
| microsoft.directory/servicePrincipals/permissions/update | Update the `servicePrincipals.permissions` property in Microsoft Entra ID. |
| microsoft.directory/servicePrincipals/policies/update | Update the `servicePrincipals.policies` property in Microsoft Entra ID. |
| microsoft.directory/signInReports/allProperties/read | Read all properties (including privileged properties) on sign-in reports in Microsoft Entra ID. |
| microsoft.directory/servicePrincipals/synchronizationCredentials/manage | Manage application provisioning secrets and credentials |
| microsoft.directory/servicePrincipals/synchronizationJobs/manage | Start, restart, and pause application provisioning synchronization jobs |
| microsoft.directory/servicePrincipals/synchronizationSchema/manage | Create and manage application provisioning synchronization jobs and schema |
| microsoft.directory/servicePrincipals/synchronization/standard/read | Read provisioning settings associated with your service principal |

#### Owned devices

Users can perform the following actions on owned devices:

| **Action** | **Description** |
| --- | --- |
| microsoft.directory/devices/bitLockerRecoveryKeys/read | Read the `devices.bitLockerRecoveryKeys` property in Microsoft Entra ID. |
| microsoft.directory/devices/disable | Disable devices in Microsoft Entra ID. |

#### Owned groups

Users can perform the following actions on owned groups.

Note

Owners of dynamic membership groups must have the Groups Administrator, Intune Administrator, or User Administrator role to edit rules for dynamic membership groups. For more information, see [Create or update a dynamic membership group in Microsoft Entra ID](../identity/users/groups-create-rule).

| **Action** | **Description** |
| --- | --- |
| microsoft.directory/groups/appRoleAssignments/update | Update the `groups.appRoleAssignments` property in Microsoft Entra ID. |
| microsoft.directory/groups/basic/update | Update basic properties on groups in Microsoft Entra ID. |
| microsoft.directory/groups/delete | Delete groups in Microsoft Entra ID. |
| microsoft.directory/groups/members/update | Update the `groups.members` property in Microsoft Entra ID. |
| microsoft.directory/groups/owners/update | Update the `groups.owners` property in Microsoft Entra ID. |
| microsoft.directory/groups/restore | Restore groups in Microsoft Entra ID. |
| microsoft.directory/groups/settings/update | Update the `groups.settings` property in Microsoft Entra ID. |