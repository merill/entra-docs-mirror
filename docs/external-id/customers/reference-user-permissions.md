---
layout: Conceptual
title: User default permissions in external tenants - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/reference-user-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about the default permissions for users in an external tenant.
ms.topic: reference
ms.date: 2025-03-10T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 164ff780-a29f-41d6-4a1e-80c6d999e338
document_version_independent_id: 6bcae341-5d96-a9bd-e823-e9a7c507640c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/reference-user-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/reference-user-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/reference-user-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: df236c59-6a36-1157-9bc3-980b28f21438
---

# User default permissions in external tenants - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

A Microsoft Entra tenant in an *external* configuration is used exclusively for [Microsoft Entra External ID](overview-customers-ciam) scenarios. An external tenant provides clear separation between your corporate workforce directory and your customer-facing app directory. By default, users created in your external tenant are restricted from accessing information about other users, groups, or devices in the external tenant. All users have default permissions unless you assign them an admin role.

To better understand the typical use cases for users in an external tenant, we can categorize them as follows:

- **External users** are consumers and business customers who use the apps registered in your external tenant. They typically retain default user permissions, meaning you don't assign them administrative roles. These users are usually created through self-service sign-up, but you can create them with the [Create new external user](../../fundamentals/how-to-create-delete-users#create-a-new-external-user) option in the Microsoft Entra admin center or with Microsoft Graph.
- **Internal users** are usually admins to whom you assign [Microsoft Entra roles](../../identity/role-based-access-control/permissions-reference). You can create internal users and assign roles using the [Create new user](../../fundamentals/how-to-create-delete-users#create-a-new-user) option in the admin center or with Microsoft Graph.
- **Invited users** are usually admins you invite to the external tenant and to whom you assign [Microsoft Entra roles](../../identity/role-based-access-control/permissions-reference). If they're not assigned a role, they have default user permissions. You can invite users and assign roles using the [Invite external user](../../fundamentals/how-to-create-delete-users#invite-an-external-user) option in the admin center or with Microsoft Graph.

When users are created in an external tenant, they all start with default permissions. However, you can assign [Microsoft Entra roles](../../identity/role-based-access-control/permissions-reference) to those users who need to perform administrative tasks within the external tenant.

## Default permissions

The following table describes the default permissions assigned to a user in an external tenant, including:

- Users who use self-service sign-up
- Users who are created by administrators
- Users who are invited

| **Area** | **Default user permissions** |
| --- | --- |
| Users and contacts | - Read and update their own profile through the app profile management experience<br>- Change their own password<br>- Sign in with a local or social account |
| Applications | - Access applications<br>- Revoke consent to applications |

## Microsoft Graph APIs and permissions

The following table indicates the API operations that enable customers to manage their profile information. The user ID or userPrincipalName is always the signed-in user's.

| User operation | API operation | Permissions required |
| --- | --- | --- |
| Read profile | [GET /me](/en-us/graph/api/user-get) or [GET /users/{id or userPrincipalName}](/en-us/graph/api/user-get) | User.Read |
| Update profile | [PATCH /me](/en-us/graph/api/user-update) or [PATCH /users/{id or userPrincipalName}](/en-us/graph/api/user-update) The following properties are updatable: city, country, displayName, givenName, jobTitle, postalCode, state, streetAddress, surname, and preferredLanguage | User.ReadWrite |
| Change password | [POST /me/changePassword](/en-us/graph/api/user-changepassword) | Directory.AccessAsUser.All |