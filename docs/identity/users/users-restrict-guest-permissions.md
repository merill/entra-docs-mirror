---
layout: Conceptual
title: Restrict guest user access permissions - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/users-restrict-guest-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Restrict guest user access permissions using the Azure portal, PowerShell, or Microsoft Graph in Microsoft Entra ID
ms.date: 2024-12-19T00:00:00.0000000Z
ms.topic: how-to
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-ga-nochange
ms.reviewer: yukarppa
locale: en-us
document_id: 06c48d2a-fec6-95c9-7509-7666f633805d
document_version_independent_id: 25a1163c-fcbf-1d8f-ba92-e0b190a05c6b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/users-restrict-guest-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/users-restrict-guest-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/users-restrict-guest-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 12a4962c-b5ab-2650-51b6-e09ff70f3f37
---

# Restrict guest user access permissions - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra ID, part of Microsoft Entra, allows you to restrict what guest users can see in their organization in Microsoft Entra ID. Guest users are set to a limited permission level by default in Microsoft Entra ID, while the default for member users is the full set of user permissions. There's another guest user permission level in your Microsoft Entra organization's external collaboration settings for even more restricted access, so that the guest access levels are:

| Permission level | Access level | Value |
| --- | --- | --- |
| Same as member users | Guests have the same access to Microsoft Entra resources as member users | a0b1b346-4d3e-4e8b-98f8-753987be4970 |
| Limited access (default) | Guests can see membership of all non-hidden groups | 10dae51f-b6af-4016-8d66-8c2a99b929b3 |
| **Restricted access (new)** | **Guests can't see membership of any groups** | **2af84b1e-32c8-42b7-82bc-daa82404023b** |

When guest access is restricted, guests can view only their own user profile. Permission to view other users isn't allowed even if the guest is searching by User Principal Name or objectId. Restricted access also restricts guest users from seeing the membership of groups they're in. For more information about the overall default user permissions, including guest user permissions, see [What are the default user permissions in Microsoft Entra ID?](../../fundamentals/users-default-permissions).

## Update in the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [User administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Select **Entra ID** &gt; **External Identities**.
3. Select **External collaboration settings**.
4. On the **External collaboration settings** page, select **Guest user access is restricted to properties and memberships of their own directory objects** option.

    ![Screenshot of Microsoft Entra external collaboration settings page.](media/users-restrict-guest-permissions/external-collaboration-settings.png)
5. Select **Save**. The changes can take up to 15 minutes to take effect for guest users.

## Update with the Microsoft Graph API

There's a new Microsoft Graph API to configure guest permissions in your Microsoft Entra organization. The following API calls can be made to assign any permission level. The value for guestUserRoleId used here is to illustrate the most restricted guest user setting. For more information about using the Microsoft Graph to set guest permissions, see [`authorizationPolicy` resource type](/en-us/graph/api/resources/authorizationpolicy).

### Configuring for the first time

```PowerShell
POST https://graph.microsoft.com/beta/policies/authorizationPolicy/authorizationPolicy

{
  "guestUserRoleId": "2af84b1e-32c8-42b7-82bc-daa82404023b"
}
```

Response should be Success 204.

Note

Azure AD and MSOnline PowerShell modules are deprecated as of March 30, 2024. To learn more, read the [deprecation update](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270). After this date, support for these modules are limited to migration assistance to Microsoft Graph PowerShell SDK and security fixes. The deprecated modules will continue to function through March, 30 2025.

We recommend migrating to [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/overview) to interact with Microsoft Entra ID (formerly Azure AD). For common migration questions, refer to the [Migration FAQ](/en-us/powershell/azure/active-directory/migration-faq). *Note:* Versions 1.0.x of MSOnline may experience disruption after June 30, 2024.

### Updating the existing value

```PowerShell
PATCH https://graph.microsoft.com/beta/policies/authorizationPolicy/authorizationPolicy

{
  "guestUserRoleId": "2af84b1e-32c8-42b7-82bc-daa82404023b"
}
```

Response should be Success 204.

### View the current value

```PowerShell
GET https://graph.microsoft.com/beta/policies/authorizationPolicy/authorizationPolicy
```

Example response:

```PowerShell
{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#policies/authorizationPolicy/$entity",
    "id": "authorizationPolicy",
    "displayName": "Authorization Policy",
    "description": "Used to manage authorization related settings across the company.",
    "enabledPreviewFeatures": [],
    "guestUserRoleId": "10dae51f-b6af-4016-8d66-8c2a99b929b3",
    "permissionGrantPolicyIdsAssignedToDefaultUserRole": [
        "user-default-legacy"
    ]
}
```

## Update with PowerShell cmdlets

With this feature, the ability to configure the restricted permissions via PowerShell v2 cmdlets has been added. Get and Update PowerShell cmdlets have been published in version `2.0.2.85`.

### Get command: Get-MgPolicyAuthorizationPolicy

Example:

```powershell
Get-MgPolicyAuthorizationPolicy | Format-List
```

```output
AllowEmailVerifiedUsersToJoinOrganization : True
AllowInvitesFrom                          : everyone
AllowUserConsentForRiskyApps              :
AllowedToSignUpEmailBasedSubscriptions    : True
AllowedToUseSspr                          : True
BlockMsolPowerShell                       : False
DefaultUserRolePermissions                : Microsoft.Graph.PowerShell.Models.MicrosoftGraphDefaultUserRolePermissions
DeletedDateTime                           :
Description                               : Used to manage authorization related settings across the company.
DisplayName                               : Authorization Policy
GuestUserRoleId                           : 10dae51f-b6af-4016-8d66-8c2a99b929b3
Id                                        : authorizationPolicy
AdditionalProperties                      : {[@odata.context, https://graph.microsoft.com/v1.0/$metadata#policies/authorizationPolicy/$entity]}
```

### Update command: Update-MgPolicyAuthorizationPolicy

Example:

```powershell
Update-MgPolicyAuthorizationPolicy -GuestUserRoleId '2af84b1e-32c8-42b7-82bc-daa82404023b'
```

## Supported Microsoft 365 services

### Supported services

By supported, the experience is as expected; specifically, that it's same as current guest experience.

- Teams
- Outlook (OWA)
- SharePoint
- Planner in Teams
- Planner mobile app
- Planner web app
- Project for the web
- Project Operations

### Services currently not supported

Services without current support might have compatibility issues with the new guest restriction setting.

- Forms
- Project Online
- Viva Engage
- Planner in SharePoint

## Frequently asked questions (FAQ)

| Question | Answer |
| --- | --- |
| Where do these permissions apply? | These directory level permissions are enforced across Microsoft Entra services including the Microsoft Graph, PowerShell v2, the Azure portal, and My Apps portal. Microsoft 365 services using Microsoft 365 groups for collaboration scenarios are also affected, specifically Outlook, Microsoft Teams, and SharePoint. |
| How do restricted permissions affect which groups guests can see? | Regardless of default or restricted guest permissions, guests can't enumerate the list of groups or users. Guests can see groups they're members of in both the Azure portal and the My Apps portal depending on permissions:<br>- **Default permissions**: To find the groups they're members of in the Azure portal, the guest must search for their object ID in the **All users** list, and then select **Groups**. Here they can see the list of groups that they're members of, including all the group details, including name, email, and so on. In the My Apps portal, they can see a list of groups they own and groups they're in.<br>- **Restricted guest permissions**: In the Azure portal, they can find the list of groups they're in by searching for their object ID in the **All users** list, and then selecting **Groups**. They can see only limited details about the group, notably the object ID. By design, the Name and Email columns are blank and Group Type is Unrecognized. In the My Apps portal, they're not able to access the list of groups they own or groups they're a member of.<br><br>For more detailed comparison of the directory permissions that come from the Graph API, see [Default user permissions](../../fundamentals/users-default-permissions#member-and-guest-users). |
| Which parts of the My Apps portal will this feature affect? | The groups functionality in the My Apps portal honors these new permissions. This functionality includes all paths to view the groups list and group memberships in My Apps. No changes were made to the group tile availability. The group tile availability is still controlled by the existing group setting in the Azure portal. |
| Do these permissions override SharePoint or Microsoft Teams guest settings? | No. Those existing settings still control the experience and access in those applications. For example, if you see issues in SharePoint, double-check your external sharing settings. Guests added by team owners at the team level have access to channel meeting chat only for standard channels, excluding any private and shared channels. |
| What are the known compatibility issues in Viva Engage? | With permissions set to "restricted", guests signed into Viva Engage aren't able to leave the group. |
| Will my existing guest permissions be changed in my tenant? | No changes were made to your current settings. Backward compatibility with your existing settings is maintained. You decide when you want to make changes. |
| Will these permissions be set by default? | No. The existing default permissions remain unchanged. You can optionally set the permissions to be more restrictive. |
| Are there any license requirements for this feature? | No, there are no new licensing requirements with this feature. |