---
layout: Conceptual
title: Convert guest user lifecycle in entitlement management - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-manage-lifecycle
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to convert guest user access package assignments for an access package in entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-06-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: b3be25e9-c3d9-0aa8-1862-aed34f613b0a
document_version_independent_id: a9866c80-ded3-0cad-5d13-44116ee517b3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-manage-lifecycle.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-manage-lifecycle
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-manage-lifecycle.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 84066603-0b2d-af07-a50a-c5414c5d324d
---

# Convert guest user lifecycle in entitlement management - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn

Entitlement management allows you to gain visibility into the state of a guest user's lifecycle through the following viewpoints:

- **Governed** - The guest user is set to be governed.
- **Ungoverned** - The guest user is set to not be governed.
- **Blank** - The lifecycle for the guest user isn't determined. This happens when the guest user had an access package assigned before managing user lifecycle was possible.

Note

When a guest user is set as **Governed**, based on entitlement management tenant-wide settings their account will be deleted or disabled in specified days after their last access package assignment expires. Learn more about entitlement management settings here: [Manage external access with Microsoft Entra entitlement management](../architecture/6-secure-access-entitlement-managment).

Guest users that already existed in your tenant by being invited are ungoverned. After an ungoverned guest that requests access packages lose their last access package assignment, they'll remain in the tenant indefinitely. If there are guests that have an access package assignment, and only need access from that access package, and there's no other need for them to remain in the tenant, you can convert them to be governed during the time they have that access package assignment. You can directly convert those ungoverned users to be governed by using the **Mark Guests as Governed** functionality in the top menu bar of an access package.

Note

Managing guest user lifecycle from access package assignments in the Microsoft Entra admin center requires the signed-in user to be able to access the admin center. Entitlement management roles, such as Access package assignment manager, authorize assignment-management actions within entitlement management, but they don't by themselves change tenant-wide access settings for the admin center. If the **Restrict access to Microsoft Entra administration portal** user setting is enabled, verify that the delegated user can access the admin center, or use an authorized programmatic method. For more information about this setting, see [Default user permissions](../fundamentals/users-default-permissions).

## Manage guest user lifecycle in the Microsoft Entra admin center

To manage user lifecycle, you'd follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, the Access package manager, and the Access package assignment manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the **Access packages** page, open the access package you want to manage guest user lifecycle of.
4. In the left menu, select **Assignments**.
5. On the assignments screen, select the user you want to manage the lifecycle for, and then select **Mark guest as governed**. Only users who requested access for themselves, and not those users who were assigned to the access package, can be changed. [![Screenshot of the governed user lifecycle selection.](media/entitlement-management-access-package-assignments/govern-user-lifecycle.png)](media/entitlement-management-access-package-assignments/govern-user-lifecycle.png#lightbox)
6. Select save.

## Manage guest user lifecycle programmatically

To manage user lifecycle programmatically using Microsoft Graph, see: [`accessPackageSubject` resource type](/en-us/graph/api/resources/accesspackagesubject).