---
layout: Conceptual
title: Bulk operations in Microsoft Entra ID (Preview) - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/bulk-operations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn about the new Microsoft Entra bulk operations experience for managing users, groups, and devices.
ms.topic: article
ms.date: 2026-06-18T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: a37616e2-f871-a51e-3f42-ae200c60bee4
document_version_independent_id: a37616e2-f871-a51e-3f42-ae200c60bee4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/bulk-operations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/bulk-operations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/bulk-operations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c96014c4-bfe9-a811-e56f-96e9a605d89b
---

# Bulk operations in Microsoft Entra ID (Preview) - Microsoft Entra | Microsoft Learn

## Overview

The new bulk operations experience in Microsoft Entra ID provides enhanced capabilities for managing **Groups**, **Devices, Administrative Unit and Role assignments.** This service enables bulk actions including create, update, and delete operations. The improved service delivers better performance, reduces timeouts, and removes scaling limitations for large tenants.

Note

The new bulk operations service currently only supports **Groups**, **Devices**, **Users** export, **Administrative Unit and Role assignment**. Support for additional entities like **Enterprise applications** will be added in a future update. Localization for templates is partially supported (exported CSV doesn't have a localization template, but import and remove are supported). Additionally, guest users cannot initiate bulk operations. The new bulk operations service doesn't support exporting hidden memberships.

For information about limitations and to learn more about the previous Bulk Operations experience, see [Bulk operations service limitations](bulk-operations-service-limitations).

## Bulk download groups

To download all groups in your organization:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade) and in the left-hand navigation pane, select the **Groups** tab and then **All groups**.

    ![Screenshot of the Microsoft Entra admin center Groups blade showing the All groups list with column headers and actions.](media/bulk-operations/groups-management-page.png)
2. Select **Download groups**.

    ![Screenshot of the Groups page with the Download groups button highlighted in the toolbar.](media/bulk-operations/download-groups-button.png)
3. Enter a filename and select **Start bulk operation**.

    ![Screenshot of the Download groups dialog prompting for a filename before starting the bulk operation.](media/bulk-operations/download-filename-dialog.png)
4. Select the **Click here to view the status of each operation** link to navigate to the **Bulk operations** blade.

    ![Screenshot of a success notification confirming the bulk groups download was submitted with a link to view status.](media/bulk-operations/success-notification.png)
5. Select the filename to download the CSV file containing all groups with the specified columns.

## Download filtered groups

To download a filtered subset of groups:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade) and in the left-hand navigation pane, select the **Groups** tab.
2. Select **Add filter** to open the **Manage filters** panel. Apply desired filters to narrow down the group list. Only selected columns appear in the CSV file.

    ![Screenshot of the Manage filters panel on the Groups page with filters applied and the Download groups action available.](media/bulk-operations/filters-download-groups.png)
3. Select **Download groups**.
4. Follow steps 3-5 from Bulk download groups.

## Bulk download group members

To download all members of a specific group:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade) and in the left-hand navigation pane, select the **Groups** tab.
2. Select a group from the list and navigate to the **Members** tab.

    ![Screenshot of a selected group’s Members tab listing users and service principals.](media/bulk-operations/group-members-tab.png)
3. On the **Members** page command bar, select **Download members**.

    If you see a **Bulk operations** menu instead, select **Bulk operations** &gt; **Download members**.
4. Enter a filename and select **Start bulk operation**.
5. Follow the download process as described in Bulk download groups.

## Bulk import group members in Microsoft Entra ID

To add multiple members to a group:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade) and in the left-hand navigation pane, select the **Groups** tab.
2. Select a group from the list and navigate to the **Members** tab.
3. Select **Bulk operations** &gt; **Import members**.

    ![Screenshot of the Bulk operations menu on the Members tab with Import members selected.](media/bulk-operations/members-bulk-operations-import.png)
4. Select **Download csv template** to get a template file with the correct column header. The template contains one column: `Member object ID or user principal name [memberObjectIdOrUpn] Required`. Delete the example row and add the Object IDs or UPNs for the members you want to import, one per row. You can use either:

    - **Object ID**: The GUID of the user (for example, `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb`)
    - **User principal name**: The UPN of the user (for example, `user@contoso.com`)

    ![Screenshot of the CSV template for importing members showing the ObjectId column for pasting member IDs.](media/bulk-operations/template-download-object-ids.png)
5. Upload the completed CSV file and select **Submit**.
6. Monitor the notification for job completion. Select the **Success!** link to view the operation status.

Important

If you add invalid Object IDs in the uploaded CSV file, the bulk operation status shows **Failed** with reason **NotAllRowsSuccessfullyProcessed**. You can select on the filename to download a detailed report showing the status of each object ID.

## Bulk remove group members

To remove multiple members from a group:

1. Follow steps 1-2 from Bulk download group members.
2. Select **Bulk operations** &gt; **Remove members**.

    ![Screenshot of the Bulk operations menu on the Members tab with Remove members selected.](media/bulk-operations/members-bulk-operations-remove.png)
3. Select **Download csv template** to get a template file with the correct column header. The template contains one column: `Member object ID or user principal name [memberObjectIdOrUpn] Required`. Delete the example row and add the Object IDs or UPNs for the members you want to remove, one per row. You can use either:

    - **Object ID**: The GUID of the user (for example, `aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb`)
    - **User principal name**: The UPN of the user (for example, `user@contoso.com`)
4. Upload the completed CSV file and select **Submit**.

    ![Screenshot of the sample CSV for removing members containing ObjectId values to be processed.](media/bulk-operations/bulk-remove-group-csv.png)
5. Monitor the notification for job completion. Select the **Success!** link to view the operation status.
6. If the operation shows **Failed** status with reason **NotAllRowsSuccessfullyProcessed**, select the filename to download a detailed report showing the status of each object ID.
7. Verify that the specified members were removed from the group.

## Delete bulk jobs

To delete completed or failed bulk operations:

1. Navigate to the [Bulk Operations (Preview)](https://entra.microsoft.com/?feature.tokencaching=true&amp;feature.internalgraphapiversion=true&amp;enableNewBulkJobsExport=true&amp;enableNewBulkJobsList=true#view/Microsoft_AAD_IAM/BulkJobsList.ReactView) page.

    ![Screenshot of the Bulk operations page listing recent bulk jobs with status, type, and timestamp columns.](media/bulk-operations/bulk-jobs.png)
2. Select the bulk job you want to delete.
3. Select **Delete**.

    ![Screenshot of a selected bulk job on the Bulk operations page with the Delete button visible.](media/bulk-operations/delete-bulk-job.png)
4. Confirm the deletion. The deleted job is removed from the list.

    ![Screenshot of a confirmation notification indicating the bulk job was deleted successfully.](media/bulk-operations/delete-bulk-job-notification.png)

## Devices scenario steps

1. Go to the **All devices** blade.

    ![Screenshot of the All devices blade in Microsoft Entra admin center showing the devices list.](media/bulk-operations/all-devices.png)
2. Select **Download devices**.

    ![Screenshot of the All devices page with Bulk operations open and the Download devices option selected.](media/bulk-operations/all-devices-bulk-operations.png)
3. Enter a filename that matches your naming convention and select **Start bulk operation**. ![Screenshot of a success notification after starting the Download devices job.](media/bulk-operations/all-devices-success.png)
4. Verify the notification message and, if the job was submitted successfully, select the **Success!** or **File is ready! Click here to download** link.

    ![Screenshot of the Bulk operations page showing a completed Download devices job with a File is ready link to download the CSV.](media/bulk-operations/all-devices-bulk-operations-result.png)
5. Select the filename for the bulk job you created to download the CSV file. Verify the CSV contains all devices with the columns you selected when the bulk job was created.

You can bulk export users following the steps in [Download a list of users in Microsoft Entra admin center](../identity/users/users-bulk-download).

## Add users to an administrative unit in a bulk operation

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as at least a [Privileged Role Administrator](../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins** &gt; **Admin units**.
3. Select the administrative unit you want to add users to.
4. Select **Users** &gt; **Bulk operations** &gt; **Bulk add members**.

    ![Screenshot of the Users page for assigning users to an administrative unit as a bulk operation.](media/bulk-operations/admin-unit-bulk-add-members.png)
5. In the **Bulk add members** pane, download the comma-separated values (CSV) template. Update and format the CSV as follows:

    Entries: Object Ids or UPN of members to add to the Admin Unit. Rename the file if desired, then select and upload the edited file.
6. Select **Submit** after successful upload.

    ![Screenshot of the bulk add members submission screen.](media/bulk-operations/admin-unit-submit-upload.png)
7. Verify the notification message and ensure the job was submitted successfully.

    ![Screenshot of success notification for bulk add members operation.](media/bulk-operations/admin-unit-success-notification.png)
8. Select **Success** to navigate to the bulk jobs list. You can sort by creation time to find your job, then select it to download.

    ![Screenshot of the bulk jobs list showing the completed operation.](media/bulk-operations/admin-unit-bulk-jobs-list.png)

    ![Screenshot of downloading the bulk operation results.](media/bulk-operations/admin-unit-download-results.png)

Note

Verify that the correct object IDs were added to the admin unit successfully. Refresh the UX if needed to see the updated state; it takes some time to reflect especially when adding groups to Admin Unit.

If the input includes an invalid Object ID or one already assigned to this admin unit, the bulk operation status shows "Failed" instead of "Success" due to not all rows successfully processed. In the results csv, you will see the failure reason as 'The request was malformed or contains invalid parameters'. This is most likely due to the object being already assigned to this admin unit pre-operation. Other valid rows should still be processed successfully, please verify accordingly.

## Remove users from an administrative unit in a bulk operation

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as at least a [Privileged Role Administrator](../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins** &gt; **Admin units**.
3. Select the administrative unit that you want to remove users from.
4. Select **Users** &gt; **Bulk operations** &gt; **Bulk remove members**.

    ![Screenshot of Users page that shows the Bulk remove members link.](media/bulk-operations/admin-unit-bulk-remove-members.png)
5. In the **Bulk remove members** pane, download the comma-separated values (CSV) template.
6. Don't change the first row of the template, and for each row fill in objectID or UPN of the users/devices/groups that you want to remove.
7. Save your changes and upload the CSV file.
8. Select **Submit**.

## Download Role Assignment

To download all active role assignments across all roles, including built-in and custom roles, follow these steps.

1. On the **Roles and administrators** page, select **All roles**.
2. Select **Download assignments**.
3. Select **Success** to navigate to the bulk jobs list. You can sort by creation time to find your job, then select it to download.

    ![Screenshot of bulk jobs list for role assignment download.](media/bulk-operations/role-assignment-bulk-jobs-list.png)

    ![Screenshot of downloading role assignment results.](media/bulk-operations/role-assignment-download-results.png)
4. Sample output:

    ![Screenshot of sample role assignment CSV output.](media/bulk-operations/role-assignment-sample-output.png)

Note

Filters and sorting are **not** supported for this bulk job type; this downloads all role assignments.