---
layout: Conceptual
title: Bulk add group members by uploading a CSV file - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-bulk-import-members
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Add group members in bulk by using a comma-separated values (CSV) file.
ms.date: 2026-06-18T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: it-pro, sfi-image-nochange
ms.reviewer: jeffsta
locale: en-us
document_id: 6d9b26a1-e401-4d6d-f37e-cceed1c04549
document_version_independent_id: 3db7c764-4815-ee19-a229-8bad3da4a381
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-bulk-import-members.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-bulk-import-members
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-bulk-import-members.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 96681177-1fc1-f21b-f49e-5e8e42c71198
---

# Bulk add group members by uploading a CSV file - Microsoft Entra ID | Microsoft Learn

## Overview

You can add multiple members to a group by using a comma-separated values (CSV) file to bulk import group members in the portal for Microsoft Entra ID.

## Understand the CSV template

Download and fill in the bulk upload CSV template to successfully add Microsoft Entra group members in bulk. Use the template that you download for the group member import operation. The current group member template starts with the column header, not a `version:v1.0` row.

### CSV template structure

The rows in a downloaded CSV template are:

- **Column headings**: Preserve the full downloaded column header exactly as-is. The property name in brackets is only one part of the header, so don't replace the full header with only `memberObjectIdOrUpn`. The current group member import header is `Member object ID or user principal name [memberObjectIdOrUpn] Required`. For group membership changes, you can use either the member object ID or the user principal name (UPN) in the rows under this header.
- **Examples row**: If the template includes a row of example values, such as `Example: 9832aad8-e4fe-496b-a604-95c6eF01ae75`, remove the examples row and replace it with your own entries.

Note

CSV template formats vary by operation. Some templates, such as bulk create or delete users, include `version:v1.0` as the first row. Other templates, such as group member operations, start with column headers. Download the template for your specific operation from the portal. Don't add a version row or any other row that isn't in the downloaded template. Keep any version row and column header row unchanged.

### More guidance

- Keep any version row and column header row in the upload template exactly as downloaded, or the upload can't be processed.
- The required columns are listed first.
- We don't recommend adding new columns to the template. Any additional columns you add are ignored and not processed.
- We recommend that you download the latest version of the CSV template as often as possible.

- Add at least two users' UPNs or object IDs to successfully upload the file.
- Enter one member per row. Don't use semicolons or other delimiters to separate multiple members in a single row.

### Example CSV file

Here's an example of a completed CSV file ready for upload, matching the current group member import template format. This example uses user principal names (UPNs):

```csv
Member object ID or user principal name [memberObjectIdOrUpn] Required
alain@contoso.com
isabella@contoso.com
joseph@contoso.com
chaya@contoso.com
```

Alternatively, you can use object IDs instead of UPNs:

```csv
Member object ID or user principal name [memberObjectIdOrUpn] Required
00aa00aa-bb11-cc22-dd33-44ee44ee44ee
11bb11bb-cc22-dd33-ee44-55ff55ff55ff
22cc22cc-dd33-ee44-ff55-66aa66aa66aa
```

Tip

To find a user's object ID, go to **Identity** &gt; **Users** &gt; **All users**, select the user, and copy the **Object ID** from the user's profile page.

## Bulk import group members

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Navigate to **Identity**.

    Note

    Group owners can also bulk import members of groups they own.
3. Select **Groups** &gt; **All groups**.
4. Open the group to which you're adding members and then select **Members**.
5. On the **Members** page, select **Bulk operations** and then choose **Import members**.
6. On the **Bulk import group members** page, select **Download** to get the CSV file template with required group member properties.

    ![Screenshot that shows the Import Members command is on the profile page for the group.](media/groups-bulk-import-members/import-panel.png)
7. Open the CSV file and add a line for each group member you want to import into the group. For each member, enter either their **User principal name** (UPN, such as `user@contoso.com`) or their **Object ID** (a GUID like `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb`). Enter one member per row. Then save the file.
8. On the **Bulk import group members** page, under **Upload your csv file**, browse to the file. When you select the file, validation of the CSV file starts.
9. When the file contents are validated, the bulk import page displays **File uploaded successfully**. If there are errors, you must fix them before you can submit the job.
10. When your file passes validation, select **Submit** to start the bulk operation that imports the group members to the group.
11. When the import operation finishes, a notification states that the bulk operation succeeded.

If you experience errors, you can download and view the results file on the **Bulk operation results** page. The file contains the reason for each error. The file submission must match the provided template and include the exact column names.

For more information about bulk operations limitations, see Bulk import service limits.

## Check import status

You can see the status of all of your pending bulk requests in the **Bulk operation results** page.

1. Navigate to **Identity** &gt; **Users** &gt; **Bulk operation results**.
2. Find your bulk operation in the list. The **Status** column shows whether the operation is **In Progress**, **Succeeded**, or **Failed**.

    ![Screenshot that shows the Check status option on the Bulk operation results page.](media/groups-bulk-import-members/bulk-center.png)

For details about each line item within the bulk operation, select the values under the **# Success**, **# Failure**, or **Total Requests** columns. If failures occurred, the reasons for failure are listed.

### Download the results file

To download detailed results:

1. On the **Bulk operation results** page, select the operation you want to review.
2. Select **Download** to get a CSV file containing the status of each row from your original upload.
3. Open the CSV file to see which members were added successfully and which failed, along with specific error messages.

Common errors include:

- **Member not found**: The UPN or object ID doesn't exist in your directory.
- **Member already exists**: The user is already a member of the group.
- **Invalid format**: The UPN or object ID format is incorrect.

## Bulk import service limits

Note

When performing bulk operations, such as import or create, you can encounter a problem if the bulk operation doesn't complete within the hour. To work around this issue, we recommend splitting the number of records processed per batch. For example, before starting an export you could limit the result set by filtering on a group type or user name to reduce the size of the results. By refining your filters, essentially you limit the data returned by the bulk operation. For more information, see [Bulk operations service limitations](../../fundamentals/bulk-operations-service-limitations).