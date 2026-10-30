---
layout: Conceptual
title: Bulk invite B2B users - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/tutorial-bulk-invite
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to bulk invite B2B collaboration users in Microsoft Entra External ID. Follow the steps to prepare a CSV file, upload it, and verify guest users in the directory.
ms.topic: tutorial
ms.date: 2026-03-27T00:00:00.0000000Z
ai-usage: ai-assisted
ms.collection: M365-identity-device-management
ms.custom: sfi-image-nochange
locale: en-us
document_id: 704378b4-148f-49a9-3b18-fad694da0dc7
document_version_independent_id: db6f6680-22ef-fc80-4914-e72ff27820ad
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/tutorial-bulk-invite.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/tutorial-bulk-invite
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/tutorial-bulk-invite.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8d07c4a6-f258-2d20-f054-452538405ca5
---

# Bulk invite B2B users - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

If you use Microsoft Entra B2B collaboration to work with external partners, you can invite multiple guest users to your organization at the same time. In this tutorial, you learn how to use the Microsoft Entra admin center to send bulk invitations to external users. Specifically, you follow these steps:

- Use **Bulk invite users** to prepare a comma-separated value (.csv) file with the user information and invitation preferences
- Upload the .csv file to Microsoft Entra ID
- Verify the users were added to the directory

## Prerequisites

- If you don’t have Microsoft Entra ID, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.
- You need two or more test email accounts that you can send the invitations to. The accounts must be from outside your organization. You can use any type of account, including social accounts such as gmail.com or outlook.com addresses.

## Invite guest users in bulk

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **Bulk operations** &gt; **Bulk invite**.

    ![Screenshot of the bulk invite button.](media/tutorial-bulk-invite/bulk-invite-button.png)
4. On the **Bulk invite users** page, select **Download** to get a [valid .csv template](tutorial-bulk-invite#understand-the-csv-template) with invitation properties.

    ![Screenshot of the download the csv file button.](media/tutorial-bulk-invite/download-button.png)
5. Open the .csv template and add a line for each guest user. Required values are:

    - **Email address to invite** - the user to whom you want to send an invitation.
    - **Redirection url** - the URL to which the invited user is forwarded after accepting the invitation. If you want to forward the user to the My Apps page, you must change this value to https://myapps.microsoft.com or https://myapplications.microsoft.com.

    ![Screenshot of the example csv file with guest users entered.](media/tutorial-bulk-invite/bulk-invite-csv.png)

    Note

    Don't use commas in the **Customized invitation message** because they'll prevent the message from being parsed successfully.
6. Save the file.
7. On the **Bulk invite users** page, under **Upload your csv file**, browse to the file. When you select the file, validation of the .csv file starts.
8. When the file contents are validated, **File uploaded successfully** appears. If there are errors, you must fix them before you can submit the job.
9. When your file passes validation, select **Submit** to start the Azure bulk operation that adds the invitations.
10. To view the job status, select **Click here to view the status of each operation**. Or, you can select **Bulk operation results** in the **Activity** section. For details about each line item within the bulk operation, select the values under the **# Success**, **# Failure**, or **Total Requests** columns. If failures occurred, the reasons for failure are listed.

    [![Screenshot of the bulk operation results.](media/tutorial-bulk-invite/bulk-operation-results.png)](media/tutorial-bulk-invite/bulk-operation-results.png#lightbox)
11. When the job completes, a notification appears indicating that the bulk operation succeeded.

## Understand the CSV template

A template is available to help you invite Microsoft Entra guest users in bulk. Download and fill in the bulk upload CSV template, which looks something like this example:

![Screenshot of a spreadsheet with callouts explaining the purpose and values for each row and column.](media/tutorial-bulk-invite/understand-template.png)

### CSV template structure

The rows in a downloaded CSV template are as follows:

- **Version number**: The first row containing the version number must be included in the upload CSV.
- **Column headings**: The format of the column headings is &lt;*Item name*&gt; [PropertyName] &lt;*Required or blank*&gt;. For example, `Email address to invite [inviteeEmail] Required`. Some older versions of the template might have slight variations.
- **Examples row**: The template includes a row of sample values for each column. Remove the examples row and replace it with your own entries.

### Further guidance

- The first two rows of the upload template must not be removed or modified, or the upload can't be processed.
- The required columns are listed first.
- We don't recommend adding new columns to the template. Any columns you add are ignored and not processed.
- We recommend that you download the latest version of the CSV template as often as possible.

## Verify guest users in the directory

Check to see that the guest users you added exist in the directory either in the Microsoft Entra admin center or by using PowerShell.

### View guest users in the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Under **Show**, select **Guest users only** and verify the users you added are listed.

### View guest users with PowerShell

To view guest users with PowerShell, you need the [`Microsoft.Graph.Users` PowerShell module](/en-us/powershell/module/microsoft.graph.users/?view=graph-powershell-1.0&amp;viewFallbackFrom=graph-powershell-beta&amp;preserve-view=true). Then sign in using the `Connect-MgGraph` command with an admin account to consent to the required scopes:

```powershell
Connect-MgGraph -Scopes "User.Read.All"
```

Run the following command:

```powershell
 Get-MgUser -Filter "UserType eq 'Guest'"
```

You should see the users that you invited listed, with a user principal name (UPN) in the format *emailaddress*#EXT#@*domain*. For example, *lstokes\_fabrikam.com#EXT#@contoso.onmicrosoft.com*, where contoso.onmicrosoft.com is the organization from which you sent the invitations.

## Clean up resources

When no longer needed, you can delete the test user accounts in the directory in the Microsoft Entra admin center on the Users page by selecting the checkbox next to the guest user and then selecting **Delete**.

Or you can run the following PowerShell command to delete a user account:

```powershell
 Remove-MgUser -UserId "<UPN>"
```

For example: `Remove-MgUser -UserId "lstokes_fabrikam.com#EXT#@contoso.onmicrosoft.com"`