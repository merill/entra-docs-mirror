---
layout: Conceptual
title: Assign sensitivity labels to groups - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-assign-sensitivity-labels
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how to assign sensitivity labels to groups. See troubleshooting information and view more resources.
ms.topic: how-to
ms.date: 2026-04-03T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro, no-azure-ad-ps-ref, sfi-image-nochange
locale: en-us
document_id: ef84a3e0-879e-4312-a89d-7a3bb0cd9a51
document_version_independent_id: 43851f8a-b71f-0a0a-8b1f-629e3528972f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-assign-sensitivity-labels.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-assign-sensitivity-labels
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-assign-sensitivity-labels.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: ac70a032-7f78-804f-b574-8a0a5e8fd626
---

# Assign sensitivity labels to groups - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra ID supports applying [sensitivity labels](/en-us/purview/sensitivity-labels) to Microsoft 365 groups when those labels are published in the [Microsoft Purview portal](/en-us/purview/purview-portal) and the labels are configured for groups and sites.

Sensitivity labels can be applied to groups across apps and services such as Outlook, Microsoft Teams, and SharePoint. For more information, see [Support for sensitivity labels](/en-us/purview/sensitivity-labels-teams-groups-sites#support-for-the-sensitivity-labels) from the Purview documentation.

Important

To configure this feature, there must be at least one active Microsoft Entra ID P1 license in your Microsoft Entra organization.

## Enable sensitivity label support in PowerShell

To apply published labels to groups, you must first enable the feature. These steps enable the feature in Microsoft Entra ID. The Microsoft Graph PowerShell SDK comes in two modules, `Microsoft.Graph` and `Microsoft.Graph.Beta`.

All Microsoft operated regions should choose Microsoft. All other regions should choose their operator if one is listed.

# [Microsoft](#tab/microsoft)
1. Open a PowerShell prompt on your computer and install the Graph modules required to run the cmdlets.

    ```powershell
    Install-Module Microsoft.Graph.Authentication -Scope CurrentUser
    Install-Module Microsoft.Graph.Beta.Identity.DirectoryManagement -Scope CurrentUser
    ```
2. Connect to your tenant.

    ```powershell
    Connect-MgGraph -Scopes "Directory.ReadWrite.All"
    ```
3. Fetch the current group settings for the Microsoft Entra organization and display the current group settings.

    ```powershell
    $grpUnifiedSetting = Get-MgBetaDirectorySetting | Where-Object { $_.Values.Name -eq "EnableMIPLabels" }
    $grpUnifiedSetting.Values
    ```

    If no group settings were created for this Microsoft Entra organization, you get an empty screen. In this case, you must first create the settings. Follow the steps in [Microsoft Entra cmdlets for configuring group settings](groups-settings-cmdlets) to create group settings for this Microsoft Entra organization.

    Note

    If the sensitivity label was enabled previously, you see `EnableMIPLabels = True`. In this case, you don't need to do anything. Also make sure that `EnableGroupCreation = False` if you don't want non-admin users to be able to create groups. See [Template settings](groups-settings-cmdlets#template-settings) for details.
4. Apply the new settings.

    ```powershell
    $params = @{
         Values = @(
     	    @{
     		    Name = "EnableMIPLabels"
     		    Value = "True"
     	    }
         )
    }
    
    Update-MgBetaDirectorySetting -DirectorySettingId $grpUnifiedSetting.Id -BodyParameter $params
    ```
5. Verify that the new value is present.

    ```powershell
    $Setting = Get-MgBetaDirectorySetting -DirectorySettingId $grpUnifiedSetting.Id
    $Setting.Values
    ```

If you receive a `Request_BadRequest` error, it's because the settings already exist in the tenant. When you try to create a new `property:value` pair, the result is an error. In this case, follow these steps:

1. Issue a `Get-MgBetaDirectorySetting | FL` cmdlet and check the ID. If several ID values are present, use the one where you see the `EnableMIPLabels` property on the **Values** settings.
2. Issue the `Update-MgBetaDirectorySetting` cmdlet by using the ID that you retrieved.

You also need to synchronize your sensitivity labels to Microsoft Entra ID. For instructions, see [Enable sensitivity labels for containers and synchronize labels](/en-us/purview/sensitivity-labels-teams-groups-sites#how-to-enable-sensitivity-labels-for-containers-and-synchronize-labels).

# [21Vianet](#tab/21Vianet)
If you're performing these Microsoft 365 operations from 21Vianet:

1. Register a Microsoft Entra ID application in Microsoft Entra ID.
2. Grant your application API permissions to access Microsoft Graph including `Directory.ReadWriteAll` and `Group.ReadWriteAll`, you might need to get tenant admin's explicit consent to grant the application access to Microsoft Graph.
3. Generate a client secret and copy it. You need the client secret to connect to Microsoft Graph.
4. Run PowerShell as administrator:

    ```PowerShell
    $ClientSecretCredential = Get-Credential -Credential
    ```

    After commands run, you'll be prompted to enter a password. The password is the new client secret you copied in an earlier step.
5. Run the following command to get access to Microsoft Graph:

    ```PowerShell
    Connect-MgGraph -TenantId "Current tenant id" -ClientSecretCredential $ClientSecretCredential -Environment China
    ```
6. Fetch the current group settings for the Microsoft Entra organization and display the current group settings.

    ```powershell
    $grpUnifiedSetting = Get-MgBetaDirectorySetting -Search DisplayName:"Group.Unified"
    ```

    If no group settings were created for this Microsoft Entra organization, you get an empty screen. In this case, you must first create the settings. Follow the steps in [Microsoft Entra cmdlets for configuring group settings](groups-settings-cmdlets) to create group settings for this Microsoft Entra organization.

    Note

    If the sensitivity label was enabled previously, you see `EnableMIPLabels = True`. In this case, you don't need to do anything. Also make sure that `EnableGroupCreation = False` if you don't want non-admin users to be able to create groups. See [Template settings](groups-settings-cmdlets#template-settings) for details.
7. Apply the new settings.

    ```powershell
    $params = @{
         Values = @(
     	    @{
     		    Name = "EnableMIPLabels"
     		    Value = "True"
     	    }
         )
    }
    
    Update-MgBetaDirectorySetting -DirectorySettingId $grpUnifiedSetting.Id -BodyParameter $params
    ```
8. Verify that the new value is present.

    ```powershell
    $Setting = Get-MgBetaDirectorySetting -DirectorySettingId $grpUnifiedSetting.Id
    $Setting.Values
    ```

If you receive a `Request_BadRequest` error, it's because the settings already exist in the tenant. When you try to create a new `property:value` pair, the result is an error. In this case, follow these steps:

1. Issue a `Get-MgBetaDirectorySetting | FL` cmdlet and check the ID. If several ID values are present, use the one where you see the `EnableMIPLabels` property on the **Values** settings.
2. Issue the `Update-MgBetaDirectorySetting` cmdlet by using the ID that you retrieved.

You also need to synchronize your sensitivity labels to Microsoft Entra ID. For instructions, see [Enable sensitivity labels for containers and synchronize labels](/en-us/purview/sensitivity-labels-teams-groups-sites#how-to-enable-sensitivity-labels-for-containers-and-synchronize-labels).

---

## Assign a label to a new group in the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Select **Microsoft Entra ID**.
3. Select **Groups** &gt; **All groups** &gt; **New group**.
4. On the **New Group** page, select **Microsoft 365**. Then fill out the required information for the new group and select a sensitivity label from the list.

    ![Screenshot that shows assigning a sensitivity label on the New groups page.](media/groups-assign-sensitivity-labels/new-group-page.png)
5. Select **Create** to save your changes.

Your group is created and the site and group settings associated with the selected label are then automatically enforced.

## Assign a label to an existing group in the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Select **Microsoft Entra ID**.
3. Select **Groups**.
4. From the **All groups** page, select the group that you want to label.
5. On the selected group's page, select **Properties** and select a sensitivity label from the list.

    ![Screenshot that shows assigning a sensitivity label on the overview page for a group.](media/groups-assign-sensitivity-labels/assign-to-existing.png)
6. Select **Save** to save your changes.

## Remove a label from an existing group in the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Select **Microsoft Entra ID**.
3. Select **Groups** &gt; **All groups**.
4. On the **All groups** page, select the group that you want to remove the label from.
5. On the **Group** page, select **Properties**.
6. Select **Remove**.
7. Select **Save** to apply your changes.

## Use classic Microsoft Entra classifications

After you enable this feature, the "classic" classifications for groups appear only on existing groups and sites. You should use them for new groups only if you create groups in apps that don't support sensitivity labels. Your admin can convert them to sensitivity labels later, if needed. Classic classifications are the old classifications you set up previously. When this feature is enabled, those classifications aren't applied to groups.

## Troubleshoot issues

This section offers troubleshooting tips for common issues.

### Sensitivity labels aren't available for assignment on a group

The sensitivity label option appears for groups only when all the following conditions are met:

1. The organization has an active Microsoft Entra ID P1 license.
2. The feature is enabled and `EnableMIPLabels` is set to **True** in the Microsoft Graph PowerShell module.
3. The sensitivity labels are published in the Microsoft Purview portal or the Microsoft Purview portal for this Microsoft Entra organization.
4. Labels are synchronized to Microsoft Entra ID with the `Execute-AzureAdLabelSync` cmdlet in the Security & Compliance PowerShell module. It can take up to 24 hours after synchronization for the label to be available to Microsoft Entra ID.
5. The [sensitivity label scope](/en-us/purview/sensitivity-labels?preserve-view=true&amp;view=o365-worldwide#label-scopes) must be configured for Groups & Sites.
6. The group is a Microsoft 365 group.
7. The current signed-in user:
    1. Has sufficient privileges to assign sensitivity labels. The user must be the group owner or at least a Groups Administrator.
    2. Must be within the scope of the [sensitivity label publishing policy](/en-us/purview/sensitivity-labels?preserve-view=true&amp;view=o365-worldwide#what-label-policies-can-do).

Make sure all the preceding conditions are met to assign labels to a group.

### The label you want to assign isn't in the list

If the label you're looking for isn't in the list:

- The label might not be published in the Microsoft Purview portal. Also, the label might no longer be published. Check with your administrator for more information.
- The label might be published, but it isn't available to the user who is signed in. Check with your administrator for more information on how to get access to the label.

### Change the label on a group

Labels can be swapped at any time by using the same steps as assigning a label to an existing group:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Select **Microsoft Entra ID**.
3. Select **Groups** &gt; **All groups**, and then select the group that you want to label.
4. On the selected group's page, select **Properties** and select a new sensitivity label from the list.
5. Select **Save**.

### Group setting changes to published labels aren't updated on the groups

When you make changes to group settings for a published label in the [Microsoft Purview portal](https://purview.microsoft.com/), those policy changes aren't automatically applied on the labeled groups. After the sensitivity label is published and applied to groups, Microsoft recommends that you don't change the group settings for the label in the portal.

If you must make a change, use a [PowerShell script](https://github.com/microsoftgraph/powershell-aad-samples/blob/master/ReassignSensitivityLabelToO365Groups.ps1) to manually apply updates to the affected groups. This method makes sure that all existing groups enforce the new setting.