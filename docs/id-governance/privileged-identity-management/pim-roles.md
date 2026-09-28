---
layout: Conceptual
title: Roles you can't manage in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-roles
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Describes the roles you can't manage in Microsoft Entra Privileged Identity Management (PIM).
ms.topic: concept-article
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
locale: en-us
document_id: bf1a1d2f-6f7f-e7e3-2c3e-e658e7179877
document_version_independent_id: 77f0313f-4513-2434-3ac6-dea428f57f40
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-roles.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-roles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bb0354e9-bb65-9044-ee16-acea7f1022ce
---

# Roles you can't manage in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn

## Overview

You can manage just-in-time assignments to all [Microsoft Entra roles](../../identity/role-based-access-control/permissions-reference) and all [Azure roles](/en-us/azure/role-based-access-control/built-in-roles) using Privileged Identity Management (PIM) in Microsoft Entra ID. Azure roles include built-in and custom roles attached to your management groups, subscriptions, resource groups, and resources. However, there are a few roles that you can't manage. This article describes the roles you can't manage in Privileged Identity Management.

## Classic subscription administrator roles

You can't manage the following classic subscription administrator roles in Privileged Identity Management:

- Account Administrator
- Service Administrator
- Co-Administrator

For more information about the classic subscription administrator roles, see [Azure roles, Microsoft Entra roles, and classic subscription administrator roles](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles).

## What about Microsoft 365 admin roles?

PIM supports all Microsoft 365 roles in the Microsoft Entra roles and Administrators portal experience, such as Exchange Administrator and SharePoint Administrator, but PIM doesn't support specific roles within Exchange RBAC or SharePoint RBAC. For more information about these Microsoft 365 services, see [Microsoft 365 admin roles](/en-us/microsoft-365/admin/add-users/about-admin-roles).

Note

For information about delays activating the Microsoft Entra Joined Device Local Administrator role, see [How to manage the local administrators group on Microsoft Entra joined devices](../../identity/devices/assign-local-admin#manage-the-microsoft-entra-joined-device-local-administrator-role).

Note

Use [PIM for Microsoft Entra roles](pim-how-to-add-role-to-user) instead of PIM for Groups to provide just-in-time access to SharePoint, Exchange, or Microsoft Purview portal. For more information, see [Privileged Identity Management (PIM) for Groups](concept-pim-for-groups#make-a-group-of-users-eligible-for-a-microsoft-entra-role).