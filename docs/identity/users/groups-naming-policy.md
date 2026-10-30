---
layout: Conceptual
title: Enforce a group naming policy in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-naming-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how to set up a naming policy for Microsoft 365 groups in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-01-14T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-ga-nochange
locale: en-us
document_id: e3fb85a8-d842-f101-909e-86751922da43
document_version_independent_id: 0c99b5ef-753e-1085-a682-c55ea4059207
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-naming-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-naming-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-naming-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4e4a64ee-6031-029d-0d90-21f7782de242
---

# Enforce a group naming policy in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

## Overview

To enforce consistent naming conventions for Microsoft 365 groups created or edited by your users, set up a group naming policy for your organizations in Microsoft Entra ID. For example, you could use the naming policy to communicate the function of a group, membership, geographic region, or person who created the group. You could also use the naming policy to help categorize groups in the address book. You can use the policy to block specific words from being used in group names and aliases.

Important

Using a Microsoft Entra ID naming policy for Microsoft 365 groups requires that you possess but not necessarily assign a Microsoft Entra ID P1 license or Microsoft Entra Basic EDU license for each unique user who's a member of one or more Microsoft 365 groups.

The naming policy is applied to creating or editing groups created across workloads, for example, Outlook, Microsoft Teams, SharePoint, Exchange, or Planner, even if no editing changes are made. It's applied to both the group name and group alias. If you set up your naming policy in Microsoft Entra ID and you have an existing Exchange group naming policy, the Microsoft Entra ID naming policy is enforced in your organization.

When a group naming policy is configured, the policy is applied to new Microsoft 365 groups created by users. A naming policy doesn't apply to certain directory roles, such as Global Administrator or User Administrator. (For the complete list of roles exempted from a group naming policy, see the "Roles and permissions" section.) For existing Microsoft 365 groups, the policy isn't immediately applied at the time of configuration. After a group owner edits the group name for these groups, the naming policy is enforced even if no changes are made.

## Naming policy features

You can enforce a naming policy for groups in two different ways:

- **Prefix-suffix naming policy**: You can define prefixes or suffixes that are then added automatically to enforce a naming convention on your groups. For example, in the group name `GRP_JAPAN_My Group_Engineering`, the prefix is `GRP_JAPAN_` and the suffix is `_Engineering`.
- **Custom blocked words**: You can upload a set of blocked words specific to your organization to be blocked in groups created by users. For example, you might use `Payroll,CEO,HR`.

### Prefix-suffix naming policy

The general structure of the naming convention is `Prefix[GroupName]Suffix`. While you can define multiple prefixes and suffixes, you can have only one instance of the `[GroupName]` in the setting. The prefixes or suffixes can be either fixed strings or user attributes, such as `[Department]`, that are substituted based on the user who's creating the group. The total allowable number of characters for your prefix and suffix strings including group name is 63 characters.

Prefixes and suffixes can contain special characters that are supported in a group name and a group alias. Any characters in the prefix or suffix that aren't supported in the group alias are still applied in the group name but removed from the group alias. Because of this restriction, the prefixes and suffixes applied to the group name might be different from the ones applied to the group alias.

#### Fixed strings

You can use strings to make it easier to scan and differentiate groups in the global address list and in the left navigation links of group workloads. Some of the common prefixes are keywords like `Grp_Name`, `#Name`, and `_Name`.

#### User attributes

You can use attributes that can help you and your users identify which department, office, or geographic region for which the group was created. For example, if you define your naming policy as `PrefixSuffixNamingRequirement = "GRP [GroupName] [Department]"` and `User's department = Engineering`, then an enforced group name might be `"GRP My Group Engineering."` Supported Microsoft Entra attributes are `\[Department\]`, `\[Company\]`, `\[Office\]`, `\[StateOrProvince\]`, `\[CountryOrRegion\]`, and `\[Title\]`. Unsupported user attributes are treated as fixed strings. An example is `"\[postalCode\]"`. Extension attributes and custom attributes aren't supported.

Use attributes that have values filled in for all users in your organization and don't use attributes that have long values.

### Custom blocked words

A blocked word list is a comma-separated list of phrases to be blocked in group names and aliases. No substring searches are performed. An exact match between the group name and one or more of the custom blocked words is required to trigger a failure. Substring search isn't performed so that users can use common words like "Class" even if "lass" is a blocked word.

Blocked word list rules:

- Blocked words aren't case sensitive.
- When a user enters a blocked word as part of a group name, they see an error message with the blocked word.
- There are no character restrictions on blocked words.
- There's an upper limit of 5,000 phrases that you can configure in the blocked words list.

### Roles and permissions

To configure a naming policy, one of the following roles is required:

- Global Administrator
- Group Administrator
- Directory Writer

Some administrator roles are exempted from these policies, across all group workloads and endpoints, so that they can create groups by using blocked words and with their own naming conventions. The following administrator roles are exempted from the group naming policy:

- Global Administrator
- User Administrator

## Configure a naming policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Group Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Select **Microsoft Entra ID**.
3. Select **All groups** &gt; **Groups**, and then select **Naming policy** to open the **Naming policy** page.

    ![Screenshot that shows opening the Naming policy page in the admin center.](media/groups-naming-policy/policy.png)

### View or edit the prefix-suffix naming policy

1. On the **Naming policy** page, select **Group naming policy**.
2. You can view or edit the current prefix or suffix naming policies individually by selecting the attributes or strings you want to enforce as part of the naming policy.
3. To remove a prefix or suffix from the list, select the prefix or suffix, and then select **Delete**. You can delete multiple items at the same time.
4. Save your changes for the new policy to go into effect by selecting **Save**.

### Edit custom blocked words

1. On the **Naming policy** page, select **Blocked words**.

    ![Screenshot that shows editing and uploading a blocked words list for a naming policy.](media/groups-naming-policy/blockedwords.png)
2. View or edit the current list of custom blocked words by selecting **Download**. You must add new entries to the existing entries.
3. Upload the new list of custom blocked words by selecting the **file** icon.
4. Save your changes for the new policy to go into effect by selecting **Save**.

## Install PowerShell cmdlets

Install the Microsoft Graph cmdlets as described in [Install the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation).

Note

Azure AD and MSOnline PowerShell modules are deprecated as of March 30, 2024. To learn more, read the [deprecation update](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270). After this date, support for these modules are limited to migration assistance to Microsoft Graph PowerShell SDK and security fixes. The deprecated modules will continue to function through March, 30 2025.

We recommend migrating to [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/overview) to interact with Microsoft Entra ID (formerly Azure AD). For common migration questions, refer to the [Migration FAQ](/en-us/powershell/azure/active-directory/migration-faq). *Note:* Versions 1.0.x of MSOnline may experience disruption after June 30, 2024.

1. Open the Windows PowerShell app as an administrator.
2. Install the Microsoft Graph cmdlets.

    ```powershell
    Install-Module Microsoft.Graph -Scope AllUsers
    ```
3. Install the Microsoft Graph beta cmdlets.

    ```powershell
    Install-Module Microsoft.Graph.Beta -Scope AllUsers
    ```

## Configure a naming policy in PowerShell

1. Open a Windows PowerShell window on your computer. You can open it without elevated privileges.
2. Run the following command to prepare to run the cmdlets.

    ```powershell
    Connect-MgGraph -Scopes "Directory.ReadWrite.All"
    ```

    On the **Sign in to your Account** screen that opens, enter your admin account and password to connect to your service.
3. Follow the steps in [Microsoft Entra cmdlets for configuring group settings](groups-settings-cmdlets) to create group settings for this organization.

### View the current settings

1. Fetch the current naming policy to view the current settings.

    ```powershell
    $Setting = Get-MgBetaDirectorySetting -DirectorySettingId (Get-MgBetaDirectorySetting | where -Property DisplayName -Value "Group.Unified" -EQ).id
    ```
2. Display the current group settings.

    ```powershell
    $Setting.Values
    ```

### Set the naming policy and custom blocked words

1. Get the setting.

    ```powershell
    $Setting = Get-MgBetaDirectorySetting -DirectorySettingId (Get-MgBetaDirectorySetting | where -Property DisplayName -Value "Group.Unified" -EQ).id
    ```
2. Set the group name prefixes and suffixes. For the feature to work properly, `[GroupName]` must be included in the setting. Also, set the custom blocked words that you want to restrict.

    ```powershell
    $params = @{
       values = @(
          @{
             name = "PrefixSuffixNamingRequirement"
             value = "GRP_[GroupName]_[Department]"
          }
          @{
             name = "CustomBlockedWordsList"
             value = "Payroll,CEO,HR"
          }
       )
    }
    ```
3. Update the settings for the new policy to go into effect, as shown in the following example.

    ```powershell
    Update-MgBetaDirectorySetting -DirectorySettingId $Setting.Id -BodyParameter $params
    ```

That's it. You set your naming policy and added your blocked words.

## Export or import custom blocked words

For more information, see [Microsoft Entra cmdlets for configuring group settings](groups-settings-cmdlets).

Here's an example of a PowerShell script to export multiple blocked words.

```powershell
$Words = (Get-MgBetaDirectorySetting).Values | where -Property Name -Value CustomBlockedWordsList -EQ 
Add-Content "c:\work\currentblockedwordslist.txt" -Value $Words.value.Split(",").Replace("`"","")
```

Here's an example PowerShell script to import multiple blocked words.

```powershell
$BadWords = Get-Content "C:\work\currentblockedwordslist.txt"
$BadWords = [string]::join(",", $BadWords)
$Setting = Get-MgBetaDirectorySetting | where {$_.DisplayName -eq "Group.Unified"}
if ($Setting.Count -eq 0) {
   $Template = Get-MgBetaDirectorySettingTemplate | where {$_.DisplayName -eq "Group.Unified"}
   $Params = @{ templateId = $Template.Id }
   $Setting = New-MgBetaDirectorySetting -BodyParameter $Params 
   }
$params = @{
   values = @(
      @{
         name = "PrefixSuffixNamingRequirement"
         value = "GRP_[GroupName]_[Department]"
      }
      @{
         name = "CustomBlockedWordsList"
         value = "$BadWords"
      }
   )
}
Update-MgBetaDirectorySetting -DirectorySettingId $Setting.Id -BodyParameter $params
```

## Remove the naming policy

You can use the Azure portal or Microsoft Graph PowerShell to remove a naming policy.

### Remove the naming policy by using the Azure portal

1. On the **Naming policy** page, select **Delete policy**.
2. After you confirm the deletion, the naming policy is removed, including all prefix-suffix naming policies and any custom blocked words.

### Remove the naming policy by using Microsoft Graph PowerShell

1. Get the setting.

    ```powershell
    $Setting = Get-MgBetaDirectorySetting -DirectorySettingId (Get-MgBetaDirectorySetting | where -Property DisplayName -Value "Group.Unified" -EQ).id
    ```
2. Empty the group name prefixes and suffixes. Empty the custom blocked words.

    ```powershell
    $params = @{
       values = @(
          @{
             name = "PrefixSuffixNamingRequirement"
             value = ""
          }
          @{
             name = "CustomBlockedWordsList"
             value = ""
          }
       )
    }
    ```
3. Update the setting.

    ```powershell
    Update-MgBetaDirectorySetting -DirectorySettingId $Setting.Id -BodyParameter $params
    ```

## Experience across Microsoft 365 apps

After you set a group naming policy in Microsoft Entra ID, when a user creates a group in a Microsoft 365 app, they see:

- A preview of the name according to your naming policy (with prefixes and suffixes) as soon as the user enters the group name.
- If the user enters blocked words, they see an error message, so they can remove the blocked words.

| Workload | Compliance |
| --- | --- |
| Azure portal | The Azure portal and the Access Panel portal show the naming policy-enforced name when the user enters a group name when creating or editing a group. When a user enters a custom blocked word, an error message with the blocked word appears so that the user can remove it. |
| Outlook Web Access (OWA) | Outlook Web Access shows the naming policy-enforced name when the user enters a group name or group alias. When a user enters a custom blocked word, an error message appears in the UI along with the blocked word so that the user can remove it. |
| Outlook desktop | Groups created in Outlook desktop are compliant with the naming policy settings. The Outlook desktop app doesn't yet show the preview of the enforced group name and doesn't return the custom blocked-word errors when the user enters the group name. However, the naming policy is automatically applied when the user creates or edits a group. Users see error messages if there are custom blocked words in the group name or alias. |
| Microsoft Teams | Microsoft Teams shows the group naming policy-enforced name when the user enters a team name. When a user enters a custom blocked word, an error message appears along with the blocked word so that the user can remove it. |
| SharePoint | SharePoint shows the naming policy-enforced name when the user enters a site name or group email address. When a user enters a custom blocked word, an error message appears, along with the blocked word so that the user can remove it. |
| Microsoft Stream | Microsoft Stream shows the group naming policy-enforced name when the user enters a group name or group email alias. When a user enters a custom blocked word, an error message appears along with the blocked word so that the user can remove it. |
| Outlook iOS and Android app | Groups created in Outlook apps are compliant with the configured naming policy. The Outlook mobile app doesn't yet show the preview of the naming policy-enforced name. The app doesn't return custom blocked-word errors when the user enters the group name. However, the naming policy is automatically applied when the user selects **Create** or **Edit**. Users see error messages if there are custom blocked words in the group name or alias. |
| Groups mobile app | Groups created in the Groups mobile app are compliant with the naming policy. The groups mobile app doesn't show the preview of the naming policy and doesn't return custom blocked-word errors when the user enters the group name. But the naming policy is automatically applied when the user creates or edits a group. Users are presented with appropriate errors if there are custom blocked words in the group name or alias. |
| Planner | Planner is compliant with the naming policy. Planner shows the naming policy preview when the user enters the plan name. When a user enters a custom blocked word, an error message appears when the user creates the plan. |
| Project for the web | Project for the web is compliant with the naming policy. |
| Dynamics 365 for Customer Engagement | Dynamics 365 for Customer Engagement is compliant with the naming policy. Dynamics 365 shows the naming policy-enforced name when the user enters a group name or group email alias. When the user enters a custom blocked word, an error message appears with the blocked word so that the user can remove it. |
| School Data Sync (SDS) | Groups created through SDS comply with a naming policy, but the naming policy isn't applied automatically. SDS administrators have to append the prefixes and suffixes to class names for which groups need to be created and then uploaded to SDS. Otherwise, create or edit for groups would fail. |
| Classroom app | Groups created in the Classroom app comply with the naming policy, but the naming policy isn't applied automatically. The naming policy preview isn't shown to users when they enter a classroom group name. Users must enter the enforced classroom group name with prefixes and suffixes. If not, the classroom group create or edit operation fails with errors. |
| Power BI | Power BI workspaces are compliant with the naming policy. |
| Yammer | When a user signs in to Yammer with their Microsoft Entra account to create a group or edit a group name, the group name complies with the naming policy. This feature applies both to Microsoft 365 connected groups and all other Yammer groups.If a Microsoft 365 connected group was created before the naming policy is in place, the group name doesn't automatically follow the naming policies. When a user edits the group name, they're prompted to add the prefix and suffix. |
| StaffHub | StaffHub teams don't follow the naming policy, but the underlying Microsoft 365 group does. A StaffHub team name doesn't apply the prefixes and suffixes and doesn't check for custom blocked words. But StaffHub does apply the prefixes and suffixes and removes blocked words from the underlying Microsoft 365 group. |
| Exchange PowerShell | Exchange PowerShell cmdlets are compliant with the naming policy. Users receive appropriate error messages with suggested prefixes and suffixes and for custom blocked words if they don't follow the naming policy in the group name and group alias (mailNickname). |
| Microsoft Graph PowerShell cmdlets | Microsoft PowerShell cmdlets are compliant with a naming policy. Users receive appropriate error messages with suggested prefixes and suffixes and for custom blocked words if they don't follow the naming convention in group names and group alias. |
| Exchange admin center | Exchange admin center is compliant with a naming policy. Users receive appropriate error messages with suggested prefixes and suffixes and for custom blocked words if they don't follow the naming convention in the group name and group alias. |
| Microsoft 365 admin center | Microsoft 365 admin center is compliant with a naming policy. When a user creates or edits group names, the naming policy is automatically applied. Users receive appropriate errors when they enter custom blocked words. The Microsoft 365 admin center doesn't yet show a preview of the naming policy and doesn't return custom blocked-word errors when the user enters the group name. |