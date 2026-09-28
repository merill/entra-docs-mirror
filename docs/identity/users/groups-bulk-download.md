---
layout: Conceptual
title: Download a list of groups in the Azure portal - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-bulk-download
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Download group properties in bulk in the Azure admin center in Microsoft Entra ID.
ms.date: 2025-12-05T00:00:00.0000000Z
ms.topic: how-to
ms.custom: it-pro, sfi-image-nochange
ms.reviewer: jeffsta
locale: en-us
document_id: 0acd5ee1-4e4b-8441-8548-f97a295a039c
document_version_independent_id: f0960ef0-2d14-e0f0-3dd5-40a9ae68673f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-bulk-download.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-bulk-download
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-bulk-download.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 1f47ed4c-0697-88b9-25a2-49208f2cdc63
---

# Download a list of groups in the Azure portal - Microsoft Entra ID | Microsoft Learn

## Overview

You can download a list of all the groups in your organization to a comma-separated values (CSV) file in the portal for Microsoft Entra ID. All admins and nonadmin users can download group lists.

## Bulk download groups

To download all groups in your organization:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade) and in the left-hand navigation pane, select the **Groups** tab and then **All groups**.

    ![Screenshot of the Microsoft Entra admin center Groups blade showing the All groups list with column headers and actions.](media/bulk-operations/groups-management-page.png)
2. Select **Download groups**.

    ![Screenshot of the Groups page with the Download groups button highlighted in the toolbar.](media/bulk-operations/download-groups-button.png)
3. Enter a filename and select **Start bulk operation**.

    ![Screenshot of the Download groups dialog prompting for a filename before starting the bulk operation.](media/bulk-operations/download-filename-dialog.png)
4. A **Success!** notification appears when the job is submitted. The notification says "Bulk operation download groups submission successful. Click on the title for more information."
5. Select the **Success!** notification title to open the job details, then select the filename to download the CSV file. A **Download successful** notification confirms when the file has been downloaded.

Tip

You can also select **Click here to view the status of each operation** in the download dialog to navigate directly to the **Bulk operation results** page, where you can monitor all pending and completed bulk operations.

### Downloaded CSV file format

The downloaded CSV file contains information about each group, including:

| Column | Description |
| --- | --- |
| Object ID | The unique identifier (GUID) of the group |
| Display name | The display name of the group |
| Mail | The email address associated with the group (if applicable) |
| Group type | Security or Microsoft 365 |
| Membership type | Assigned or Dynamic |

Tip

You can use the downloaded CSV file to get object IDs that you need for other bulk operations, such as adding members to groups.

## Download filtered groups

To download a filtered subset of groups:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade) and in the left-hand navigation pane, select the **Groups** tab.
2. Select **Manage filters** to edit the column filters.
3. Select **Download groups**.
4. Follow steps 3-5 from Bulk download groups.

Note

When filtering groups, only the selected columns appear in the CSV file after editing filters.

If you experience errors, you can download and view the results file on the **Bulk operation results** page. The file contains the reason for each error. The file submission must match the provided template and include the exact column names. For more information about bulk operations limitations, see Bulk download service limits.

## Check download status

You can see the status of all of your pending bulk requests in the **Bulk operation results** page.

[![Screenshot that shows the Check status option on the Bulk operation results page.](media/groups-bulk-download/bulk-center.png)](media/groups-bulk-download/bulk-center.png#lightbox)

## Bulk download service limits

Note

When performing bulk operations, such as import or create, you can encounter a problem if the bulk operation doesn't complete within the hour. To work around this issue, we recommend splitting the number of records processed per batch. For example, before starting an export you could limit the result set by filtering on a group type or user name to reduce the size of the results. By refining your filters, essentially you limit the data returned by the bulk operation. For more information, see [Bulk operations service limitations](../../fundamentals/bulk-operations-service-limitations).