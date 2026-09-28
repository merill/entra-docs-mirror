---
layout: Conceptual
title: Bulk delete users in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/users-bulk-delete
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Delete users in bulk in Microsoft Entra ID
ms.date: 2026-03-05T00:00:00.0000000Z
ms.topic: how-to
ms.custom: it-pro, sfi-image-nochange
ms.reviewer: jeffsta
locale: en-us
document_id: 1ec44f25-325a-beec-79c6-2f4991088fa0
document_version_independent_id: af186ee8-d08e-0bbb-3b32-9cc2845bbe01
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/users-bulk-delete.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/users-bulk-delete
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/users-bulk-delete.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 496d8e7b-e9a3-622f-a74d-fc113560dead
---

# Bulk delete users in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

## Overview

Using the admin center in Microsoft Entra ID, part of Microsoft Entra, you can remove a large number of users by using a comma-separated values (CSV) file to bulk delete users.

## To bulk delete users

Important

Updates are being made to bulk operations. While this issue is being addressed, you might experience problems deleting users assigned to privileged roles. This problem is temporary and is being resolved as soon as possible.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Select **Microsoft Entra ID**.
3. Select **Users** &gt; **All users** &gt; **Bulk operations** &gt; **Bulk delete**.

    ![Screenshot of the Users page with the Bulk delete option selected.](media/users-bulk-delete/users-bulk-delete.png)
4. On the **Bulk delete user** page, select **Download** to download the latest version of the CSV template.
5. Open the CSV file and add a line for each user you want to delete. The only required value is **User principal name**. Save the file.
6. On the **Bulk delete user** page, under **Upload your csv file**, browse to the file. When you select the file and select **Submit**, validation of the CSV file starts.
7. When the file contents are validated, you’ll see **File uploaded successfully**. If there are errors, you must fix them before you can submit the job.
8. When your file passes validation, select **Submit** to start the bulk operation that deletes the users.
9. When the deletion operation completes, you see a notification that the bulk operation succeeded.

If you experience errors, you can download and view the results file on the **Bulk operation results** page. The file contains the reason for each error. The file submission must match the provided template and include the exact column names.

For more information about bulk operations limitations, see Bulk delete service limits.

## CSV template structure

The rows in the example downloaded CSV template below are as follows:

- **Version number**: The first row containing the version number (for example, `version:v1.0`) must be included in the upload CSV. If your downloaded template includes this row, don't remove or modify it.
- **Column headings**: `User name [userPrincipalName] Required`. Older versions of the template might vary.
- **Examples row**: The template might include a row of example values. `Example: chris@contoso.com` You must remove the example row and replace it with your own entries.

![Screenshot of the CSV file contains names and IDs of the users to delete.](media/users-bulk-delete/delete-csv-file.png)

Note

CSV template formats vary by operation. Some templates, such as bulk create or delete users, include `version:v1.0` as the first row. Other templates, such as group member operations, start with column headers. Download the template for your specific operation from the portal. Don't add a version row or any other row that isn't in the downloaded template. Keep any version row and column header row unchanged.

### Example CSV file

Here's an example of a completed CSV file ready for upload:

```csv
version:v1.0
User name [userPrincipalName] Required
alain@contoso.com
isabella@contoso.com
joseph@contoso.com
chaya@contoso.com
```

### Additional guidance for the CSV template

- Keep any version row and column header row in the upload template exactly as downloaded, or the upload can't be processed.
- The required columns are listed first.
- We don't recommend adding new columns to the template. Any additional columns you add are ignored and not processed.
- We recommend that you download the latest version of the CSV template as often as possible.

- Enter one user per row.

## Check status

You can see the status of all of your pending bulk requests in the **Bulk operation results** page.

[![Screenshot of checking delete status in the Bulk Operations Results page.](media/users-bulk-delete/bulk-center.png)](media/users-bulk-delete/bulk-center.png#lightbox)

Next, you can check to see that the users you deleted exist in the Microsoft Entra organization either in the portal or by using PowerShell.

## Verify deleted users

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Select **Microsoft Entra ID**.
3. Select **All users** only and verify that the users you deleted are no longer listed.

### Verify deleted users with PowerShell

Run the following command:

```PowerShell
Get-MgUser -Filter "UserType eq 'Member'"
```

Verify that the users that you deleted are no longer listed.

## Bulk delete service limits

Note

When performing bulk operations, such as import or create, you can encounter a problem if the bulk operation doesn't complete within the hour. To work around this issue, we recommend splitting the number of records processed per batch. For example, before starting an export you could limit the result set by filtering on a group type or user name to reduce the size of the results. By refining your filters, essentially you limit the data returned by the bulk operation. For more information, see [Bulk operations service limitations](../../fundamentals/bulk-operations-service-limitations).