---
layout: Conceptual
title: Add users to a dynamic group - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-dynamic-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Use groups with user membership rules to add or remove users automatically
ms.topic: tutorial
ms.date: 2025-01-31T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.collection: M365-identity-device-management
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: a44453d5-3e4d-56c0-b289-3439f382b95c
document_version_independent_id: 04c64b9b-86c3-2d0d-f2b6-95f66b603a54
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-dynamic-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-dynamic-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-dynamic-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3142dda9-fcdc-0c8e-fd87-17ed6abff746
---

# Add users to a dynamic group - Microsoft Entra ID | Microsoft Learn

## Overview

In Microsoft Entra ID, part of Microsoft Entra, you can automatically add or remove users to security groups or Microsoft 365 groups, so you don't always have to do it manually. Whenever any properties of a user or device change, Microsoft Entra ID evaluates all rules for dynamic membership groups in your Microsoft Entra organization to see if the change should add or remove members.

In this tutorial, you learn how to:

- Create an automatically populated group of guest users from a partner company
- Assign licenses to the group for the partner-specific features for guest users to access
- Bonus: secure the **All users** group by removing guest users so that, for example, you can give your member users access to internal-only sites

If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

This feature requires one Microsoft Entra ID P1 or P2 license for the administrator of the organization. If you don't have one, in Microsoft Entra ID, select **Licenses** &gt; **Products** &gt; **Try/Buy**.

You're not required to assign licenses to the users for them to be members in dynamic membership groups. You only need the minimum number of available Microsoft Entra ID P1 licenses in the organization to cover all such users.

## Create a group of guest users

First, you create a group for your guest users who all are from a single partner company. They need special licensing, so it's often more efficient to create a group for this purpose.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Select **Microsoft Entra ID**.
3. Select **Groups** &gt; **All groups** &gt; **New group**.

    ![Screenshot of using the Select command to start a new group.](media/groups-dynamic-tutorial/new-group.png)
4. On the **New Group** pane:

    - Enter a *Guest users name*, *email address*, and *description* for the group.
    - Change **Membership type** to **Dynamic User**.

    ![Screenshot of Group page where user enters the dynamic membership group details.](media/groups-dynamic-tutorial/new-dynamic-group.png)
5. Select **No owners selected** and on the **Add Owners** pane, scroll to locate the desired owners. Select on the name to add owners to the group.
6. Select **Select** to save the owners and close the **Add Owners** pane.
7. Select **Add dynamic query** in the **Dynamic user members** box.
8. On the **Dynamic membership rules** pane:

    - In the **Property** field, select on the existing value and select **userType**.
    - Verify that the **Operator** field has **Equals** selected.
    - Select the **Value** field and enter **Guest**.
    - Select the **Add Expression** hyperlink to add another line.
    - In the **And/Or** field, select **And**.
    - In the **Property** field, select **companyName**.
    - Verify that the **Operator** field has **Equals** selected.
    - In the **Value** field, enter **Contoso**.
    - Select **Get custom extension properties** to enter an application ID to retrieve all available custom extension properties for creating a rule.
    - When you're done, select **Save** to close **Dynamic membership rules**.
9. To finish and create the group, select **Create** on the **Group** pane.

## Assign licenses

Now that you have your new group, you can apply the licenses that these partner users need.

1. In the [Microsoft 365 admin center](https://admin.microsoft.com/), go to **Billing** &gt; **Licenses**.
2. On the **Subscriptions** tab, select the product that you want to assign.
3. On the **Licenses** page, select the **Groups** tab, and then select **Assign licenses**.
4. Search for the group name that you want to add, and then select the group from the suggested groups list.
5. To assign or remove access to specific items, select **Turn apps and services on or off**.
6. When you're finished, select **Assign**, and then select **Close**.

## Remove guests from All users group

Perhaps your ultimate administrative plan is to assign all of your guest users to their own groups by company. You can also now change the **All users** group so that you can limit it to include users in your organization. Then you can use it to assign apps and licenses that are specific to your home organization.

![Screenshot of using the Change all users group to members only.](media/groups-dynamic-tutorial/all-users-edit.png)

## Clean up resources

When you're finished with the tutorial, clean up the resources you created.

### Remove the guest users group

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Browse to **Groups** &gt; **All groups**.
3. Select the **Guest users** group, select the ellipsis (...), and then select **Delete**. When you delete the group, any assigned licenses are removed.

### Restore the All Users group

1. Select **Entra ID** &gt; **Groups** &gt; **All groups**. Select the name of the **All users** group to open the group.
2. Select **Dynamic membership rules**, clear all the text in the rule, and select **Save**.