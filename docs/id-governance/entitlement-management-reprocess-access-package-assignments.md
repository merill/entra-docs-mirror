---
layout: Conceptual
title: Reprocess assignments for an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-reprocess-access-package-assignments
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to reprocess assignments for an access package in entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2024-07-15T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: aa73c20a-dced-8c17-b5af-0b9955d54b90
document_version_independent_id: 48ec926f-1aba-7d19-13bf-41d685adb6ac
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-reprocess-access-package-assignments.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-reprocess-access-package-assignments
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-reprocess-access-package-assignments.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c5bd7a95-a5df-d798-4cbf-c0ef47dbcab3
---

# Reprocess assignments for an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

As an access package manager, you can automatically reevaluate and enforce users’ original assignments in an access package using the reprocess functionality. Reprocessing eliminates the need for users to repeat the access package request process if their access to resources was impacted by changes outside of Entitlement Management.

For example, a user could have been removed from a group manually, thereby causing that user to lose access to necessary resources.

Entitlement Management doesn't block outside updates to the access package’s resources, so the Entitlement Management UI wouldn't accurately display this change. Therefore, the user’s assignment status would be shown as “Delivered” even though the user doesn't have access to the resources anymore. However, if the user’s assignment is reprocessed, they're added to the access package’s resources again. Reprocessing ensures that the access package assignments are up to date, that users have access to necessary resources, and that assignments are accurately reflected in the UI.

This article describes how to reprocess assignments in an existing access package.

Note

Reprocessing access package assignments in the Microsoft Entra admin center requires the signed-in user to be able to access the admin center. Entitlement management roles, such as Access package assignment manager, authorize assignment-management actions within entitlement management, but they don't by themselves change tenant-wide access settings for the admin center. If the **Restrict access to Microsoft Entra administration portal** user setting is enabled, verify that the delegated user can access the admin center, or use an authorized programmatic method. For more information about this setting, see [Default user permissions](../fundamentals/users-default-permissions).

## Prerequisites

To use entitlement management and assign users to access packages, you must have one of the following licenses:

- Microsoft Entra ID P2 or Microsoft Entra ID Governance
- Enterprise Mobility + Security (EMS) E5 license

## Open an existing access package and reprocess user assignments

If you have users who are in the "Delivered" state but don't have access to resources that are a part of the access package, you'll likely need to reprocess the assignments to reassign those users to the access package's resources. Follow these steps to reprocess assignments for an existing access package:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, Access package manager, and Access package assignment manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages page, open the access package with the user assignment you want to reprocess.
4. Underneath **Manage** on the left side, select **Assignments**.

    ![Entitlement management in the Microsoft Entra admin center](media/entitlement-management-reprocess-access-package-assignments/reprocess-access-package-assignment.png)
5. Select all users whose assignments you wish to reprocess.
6. Select **Reprocess**.