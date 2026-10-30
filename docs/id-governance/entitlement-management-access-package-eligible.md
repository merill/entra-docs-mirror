---
layout: Conceptual
title: Assign eligible group membership and ownership in access packages via Privileged Identity Management for Groups - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-eligible
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This how-to article describes how to assign eligible membership and ownership to a group via Privileged Identity Management in an access package.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-11-04T00:00:00.0000000Z
locale: en-us
document_id: 1b84acde-bfc3-11c7-3ea0-b55e8827cc70
document_version_independent_id: 1b84acde-bfc3-11c7-3ea0-b55e8827cc70
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-eligible.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-eligible
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-eligible.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b86c3d22-9fa9-f7ab-582c-68e94da20be1
---

# Assign eligible group membership and ownership in access packages via Privileged Identity Management for Groups - Microsoft Entra ID Governance | Microsoft Learn

As an access package manager, you can assign which role you want to provide a user for a group within an access package. By [managing groups with Privileged Identity Management(PIM)](privileged-identity-management/groups-discover-groups), you're able to enhance security by designating that group access happens just-in-time. This article describes how to enable PIM for a group, adding the group to an access package, and verifying eligible assignments are available.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Create a group

This section walks you through creating the group that you enable to be managed by PIM. If you've already created the group you want to be managed by PIM, skip to [Enable management of group with PIM](entitlement-management-access-package-eligible#enable-management-of-group-with-pim).

To create a group, you'd do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Select **New group**.
4. Give the group a name and description and then complete the other required options:

    - **Group Type:** Security
    - **Membership type:** Select *Assigned*. [![Picture of creating the group for the access package.](media/entitlement-management-access-package-eligible/create-group-eligible.png)](media/entitlement-management-access-package-eligible/create-group-eligible.png#lightbox)
5. Select **Create**.

## Enable management of group with PIM

To enable PIM management for the group, you'd do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Groups**.
3. Select **Discover groups** and select a group that you want to bring under management with PIM.
4. Select **Manage groups** and **OK**.
5. Select **Groups** to return to the list of groups enabled in PIM for Groups, and notice the group you added is now on the list. [![Screenshot of groups managed by PIM list.](media/entitlement-management-access-package-eligible/groups-managed-pim-list.png)](media/entitlement-management-access-package-eligible/groups-managed-pim-list.png#lightbox)

Important

Once a group is managed, it can't be taken out of management. This prevents another resource administrator from removing PIM settings. If a group is deleted from Microsoft Entra ID, it can take up to 24 hours for the group to be removed from the **PIM for Groups** option.

## Add the resource to an access package

Once the resource is managed by PIM, eligible roles can be added as its role assignment in an access package. To verify this, do the following:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privileged roles that can complete this task include the Catalog owner and the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the **Access packages** page, open the access package you want to add resource roles to.
4. In the left menu, select **Resource roles**.
5. Select **Add resource roles** to open the Add resource roles to access package page.
6. On the resource roles page, select **Groups and Teams**.
7. Select the group you want to add, and under roles verify that you can assign both active and eligible roles. After choosing the role, select **Next**. [![Screenshot of eligible roles list for a group.](media/entitlement-management-access-package-eligible/eligible-roles-list.png)](media/entitlement-management-access-package-eligible/eligible-roles-list.png#lightbox)
8. When you're finished filling in required **Requests** information, go to **Lifecycle**.
9. Verify the Access Package expiration period doesn't exceed the **Expire eligible assignments after** setting in the PIM managed group.

Note

If an Access Package expiration period exceeds the "*Expire eligible assignments after*" policy setting in the PIM managed group, it can cause discrepancies between Entitlement Management and Privileged Identity Management, leading to identities losing access while EM shows they're still assigned. For more information, see: [Using groups managed by Privileged Identity Management with access packages reference](entitlement-management-access-package-pim-reference).