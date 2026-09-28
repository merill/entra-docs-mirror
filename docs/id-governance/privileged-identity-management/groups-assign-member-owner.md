---
layout: Conceptual
title: Assign eligibility for a group in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/groups-assign-member-owner
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to assign eligibility for a group in Privileged Identity Management.
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: ilyal
ms.custom: pim, sfi-image-nochange
locale: en-us
document_id: f4da66b2-36f2-753f-4170-bcbf51824033
document_version_independent_id: c9e72e4f-effc-37f0-f418-c92af00f0523
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/groups-assign-member-owner.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/groups-assign-member-owner
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/groups-assign-member-owner.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 65912d17-15fe-52f6-1590-a6d6dd2bd862
---

# Assign eligibility for a group in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn

## Overview

In Microsoft Entra ID, you can use Privileged Identity Management (PIM) to manage just-in-time membership in the group or just-in-time ownership of the group.

When a membership or ownership is assigned, the assignment:

- Can't be assigned for a duration of less than five minutes
- Can't be removed within five minutes of it being assigned

Note

Every user who is eligible for membership in or ownership of a PIM for Groups must have a Microsoft Entra ID P2 or Microsoft Entra ID Governance license. For more information, see [License requirements to use Privileged Identity Management](../licensing-fundamentals).

## Permissions

You need appropriate permissions to manage group membership or ownership in Microsoft Entra PIM.

- To manage ownership of a role-assignable group, you need a Microsoft Entra role with the `microsoft.directory/groupsAssignableToRoles/owners/update` permission, such as Privileged Role Administrator or Global Administrator, or be an active owner of the group.
- To manage membership in a role-assignable group, you need a Microsoft Entra role with the `microsoft.directory/groupsAssignableToRoles/members/update` permission, such as Privileged Role Administrator or Global Administrator, or be an active owner of the group.
- To manage ownership of a non-role-assignable group, you need a Microsoft Entra role with the `microsoft.directory/groups/owners/update` permission, such as Groups Administrator or Identity Governance Administrator, or be an active owner of the group.
- To manage membership in a non-role-assignable group, you need a Microsoft Entra role with the `microsoft.directory/groups/members/update` permission, such as Groups Administrator or Identity Governance Administrator, or be an active owner of the group.

Role assignments for administrators can be scoped at directory level or administrative unit level. Built-in and custom Microsoft Entra roles are supported.

Privileged Identity Management doesn't support permissions that start with `microsoft.directory/groups.security/` or `microsoft.directory/groups.unified/`. Use permissions that start with `microsoft.directory/groups/` instead.

Privileged Identity Management doesn't support groups in Restricted Management Administrative Units (RMAU).

## Assign an owner or member of a group

Follow these steps to make a user an eligible member or owner of a group.

Note

Administrators and group owners can manage groups through the Groups experience and other interfaces, overriding changes made in Microsoft Entra PIM.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Groups**.
3. Here you can view groups that are already enabled for PIM for Groups.

    [![Screenshot of where to view groups that are already enabled for PIM for Groups.](media/pim-for-groups/pim-group-1.png)](media/pim-for-groups/pim-group-1.png#lightbox)
4. Select the group you need to manage.
5. Select **Assignments**.
6. Use **Eligible assignments** and **Active assignments** blades to review existing membership or ownership assignments for selected group.

    [![Screenshot of where to review existing membership or ownership assignments for selected group.](media/pim-for-groups/pim-group-3.png)](media/pim-for-groups/pim-group-3.png#lightbox)
7. Select **Add assignments**.
8. Under **Select role**, choose between **Member** and **Owner** to assign membership or ownership.
9. Select the members or owners you want to make eligible for the group.

    [![Screenshot of where to select the members or owners you want to make eligible for the group.](media/pim-for-groups/pim-group-4.png)](media/pim-for-groups/pim-group-4.png#lightbox)
10. Select **Next**.
11. In the **Assignment type** list, select **Eligible** or **Active**. Privileged Identity Management provides two distinct assignment types:

    - Eligible assignment requires member or owner to perform an activation to use the role. Activations might also require providing a multifactor authentication (MFA), providing a business justification, or requesting approval from designated approvers.

    Important

    For groups used for elevating into Microsoft Entra roles, Microsoft recommends that you require an approval process for eligible member assignments. Assignments that can be activated without approval can leave you vulnerable to a security risk from another administrator with permission to reset an eligible user's passwords.

    - Active assignments don't require the member to perform any activations to use the role. Members or owners assigned as active have the privileges assigned to the role always.
12. If the assignment should be permanent (permanently eligible or permanently assigned), select the **Permanently** check box. Depending on the group's settings, the check box might not appear or might not be editable. For more information, check out the [Configure PIM for Groups settings in Privileged Identity Management](groups-role-settings#assignment-duration) article.

    [![Screenshot of where to configure the setting for add assignments.](media/pim-for-groups/pim-group-5.png)](media/pim-for-groups/pim-group-5.png#lightbox)
13. Select **Assign**.

## Update or remove an existing role assignment

Follow these steps to update or remove an existing role assignment.

Note

Administrators and group owners can manage groups through the Groups experience and other interfaces, overriding changes made in Microsoft Entra PIM.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with a role that has the required permissions.
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Groups**.
3. Here you can view groups that are already enabled for PIM for Groups.

    [![Screenshot of where to view groups that are already enabled for PIM for Groups.](media/pim-for-groups/pim-group-1.png)](media/pim-for-groups/pim-group-1.png#lightbox)
4. Select the group you need to manage.
5. Select **Assignments**.
6. Use **Eligible assignments** and **Active assignments** blades to review existing membership or ownership assignments for selected group.

    [![Screenshot of where to review existing membership or ownership assignments for selected group.](media/pim-for-groups/pim-group-3.png)](media/pim-for-groups/pim-group-3.png#lightbox)
7. Select **Update** or **Remove** to update or remove the membership or ownership assignment.