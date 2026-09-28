---
layout: Conceptual
title: Configure group settings using PowerShell - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-settings-cmdlets
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: How to manage the settings for groups using Microsoft Entra cmdlets
ms.topic: how-to
ms.date: 2025-06-05T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done
locale: en-us
document_id: 4cd7a703-534a-5fbd-6470-5d29bf512fd2
document_version_independent_id: 4f70ed16-6a1c-c0be-3c5e-d56e1b7c7275
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-settings-cmdlets.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-settings-cmdlets
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-settings-cmdlets.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 297db879-3a0b-fdbb-5b6f-8a051fcc6c70
---

# Configure group settings using PowerShell - Microsoft Entra ID | Microsoft Learn

## Overview

This article contains instructions for using PowerShell cmdlets to create and update groups in Microsoft Entra ID, part of Microsoft Entra. This content applies only to Microsoft 365 groups.

Important

Some settings require a Microsoft Entra ID P1 license. For more information, see the Template settings table.

For more information on how to prevent nonadministrator users from creating security groups, set the `AllowedToCreateSecurityGroups` property to False as described in [Update-MgPolicyAuthorizationPolicy](/en-us/powershell/module/microsoft.graph.identity.signins/update-mgpolicyauthorizationpolicy).

Microsoft 365 groups settings are configured using a Settings object and a SettingsTemplate object. Initially, you don't see any Settings objects in your directory, because your directory is configured with the default settings. To change the default settings, you must create a new settings object using a settings template. Microsoft provides several settings templates. To configure Microsoft 365 group settings for your directory, you use the template named "Group.Unified". To configure Microsoft 365 group settings on a single group, use the template named "Group.Unified.Guest". This template is used to manage guest access to a Microsoft 365 group.

The cmdlets are part of the [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/) module. For instructions how to download and install the module on your computer, see [Install the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation).

Note

Even with the restrictions enabled to prevent the addition of guests to Microsoft 365 groups, administrators can still add guest users. The restriction only applies to non-admin users.

## Install PowerShell cmdlets

Install the Microsoft Graph cmdlets as described in [Install the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation).

1. Open the Windows PowerShell app as an administrator.
2. Install the Microsoft Graph cmdlets.

    ```powershell
    Install-Module Microsoft.Graph -Scope AllUsers
    ```
3. Install the Microsoft Graph beta cmdlets.

    ```powershell
    Install-Module Microsoft.Graph.Beta -Scope AllUsers
    ```

## Connect to Microsoft Graph

Before running any `Get-Mg*`, `New-Mg*`, or `Update-Mg*` cmdlets in this article, you must first authenticate to Microsoft Graph.

### Sign in

```PowerShell
Connect-MgGraph -Scopes "Directory.ReadWrite.All"
```

You'll be prompted to sign in and consent to the required permissions.

1. Verify your connection

    ```powershell
    Get-MgContext
    ```

    This command confirms that you're signed in and shows the currently selected Microsoft Graph profile.
2. Some examples in this article use Microsoft Graph beta API. To switch profiles:

    ```powershell
    Select-MgProfile -Name "beta"
    ```

Note

If you don't run `Connect-MgGraph`, all `Get-Mg*`, `New-Mg*`, and `Update-Mg*` commands in this document will fail.

## Create settings at the directory level

These steps create settings at directory level, which apply to all Microsoft 365 groups in the directory.

1. In the DirectorySettings cmdlets, you must specify the ID of the SettingsTemplate you want to use. If you don't know this ID, this cmdlet returns the list of all settings templates:

    ```powershell
    Get-MgBetaDirectorySettingTemplate
    ```

    This cmdlet call returns all templates that are available:

    ```output
    Id                                   DisplayName         Description
    --                                   -----------         -----------
    62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
    08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Microsoft 365 group
    16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define the different settings that can be used for the associ...
    4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
    898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
    5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
    ```
2. To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:

    ```powershell
    $TemplateId = (Get-MgBetaDirectorySettingTemplate | where { $_.DisplayName -eq "Group.Unified" }).Id
    $Template = Get-MgBetaDirectorySettingTemplate | where -Property Id -Value $TemplateId -EQ
    ```
3. Create an object that contains values to be used for the directory setting. These values change the usage guideline value and enable sensitivity labels. Set these or any other setting in the template as required:

    ```powershell
    $params = @{
       templateId = "$TemplateId"
       values = @(
          @{
             name = "UsageGuidelinesUrl"
             value = "https://guideline.example.com"
          }
          @{
             name = "EnableMIPLabels"
             value = "True"
          }
       )
    }
    ```
4. Create the directory setting by using the [New-MgBetaDirectorySetting](/en-us/powershell/module/microsoft.graph.beta.identity.directorymanagement/new-mgbetadirectorysetting):

    ```powershell
    New-MgBetaDirectorySetting -BodyParameter $params
    ```
5. You can read the values by using the following commands:

    ```powershell
    $Setting = Get-MgBetaDirectorySetting | where { $_.DisplayName -eq "Group.Unified"}
    $Setting.Values
    ```

## Update settings at the directory level

To update the value for UsageGuideLinesUrl in the setting template, read the current settings from Microsoft Entra ID, otherwise you could end up overwriting existing settings other than the UsageGuideLinesUrl.

1. Get the current settings from the Group.Unified SettingsTemplate:

    ```powershell
    $Setting = Get-MgBetaDirectorySetting | where { $_.DisplayName -eq "Group.Unified"}
    ```
2. Check the current settings:

    ```powershell
    $Setting.Values
    ```

    This command returns the following values:

    ```output
    Name                            Value
    ----                            -----
    EnableMIPLabels                 True
    CustomBlockedWordsList
    EnableMSStandardBlockedWords    False
    ClassificationDescriptions
    DefaultClassification
    PrefixSuffixNamingRequirement
    AllowGuestsToBeGroupOwner       False
    AllowGuestsToAccessGroups       True
    GuestUsageGuidelinesUrl
    GroupCreationAllowedGroupId
    AllowToAddGuests                True
    UsageGuidelinesUrl              https://guideline.example.com
    ClassificationList
    EnableGroupCreation             True
    NewUnifiedGroupWritebackDefault True
    ```
3. To remove the value of UsageGuideLinesUrl, edit the URL to be an empty string:

    ```powershell
    $params = @{
       Values = @(
          @{
             Name = "UsageGuidelinesUrl"
             Value = ""
          }
       )
    }
    ```
4. Update the value by using the [Update-MgBetaDirectorySetting](/en-us/powershell/module/microsoft.graph.beta.identity.directorymanagement/update-mgbetadirectorysetting) cmdlet:

    ```powershell
    Update-MgBetaDirectorySetting -DirectorySettingId $Setting.Id -BodyParameter $params
    ```

## Template settings

Here are the settings defined in the `Group.Unified SettingsTemplate`. Unless otherwise indicated, these features require a Microsoft Entra ID P1 license.

| **Setting** | **Description** |
| --- | --- |
| **EnableGroupCreation**Type: `Boolean`Default: `True` | This flag indicates whether nonadmin users can create Microsoft 365 groups in the directory. This setting doesn't require a Microsoft Entra ID P1 license. |
| **GroupCreationAllowedGroupId**Type: `String`Default: `""` | GUID of the security group for which the members are allowed to create Microsoft 365 groups even when `EnableGroupCreation == false`. |
| **UsageGuidelinesUrl**Type: `String`Default: `""` | A link to the Group Usage Guidelines. |
| **ClassificationDescriptions**Type: `String`Default: `""` | A comma-delimited list of classification descriptions. The value of `ClassificationDescriptions` is only valid in this format:`$setting["ClassificationDescriptions"] ="Classification:Description,Classification:Description"`where Classification matches an entry in the ClassificationList.This setting doesn't apply when `EnableMIPLabels == True`.Character limit for property `ClassificationDescriptions` is 300, and commas can't be escaped. |
| **DefaultClassification**Type: `String`Default: `""` | The classification that is to be used as the default classification for a group if none was specified.This setting doesn't apply when `EnableMIPLabels == True`. This value can only be set when `ClassificationList` is set in the same call. |
| **PrefixSuffixNamingRequirement**Type: `String`Default: `""` | String of a maximum length of 64 characters that defines the naming convention configured for Microsoft 365 groups. For more information, see [Enforce a naming policy for Microsoft 365 groups](groups-naming-policy). |
| **CustomBlockedWordsList**Type: `String`Default: `""` | Comma-separated string of phrases that users aren't allowed to use in group names or aliases. For more information, see [Enforce a naming policy for Microsoft 365 groups](groups-naming-policy). |
| **EnableMSStandardBlockedWords**Type: `Boolean`Default: `False` | Deprecated. Don't use. |
| **AllowGuestsToBeGroupOwner**Type: `Boolean`Default: `False` | Boolean indicating whether or not a guest user can be an owner of groups. |
| **AllowGuestsToAccessGroups**Type: `Boolean`Default: `True` | Boolean indicating whether or not a guest user can have access to Microsoft 365 groups content. This setting doesn't require a Microsoft Entra ID P1 license. |
| **GuestUsageGuidelinesUrl**Type: `String`Default: `""` | The URL of a link to the guest usage guidelines. |
| **AllowToAddGuests**Type: `Boolean`Default: `True` | A boolean indicating whether or not it is allowed to add guests to this directory. This setting might be overridden and become read-only if `EnableMIPLabels` is set to *True* and a guest policy is associated with the sensitivity label assigned to the group.If the `AllowToAddGuests` setting is set to False at the organization level, any `AllowToAddGuests` setting at the group level is ignored. If you want to enable guest access for only a few groups, you must set `AllowToAddGuests` to be true at the organization level, and then selectively disable it for specific groups. |
| **ClassificationList**Type: `String`Default: `""` | A comma-delimited list of valid classification values that can be applied to Microsoft 365 groups. This setting doesn't apply when EnableMIPLabels == True. |
| **EnableMIPLabels**Type: `Boolean`Default: `False` | The flag indicating whether sensitivity labels published in Microsoft Purview portal can be applied to Microsoft 365 groups. For more information, see [Assign Sensitivity Labels for Microsoft 365 groups](groups-assign-sensitivity-labels). |
| **NewUnifiedGroupWritebackDefault**Type: `Boolean`Default: `True` | The flag that allows an admin to create new Microsoft 365 groups without setting the groupWritebackConfiguration resource type in the request payload. This setting is applicable when group writeback is configured in Microsoft Entra Connect. `NewUnifiedGroupWritebackDefault` is a global Microsoft 365 group setting. Default value is true. Updating the setting value to false changes the default writeback behavior for newly created Microsoft 365 groups, and doesn't change the **isEnabled** property value for existing Microsoft 365 groups. Group admin needs to explicitly update the group isEnabled property value to change the writeback state for existing Microsoft 365 groups. |

## Example: Configure Guest policy for groups at the directory level

1. Get all the setting templates:

    ```powershell
    Get-MgBetaDirectorySettingTemplate
    ```
2. To set guest policy for groups at the directory level, you need the Group.Unified template.

    ```powershell
    $Template = Get-MgBetaDirectorySettingTemplate | where -Property Id -Value "62375ab9-6b52-47ed-826b-58e47e0e304b" -EQ
    ```
3. Set a value for AllowToAddGuests for the specified template:

    ```powershell
    $params = @{
       templateId = "62375ab9-6b52-47ed-826b-58e47e0e304b"
       values = @(
          @{
             name = "AllowToAddGuests"
             value = "False"
          }
       )
    }
    ```
4. Next, create a new settings object by using the [New-MgBetaDirectorySetting](/en-us/powershell/module/microsoft.graph.beta.identity.directorymanagement/new-mgbetadirectorysetting) cmdlet:

    ```powershell
    $Setting = New-MgBetaDirectorySetting -BodyParameter $params
    ```
5. You can read the values using:

    ```powershell
    $Setting.Values
    ```

## Read settings at the directory level

If you know the name of the setting you want to retrieve, you can use the below cmdlet to retrieve the current settings value. In this example, the value for a setting named `UsageGuidelinesUrl` is retrieved.

```powershell
(Get-MgBetaDirectorySetting).Values | where -Property Name -Value UsageGuidelinesUrl -EQ
```

These steps read settings at directory level, which apply to all Microsoft 365 groups in the directory.

1. Read all existing directory settings:

    ```powershell
    Get-MgBetaDirectorySetting -All
    ```

    This cmdlet returns a list of all directory settings:

    ```output
    Id                                   DisplayName   TemplateId                           Values
    --                                   -----------   ----------                           ------
    c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
    ```
2. Read all settings for a specific group:

    ```powershell
    Get-MgBetaGroupSetting -GroupId "ab6a3887-776a-4db7-9da4-ea2b0d63c504"
    ```
3. Read all directory settings values of a specific directory settings object, using Settings ID GUID:

    ```powershell
    (Get-MgBetaDirectorySetting -DirectorySettingId "c391b57d-5783-4c53-9236-cefb5c6ef323").values
    ```

    This cmdlet returns the names and values in this settings object for this specific group:

    ```output
    Name                          Value
    ----                          -----
    ClassificationDescriptions
    DefaultClassification
    PrefixSuffixNamingRequirement
    CustomBlockedWordsList        
    AllowGuestsToBeGroupOwner     False 
    AllowGuestsToAccessGroups     True
    GuestUsageGuidelinesUrl
    GroupCreationAllowedGroupId
    AllowToAddGuests              True
    UsageGuidelinesUrl            https://guideline.example.com
    ClassificationList
    EnableGroupCreation           True
    ```

## Remove settings at the directory level

This step removes settings at directory level, which apply to all Microsoft 365 groups in the directory.

```powershell
Remove-MgBetaDirectorySetting –DirectorySettingId "c391b57d-5783-4c53-9236-cefb5c6ef323c"
```

## Create settings for a specific group

1. Get the settings templates.

    ```powershell
    Get-MgBetaDirectorySettingTemplate
    ```
2. In the results, find for the settings template named "Groups.Unified.Guest":

    ```output
    Id                                   DisplayName            Description
    --                                   -----------            -----------
    62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
    08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Microsoft 365 group
    4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
    898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
    5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
    ```
3. Retrieve the template object for the Groups.Unified.Guest template:

    ```powershell
    $Template1 = Get-MgBetaDirectorySettingTemplate | where -Property Id -Value "08d542b9-071f-4e16-94b0-74abb372e3d9" -EQ
    ```
4. Get the ID of the group you want to apply this setting to:

    ```powershell
    $GroupId = (Get-MgGroup -Filter "DisplayName eq '<YourGroupName>'").Id
    ```
5. Create the new setting:

    ```powershell
    $params = @{
       templateId = "08d542b9-071f-4e16-94b0-74abb372e3d9"
       values = @(
          @{
             name = "AllowToAddGuests"
             value = "False"
          }
       )
    }
    ```
6. Create the group setting:

    ```powershell
    New-MgBetaGroupSetting -GroupId $GroupId -BodyParameter $params
    ```
7. To verify the settings, run this command:

    ```powershell
    Get-MgBetaGroupSetting -GroupId $GroupId | FL Values
    ```

## Update settings for a specific group

1. Get the ID of the group whose setting you want to update:

    ```powershell
    $groupId = (Get-MgGroup -Filter "DisplayName eq '<YourGroupName>'").Id
    ```
2. Retrieve the setting of the group:

    ```powershell
    $Setting = Get-MgBetaGroupSetting -GroupId $GroupId
    ```
3. Update the setting of the group as you need:

    ```powershell
    $params = @{
       values = @(
          @{
             name = "AllowToAddGuests"
             value = "True"
          }
       )
    }
    ```
4. Then you can set the new value for this setting:

    ```powershell
    Update-MgBetaGroupSetting -DirectorySettingId $Setting.Id -GroupId $GroupId -BodyParameter $params
    ```
5. You can read the value of the setting to make sure it has been updated correctly:

    ```powershell
    Get-MgBetaGroupSetting -GroupId $GroupId  | FL Values
    ```

## Cmdlet syntax reference

You can find more Microsoft Graph PowerShell documentation at [Microsoft Entra Cmdlets](/en-us/powershell/microsoftgraph/).

## Manage group settings using Microsoft Graph

To configure and manage group settings using Microsoft Graph, see the [`groupSetting` resource type](/en-us/graph/api/resources/groupsetting?view=graph-rest-1.0&amp;preserve-view=true) and its associated methods.