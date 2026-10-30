---
layout: Conceptual
title: Group management permissions for Microsoft Entra custom roles - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/custom-group-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Group management permissions for Microsoft Entra custom roles in the Microsoft Entra admin center, PowerShell, or Microsoft Graph API.
ms.topic: reference
ms.date: 2024-08-25T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: e96ff53d-b766-e8d9-84fb-710571f0c169
document_version_independent_id: 6c6d7a9d-6150-6998-b1d1-b7b1b3ca2381
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/custom-group-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/custom-group-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/custom-group-permissions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4d1dadec-d8c7-a635-e32f-2217c5bc73c3
---

# Group management permissions for Microsoft Entra custom roles - Microsoft Entra ID | Microsoft Learn

Group management permissions can be used in custom role definitions in Microsoft Entra ID to grant fine-grained access such as the following:

- Manage group properties like name and description
- Manage members and owners
- Create or delete groups
- Read audit logs
- Manage a specific type of group

This article lists the permissions you can use in your custom roles for different group management scenarios. For information about how to create custom roles, see [Create a custom role in Microsoft Entra ID](custom-create).

## License requirements

Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## How to interpret group management permissions

To interpret the group management permissions, it helps to understand what the different permission subtypes mean.

| Permission subtype | Permission subtype description |
| --- | --- |
| groups | Manage security groups and Microsoft 365 groups, excluding role-assignable groups |
| groups.unified | Manage Microsoft 365 groups of both dynamic and assigned membership type, excluding role-assignable groups |
| groups.unified.assignedMembership | Manage Microsoft 365 groups of only assigned membership type, excluding role-assignable groups |
| groups.security | Manage security groups of both dynamic and assigned membership type, excluding role-assignable groups |
| groups.security.assignedMembership | Manage security groups of only assigned membership type, excluding role-assignable groups |

The following table has example permissions for updating group members of different subtypes.

| Permission example | Permission description |
| --- | --- |
| microsoft.directory/**groups**/members/update | Update members of Security groups and Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/**groups.unified**/members/update | Update members of Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/**groups.unified.assignedMembership**/members/update | Update members of Microsoft 365 groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/**groups.security**/members/update | Update members of Security groups, excluding role-assignable groups |
| microsoft.directory/**groups.security.assignedMembership**/members/update | Update members of Security groups of assigned membership type, excluding role-assignable groups |

## Read group information

The following permissions are available to read properties, members, and owners of groups.

| Permission | Description |
| --- | --- |
| microsoft.directory/groups/allProperties/read | Read all properties (including privileged properties) on Security groups and Microsoft 365 groups, including role-assignable groups |
| microsoft.directory/groups/standard/read | Read standard properties of Security groups and Microsoft 365 groups, including role-assignable groups |
| microsoft.directory/groups/members/read | Read members of Security groups and Microsoft 365 groups, including role-assignable groups |
| microsoft.directory/groups/memberOf/read | Read the memberOf property on Security groups and Microsoft 365 groups, including role-assignable groups |
| microsoft.directory/groups/owners/read | Read owners of Security groups and Microsoft 365 groups, including role-assignable groups |

## Create groups

The following permissions are available to create groups of different types.

| Permission | Description |
| --- | --- |
| microsoft.directory/groups/create | Create Security groups and Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified/create | Create Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified.assignedMembership/create | Create Microsoft 365 groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/groups.security/create | Create Security groups, excluding role-assignable groups |
| microsoft.directory/groups.security.assignedMembership/create | Create Security groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/groups/createAsOwner | Create Security groups and Microsoft 365 groups, excluding role-assignable groups. Creator is added as the first owner. |
| microsoft.directory/groups.unified/createAsOwner | Create Microsoft 365 groups, excluding role-assignable groups. Creator is added as the first owner. |
| microsoft.directory/groups.unified.assignedMembership/createAsOwner | Create Microsoft 365 groups of assigned membership type, excluding role-assignable groups. Creator is added as the first owner. |
| microsoft.directory/groups.security/createAsOwner | Create Security groups, excluding role-assignable groups. Creator is added as the first owner. |
| microsoft.directory/groups.security.assignedMembership/createAsOwner | Create Security groups of assigned membership type, excluding role-assignable groups. Creator is added as the first owner. |

## Update group information

The following permissions are available to update properties and members of groups.

| Permission | Description |
| --- | --- |
| microsoft.directory/groups/allProperties/update | Update all properties (including privileged properties) on Security groups and Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified/allProperties/update | Update all properties (including privileged properties) on Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified.assignedMembership/allProperties/update | Update all properties (including privileged properties) on Microsoft 365 groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/groups.security/allProperties/update | Update all properties (including privileged properties) on Security groups, excluding role-assignable groups |
| microsoft.directory/groups.security.assignedMembership/allProperties/update | Update all properties (including privileged properties) on Security groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/groups/basic/update | Update basic properties on Security groups and Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified/basic/update | Update basic properties on Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified.assignedMembership/basic/update | Update basic properties on Microsoft 365 groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/groups.security/basic/update | Update basic properties on Security groups, excluding role-assignable groups |
| microsoft.directory/groups.security.assignedMembership/basic/update | Update basic properties on Security groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/groups/classification/update | Update the classification property on Security groups and Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified/classification/update | Update the classification property on Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified.assignedMembership/classification/update | Update the classification property on Microsoft 365 groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/groups.security/classification/update | Update the classification property on Security groups, excluding role-assignable groups |
| microsoft.directory/groups.security.assignedMembership/classification/update | Update the classification property on Security groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/groups/dynamicMembershipRule/update | Update the rule for dynamic membership groups on Security groups and Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified/dynamicMembershipRule/update | Update the rule for dynamic membership groups on Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.security/dynamicMembershipRule/update | Update the rule for dynamic membership groups on Security groups, excluding role-assignable groups |
| microsoft.directory/groups/members/update | Update members of Security groups and Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified/members/update | Update members of Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified.assignedMembership/members/update | Update members of Microsoft 365 groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/groups.security/members/update | Update members of Security groups, excluding role-assignable groups |
| microsoft.directory/groups.security.assignedMembership/members/update | Update members of Security groups of assigned membership type, excluding role-assignable groups |

## Update members of different group types

The following permissions are available to update members of different group types.

| Permission | Description |
| --- | --- |
| microsoft.directory/groups/members/update | Update members of Security groups and Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified/members/update | Update members of Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified.assignedMembership/members/update | Update members of Microsoft 365 groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/groups.security/members/update | Update members of Security groups, excluding role-assignable groups |
| microsoft.directory/groups.security.assignedMembership/members/update | Update members of Security groups of assigned membership type, excluding role-assignable groups |

## Delete groups

The following permissions are available to delete groups.

| Permission | Description |
| --- | --- |
| microsoft.directory/groups/delete | Delete Security groups and Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified/members/update | Update members of Microsoft 365 groups, excluding role-assignable groups |
| microsoft.directory/groups.unified.assignedMembership/members/update | Update members of Microsoft 365 groups of assigned membership type, excluding role-assignable groups |
| microsoft.directory/groups.security/members/update | Update members of Security groups, excluding role-assignable groups |
| microsoft.directory/groups.security.assignedMembership/members/update | Update members of Security groups of assigned membership type, excluding role-assignable groups |