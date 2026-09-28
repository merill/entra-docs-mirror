---
layout: Conceptual
title: Manage Microsoft Entra user roles - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/how-to-assign-roles-to-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn how to assign and update user roles with Microsoft Entra ID.
ms.reviewer: jeffsta
ms.date: 2026-06-19T00:00:00.0000000Z
ms.topic: how-to
locale: en-us
document_id: 525a66c8-448c-5aa1-752b-c84039cdb65b
document_version_independent_id: 525a66c8-448c-5aa1-752b-c84039cdb65b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/how-to-assign-roles-to-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/how-to-assign-roles-to-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/how-to-assign-roles-to-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: ee4b9aed-e06f-1840-7c8b-7bc8a2b36a2d
---

# Manage Microsoft Entra user roles - Microsoft Entra | Microsoft Learn

The ability to manage resources is granted by assigning roles that provide the required permissions. Roles can be assigned to individual users or groups. To align with the [Zero Trust guiding principles](/en-us/azure/security/fundamentals/zero-trust), use Just-In-Time and Just-Enough-Access policies when assigning roles.

This article provides instructions on how to assign roles directly to users in the Microsoft Entra admin center.

## Prerequisites

Before assigning roles to users, review the following Microsoft Learn articles:

- [Learn about Microsoft Entra roles](../identity/role-based-access-control/concept-understand-roles)
- [Learn about role based access control](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles)
- [Explore the Azure built-in roles](../identity/role-based-access-control/permissions-reference)

To use Privileged Identity Management, you must have a Microsoft Entra ID P2 or Microsoft Entra ID Governance license. For more information on licensing, see [Microsoft Entra ID Governance licensing fundamentals](../id-governance/licensing-fundamentals).

## Assign roles

If you need to assign a role directly to a user, you select the user, choose the role, and adjust the settings. While assigning roles directly to users might be necessary for one-off scenarios, consider using groups to manage role assignments at scale. For more information, see [Use group to manage role assignments](../identity/role-based-access-control/groups-concept)

Eligible roles are assigned to a user but must be elevated Just-In-Time by the user through Privileged Identity Management (PIM). For more information about how to use PIM, see [Privileged Identity Management](../id-governance/privileged-identity-management/).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Privileged Role Administrator](../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Search for and select the user getting the role assignment.

    [![Screenshot of the All Users list with a user highlighted.](media/how-to-assign-roles-to-users/select-existing-user.png)](media/how-to-assign-roles-to-users/select-existing-user.png#lightbox)
4. Select **Assigned roles** from the side menu, then select **Add assignments**.

    [![Screenshot of assigned roles page with Add assignments highlighted.](media/how-to-assign-roles-to-users/assigned-roles-add-assignment.png)](media/how-to-assign-roles-to-users/assigned-roles-add-assignment.png#lightbox)
5. Select a role to assign from the dropdown list and select the **Next** button.
6. Select an **Assignment type**.

    If your organization has a Microsoft Entra ID P2, Microsoft Entra ID Governance, or Microsoft Entra Suite license, you can assign roles as either *eligible* or *active*. If your organization has a Free or Microsoft Entra ID P1 license, you can only assign roles as *active*.

    [![Screenshot of the role assignment settings.](media/how-to-assign-roles-to-users/role-assignment-settings.png)](media/how-to-assign-roles-to-users/role-assignment-settings.png#lightbox)
7. Leave the **Permanently eligible** option selected if the role should always be *available* to elevate for the user.

    If you uncheck this option, you can specify a date range for the role eligibility.
8. Select the **Assign** button.

    Assigned roles appear in the associated section for the user, so eligible and active roles are listed separately.

## Update roles

You can change the settings of a role assignment, for example to change an active role to eligible.

1. Browse to **Entra ID** &gt; **Users**.
2. Search for and select the user getting their role updated.
3. Select **Assigned roles** from the side menu, then select either **Eligible assignments** or **Active assignments**.
4. Select the **Update** link for the role that needs to be changed.

    [![Screenshot of assigned roles page with the Remove and Update options highlighted.](media/how-to-assign-roles-to-users/remove-update-role-assignment.png)](media/how-to-assign-roles-to-users/remove-update-role-assignment.png#lightbox)
5. Change the settings as needed and select the **Save** button.

    [![Screenshot of the role membership settings panel.](media/how-to-assign-roles-to-users/update-role-settings.png)](media/how-to-assign-roles-to-users/update-role-settings.png#lightbox)

## Remove roles

You can remove role assignments from the **Administrative roles** page for a selected user.

1. Browse to **Entra ID** &gt; **Users**.
2. Search for and select the user getting the role assignment removed.
3. Go to the **Assigned roles** page and select the **Remove** link for the role that needs to be removed. Confirm the change in the pop-up message.