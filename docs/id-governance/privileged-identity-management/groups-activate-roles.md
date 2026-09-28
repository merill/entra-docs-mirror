---
layout: Conceptual
title: Activate your group membership or ownership in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/groups-activate-roles
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to activate your group membership or ownership in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: ilyal
ms.custom: pim
locale: en-us
document_id: 5b5337a5-a4ab-2c6b-8d86-00c907e5f951
document_version_independent_id: 574a92d9-5f94-fc74-2ae0-cb5237db34d4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/groups-activate-roles.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/groups-activate-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/groups-activate-roles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: dfc6f511-e448-447a-3144-779b9cfd2695
---

# Activate your group membership or ownership in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn

## Overview

You can use Privileged Identity Management (PIM) in Microsoft Entra ID to have just-in-time membership in the group or just-in-time ownership of the group.

This article is for eligible members or owners who want to activate their group membership or ownership in PIM.

Important

When a group membership or ownership is activated, Microsoft Entra PIM temporarily adds an active assignment. Microsoft Entra PIM creates an active assignment (adds user as member or owner of the group) within seconds. When deactivation (manual or through activation time expiration) happens, Microsoft Entra PIM removes the user’s group membership or ownership within seconds as well.

An application might provide access to users based on their group membership. In some situations, application access might not immediately reflect the fact that user was added to the group or removed from it. If application previously cached the fact that user isn't member of the group – when user tries to access application again, access might not be provided. Similarly, if application previously cached the fact that user is member of the group – when group membership is deactivated, user might still get access. Specific situation depends on the application’s architecture. For some applications, signing out and signing back in might help to get access added or removed.

## PIM for Groups and ownership deactivation

Microsoft Entra ID doesn't allow you to remove the last (active) owner of a group. For example, consider a group that has active owner A and eligible owner B. If user B activates their ownership with PIM and then later user A is removed from the group or from the tenant, deactivation of user B's ownership won't succeed.

PIM will try to deactivate user B's ownership for up to 30 days. If another active owner C is added to the group, the deactivation will succeed. If deactivation is unsuccessful after 30 days, PIM will stop trying to deactivate user B's ownership and user B will continue to be an active owner.

## Activate a role

When you need to take on a group membership or ownership, you can request activation by using the **My roles** navigation option in PIM.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **My roles** &gt; **Groups**.

    Note

    You might also use this [short link](https://aka.ms/pim) to open the **My roles** page directly.
3. In the **Eligible assignments** blade, review the list of groups that you have eligible membership or ownership for.

    [![Screenshot of the list of groups that you have eligible membership or ownership for.](media/pim-for-groups/pim-group-6.png)](media/pim-for-groups/pim-group-6.png#lightbox)
4. Select **Activate** for the eligible assignment you want to activate.
5. Depending on the group’s setting, you might be asked to provide multifactor authentication or another form of credential.
6. If necessary, specify a custom activation start time. The membership or ownership activates only after the selected time.
7. Depending on the group’s setting, justification for activation might be required. If needed, provide the justification in the **Reason** box.

    [![Screenshot of where to provide a justification in the Reason box.](media/pim-for-groups/pim-group-7.png)](media/pim-for-groups/pim-group-7.png#lightbox)
8. Select **Activate**.

If the [role requires approval](pim-resource-roles-approval-workflow) to activate, an Azure notification appears in the upper right corner of your browser informing you the request is pending approval.

## View the status of your requests

You can view the status of your pending requests to activate. It's important when your requests undergo approval of another person.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **My requests** &gt; **Groups**.
3. Review the list of requests.

    [![Screenshot of where to review the list of requests.](media/pim-for-groups/pim-group-8.png)](media/pim-for-groups/pim-group-8.png#lightbox)

## Cancel a pending request

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **My requests** &gt; **Groups**.

    [![Screenshot of where to select the request you want to cancel.](media/pim-for-groups/pim-group-8.png)](media/pim-for-groups/pim-group-8.png#lightbox)
3. For the request that you want to cancel, select **Cancel**.

When you select **Cancel**, the request is canceled. To activate the role again, you have to submit a new request for activation.