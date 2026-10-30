---
layout: Conceptual
title: Bulk remove group members by uploading a CSV file - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-bulk-remove-members
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Remove group members in bulk operations by using a comma-separated values (CSV) file.
ms.date: 2026-06-18T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: it-pro, sfi-image-nochange
ms.reviewer: jeffsta
locale: en-us
document_id: decc29d5-7228-0c43-d603-e98304fe4fd5
document_version_independent_id: 876b9d00-7f70-b53f-bb2b-5f47eb7ec49b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-bulk-remove-members.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-bulk-remove-members
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-bulk-remove-members.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: bbeb5363-a57a-32eb-5d4b-966904de050a
---

# Bulk remove group members by uploading a CSV file - Microsoft Entra ID | Microsoft Learn

## Overview

You can remove a large number of members from a group by using a comma-separated values (CSV) file in the portal for Microsoft Entra ID.

## Understand the CSV template

Download and fill in the bulk upload CSV template to successfully remove Microsoft Entra group members in bulk. Use the template that you download for the group member removal operation. The current group member template starts with the column header, not a `version:v1.0` row.

### CSV template structure

The rows in a downloaded CSV template are:

- **Column headings**: Preserve the full downloaded column header exactly as-is. The property name in brackets is only one part of the header, so don't replace the full header with only `memberObjectIdOrUpn`. The current group member removal header is `Member object ID or user principal name [memberObjectIdOrUpn] Required`. For group membership changes, you can use either the member object ID or the user principal name (UPN) in the rows under this header.
- **Examples row**: If the template includes a row of example values, such as `Example: 9832aad8-e4fe-496b-a604-95c6eF01ae75`, remove the examples row and replace it with your own entries.

Note

CSV template formats vary by operation and can change. Download the latest template for your operation from the Microsoft Entra admin center. Preserve the column headers exactly as downloaded. If the template includes a version row, preserve it. If the template doesn't include a version row, don't add one. Follow the operation-specific instructions for handling the examples row.

### More guidance

- Preserve the column headers exactly as downloaded. If the template includes a version row, preserve it.
- The required columns are listed first.
- We don't recommend adding new columns to the template. Any additional columns you add are ignored and not processed.
- We recommend that you download the latest version of the CSV template as often as possible.

- Enter one member per row. Don't use semicolons or other delimiters to separate multiple members in a single row.

### Example CSV file

Here's an example of a completed CSV file ready for upload:

```csv
Member object ID or user principal name [memberObjectIdOrUpn] Required
alain@contoso.com
isabella@contoso.com
joseph@contoso.com
```

Tip

To get a list of current group members that you can edit, use the **Download members** bulk operation first. This gives you a CSV file with all current members that you can modify to include only the members you want to remove.

## Bulk remove group members

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Open the group from which you're removing members and then select **Members**.
4. On the **Members** page, select **Remove members**.
5. On the **Bulk remove group members** page, select **Download** to get the CSV file template with required group member properties.

    ![Screenshot that shows the Remove Members command is on the profile page for the group.](media/groups-bulk-remove-members/remove-panel.png)
6. Open the CSV file and add a line for each group member you want to remove from the group. For each member, enter either their **User principal name** (UPN, such as `user@contoso.com`) or their **Object ID** (a GUID like `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb`). Enter one member per row. Then save the file.
7. On the **Bulk remove group members** page, under **Upload your csv file**, browse to the file. When you select the file, validation of the CSV file starts.
8. When the file contents are validated, the bulk remove page displays **File uploaded successfully**. If there are errors, you must fix them before you can submit the job.
9. When your file passes validation, select **Submit** to start the bulk operation that removes the group members from the group.
10. When the removal operation finishes, a notification states that the bulk operation succeeded.

If you experience errors, you can download and view the results file on the **Bulk operation results** page. The file contains the reason for each error. The file submission must match the provided template and include the exact column names.

For more information about bulk operations limitations, see Bulk removal service limits.

## Check removal status

You can see the status of all of your pending bulk requests in the **Bulk operation results** page.

![Screenshot that shows the Check status option on the Bulk operation results page.](media/groups-bulk-remove-members/bulk-center.png)

For details about each line item within the bulk operation, select the values under the **# Success**, **# Failure**, or **Total Requests** columns. If failures occurred, the reasons for failure are listed.

## Bulk removal service limits

Note

When performing bulk operations, such as import or create, you can encounter a problem if the bulk operation doesn't complete within the hour. To work around this issue, we recommend splitting the number of records processed per batch. For example, before starting an export you could limit the result set by filtering on a group type or user name to reduce the size of the results. By refining your filters, essentially you limit the data returned by the bulk operation. For more information, see [Bulk operations service limitations](../../fundamentals/bulk-operations-service-limitations).