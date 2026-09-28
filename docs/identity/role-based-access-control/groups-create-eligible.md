---
layout: Conceptual
title: Create a role-assignable group in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/groups-create-eligible
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Learn how to a role-assignable group in Microsoft Entra ID using the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API.
ms.topic: how-to
ms.date: 2025-01-03T00:00:00.0000000Z
ms.reviewer: vincesm
ms.custom: it-pro, no-azure-ad-ps-ref
locale: en-us
document_id: 8b20c1bb-dbfc-06db-b5b4-ce9d67c004cd
document_version_independent_id: acbdb973-4c76-db09-400d-013e364f2dba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/groups-create-eligible.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/groups-create-eligible
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/groups-create-eligible.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 99d8b594-31af-6d24-31a5-28b239eac348
---

# Create a role-assignable group in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes how to create a role-assignable group using the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API.

With Microsoft Entra ID P1 or P2, you can create [role-assignable groups](groups-concept) and assign Microsoft Entra roles to these groups. You create a new role-assignable group by setting **Microsoft Entra roles can be assigned to the group** to **Yes** or by setting the `isAssignableToRole` property set to `true`. A role-assignable group can't be a part of a [dynamic membership group](../users/groups-dynamic-membership) type. In Microsoft Entra, a single tenant can have a maximum of 500 role-assignable groups.

## Prerequisites

- Microsoft Entra ID P1 or P2 license
- [Privileged Role Administrator](permissions-reference#privileged-role-administrator)
- [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) module when using PowerShell
- Admin consent when using Graph explorer for Microsoft Graph API

For more information, see [Prerequisites to use PowerShell or Graph Explorer](prerequisites).

## Create a role-assignable group

# [Admin center](#tab/admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Select **New group**.
4. On the **New Group** page, provide group type, name, and description.
5. Set **Microsoft Entra roles can be assigned to the group** to **Yes**.

    This option is visible to Privileged Role Administrators because this role can set this option.

    [![Screenshot of option to make group a role-assignable group.](media/groups-create-eligible/eligible-switch.png)](media/groups-create-eligible/eligible-switch.png#lightbox)
6. Select the members and owners for the group. You also have the option to assign roles to the group, but assigning a role isn't required here.
7. Select **Create**.

    You see the following message:

    Creating a group to which Microsoft Entra roles can be assigned is a setting that cannot be changed later. Are you sure you want to add this capability?

    [![Screenshot of confirm message when creating a role-assignable group.](media/groups-create-eligible/group-create-message.png)](media/groups-create-eligible/group-create-message.png#lightbox)
8. Select **Yes**.

    The group is created with any roles you might have assigned to it.

# [PowerShell](#tab/ms-powershell)
Use the [New-MgGroup](/en-us/powershell/module/microsoft.graph.groups/new-mggroup?branch=main) command to create a role-assignable group.

This example shows how to create a Security role-assignable group.

```powershell
Connect-MgGraph -Scopes "Group.ReadWrite.All"
$group = New-MgGroup -DisplayName "Contoso_Helpdesk_Administrators" -Description "Helpdesk Administrator role assigned to group" -MailEnabled:$false -SecurityEnabled -MailNickName "contosohelpdeskadministrators" -IsAssignableToRole:$true
```

This example shows how to create a Microsoft 365 role-assignable group.

```powershell
Connect-MgGraph -Scopes "Group.ReadWrite.All"
$group = New-MgGroup -DisplayName "Contoso_Helpdesk_Administrators" -Description "Helpdesk Administrator role assigned to group" -MailEnabled:$true -SecurityEnabled -MailNickName "contosohelpdeskadministrators" -IsAssignableToRole:$true -GroupTypes "Unified"
```

# [Graph API](#tab/ms-graph)
Use the [Create group](/en-us/graph/api/group-post-groups?branch=main) API to create a role-assignable group.

This example shows how to create a Security role-assignable group.

```http
POST https://graph.microsoft.com/v1.0/groups
{
    "description": "Helpdesk Administrator role assigned to group",
    "displayName": "Contoso_Helpdesk_Administrators",
    "isAssignableToRole": true,
    "mailEnabled": false,
    "mailNickname": "contosohelpdeskadministrators",
    "securityEnabled": true
}
```

Response

```http
HTTP/1.1 201 Created
```

This example shows how to create a Microsoft 365 role-assignable group.

```http
POST https://graph.microsoft.com/v1.0/groups
{
  "description": "Helpdesk Administrator role assigned to group",
  "displayName": "Contoso_Helpdesk_Administrators",
  "groupTypes": [
    "Unified"
  ],
  "isAssignableToRole": true,
  "mailEnabled": true,
  "mailNickname": "contosohelpdeskadministrators",
  "securityEnabled": true,
  "visibility" : "Private"
}
```

For this type of group, `isPublic` is always false and `isSecurityEnabled` is always true.

---