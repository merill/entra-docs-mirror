---
layout: Conceptual
title: Tutorial for bulk inviting B2B collaboration users - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/bulk-invite-powershell
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: In this tutorial, you learn how to use PowerShell and a CSV file to send bulk invitations to external Microsoft Entra B2B collaboration guest users.
ms.topic: tutorial
ms.date: 2025-03-13T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
locale: en-us
document_id: 8984951b-7ece-4964-ed6e-5266174d2ffb
document_version_independent_id: 163b743d-fd7f-9c50-f01c-79a4521c5236
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/bulk-invite-powershell.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/bulk-invite-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/bulk-invite-powershell.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ba3b51b2-721a-b0f9-fe60-8097039714b7
---

# Tutorial for bulk inviting B2B collaboration users - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

If you use Microsoft Entra B2B collaboration to work with external partners, you can invite multiple guest users to your organization at the same time via the portal or PowerShell. In this tutorial, you learn how to use PowerShell to send bulk invitations to external users. Specifically, you do the following:

- Prepare a comma-separated value (.csv) file with the user information
- Run a PowerShell script to send invitations
- Verify the users are added to the directory

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

### Install the latest Microsoft Graph PowerShell module

Make sure you install the latest version of the Microsoft Graph PowerShell module.

First, check which modules you've installed. Open PowerShell as an elevated user (run as administrator), and run the following command:

```powershell
Get-InstalledModule Microsoft.Graph
```

To install the v1 module of the SDK in PowerShell Core or Windows PowerShell, run this command:

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```

Optionally, change the scope of the installation using the `-Scope` parameter. This requires admin permissions.

```powershell
Install-Module Microsoft.Graph -Scope AllUsers
```

To install the beta module, run this command.

```powershell
Install-Module Microsoft.Graph.Beta
```

You might receive a prompt that you're installing the module from an untrusted repository. This occurs if you haven't previously set the PSGallery repository as a trusted repository. Press `Y` to install the module.

### Get test email accounts

You need two or more test email accounts to send the invitations to. The accounts must be from outside your organization. You can use any type of account, including social accounts such as `gmail.com` or `outlook.com` addresses.

## Prepare the CSV file

In Microsoft Excel, create a CSV file with the list of invitee usernames and email addresses. Make sure to include the **Name** and **InvitedUserEmailAddress** column headings.

For example, create a worksheet in the following format:

![Screenshot that shows the csv file columns of Name and InvitedUserEmailAddress.](media/tutorial-bulk-invite/addusersexcel.png)

Save the file as **C:\BulkInvite\Invitations.csv**.

If you don't have Excel, create a CSV file in any text editor, such as Notepad. Separate each value with a comma, and each row with a new line.

## Sign in to your tenant

Run the following command to connect to the tenant:

```powershell
Connect-MgGraph -TenantId "<YOUR_TENANT_ID>"
```

For example, `Connect-MgGraph -TenantId "aaaabbbb-0000-cccc-1111-dddd2222eeee"`. You can also use the tenant domain, but the parameter remains the `-TenantId`. For example, `Connect-MgGraph -TenantId "contoso.onmicrosoft.com"`.

When prompted, enter your credentials.

## Send bulk invitations

To send the invitations, run the following PowerShell script (where \* \* *c:\bulkinvite\invitations.csv* is the path of the CSV file):

```powershell
$invitations = import-csv c:\bulkinvite\invitations.csv

$messageInfo = New-Object Microsoft.Graph.PowerShell.Models.MicrosoftGraphInvitedUserMessageInfo

$messageInfo.customizedMessageBody = "Hello. You are invited to the Contoso organization."

foreach ($email in $invitations) {New-MgInvitation ` 
      -InvitedUserEmailAddress $email.InvitedUserEmailAddress `	-InvitedUserDisplayName $email.Name `	-InviteRedirectUrl https://myapplications.microsoft.com/?tenantid=aaaabbbb-0000-cccc-1111-dddd2222eeee `	-InvitedUserMessageInfo $messageInfo `	-SendInvitationMessage
}
```

The script sends an invitation to the email addresses in the *invitations.csv* file. You see output similar to the following for each user:

![Screenshot that shows PowerShell output that includes pending user acceptance.](media/tutorial-bulk-invite/b2bbulkimport.png)

## Verify users exist in the directory

To verify that the invited users were added to Microsoft Entra ID, run the following command:

```powershell
 Get-MgUser -Filter "UserType eq 'Guest'"
```

You should see the users that you invited listed, with a user principal name (UPN) in the format *emailaddress*#EXT#@*domain*. For example, *msullivan\_fabrikam.com#EXT#@contoso.onmicrosoft.com*, where `contoso.onmicrosoft.com` is the organization from which you sent the invitations.

## Clean up resources

When no longer needed, you can delete the test user accounts in the directory. Run the following command to delete a user account:

```powershell
 Remove-MgUser -UserId "<String>"
```

For example: `Remove-MgUser -UserId "00aa00aa-bb11-cc22-dd33-44ee44ee44ee"`