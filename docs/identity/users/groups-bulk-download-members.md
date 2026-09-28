---
layout: Conceptual
title: Bulk download group membership list - Azure portal - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-bulk-download-members
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Download group members in bulk in the Microsoft Entra admin center.
ms.date: 2026-06-18T00:00:00.0000000Z
ms.topic: how-to
ms.custom: it-pro
ms.reviewer: yuan.karppanen
locale: en-us
document_id: 5a414dfa-0ea9-3c4c-e5e0-7ff88dc2dfa6
document_version_independent_id: 8c14bb9f-1acd-d55e-dd8b-ef11cb18aab5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-bulk-download-members.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-bulk-download-members
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-bulk-download-members.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 0b8a64fb-25b8-6600-fd3e-4801a0f0389a
---

# Bulk download group membership list - Azure portal - Microsoft Entra ID | Microsoft Learn

## Overview

You can bulk download the members of a group in your organization to a comma-separated values (CSV) file from the Microsoft Entra admin center. All admins and nonadmin users can download group membership lists.

## Bulk download group members

To download all members of a specific group:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade) and in the left-hand navigation pane, select the **Groups** tab.
2. Select a group from the list and navigate to the **Members** tab.

    ![Screenshot of a selected group's Members tab listing users and service principals.](media/bulk-operations/group-members-tab.png)
3. On the **Members** page command bar, select **Download members**.

    If you see a **Bulk operations** menu instead, select **Bulk operations** &gt; **Download members**.
4. Enter a filename and select **Start bulk operation**.
5. A **Success!** notification appears when the job is submitted. The notification says "Bulk operation download group members submission successful. Click on the title for more information."
6. Select the **Success!** notification title to open the job details. Select the filename to start downloading the CSV file.
7. A **Download successful** notification confirms when the file has been downloaded. You can also select **More activity in the audit log** at the top of the Notifications panel to view all bulk operation activity.

Tip

You can also select **Click here to view the status of each operation** in the download dialog to navigate directly to the **Bulk operation results** page, where you can monitor all pending and completed bulk operations.

### Downloaded CSV file format

The downloaded CSV file contains the following information for each group member:

| Column | Description |
| --- | --- |
| Object ID | The unique identifier (GUID) of the member |
| User principal name | The UPN (for example, `user@contoso.com`) for user members |
| Display name | The display name of the member |
| Member type | Whether the member is a User, Group, or Service Principal |

Tip

You can use the downloaded CSV file as a starting point when you need to remove members from a group. Simply edit the file to include only the members you want to remove, then upload it using the **Remove members** bulk operation.

If you experience errors, you can download and view the results file on the **Bulk operation results** page. The file contains the reason for each error.

## Check download status

You can see the status of all of your pending bulk requests in the **Bulk operation results** page.

1. Navigate to **Identity** &gt; **Users** &gt; **Bulk operation results**.
2. Find your download operation in the list.
3. When **Status** shows **Completed**, select the filename to download the CSV file.

    [![Screenshot that shows the Check status option on the Bulk operation results page.](media/groups-bulk-download-members/bulk-center.png)](media/groups-bulk-download-members/bulk-center.png#lightbox)

## Bulk download service limits

Note

When performing bulk operations, such as import or create, you can encounter a problem if the bulk operation doesn't complete within the hour. To work around this issue, we recommend splitting the number of records processed per batch. For example, before starting an export you could limit the result set by filtering on a group type or user name to reduce the size of the results. By refining your filters, essentially you limit the data returned by the bulk operation. For more information, see [Bulk operations service limitations](../../fundamentals/bulk-operations-service-limitations).