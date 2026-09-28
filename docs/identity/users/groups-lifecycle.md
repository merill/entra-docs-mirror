---
layout: Conceptual
title: Set expiration for Microsoft 365 groups - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-lifecycle
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how to set up expiration for Microsoft 365 groups in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-01-15T00:00:00.0000000Z
ms.reviewer: jodah
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
locale: en-us
document_id: ee217532-6b64-61f7-d965-bc95d9198cdb
document_version_independent_id: f6bab9a9-1b8b-01db-6e42-045eb04efe9e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-lifecycle.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-lifecycle
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-lifecycle.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ed32568c-40fc-ed14-026b-623924df2b09
---

# Set expiration for Microsoft 365 groups - Microsoft Entra ID | Microsoft Learn

## Overview

This article tells you how to manage the lifecycle of Microsoft 365 groups by setting an expiration policy for them. You can set an expiration policy only for Microsoft 365 groups in Microsoft Entra ID.

After you set a group to expire:

- Groups with user activities are automatically renewed as the expiration nears.
- Owners of the group are notified to renew the group, if the group isn't autorenewed.
- Any group that isn't renewed is deleted.
- Any Microsoft 365 group that was deleted can be restored within 30 days by the group owners or the administrator.

Currently, you can configure only one expiration policy for all Microsoft 365 groups in a Microsoft Entra organization.

Note

Configuring and using the expiration policy for Microsoft 365 groups requires you to possess but not necessarily assign Microsoft Entra ID P1 or P2 licenses for the members of all groups to which the expiration policy is applied.

For information on how to download and install Microsoft Graph PowerShell cmdlets, see [Install the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation).

Note

Azure AD and MSOnline PowerShell modules are deprecated as of March 30, 2024. To learn more, read the [deprecation update](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270). After this date, support for these modules are limited to migration assistance to Microsoft Graph PowerShell SDK and security fixes. The deprecated modules will continue to function through March, 30 2025.

We recommend migrating to [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/overview) to interact with Microsoft Entra ID (formerly Azure AD). For common migration questions, refer to the [Migration FAQ](/en-us/powershell/azure/active-directory/migration-faq). *Note:* Versions 1.0.x of MSOnline may experience disruption after June 30, 2024.

## Activity-based automatic renewal

With Microsoft Entra intelligence, groups are now automatically renewed based on whether they were recently used. This feature eliminates the need for manual action by group owners. It's based on user activity in groups across Microsoft 365 services like Outlook, SharePoint, Teams, or Viva Engage.

For example, an owner or a group member might do something like:

- Send an email to the group in Outlook.
- Upload a document to SharePoint.
- Visit a Teams channel.
- View a post in Viva Engage.

In the preceding scenarios, the group is automatically renewed around 35 days before the group expires and the owner doesn't get any renewal notifications.

Now consider an expiration policy that was set so that a group expires after 30 days of inactivity. To keep from sending an expiration email the day that group expiration is enabled (because there's no record activity yet), Microsoft Entra first waits five days. Then:

- If there's activity in those five days, the expiration policy works as expected.
- If there's no activity within five days, Microsoft Entra ID sends an expiration or renewal email.
- If the group was inactive for five days, an email was sent, and then the group was active, Microsoft Entra autorenews it and starts the expiration period again.

### Activities that automatically renew group expiration

The following user actions cause automatic group renewal:

- **SharePoint**: View, edit, download, move, share, or upload files.
- **Outlook**: Join a group, read or write a group message from a group space, or "like" a message (in Outlook Web Access).
- **Teams**: Visit a Teams channel.
- **Viva Engage**: View a post within a Viva Engage community or an interactive email in Outlook.

### Audit and report

Administrators can get a list of automatically renewed groups from the activity audit logs in Microsoft Entra ID.

![Screenshot that shows automatic renewal of groups based on activity.](media/groups-lifecycle/audit-logs-autorenew-group.png)

## Roles and permissions

The following roles can configure and use expiration for Microsoft 365 groups in Microsoft Entra ID.

| Role | Permissions |
| --- | --- |
| Groups Administrator, or User Administrator | Can create, read, update, or delete the Microsoft 365 groups expiration policy settingsCan renew any Microsoft 365 group |
| User | Can renew a Microsoft 365 group that they ownCan restore a Microsoft 365 group that they ownCan read the expiration policy settings |

For more information on permissions to restore a deleted group, see [Restore a deleted Microsoft 365 group in Microsoft Entra ID](groups-restore-deleted).

## Set group expiration

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Select **Identity**.
3. Select **Groups** &gt; **All groups**, and then select **Expiration** to open the expiration settings.

    ![Screenshot that shows expiration settings for groups.](media/groups-lifecycle/expiration-settings.png)
4. On the **Expiration** page, you can:

    - Set the group lifetime in days. You can select one of the preset values or a custom value. It should be 30 days or more.
    - Specify an email address where the renewal and expiration notifications are sent when a group has no owner.
    - Select which Microsoft 365 groups expire. You can set expiration for:
        - **All** Microsoft 365 groups.
        - **Selected** Microsoft 365 groups.
        - **None** to restrict expiration for all groups.
    - Save your settings when you're done by selecting **Save**.

    Note

    - When you first set up expiration, any groups that are older than the expiration interval are set to 35 days until expiration unless the group is automatically renewed or the owner renews it.
    - When a dynamic group is deleted and restored, it's seen as a new group and repopulated according to the rule. This process can take up to 24 hours.
    - Expiration notices for groups used in Teams appear in the Teams Owners feed.
    - When you enable expiration for selected groups, you can add up to 500 groups to the list. If you need to add more than 500 groups, you can enable expiration for all your groups. In that scenario, the 500-group limitation doesn't apply.
    - Groups don't renew immediately when auto-renew activities occur. In the event of an activity, a flag is placed on the group to indicate it's ready for renewal when it's near expiry. If the group is near expiry, renewal occurs within 24 hours.

## Email notifications

If groups aren't automatically renewed, email notifications like the following example are sent to the Microsoft 365 group owners 30 days, 15 days, and 1 day before group expiration.

The groups owner's preferred language or the Microsoft Entra language setting determines the language of the email. If the group owner defined a preferred language, or multiple owners have the same preferred language, that language is used. For all other cases, the Microsoft Entra language setting is used.

![Screenshot that shows expiration email notifications.](media/groups-lifecycle/expiration-notification.png)

From the **Renew group** notification email, group owners can directly access the group details page in the [Access Panel](https://account.activedirectory.windowsazure.com/r#/applications). There, users can get more information about the group, such as its description, when it was last renewed, when it expires, and also the ability to renew the group. The group details page now also includes links to the Microsoft 365 group resources so that the group owner can conveniently view the content and activity in their group.

Important

If there's any problem with the notification emails and they aren't sent out or they're delayed, be assured that Microsoft never deletes a group before the last email is sent.

When a group expires, the group is deleted one day after the expiration date. An email notification such as this one is sent to the Microsoft 365 group owners informing them about the expiration and subsequent deletion of their Microsoft 365 group.

![Screenshot that shows group deletion email notifications.](media/groups-lifecycle/deletion-notification.png)

You can restore the group within 30 days of its deletion by selecting **Restore group** or by using PowerShell cmdlets. For more information, see [Restore a deleted Microsoft 365 group in Microsoft Entra ID](groups-restore-deleted). The 30-day group restoration period isn't customizable.

If the group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up to 24 hours to fully restore the group and its contents.

## Retrieve the Microsoft 365 group expiration date

In addition to using Access Panel to view group details like expiration date and last renewed date, you can retrieve the expiration date of a Microsoft 365 group from Microsoft Graph REST API Beta. The group property `expirationDateTime` is enabled in Microsoft Graph Beta. You can retrieve it with a GET request. For more information, see [this example](/en-us/graph/api/group-get?view=graph-rest-beta&amp;preserve-view=true#example).

Note

To manage group memberships on the Access Panel, **Restrict access to Groups in Access Panel** must be set to **No** in the Microsoft Entra groups **General** setting.

## Microsoft 365 group expiration with a mailbox on legal hold

When a group expires and is deleted, 30 days after deletion the group's data from apps like Planner, Sites, or Teams is permanently deleted. The group mailbox that's on legal hold is retained and isn't permanently deleted. The administrator can use Exchange cmdlets to restore the mailbox to fetch the data.

## Microsoft 365 group expiration with a retention policy

You can configure the retention policy in the Security & Compliance portal. There you can set up a retention policy for Microsoft 365 groups. When a group expires and is deleted, the group conversations in the group mailbox and files in the group site are retained in the retention container for the specific number of days defined in the retention policy. Users won't see the group or its content after expiration. They can recover the site and mailbox data via e-discovery.

## PowerShell examples

Here are examples of how you can use PowerShell cmdlets to configure the expiration settings for Microsoft 365 groups in your Microsoft Entra organization:

1. Install the Microsoft Graph PowerShell module and sign in at the PowerShell prompt.

    ```PowerShell
    Install-Module Microsoft.Graph -Scope CurrentUser
    Connect-MgGraph -Scopes "Directory.ReadWrite.All"
    ```
2. Configure the expiration settings. Use the [New-MgGroupLifecyclePolicy](/en-us/powershell/module/microsoft.graph.groups/new-mggrouplifecyclepolicy) cmdlet to set the lifetime for all Microsoft 365 groups in the Microsoft Entra organization to 365 days. Renewal notifications for Microsoft 365 groups without owners are sent to `emailaddress@contoso.com`.

    ```PowerShell
    New-MgGroupLifecyclePolicy -AlternateNotificationEmails emailaddress@contoso.com `
       -GroupLifetimeInDays 365 -ManagedGroupTypes All
    ```
3. Retrieve the existing policy by using [Get-MgGroupLifecyclePolicy](/en-us/powershell/module/microsoft.graph.groups/get-mggrouplifecyclepolicy). This cmdlet retrieves the current Microsoft 365 group expiration settings that were configured.

    ```powershell
    Get-MgGroupLifecyclePolicy
    ```

    In this example, you can see:

    - The policy ID.
    - Renewal notifications for Microsoft 365 groups without owners are sent to `emailaddress@contoso.com`.
    - The lifetime for all Microsoft 365 groups in the Microsoft Entra organization is set to 365 days.

    ```output
    Id                                   AlternateNotificationEmails GroupLifetimeInDays ManagedGroupTypes
    --                                   --------------------------- ------------------- -----------------
    1aaaaaa1-2bb2-3cc3-4dd4-5eeeeeeeeee5 emailaddress@contoso.com    365                 All
    ```
4. Update the existing policy by using [Update-MgGroupLifecyclePolicy](/en-us/powershell/module/microsoft.graph.groups/update-mggrouplifecyclepolicy). This cmdlet is used to update an existing policy. In the following example, the group lifetime in the existing policy is changed from 365 days to 180 days.

    ```powershell
    Update-MgGroupLifecyclePolicy -GroupLifecyclePolicyId "1aaaaaa1-2bb2-3cc3-4dd4-5eeeeeeeeee5" -GroupLifetimeInDays 180 -AlternateNotificationEmails "emailaddress@contoso.com"
    ```
5. Add specific groups to the policy by using [Add-MgGroupToLifecyclePolicy](/en-us/powershell/module/microsoft.graph.groups/add-mggrouptolifecyclepolicy). This cmdlet adds a group to the lifecycle policy. As an example:

    ```powershell
    Add-MgGroupToLifecyclePolicy -GroupLifecyclePolicyId "1aaaaaa1-2bb2-3cc3-4dd4-5eeeeeeeeee5" -GroupId "cffd97bd-6b91-4c4e-b553-6918a320211c"
    ```
6. Remove the existing policy by using [Remove-MgGroupLifecyclePolicy](/en-us/powershell/module/microsoft.graph.groups/remove-mggrouplifecyclepolicy). This cmdlet deletes the Microsoft 365 group expiration settings but requires the policy ID. This cmdlet disables expiration for Microsoft 365 groups.

    ```powershell
    Remove-MgGroupLifecyclePolicy -GroupLifecyclePolicyId "1aaaaaa1-2bb2-3cc3-4dd4-5eeeeeeeeee5"
    ```

You can use the following cmdlets to configure the policy in more detail. For more information, see [Microsoft Graph PowerShell documentation](/en-us/powershell/microsoftgraph/).

- [Get-MgGroupLifecyclePolicy](/en-us/powershell/module/microsoft.graph.groups/get-mggrouplifecyclepolicy)
- [New-MgGroupLifecyclePolicy](/en-us/powershell/module/microsoft.graph.groups/new-mggrouplifecyclepolicy)
- [Remove-MgGroupLifecyclePolicy](/en-us/powershell/module/microsoft.graph.groups/remove-mggrouplifecyclepolicy)
- [Update-MgGroupLifecyclePolicy](/en-us/powershell/module/microsoft.graph.groups/update-mggrouplifecyclepolicy)
- [Add-MgGroupToLifecyclePolicy](/en-us/powershell/module/microsoft.graph.groups/add-mggrouptolifecyclepolicy)
- [Remove-MgGroupFromLifecyclePolicy](/en-us/powershell/module/microsoft.graph.groups/remove-mggroupfromlifecyclepolicy)
- [Invoke-MgRenewGroup](/en-us/powershell/module/microsoft.graph.groups/invoke-mgrenewgroup)