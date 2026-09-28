---
layout: Conceptual
title: Fix problems with dynamic membership groups - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-troubleshooting
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Troubleshooting tips for dynamic membership groups in Microsoft Entra ID
ms.topic: troubleshooting
ms.date: 2025-01-15T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro
locale: en-us
document_id: a360d153-0892-fd9f-83e5-a4128fbfb557
document_version_independent_id: d996e375-9dbc-db5a-c639-7da7616bc3bb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-troubleshooting.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-troubleshooting
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-troubleshooting.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f40a8e70-bb9b-0644-6d5f-524a7e35aee3
---

# Fix problems with dynamic membership groups - Microsoft Entra ID | Microsoft Learn

## Overview

This article contains troubleshooting information for groups in Microsoft Entra ID, part of Microsoft Entra.

## Troubleshoot group creation issues

**I disabled security group creation in the Azure portal but groups can still be created via PowerShell** The **User can create security groups in Azure portals** setting in the Azure portal controls whether or not non-admin users can create security groups in the Access panel or the Azure portal. It doesn't control security group creation via PowerShell.

To disable group creation for nonadmin users in PowerShell:

1. Verify that nonadmin users are allowed to create groups:

    ```powershell
    Get-MgBetaDirectorySetting | select -ExpandProperty values
    ```
2. If it returns `EnableGroupCreation : True`, then nonadmin users can create groups. To disable this feature:

    ```powershell
    Install-Module Microsoft.Graph.Beta.Identity.DirectoryManagement
    Import-Module Microsoft.Graph.Beta.Identity.DirectoryManagement
    $params = @{
    TemplateId = "62375ab9-6b52-47ed-826b-58e47e0e304b"
    Values = @(    
     @{
       Name = "EnableGroupCreation"
       Value = "false"
     }    
    )
     }
    Connect-MgGraph -Scopes "Directory.ReadWrite.All"
    New-MgBetaDirectorySetting -BodyParameter $params
    ```

**I received a max groups allowed error when trying to create a Dynamic Group in PowerShell**

The max number of dynamic groups per organization is 5,000. When you reach the maximum number of dynamic groups in your organization, you receive a message in PowerShell that says *Dynamic group policies max allowed groups count reached*.

If you run into this limit, to create any new dynamic groups, you first need to delete some existing dynamic groups. There's no way to increase the limit.

## Troubleshoot dynamic membership groups

**I configured a rule on a group but no memberships get updated in the group**

1. Verify the values for user or device attributes in the rule. Ensure there are users that satisfy the rule. For devices, check the device properties to ensure any synced attributes contain the expected values.
2. Check the membership processing status to confirm if it's complete. You can check the [membership processing status](groups-create-rule#check-the-processing-status-for-a-rule) and the last updated date on the **Overview** page for the group.

If everything looks good, allow some time for the group to populate. Depending on the size of your Microsoft Entra organization, the group could take up to 24 hours for populating for the first time or after a rule change.

**I configured a rule, but now the existing members of the rule are removed** This is expected behavior. Existing members of the group are removed when a rule is enabled or changed. Not all existing members are deleted, only users who no longer meet the new rule. The users returned from evaluation of the new rule are added as members to the group. Users who meet both existing rules and new rules remain in the dynamic group. Their license assignments aren't temporarily deleted and their role assignments aren't removed.

**I don't see membership changes instantly when I add or change a rule, why not?**

Dedicated membership evaluation is done periodically in an asynchronous background process. Both the number of users in your directory and the size of the resulting group affect processing time.

Typically, directories with small numbers of users see the dynamic membership group changes in less than a few minutes. Directories with a large number of users can take 30 minutes or longer to populate.

**How can I force the group to be processed now?** Currently, there's no way to automatically trigger the group to be processed on demand. However, you can manually trigger the reprocessing by updating the membership rule to add a whitespace at the end.

**I encountered a rule processing error** The following table lists common rule errors for dynamic membership groups and how to correct them.

| Rule parser error | Error usage | Corrected usage |
| --- | --- | --- |
| Error: Attribute not supported. | (user.invalidProperty -eq "Value") | (user.department -eq "value")Make sure the attribute is on the [supported properties list](groups-dynamic-membership#supported-properties). |
| Error: Operator isn't supported on attribute. | (user.accountEnabled -contains true) | (user.accountEnabled -eq true)The operator used isn't supported for the property type (in this example, -contains can't be used on type boolean). Use the correct operators for the property type. |
| Error: Query compilation error. | 1. (user.department -eq "Sales") (user.department -eq "Marketing")2. (user.userPrincipalName -match "\*@domain.ext") | 1. Missing operator. Use -and or -or to join predicates(user.department -eq "Sales") -or (user.department -eq "Marketing")2. Error in regular expression used with -match(user.userPrincipalName -match ".\*@domain.ext")or alternatively: (user.userPrincipalName -match "@domain.ext$") |