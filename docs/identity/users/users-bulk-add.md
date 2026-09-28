---
layout: Conceptual
title: Bulk create users in the Azure portal - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/users-bulk-add
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Add users in bulk in Microsoft Entra ID
ms.date: 2026-04-02T00:00:00.0000000Z
ms.topic: how-to
ms.custom: it-pro, sfi-image-nochange
ms.reviewer: jeffsta
locale: en-us
document_id: 277a5d8f-7fce-bf5d-1ebd-2061e9ac8a69
document_version_independent_id: 02d2bc44-dc9f-a23a-9c60-facf7e0c1a41
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/users-bulk-add.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/users-bulk-add
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/users-bulk-add.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ee0c852c-0a39-004e-1043-dcfed8cc8cd3
---

# Bulk create users in the Azure portal - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra ID, part of Microsoft Entra, supports bulk user create and delete operations and supports downloading lists of users. Just fill out the comma-separated values (CSV) template you can download from Microsoft Entra ID.

## Required permissions

In order to bulk create users in the administration portal, you must be signed in as at least a User Administrator.

## Understand the CSV template

Download and fill in the bulk upload CSV template to help you successfully create Microsoft Entra users in bulk. The CSV template you download might look like this example:

![Screenshot of spreadsheet for upload and call-outs explaining the purpose and values for each row and column.](media/users-bulk-add/create-template-example.png)

Warning

If you're adding only one entry using the CSV template, you must preserve row 3 and add your new entry to row 4.

Ensure that you add the `.csv` file extension and remove any leading spaces before `userPrincipalName`, `passwordProfile`, and `accountEnabled`.

### CSV template structure

The rows in a downloaded CSV template are as follows:

- **Version number**: The first row containing the version number (for example, `version:v1.0`) must be included in the upload CSV. If your downloaded template includes this row, don't remove or modify it.
- **Column headings**: The format of the column headings is &lt;*Item name*&gt; [PropertyName] &lt;*Required or blank*&gt;. For example, `Name [displayName] Required`. Some older versions of the template might have slight variations.
- **Examples row**: The template might include a row of example values for each column. You must remove the examples row and replace it with your own entries.

Note

CSV template formats vary by operation. Some templates, such as bulk create or delete users, include `version:v1.0` as the first row. Other templates, such as group member operations, start with column headers. Download the template for your specific operation from the portal. Don't add a version row or any other row that isn't in the downloaded template. Keep any version row and column header row unchanged.

### Additional guidance

- Keep any version row and column header row in the upload template exactly as downloaded, or the upload can't be processed.
- The required columns are listed first.
- We don't recommend adding new columns to the template. Any additional columns you add are ignored and not processed.
- We recommend that you download the latest version of the CSV template as often as possible.

- Make sure to check there is no unintended whitespace before/after any field. For **User principal name**, having such whitespace would cause import failure.
- Ensure that values in **Initial password** comply with the currently active [password policy](../authentication/concept-sspr-policy#username-policies).
- Enter one user per row.

### Example CSV file

Here's an example of a completed CSV file ready for upload:

```csv
version:v1.0
Name [displayName] Required,User name [userPrincipalName] Required,Initial password [passwordProfile] Required,Block sign in (Yes/No) [accountEnabled] Required,First name [givenName],Last name [surname],Job title [jobTitle],Department [department],Usage location [usageLocation],Street address [streetAddress],State or province [state],Country or region [country],Office [physicalDeliveryOfficeName],City [city],ZIP or postal code [postalCode],Office phone [telephoneNumber],Mobile phone [mobile]
Alain Charon,alain@contoso.com,Password1!,No,Alain,Charon,Software Engineer,Engineering,US,,,,,,,
Isabella Simonsen,isabella@contoso.com,Password1!,No,Isabella,Simonsen,Product Manager,Product,US,,,,,,,
Joseph Price,joseph@contoso.com,Password1!,No,Joseph,Price,Sales Representative,Sales,US,,,,,,,
```

Important

Only the first four columns are required: **Name**, **User name**, **Initial password**, and **Block sign in**. All other columns are optional and can be left empty.

## To create users in bulk

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users** &gt; **Bulk create**.
3. On the **Bulk create user** page, select **Download** to receive a valid comma-separated values (CSV) file of user properties, and then add users you want to create.

    ![Screenshot showing how to select a local CSV file in which you list the users you want to add.](media/users-bulk-add/upload-button.png)
4. Open the CSV file and add a line for each user you want to create. The only required values are **Name**, **User principal name**, **Initial password**, and **Block sign in (Yes/No)**. Then save the file.

    ![Screenshot showing an example of the CSV file containing the names and IDs of the users to create.](media/users-bulk-add/add-csv-file.png)
5. On the **Bulk create user** page, under Upload your CSV file, browse to the file. When you select the file and select **Submit**, validation of the CSV file starts.
6. After the file contents are validated, you’ll see **File uploaded successfully**. If there are errors, you must fix them before you can submit the job.
7. When your file passes validation, select **Submit** to start the bulk operation that imports the new users.
8. When the import operation completes, you see a notification of the bulk operation job status.

Note

The bulk create operation creates internal member accounts with the passwords specified in the CSV file. No invitation emails are sent to the new users. You must communicate the sign-in credentials to the users through your own process. To bulk invite external guest users and send invitation emails, see [Bulk invite B2B users](../../external-id/tutorial-bulk-invite).

If you experience errors, you can download and view the results file on the **Bulk operation results** page. The file contains the reason for each error. The file submission must match the provided template and include the exact column names.

For more information about bulk operations limitations, see Bulk import service limits.

## Check status

You can see the status of all of your pending bulk requests in the **Bulk operation results** page.

![Screenshot showing how to check the status of the operation in the bulk operations results page.](media/users-bulk-add/bulk-center.png)

Next, you can check to see that the users you created exist in the Microsoft Entra organization either in the Microsoft Entra admin center or by using PowerShell.

## Verify users

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Select Microsoft Entra ID.
3. Select **Users** &gt; **All users**.
4. Under **Show**, select **All users** and verify that the users you created are listed.

### Verify users with PowerShell

Run the following command:

```PowerShell
Get-MgUser -Filter "UserType eq 'Member'"
```

You should see that the users that you created are listed.

## Bulk import service limits

Note

When performing bulk operations, such as import or create, you can encounter a problem if the bulk operation doesn't complete within the hour. To work around this issue, we recommend splitting the number of records processed per batch. For example, before starting an export you could limit the result set by filtering on a group type or user name to reduce the size of the results. By refining your filters, essentially you limit the data returned by the bulk operation. For more information, see [Bulk operations service limitations](../../fundamentals/bulk-operations-service-limitations).