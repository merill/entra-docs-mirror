---
layout: Conceptual
title: Use a group to manage access to SaaS apps - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-saasapps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how to use groups in Microsoft Entra ID to assign access to SaaS applications that are integrated with Microsoft Entra ID.
ms.topic: how-to
ms.date: 2024-12-13T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: acb4037a-0ffe-8b87-6645-d773551bb34d
document_version_independent_id: 6b6e3230-af26-21e0-b3ba-a78bc5119673
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-saasapps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-saasapps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-saasapps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c0439c36-80e3-415f-8e4c-6951e3f1b136
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/2812d699-d85f-4a7f-839d-44e218b35d24
platformId: 23abfc9e-2539-b83e-5ed3-8ff2f727a2d6
---

# Use a group to manage access to SaaS apps - Microsoft Entra ID | Microsoft Learn

## Overview

When you use Microsoft Entra ID with a Microsoft Entra ID P1 or P2 license plan, you can use groups to assign access to software as a service (SaaS) applications integrated with Microsoft Entra ID.

For example, if you want to assign access for a marketing department to use five different SaaS applications, you can create an Office 365 or security group that contains the users in the marketing department. Then you can assign that group to the five SaaS applications that the marketing department needs.

With Microsoft Entra ID, you can save time by managing the membership of the marketing department in one place. Users then are assigned to the application when they're added as members of the marketing group. They have their assignments removed from the application when they're removed from the marketing group. You can use this capability with hundreds of applications that you can add from within the Microsoft Entra Application Gallery.

Important

You can use this feature only after you start a Microsoft Entra ID P1 or P2 trial or purchase a Microsoft Entra ID P1 or P2 license plan. Group-based assignment is supported only for security groups. Nested group memberships aren't supported for group-based assignment to applications at this time.

## Assign access for a user or group to a SaaS application

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Go to **Applications** &gt; **Enterprise applications** to open **All applications** in the Application Gallery.

    ![Screenshot that shows the Application Gallery.](media/domains-manage/enterprise-apps.png)
3. Select an application that you added from the Application Gallery to open it.
4. On the left pane, select **Users and groups**, and then select **Add user/group**.
5. On **Add Assignment**, select **Users and groups** to open the **Users and groups** selection list.
6. Select as many groups or users as you want, and then select **Select** to add them to the **Add Assignment** list. You can also assign a role to a user at this stage.
7. Select **Assign** to assign the users or groups to the selected enterprise application.