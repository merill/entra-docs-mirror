---
layout: Conceptual
title: User management permissions for Microsoft Entra custom roles - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/custom-user-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: User management permissions for Microsoft Entra custom roles in the Microsoft Entra admin center, PowerShell, or Microsoft Graph API.
ms.topic: reference
ms.date: 2023-06-09T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 9661198d-b7ad-f939-637b-5a879b50e5a2
document_version_independent_id: 8a286ca6-982f-cfd7-77ce-ad2cb1fa325d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/custom-user-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/custom-user-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/custom-user-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1024623c-5d4d-5ff9-19ba-03dad97b868d
---

# User management permissions for Microsoft Entra custom roles - Microsoft Entra ID | Microsoft Learn

User management permissions can be used in custom role definitions in Microsoft Entra ID to grant fine-grained access such as the following:

- Read or update basic properties of users
- Read identity of users
- Read or update job information of users
- Update contact information of users
- Update parental controls of users
- Update settings of users
- Read direct reports of users
- Update extension properties of users
- Read device information of users
- Read or manage licenses of users
- Update password policies of users
- Read assignments and memberships of users

This article lists the permissions you can use in your custom roles for different user management scenarios. For information about how to create custom roles, see [Create a custom role in Microsoft Entra ID](custom-create).

## License requirements

Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## Read or update basic properties of users

The following permissions are available to read or update basic properties of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/standard/read | Read basic properties on users |
| microsoft.directory/users/basic/update | Update basic properties on users |

## Read identity of users

The following permissions are available to read identity of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/identities/read | Read identities of users |

## Read or update job information of users

The following permissions are available to read or update job information of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/manager/read | Read manager of users |
| microsoft.directory/users/manager/update | Update manager for users |
| microsoft.directory/users/jobInfo/update | Update job information of users |

## Update contact information of users

The following permissions are available to update contact information of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/contactInfo/update | Update contact properties on users |

## Update parental controls of users

The following permissions are available to update parental controls of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/parentalControls/update | Update parental controls of users |

## Update settings of users

The following permissions are available to update settings of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/usageLocation/update | Update usage location of users |

## Read direct reports of users

The following permissions are available to read direct reports of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/directReports/read | Read the direct reports for users |

## Update extension properties of users

The following permissions are available to update extension properties of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/extensionProperties/update | Update extension properties of users |

## Read device information of users

The following permissions are available to read device information of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/ownedDevices/read | Read owned devices of users |
| microsoft.directory/users/registeredDevices/read | Read registered devices of users |
| microsoft.directory/users/deviceForResourceAccount/read | Read deviceForResourceAccount of users |

## Read or manage licenses of users

The following permissions are available to read or manage licenses of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/licenseDetails/read | Read license details of users |
| microsoft.directory/users/assignLicense | Manage user licenses |
| microsoft.directory/users/reprocessLicenseAssignment | Reprocess license assignments for users |

## Update password policies of users

The following permissions are available to update password policies of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/passwordPolicies/update | Update password policies properties of users |

## Read assignments and memberships of users

The following permissions are available to read assignments and memberships of users.

| Permission | Description |
| --- | --- |
| microsoft.directory/users/appRoleAssignments/read | Read application role assignments for users |
| microsoft.directory/users/scopedRoleMemberOf/read | Read user's membership of a Microsoft Entra role, that is scoped to an administrative unit |
| microsoft.directory/users/memberOf/read | Read the dynamic membership group for users |

## Full list of permissions

| Permission | Description |
| --- | --- |
| microsoft.directory/users/appRoleAssignments/read | Read application role assignments for users |
| microsoft.directory/users/assignLicense | Manage user licenses |
| microsoft.directory/users/basic/update | Update basic properties on users |
| microsoft.directory/users/contactInfo/update | Update contact properties on users |
| microsoft.directory/users/deviceForResourceAccount/read | Read deviceForResourceAccount of users |
| microsoft.directory/users/directReports/read | Read the direct reports for users |
| microsoft.directory/users/extensionProperties/update | Update extension properties of users |
| microsoft.directory/users/identities/read | Read identities of users |
| microsoft.directory/users/jobInfo/update | Update job information of users |
| microsoft.directory/users/licenseDetails/read | Read license details of users |
| microsoft.directory/users/manager/read | Read manager of users |
| microsoft.directory/users/manager/update | Update manager for users |
| microsoft.directory/users/memberOf/read | Read the dynamic membership group for users |
| microsoft.directory/users/ownedDevices/read | Read owned devices of users |
| microsoft.directory/users/parentalControls/update | Update parental controls of users |
| microsoft.directory/users/passwordPolicies/update | Update password policies properties of users |
| microsoft.directory/users/registeredDevices/read | Read registered devices of users |
| microsoft.directory/users/reprocessLicenseAssignment | Reprocess license assignments for users |
| microsoft.directory/users/scopedRoleMemberOf/read | Read user's membership of a Microsoft Entra role, that is scoped to an administrative unit |
| microsoft.directory/users/standard/read | Read basic properties on users |
| microsoft.directory/users/usageLocation/update | Update usage location of users |