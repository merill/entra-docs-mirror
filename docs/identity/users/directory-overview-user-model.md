---
layout: Conceptual
title: Users, groups, licensing, and roles in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/directory-overview-user-model
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: The relationship between users and licenses assigned, administrator roles, dynamic membership groups in Microsoft Entra ID
keywords: 
ms.reviewer: yukarppa
ms.date: 2025-01-31T00:00:00.0000000Z
ms.topic: overview
ms.collection: M365-identity-device-management
ms.custom: it-pro, sfi-ga-nochange
locale: en-us
document_id: 5e434b86-3ce5-0e90-1ad0-b7f35f4c88df
document_version_independent_id: 66d94ffb-9140-4960-ccb2-54e54d1ece86
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/directory-overview-user-model.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/directory-overview-user-model
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/directory-overview-user-model.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 9db595ad-ec2f-e4e0-e3d1-c3a34145a209
---

# Users, groups, licensing, and roles in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

## Overview

This article introduces an administrator for Microsoft Entra ID, part of Microsoft Entra, to the relationship between top [identity management](../../fundamentals/what-is-entra?context=azure/active-directory/users-groups-roles/context/ugr-context) tasks for users in terms of their groups, licenses, deployed enterprise apps, and administrator roles. As your organization grows, you can use Microsoft Entra groups and administrator roles to:

- Assign licenses to groups instead of assigning licenses to individual users.
- Grant permissions to delegate Microsoft Entra management work to personnel in less-privileged roles.
- Assign enterprise app access to groups.

## Assign users to groups

You can use groups in Microsoft Entra ID to assign licenses, or deployed enterprise apps, to large numbers of users. You can also use groups to assign all administrator roles except for Microsoft Entra Global Administrator, or you can grant access to external resources, such as SaaS applications or SharePoint sites.

You can use [dynamic membership groups](groups-create-rule) in Microsoft Entra ID to expand and contract dynamic membership groups automatically. Dynamic groups give you greater flexibility and reduce dynamic membership group management work.

Note

You need a Microsoft Entra ID P1 license for each unique user that is a member of one or more dynamic membership groups.

## Assign licenses to groups

Managing user license assignments individually is time consuming and error prone. If you [assign licenses to groups](../../fundamentals/licensing?context=azure/active-directory/users-groups-roles/context/ugr-context) instead, you experience easier large-scale license management.

Microsoft Entra users who join a licensed group are automatically assigned the appropriate licenses. When users leave the group, Microsoft Entra ID removes their license assignments. Without Microsoft Entra groups, you'd have to write a PowerShell script or use Graph API to bulk add or remove user licenses for users joining or leaving the organization. For more information about group bulk operations, see [Bulk add group members by uploading a CSV file](groups-bulk-import-members).

If there aren't enough licenses available, or an issue occurs like service plans that can't be assigned at the same time, you can see the status of any licensing issue for the group in the Azure portal.

## Delegate administrator roles

Many large organizations want options for their users to obtain sufficient permissions for their work tasks without assigning the powerful Global Administrator role to, for example, users who must register applications. Here's an example of new Microsoft Entra administrator roles to help you distribute the work of application management with more specificity:

| Role name | Permissions summary |
| --- | --- |
| **Application Administrator** | Can add and manage enterprise applications and application registrations, and configure proxy application settings. Application Administrators can view Conditional Access policies and devices, but not manage them. |
| **Cloud Application Administrator** | Can add and manage enterprise applications and enterprise app registrations. This role has all of the permissions of the Application Administrator, except it can't manage application proxy settings. |
| **Application Developer** | Can add and update application registrations, but can't manage enterprise applications or configure an application proxy. |

New Microsoft Entra administrator roles continue to be added. Check the Azure portal or the [administrator role permission reference](../role-based-access-control/permissions-reference) for currently available roles.

## Assign app access

You can use Microsoft Entra ID to assign group access to [enterprise apps deployed in your Microsoft Entra organization](../enterprise-apps/assign-user-or-group-access-portal?context=azure/active-directory/users-groups-roles/context/ugr-context). If you combine dynamic membership groups with group assignment to apps, you can automate user app access assignments as your organization grows. You need a Microsoft Entra ID P1 or Premium P2 license to assign access to enterprise apps.

Microsoft Entra ID also gives you specific control of the data that flows between the app and the groups to whom you assign access. In [Enterprise Applications](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps), open an app and select **Provisioning** to:

- Set up automatic provisioning for apps that support it
- Provide credentials to connect to the app's user management API
- Set up the mappings that control which user attributes flow between Microsoft Entra ID and the app when user accounts are provisioned or updated
- Start and stop the Microsoft Entra provisioning service for an app, clear the provisioning cache, or restart the service
- View the **Provisioning activity report** that provides a log of all users and groups created, updated, and removed between Microsoft Entra ID and the app, and the **Provisioning error report** that provides more detailed error messages