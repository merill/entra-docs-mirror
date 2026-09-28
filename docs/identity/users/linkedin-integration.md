---
layout: Conceptual
title: Admin consent for LinkedIn account connections - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/linkedin-integration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Explains how to enable or disable LinkedIn integration account connections in Microsoft apps in Microsoft Entra ID
ms.topic: how-to
ms.date: 2024-12-13T00:00:00.0000000Z
ms.reviewer: beengen
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-ga-nochange
ms.collection: M365-identity-device-management
locale: en-us
document_id: 22b21ab5-ea75-2f79-f497-4dfd2235fa52
document_version_independent_id: a05c8fd9-f1fb-f860-678e-61445886daf8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/linkedin-integration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/linkedin-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/linkedin-integration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/aec7dc3e-0dad-4b82-accf-63218d8767d5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f260444a-7ec6-4768-8e41-ad2438092724
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 162322b3-6c6d-97fd-4dd9-635b247f1f83
---

# Admin consent for LinkedIn account connections - Microsoft Entra ID | Microsoft Learn

## Overview

You can allow users in your organization to access their LinkedIn connections within some Microsoft apps. No data is shared until users consent to connect their accounts. You can integrate your organization with Microsoft Entra ID, part of Microsoft Entra.

Important

The LinkedIn account connections setting is currently being rolled out to Microsoft Entra organizations. When it's rolled out to your organization, it's enabled by default.

Exceptions:

- The setting isn't available for customers using Microsoft Cloud for US Government, Microsoft Cloud Germany, or Azure and Microsoft 365 operated by 21Vianet in China.
- The setting is off by default for Microsoft Entra organizations provisioned in Germany. Note that the setting isn't available for customers using Microsoft Cloud Germany.
- The setting is off by default for organizations provisioned in France.

Once LinkedIn account connections are enabled for your organization, the account connections work after users consent to apps accessing company data on their behalf. For information about the user consent setting, see [How to remove a user's access to an application](../enterprise-apps/methods-for-removing-user-access).

## Enable LinkedIn account connections in the Azure portal

You can enable LinkedIn account connections for only the users you want to have access, from your entire organization to only selected users in your organization.

Important

Microsoft recommends that you use roles with the fewest permissions. This practice helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios or when you can't use an existing role.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
2. Select Microsoft Entra ID.
3. Select **Users** &gt; **All users**.
4. Select **User settings**.
5. Under **LinkedIn account connections**, allow users to connect their accounts to access their LinkedIn connections within some Microsoft apps. No data is shared until users consent to connect their accounts.

    - Select **Yes** to enable the service for all users in your organization.
    - Select **Selected group** to enable the service for only a group of selected users in your organization.
    - Select **No** to withdraw consent from all users in your organization.

    ![Screenshot of integrating LinkedIn account connections in the organization.](media/linkedin-integration/linkedin-integration.png)
6. When you're done, select **Save** to save your settings.

Important

While LinkedIn integration isn't fully enabled until your users consent to connect their accounts, access to public LinkedIn profile information is available without requiring individual consent. Full integration (two-way consent and additional fields) isn't enabled without each user's consent. Your users can see the available LinkedIn profile of anyone that matches the name searched, regardless of whether that match is in the same enabled group or not.

### Assign selected users by using a group

The 'Selected' option that specifies a list of users was replaced with the option to select a group of users so that you can enable the ability to connect LinkedIn and Microsoft accounts for a single group instead of many individual users. If you don't have LinkedIn account connections enabled for selected individual users, you don't need to do anything. If you have previously enabled LinkedIn account connections for selected individual users, you should:

1. Get the current list of individual users.
2. Move the currently enabled individual users to a group.
3. Use the group from the previous as the selected group in the LinkedIn account connections setting in the Azure portal.

Note

Even if you don't move your currently selected individual users to a group, they can still see LinkedIn information in Microsoft apps.

### Move selected users to a group

1. Create a CSV file of the users who are selected for LinkedIn account connections.
2. Sign in to Microsoft 365 with your administrator account.
3. Launch PowerShell.
4. Install the Microsoft Graph PowerShell module by running `Install-Module Microsoft.Graph -Scope CurrentUser`.
5. Run the following script:

    ```PowerShell
    $groupId = "GUID of the target group"
    
    $users = Get-Content
    Path to the CSV file
    
    $i = 1
    foreach($user in $users) { 
      New-MgGroupMember -GroupId "$groupId" -DirectoryObjectId "$user" ;
      Write-Host $i Added $user ; $i++ ;
      Start-Sleep -Milliseconds 10
    }
    ```

To use the group from step two as the selected group in the LinkedIn account connections setting in the Azure portal, see Enable LinkedIn account connections in the Azure portal.

## Use Group Policy to enable LinkedIn account connections

1. Download the [Office 2016 Administrative Template files (ADMX/ADML)](https://www.microsoft.com/download/details.aspx?id=49030).
2. Extract the **ADMX** files and copy them to your central store.
3. Open Group Policy Management.
4. Create a Group Policy Object with the following setting: **User Configuration** &gt; **Administrative Templates** &gt; **Microsoft Office 2016** &gt; **Miscellaneous** &gt; **Show LinkedIn features in Office applications**.
5. Select **Enabled** or **Disabled**.

    | State | Effect |
    | --- | --- |
    | **Enabled** | The **Show LinkedIn features in Office applications** setting in Office 2016 Options is enabled. Users in your organization can use LinkedIn features in their Office 2016 applications. |
    | **Disabled** | The **Show LinkedIn features in Office applications** setting in Office 2016 Options is disabled and end users can't change this setting. Users in your organization can't use LinkedIn features in their Office 2016 applications. |

This group policy affects only Office 2016 apps for a local computer. If users disable LinkedIn in their Office 2016 apps, they can still see LinkedIn features in Microsoft 365.