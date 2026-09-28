---
layout: Conceptual
title: 'Quickstart: Add a guest user with PowerShell - Microsoft Entra External ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/b2b-quickstart-invite-powershell
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: In this quickstart, you learn how to use PowerShell to send an invitation to a Microsoft Entra B2B collaboration user. You'll use the Microsoft Graph Identity Sign-ins and the Microsoft Graph Users PowerShell modules.
ms.date: 2026-04-17T00:00:00.0000000Z
ms.topic: quickstart
ms.custom: it-pro, mode-api, has-azure-ad-ps-ref, azure-ad-ref-level-one-done
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
locale: en-us
document_id: c7ea676e-0678-9e2d-e009-fb44587f93dd
document_version_independent_id: 40b581da-26ea-2890-4a78-54b29f5dc610
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/b2b-quickstart-invite-powershell.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/b2b-quickstart-invite-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/b2b-quickstart-invite-powershell.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 5f88a60d-a327-5857-c6a2-afbcb633a76d
---

# Quickstart: Add a guest user with PowerShell - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

There are many ways to invite external partners to your apps and services with Microsoft Entra B2B collaboration. In the previous quickstart, you saw how to add guest users directly in the Microsoft Entra admin center. You can also use PowerShell to add guest users, either one at a time or in bulk. In this quickstart, you use the `New-MgInvitation` command to add one guest user to your Microsoft Entra tenant.

This article explains how to invite guest users with Microsoft Graph PowerShell. You can also manage guest users with [Microsoft Entra PowerShell](/en-us/powershell/entra-powershell/manage-guest-users).

## Prerequisites

To complete the scenario in this quickstart, you need:

- An Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.
- A role that allows you to create users in your tenant directory, such as at least a [Guest Inviter role](../identity/role-based-access-control/permissions-reference#guest-inviter) or a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
- Install the [Microsoft Graph Identity Sign-ins module](/en-us/powershell/module/microsoft.graph.identity.signins/?viewFallbackFrom=graph-powershell-beta&amp;preserve-view=true&amp;view=graph-powershell-1.0) (Microsoft.Graph.Identity.SignIns) and the [Microsoft Graph Users module](/en-us/powershell/module/microsoft.graph.users/?viewFallbackFrom=graph-powershell-beta&amp;preserve-view=true&amp;view=graph-powershell-1.0) (Microsoft.Graph.Users). You can use the `#Requires` statement to prevent running a script unless the required PowerShell modules are met.

```powershell
#Requires -Modules Microsoft.Graph.Identity.SignIns, Microsoft.Graph.Users
```

- Get a test email account. You need a test email account that you can send the invitation to. The account must be from outside your organization. You can use any type of account, including a social account such as a Gmail.com or Outlook.com address.

Note

This article uses Microsoft Graph PowerShell, which replaces the retired Azure AD and MSOnline PowerShell modules.

## Sign in to your tenant

Run the following command to connect to your tenant:

```powershell
Connect-MgGraph -Scopes 'User.Invite.All','User.Read.All'
```

When prompted, enter your credentials.

## Send an invitation

1. To send an invitation to your test email account, run the following PowerShell command (replace **"Henry Ross"** and **henry@contoso.com** with your test email account name and email address):

    ```powershell
    New-MgInvitation -InvitedUserDisplayName "Henry Ross" -InvitedUserEmailAddress henry@contoso.com -InviteRedirectUrl "https://myapplications.microsoft.com" -SendInvitationMessage:$true
    ```
2. The command sends an invitation to the email address specified. Check the output, which should look similar to the following example:

    ```Output
    Id                                   InviteRedeemUrl                                                                                                   
    --                                   ---------------                                                                                                   
    00aa00aa-bb11-cc22-dd33-44ee44ee44ee https://login.microsoftonline.com/redeem?...
    ```

## Verify the user exists in the directory

1. To verify that the invited user was added to Microsoft Entra ID, run the following command (replace **henry@contoso.com** with your invited email):

    ```powershell
    Get-MgUser -Filter "Mail eq 'henry@contoso.com'"
    ```
2. Check the output to make sure the user you invited is listed, with a user principal name (UPN) in the format *emailaddress*#EXT#@*domain*. For example, *henry\_contoso.com#EXT#@fabrikam.onmicrosoft.com*, where fabrikam.onmicrosoft.com is the organization from which you sent the invitations.

    ```Output
    Id                                   DisplayName              Mail                           UserPrincipalName        
    --                                   -----------              ----                           -----------------               
    00aa00aa-bb11-cc22-dd33-44ee44ee44ee Henry Ross               henry@contoso.com              henry_contoso.com#EXT#@fabrikam.onmicrosoft.com
    ```

## Clean up resources

When no longer needed, you can delete the test user account in the directory. Run the following command to delete a user account:

```powershell
Remove-MgUser -UserId '<String>'
```

For example:

```powershell
Remove-MgUser -UserId 'henry_contoso.com#EXT#@fabrikam.onmicrosoft.com'
```

Or

```powershell
Remove-MgUser -UserId '00aa00aa-bb11-cc22-dd33-44ee44ee44ee'
```