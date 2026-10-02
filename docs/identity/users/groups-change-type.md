---
layout: Conceptual
title: Change Static Groups to Dynamic Membership Groups - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-change-type
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how to convert existing membership groups from static to dynamic by using either the Azure portal or PowerShell cmdlets.
ms.topic: how-to
ms.date: 2025-07-10T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
locale: en-us
document_id: 31e6466f-2c97-2c85-98bc-6f5ed8a5b60e
document_version_independent_id: 349f34d6-02dc-fcbe-65bd-d53e66833b98
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-change-type.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-change-type
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-change-type.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: 0a703dfd-943e-18ba-280b-c4bb49d5ec34
---

# Change Static Groups to Dynamic Membership Groups - Microsoft Entra ID | Microsoft Learn

## Overview

You can change a group's membership from static to dynamic (or vice versa) in Microsoft Entra ID. Microsoft Entra ID keeps the same group name and ID in the system, so all existing references to the group are still valid. If you create a new group instead, you need to update those references.

Creating dynamic membership groups eliminates the management overhead of adding and removing users. This article shows you how to convert existing membership groups from static to dynamic, by using either the Azure portal or PowerShell cmdlets. In Microsoft Entra, a single tenant can have a maximum of 15,000 dynamic membership groups.

Note

When a static group is converted to a dynamic membership group, existing members who meet the membership rule remain. Members who don't are removed. Other users who satisfy the membership rule are added automatically. If the group is used to control access to apps or resources, the original members might lose access until the membership rule is fully processed.

Test the new membership rule beforehand to make sure that the new membership in the group is as expected. If you encounter errors during your test, see [Manage group-based licensing errors](/en-us/microsoft-365/admin/manage/manage-group-licenses?view=o365-worldwide&amp;preserve-view=true#manage-group-based-licensing-errors).

## Prerequisites

- To change the membership type by using the portal, you need an account that has at least the [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator) role.
- To change dynamic group properties by using PowerShell, you need to use cmdlets from the Microsoft Graph PowerShell module. For more information, see [Install the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation).

## Change the membership type for a group (portal)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a Groups Administrator.
2. Select **Microsoft Entra ID**.
3. Select **Groups**.
4. In the **All groups** list, open the group that you want to change.
5. Select **Properties**.
6. On the **Properties** page for the group, select a **Membership type** value of **Assigned (static)**, **Dynamic User**, or **Dynamic Device**, depending on your desired membership type. For dynamic membership groups, you can use the rule builder to select options for a simple rule or write a membership rule yourself.

    The following steps are an example of changing a group of users from static to dynamic membership groups:

    1. For **Membership type**, select **Dynamic User**. In the dialog that explains the changes to the dynamic membership groups, select **Yes** to continue.

        [![Screenshot of selecting a membership type of dynamic user.](media/groups-change-type/select-group-to-convert.png)](media/groups-change-type/select-group-to-convert.png#lightbox)
    2. Select **Add dynamic query**, and then provide the rule.

        [![Screenshot of entering a rule for a dynamic group.](media/groups-change-type/enter-rule.png)](media/groups-change-type/enter-rule.png#lightbox)
7. After you create the rule, select **Add query**.
8. On the **Properties** page for the group, select **Save** to save your changes. The **Membership type** of the group is immediately updated in the group list.

Tip

Group conversion might fail if the membership rule that you entered was incorrect. In the upper-right corner of the portal, a notification explains why the rule can't be accepted. Read it carefully to understand how you can adjust the rule to make it valid. For examples of rule syntax and a complete list of the supported properties, operators, and values for a membership rule, see [Manage rules for dynamic membership groups in Microsoft Entra ID](groups-dynamic-membership).

## Change the membership type for a group (PowerShell)

Here's an example of functions that switch membership management on an existing group. This example correctly manipulates the `GroupTypes` property to preserve any values that are unrelated to dynamic membership groups.

```powershell
#The moniker for dynamic membership groups, as used in the GroupTypes property of a group object
$dynamicGroupTypeString = "DynamicMembership"

function ConvertDynamicGroupToStatic
{
    Param([string]$groupId)

    #Existing group types
    [System.Collections.ArrayList]$groupTypes = (Get-MgGroup -GroupId $groupId).GroupTypes

    if($groupTypes -eq $null -or !$groupTypes.Contains($dynamicGroupTypeString))
    {
        throw "This group is already a static group. Aborting conversion.";
    }

    #Remove the type for dynamic membership groups, but keep the other type values
    $groupTypes.Remove($dynamicGroupTypeString)

    #Modify the group properties to make it a static group: change GroupTypes to remove the dynamic type, and then pause execution of the current rule
    Update-MgGroup -GroupId $groupId -GroupTypes $groupTypes.ToArray() -MembershipRuleProcessingState "Paused"
}

function ConvertStaticGroupToDynamic
{
    Param([string]$groupId, [string]$dynamicMembershipRule)

    #Existing group types
    [System.Collections.ArrayList]$groupTypes = (Get-MgGroup -GroupId $groupId).GroupTypes

    if($groupTypes -ne $null -and $groupTypes.Contains($dynamicGroupTypeString))
    {
        throw "This group is already a dynamic group. Aborting conversion.";
    }
    #Add the dynamic group type to existing types
    $groupTypes.Add($dynamicGroupTypeString)

    #Modify the group properties to make it a static group: change GroupTypes to add the dynamic type, start execution of the rule, and then set the rule
    Update-MgGroup -GroupId $groupId -GroupTypes $groupTypes.ToArray() -MembershipRuleProcessingState "On" -MembershipRule $dynamicMembershipRule
}
```

To make a group static, use this command:

```powershell
ConvertDynamicGroupToStatic "a58913b2-eee4-44f9-beb2-e381c375058f"
```

To make a group dynamic, use this command:

```powershell
ConvertStaticGroupToDynamic "a58913b2-eee4-44f9-beb2-e381c375058f" "user.displayName -startsWith ""Peter"""
```