---
layout: Conceptual
title: Bring groups into Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/groups-discover-groups
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to bring groups into Privileged Identity Management.
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: ilyal
ms.custom: sfi-image-nochange
locale: en-us
document_id: 581995d1-f559-25db-9e0a-ca8bdefd9bea
document_version_independent_id: d7736935-34b8-acb1-9025-76bd24b52645
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/groups-discover-groups.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/groups-discover-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/groups-discover-groups.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ea30f8d1-54ea-e804-ed6a-08a1d594e66e
---

# Bring groups into Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn

## Overview

In Microsoft Entra ID, you can use Privileged Identity Management (PIM) to manage just-in-time membership in the group or just-in-time ownership of the group. Use groups to provide access to Microsoft Entra roles, Azure roles, and various other scenarios. To manage a Microsoft Entra group in PIM, you must bring it under management in PIM.

## Identify groups to manage

Before starting, you need a Microsoft Entra Security group or Microsoft 365 group. To learn more about group management in Microsoft Entra ID, see [Manage Microsoft Entra groups and group membership](/en-us/entra/fundamentals/how-to-manage-groups).

Dynamic groups and groups synchronized from an on-premises environment can't be managed in PIM for Groups.

You need appropriate permissions to bring groups into Microsoft Entra PIM. For role-assignable groups, you need a Microsoft Entra role with `microsoft.directory/groupsAssignableToRoles/owners/update` and `microsoft.directory/groupsAssignableToRoles/members/update` permissions, such as Privileged Role Administrator or Global Administrator, or be an active owner of the group. For non-role-assignable groups, you need a Microsoft Entra role with `microsoft.directory/groups/owners/update` and `microsoft.directory/groups/members/update` permissions, such as Groups Administrator or Identity Governance Administrator, or be an active owner of the group. Role assignments for administrators can be scoped at directory level or administrative unit level. Built-in and custom Microsoft Entra roles are supported.

Privileged Identity Management doesn't support permissions that start with `microsoft.directory/groups.security/` or `microsoft.directory/groups.unified/`. Use permissions that start with `microsoft.directory/groups/` instead.

Privileged Identity Management doesn't support groups in Restricted Management Administrative Units (RMAU).

Note

Administrators and group owners can manage groups through the Groups experience and other interfaces, overriding changes made in Microsoft Entra PIM.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with a Microsoft Entra role that has permissions to manage groups as outlined in the previous section.
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Groups**.
3. View groups that are already enabled for PIM for Groups.

    [![Screenshot of where to view groups that are already enabled for PIM for Groups.](media/pim-for-groups/pim-group-1.png)](media/pim-for-groups/pim-group-1.png#lightbox)
4. Select **Discover groups** and select a group that you want to bring under management with PIM.

    [![Screenshot of where to select a group that you want to bring under management with PIM.](media/pim-for-groups/pim-group-2.png)](media/pim-for-groups/pim-group-2.png#lightbox)
5. Select **Manage groups** and **OK**.
6. Select **Groups** to return to the list of groups enabled in PIM for Groups.

Or, you can use the Groups pane to bring a group under Privileged Identity Management.

[![Screenshot of the Groups pane, so you can select a group to bring under management with PIM.](media/pim-for-groups/enable-pim-group.png)](media/pim-for-groups/enable-pim-group.png#lightbox)

Important

Once a group is managed, it can't be taken out of management. This prevents another resource administrator from removing PIM settings. If a group is deleted from Microsoft Entra ID, it might take up to 24 hours for the group to be removed from the **PIM for Groups** option.