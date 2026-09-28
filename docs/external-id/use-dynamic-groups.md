---
layout: Conceptual
title: Dynamic groups setup - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/use-dynamic-groups
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to create and manage dynamic membership groups in Microsoft Entra External ID. Set rules based on user attributes to automate group membership for B2B collaboration.
ms.topic: how-to
ms.date: 2024-10-21T00:00:00.0000000Z
ms.custom: it-pro
ms.collection: M365-identity-device-management
locale: en-us
document_id: d955ab2a-eed7-fb67-f1ec-d135094837cb
document_version_independent_id: c723b4a8-ad3a-0693-bfe7-e1a4339ee12e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/use-dynamic-groups.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/use-dynamic-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/use-dynamic-groups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 4a39f9e2-5ab6-326d-95c5-3ee9df268ac3
---

# Dynamic groups setup - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

## What are dynamic membership groups?

A dynamic membership group is a security-based configuration for Microsoft Entra available in the [Microsoft Entra admin center](https://entra.microsoft.com). Administrators can set rules to populate dynamic membership groups that are created in Microsoft Entra ID based on user attributes (such as [userType](user-properties), department, or country/region). Members can be automatically added to or removed from a security group based on their attributes. These groups can provide access to applications or cloud resources (SharePoint sites, documents) and to assign licenses to members. Learn more about [dedicated groups in Microsoft Entra ID](/en-us/entra/fundamentals/how-to-manage-groups).

## Prerequisites

[Microsoft Entra ID P1 or P2 licensing](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing) is required to create and use dynamic membership groups. Learn more in [Create attribute-based rules for dynamic membership groups in Microsoft Entra ID](../identity/users/groups-dynamic-membership).

## Creating an "all users" dynamic group

You can create a group containing all users within a tenant using a membership rule. When users are added or removed from the tenant in the future, the group's membership is adjusted automatically.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**, and then select **New group**.
3. On the **New Group** page, under **Group type**, select **Security**. Enter a **Group name** and **Group description** for the new group.
4. Under **Membership type**, select **Dynamic User**, and then select **Add dynamic query**.
5. Above the **Rule syntax** text box, select **Edit**. On the **Edit rule syntax** page, type the following expression in the text box:

    ```
    user.objectId -ne null
    ```
6. Select **OK**. The rule appears in the Rule syntax box:

    [![Screenshot of rule syntax for all users dynamic group.](media/use-dynamic-groups/all-user-rule-syntax.png)](media/use-dynamic-groups/all-user-rule-syntax.png#lightbox)
7. Select **Save**. The new dynamic group will now include B2B guest users and member users.
8. Select **Create** on the **New group** page to create the group.

## Creating a group of members only

If you want your group to exclude guest users and include only members of your tenant, create a dynamic group as described above, but in the **Rule syntax** box, enter the following expression:

```
(user.objectId -ne null) and (user.userType -eq "Member")
```

The following image shows the rule syntax for a dynamic group modified to include members only and exclude guests.

[![Screenshot of rule syntax where user type equals member.](media/use-dynamic-groups/all-member-user-rule-syntax.png)](media/use-dynamic-groups/all-member-user-rule-syntax.png#lightbox)

## Creating a group of guests only

You might also find it useful to create a new dynamic group that contains only guest users, so that you can apply policies (such as Microsoft Entra Conditional Access policies) to them. Create a dynamic group as described above, but in the **Rule syntax** box, enter the following expression:

```
(user.objectId -ne null) and (user.userType -eq "Guest")
```

The following image shows the rule syntax for a dynamic group modified to include guests only and exclude member users.

[![Screenshot of rule syntax where user type equals guest.](media/use-dynamic-groups/all-guest-user-rule-syntax.png)](media/use-dynamic-groups/all-guest-user-rule-syntax.png#lightbox)