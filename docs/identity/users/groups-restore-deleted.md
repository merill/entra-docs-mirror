---
layout: Conceptual
title: Restore a deleted Microsoft 365 group or cloud security group - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-restore-deleted
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how to restore a deleted group, view restorable groups, and permanently delete a group in Microsoft Entra ID.
ms.topic: quickstart
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro, mode-other, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-ga-nochange
locale: en-us
document_id: 15f3d6f9-06fa-f9f8-233d-97b239153e45
document_version_independent_id: bdac0301-26d3-d52c-c883-3e588ed55296
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-restore-deleted.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-restore-deleted
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-restore-deleted.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6e73d156-559d-3e49-b57f-a03f14000b06
---

# Restore a deleted Microsoft 365 group or cloud security group - Microsoft Entra ID | Microsoft Learn

## Overview

When you delete a Microsoft 365 group or cloud security group in Microsoft Entra ID, the deleted group is retained but not visible for 30 days from the deletion date. This behavior is so that the group and its contents can be restored if needed. This functionality is available for Microsoft 365 groups and cloud security groups in Microsoft Entra ID. It isn't available for distribution groups. The 30-day group restoration period isn't customizable.

Permissions that are required to restore a group are listed in the following table.

| Role | Permissions |
| --- | --- |
| Global Administrator, Group Administrator, Partner Tier 2 Support, and Intune Administrator | Can restore any deleted Microsoft 365 group or cloud security group |
| User Administrator and Partner Tier 1 Support | Can restore any deleted Microsoft 365 group or cloud security group except those groups assigned to the Global Administrator role |
| User | Can restore any deleted Microsoft 365 or cloud security group that they own |

Note

Soft delete is available for Microsoft 365 groups with assigned membership, Microsoft 365 groups with dynamic membership, and cloud security groups. Soft delete and restore for cloud security groups is in preview and available only in public clouds.

Important

Soft delete for security groups isn't supported in the following scenarios:

- EDU tenants using OneDrive for Business (OBD) storage
- Audience targeting with classic web parts (all tenancies)

## View and manage the deleted Microsoft 365 groups and cloud security groups that are available to restore

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Select **Microsoft Entra ID**.
3. Select **Groups** &gt; **All groups** and then select **Deleted groups** to view the deleted groups that are available to restore.

    ![Screenshot that shows viewing groups that are available to restore.](media/groups-restore-deleted/deleted-groups3.png)
4. On the **Deleted groups** pane, you can:

    - Restore the deleted group and its contents by selecting **Restore group**.
    - Permanently remove the deleted group by selecting **Delete permanently**. To permanently remove a group, you must be an administrator.

## View the deleted Microsoft 365 groups and cloud security groups that are available to restore by using PowerShell

Use the following cmdlets to view the deleted groups. You need to verify that the groups you're interested in weren't permanently purged. These cmdlets are part of the [Microsoft Graph PowerShell module](/en-us/powershell/microsoftgraph/installation?view=graph-powershell-1.0&amp;preserve-view=true). For more information about this module, see [Microsoft Graph PowerShell overview](/en-us/powershell/microsoftgraph/overview?view=graph-powershell-1.0&amp;preserve-view=true).

Run the following cmdlet to display all deleted Microsoft 365 groups and cloud security groups in your Microsoft Entra organization that are still available to restore. Install the [Graph](/en-us/powershell/microsoftgraph/installation?view=graph-powershell-1.0&amp;preserve-view=true) beta version if it isn't already installed on the machine.

```powershell
Install-Module Microsoft.Graph.Beta
Connect-MgGraph -Scopes "Group.ReadWrite.All"
Get-MgBetaDirectoryDeletedGroup
```

Alternatively, if you know the object ID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet. You need to verify that the specific deleted group wasn't permanently purged.

```powershell
Get-MgBetaDirectoryDeletedGroup -DirectoryObjectId <objectId>
```

## Restore your deleted Microsoft 365 group or cloud security group

After you verify that the group is still available to restore, restore the deleted group with one of the following steps. If the group contains documents, SharePoint sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.

Run the following cmdlet to restore the group and its contents.

```powershell
Restore-MgBetaDirectoryDeletedItem -DirectoryObjectId <objectId>
```

Alternatively, you can run the following cmdlet to permanently remove the deleted group.

```powershell
Remove-MgBetaDirectoryDeletedItem -DirectoryObjectId <objectId>
```

## How do you know restoration worked?

To verify that you successfully restored a Microsoft 365 group or cloud security group, run the `Get-MgBetaGroup –GroupId <objectId>` cmdlet to display information about the group. After the restore request is completed:

- The group appears in the left navigation pane on Exchange.
- The plan for the group appears in Planner.
- Any SharePoint sites and all their contents are available.
- You can access the group from any of the Exchange endpoints and other Microsoft 365 workloads that support Microsoft 365 groups.