---
layout: Conceptual
title: How to use the BypassDirSyncOverridesEnabled feature of a Microsoft Entra tenant - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-bypassdirsyncoverrides
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Describes how to use BypassDirSyncOverridesEnabled tenant feature to restore synchronization of Mobile and OtherMobile attributes from on-premises Active Directory.
ms.date: 2025-04-09T00:00:00.0000000Z
ms.topic: how-to
ms.custom: no-azure-ad-ps-ref, sfi-ga-nochange
ms.subservice: hybrid-connect
locale: en-us
document_id: a6cb547b-5c9f-4a5e-87c6-6705a17bb5a2
document_version_independent_id: edd3b439-9f25-79a6-6621-d453783828eb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-bypassdirsyncoverrides.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-bypassdirsyncoverrides
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-bypassdirsyncoverrides.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: a84973aa-122a-8e1d-ff0a-1fb8d22face7
---

# How to use the BypassDirSyncOverridesEnabled feature of a Microsoft Entra tenant - Microsoft Entra ID | Microsoft Learn

This article describes the *BypassDirSyncOverridesEnabled* feature and how to restore synchronization of *mobile* and *otherMobile* attributes from Microsoft Entra ID to on-premises Active Directory.

Synchronized users properties cannot be changed from Microsoft Entra ID or Microsoft 365 admin portals, neither through any available PowerShell modules. Up until recently, the exception to this was the Microsoft Entra user’s attributes called *MobilePhone* and *AlternateMobilePhones*. These attributes are synchronized from on-premises Active Directory attributes *mobile* and *otherMobile*, respectively, but end users used to be able to update their own phone number in *MobilePhone* attribute in Microsoft Entra ID through their profile page. Changes to *MobilePhone* and *AlternateMobilePhones* attributes are no longer possible for Synchronized users except through the use of Microsoft Entra Connect or Microsoft Entra Cloud Sync.

Previously, administrators and synchronized users had the capability to update the values of the *MobilePhone* and *AlternateMobilePhones* attributes in Microsoft Entra ID. This is no longer possible for synchronized users. When this was possible the synchronization API was not honoring updates to these attributes when they originated from on-premises Active Directory. This was commonly known as a “DirSyncOverrides” feature. Administrators noticed this behavior when updates to *mobile* or *otherMobile* attributes in Active Directory did not update the corresponding user’s *MobilePhone* or *AlternateMobilePhones* in Microsoft Entra ID accordingly, even though the object was successfully synchronized through Microsoft Entra Connect's engine.

## Identifying users with different Mobile values

You can export a list of users with different Mobile values between Active Directory and Microsoft Entra ID using *‘Compare-ADSyncToolsDirSyncOverrides’* from *ADSyncTools* PowerShell module. This will allow you to determine the users and respective values that are different between on-premises Active Directory and Microsoft Entra ID. This is important to know because enabling the BypassDirSyncOverridesEnabled feature will overwrite all the different values in Microsoft Entra ID with the value coming from on-premises Active Directory.

### Using Compare-ADSyncToolsDirSyncOverrides

As a prerequisite you need to be running Microsoft Entra Connect version 2 or later and install the latest ADSyncTools module from PowerShell Gallery with the following command:

```powershell
Install-Module ADSyncTools 
```

To compare all the synchronized user’s Mobile values, run the following command:

```powershell
Compare-ADSyncToolsDirSyncOverrides
```

This function will export a CSV file with a list of users where Mobile values in on-premises Active Directory are different than the respective *MobilePhone* in Microsoft Entra ID.

At this stage you can use this data to reset the values of the on-premises Active Directory *Mobile* properties to the values that are present in Microsoft Entra ID. This way you can capture the most updated phone numbers from Microsoft Entra ID and persist this data in on-premises Active Directory, before enabling *BypassDirSyncOverridesEnabled* feature. To do this, import the data from the resulting CSV file and then use the *'Set-ADSyncToolsDirSyncOverrides'* from *ADSyncTools* module to persist the value in on-premises Active Directory.

For example, to import data from the CSV file and extract the values in Microsoft Entra ID for a given UserPrincipalName, use the following command:

```powershell
$upn = '<UserPrincipalName>' 
$user = Import-Csv 'ADSyncTools-DirSyncOverrides_yyyyMMMdd-HHmmss.csv' | where UserPrincipalName -eq $upn | select UserPrincipalName,MobileInEntra  
Set-ADSyncToolsDirSyncOverridesUser -Identity $upn -MobileInAD $user.MobileInEntra
```

## Enabling BypassDirSyncOverridesEnabled feature

By default, *BypassDirSyncOverridesEnabled* feature is turned off. Enabling *BypassDirSyncOverridesEnabled* allows your tenant to bypass any changes made earlier in *MobilePhone* or *AlternateMobilePhones* by users or admins directly in Microsoft Entra ID and honor the values present in on-premises Active Directory *Mobile* or *OtherMobile*.

### Enable the BypassDirSyncOverridesEnabled feature:

To enable BypassDirSyncOverridesEnabled feature, use the [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/overview) module.

```powershell
Connect-MgGraph -Scopes "Directory.ReadWrite.All"
$directorySynchronization = Get-MgDirectoryOnPremiseSynchronization
$directorySynchronization.Features.BypassDirSyncOverridesEnabled = $true
Update-MgDirectoryOnPremiseSynchronization -OnPremisesDirectorySynchronizationId $directorySynchronization.Id -Features $directorySynchronization.Features
```

### Verify the status of the BypassDirSyncOverridesEnabled feature:

```powershell
(Get-MgDirectoryOnPremiseSynchronization).Features.BypassDirSyncOverridesEnabled
```

Once the feature is enabled, start a full synchronization cycle in Microsoft Entra Connect using the following command:

```powershell
Start-ADSyncSyncCycle -PolicyType Initial
```

Note

Only objects with a different *MobilePhone* or *AlternateMobilePhones* value from on-premises Active Directory will be updated.

## Managing mobile phone numbers in Microsoft Entra ID and on-premises Active Directory

To manage the user’s phone numbers, an admin can use the following set of functions from *ADSyncTools* module to read, write and clear the values in on-premises Active Directory, and to read *mobilePhone* from Microsoft Entra ID.

### Get *Mobile* property from on-premises Active Directory:

```powershell
Get-ADSyncToolsDirSyncOverridesUser 'User1@Contoso.com' -FromAD
```

### Get *MobilePhone* property from Microsoft Entra ID:

```powershell
Get-ADSyncToolsDirSyncOverridesUser 'User1@Contoso.com' -FromEntraID
```

### Set *Mobile* property in on-premises Active Directory:

```powershell
Set-ADSyncToolsDirSyncOverridesUser 'User1@Contoso.com' -MobileInAD '999888777'
```

### Clear *Mobile* property in on-premises Active Directory:

```powershell
Clear-ADSyncToolsDirSyncOverridesUser 'User1@Contoso.com'
```