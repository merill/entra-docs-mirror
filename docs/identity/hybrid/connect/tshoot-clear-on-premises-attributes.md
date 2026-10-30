---
layout: Conceptual
title: 'Microsoft Entra Connect: Clear on-premises attributes from migrated Microsoft Entra ID users - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/tshoot-clear-on-premises-attributes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to clean up on-premises attributes from migrated users in Microsoft Entra ID.
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: has-adal-ref, has-azure-ad-ps-ref
locale: en-us
document_id: 9a2ad0b9-b07f-58e7-23c4-ec151da0ec27
document_version_independent_id: 9a2ad0b9-b07f-58e7-23c4-ec151da0ec27
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/tshoot-clear-on-premises-attributes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/tshoot-clear-on-premises-attributes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/tshoot-clear-on-premises-attributes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 97edacc4-2717-bb24-1dfd-af379e57fee7
---

# Microsoft Entra Connect: Clear on-premises attributes from migrated Microsoft Entra ID users - Microsoft Entra ID | Microsoft Learn

After migrating your users and groups to Microsoft Entra ID, you might be ready to decommission your on-premises Active Directory and uninstall sync tools. After turning off directory synchronization, you can manage these objects directly in Microsoft Entra ID.

However, you may encounter issues in Windows, Intune, and Outlook due to legacy values remaining in the user attributes that were previously synchronized from on-premises. For example, hybrid device joining may fail because the system pulls the username and domain from these outdated attributes.

To prevent these issues, we recommend that customers clear the following on-premises attributes:

- onPremisesDistinguishedName
- onPremisesDomainName
- onPremisesImmutableId
- onPremisesObjectIdentifier
- onPremisesSamAccountName
- onPremisesSecurityIdentifier
- onPremisesUserPrincipalName

## How to update these attributes

You can update these attributes via Microsoft Graph Beta with [Update User](/en-us/graph/api/user-update) API call. You can update these attributes in Microsoft Entra ID only for Cloud‑Only users. This includes users that were previously synchronized and later converted to Cloud‑Only when tenant synchronization was disabled.

### Required roles

The Entra ID roles that can update on-premises attributes are:

- [User Administrator](../../role-based-access-control/permissions-reference#user-administrator)
- [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator)

### Required permissions

The required application permissions are **User.ReadWrite.All** and **User-OnPremisesSyncBehavior.ReadWrite.All** (the latter is required specifically for the **onPremisesObjectIdentifier** attribute).

## Using ADSyncTools PowerShell module

You can also view and update these on-premises attributes with the PowerShell scripts provided.

### Prerequisites for managing on-premises attributes with ADSyncTools PowerShell module:

- [Windows PowerShell 7](/en-us/powershell/scripting/install/installing-powershell-on-windows)
- [Microsoft Graph SDK PowerShell module](/en-us/powershell/microsoftgraph/installation)

Install the [ADSyncTools](reference-connect-adsynctools) module from PowerShell Gallery:

```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 
Install-Module ADSyncTools # If ADSyncTools isn’t installed, or; 
Update-Module ADSyncTools # If ADSyncTools is already installed 
```

Note

The minimum required version to manage on-premises attributes in Entra ID is v2.5.0.

Use the following commands to get started with ADSyncTools.

```powershell
Import-Module ADSyncTools 
```

See the cmdlets available for managing on-premises attributes:

```powershell
Get-Command *onpremises* -Module ADSyncTools 
```

Result:

```
CommandType   Name                      Version  Source 
-----------   ----                      -------  ------ 
Function    Clear-ADSyncToolsOnPremisesAttribute      2.5.0   ADSyncTools 
Function    Get-ADSyncToolsOnPremisesAttribute       2.5.0   ADSyncTools 
Function    Set-ADSyncToolsOnPremisesAttribute       2.5.0   ADSyncTools 

```

Get all the details of a cmdlet (for example, Syntax and Examples) with Get-Help &lt;cmdlet&gt; -Full:

`Get-Help Get-ADSyncToolsOnPremisesAttribute -Full `

## Get-ADSyncToolsOnPremisesAttribute

### Description

Gets a specific user or all users containing on-premises properties in Entra ID. It only returns the users that have on-premises attributes populated. By Default, it returns all cloud-only users, but you can specify `-IncludeSyncedUsers` to return all users, including users synced from on-premises AD.

This operation requires Microsoft Graph PowerShell SDK, preauthenticated with `Connect-MgGraph -Scopes "User.ReadWrite.All, User-OnPremisesSyncBehavior.ReadWrite.All"`

### SYNTAX

#### By Identity

```powershell
 Get-ADSyncToolsOnPremisesAttribute [-Id] <String> [[-Property] <String[]>] [<CommonParameters>] 
```

#### By IncludeSyncedUsers

```powershell
Get-ADSyncToolsOnPremisesAttribute [[-IncludeSyncedUsers]] [[-Property] <String[]>] [<CommonParameters>] 
```

### EXAMPLES

#### Example 1

Get the on-premises attributes of all cloud-users that have on-premises attributes populated.

```powershell
Get-ADSyncToolsOnPremisesAttribute 
```

### Clearing all on-premises attributes for all users

To clear all on-premises attributes from all users in a bulk fashion, use the get function to retrieve a list of all cloud-only users containing on-premises attributes and then pipeline the results to the Clear cmdlet adding the parameter -All.

This operation requires Microsoft Graph PowerShell SDK, preauthenticated with `Connect-MgGraph -Scopes "User.ReadWrite.All, User-OnPremisesSyncBehavior.ReadWrite.All"`

Important

Before clearing on‑premises attributes from Entra ID users in production, back up the user’s on‑premises properties so that you can roll back the operation if needed.

You can back up all the current values with the following command:

```powershell
Get-ADSyncToolsOnPremisesAttribute | Export-Csv backupOnpremisesAttributes.csv -Delimiter ';' 
```

To clear all on-premises attributes from all users, run:

```powershell
Get-ADSyncToolsOnPremisesAttribute | Select-Object id | Clear-ADSyncToolsOnPremisesAttribute -All -Verbose 
```

### Clearing all on-premises attributes for one user

To clear all on-premises attributes for one particular user, specify the objectId or UserPrincipalName followed by the parameter -All.

This operation requires Microsoft Graph PowerShell SDK, preauthenticated with `Connect-MgGraph -Scopes "User.ReadWrite.All, User-OnPremisesSyncBehavior.ReadWrite.All"`

```powershell
Clear-ADSyncToolsOnPremisesAttribute 'User1@Contoso.com' -All 
```

You can also use `Clear-ADSyncToolsOnPremisesAttribute ` to clear any of the following on-premises attributes individually:

- onPremisesDistinguishedName
- onPremisesDomainName
- onPremisesImmutableId
- onPremisesObjectIdentifier
- onPremisesSamAccountName
- onPremisesSecurityIdentifier
- onPremisesUserPrincipalName

## Clear-ADSyncToolsOnPremisesAttribute

### Description

Clears the on-premises properties of a specific Cloud-Only user or all CLoud-Only users in Entra ID.

### SYNTAX

```powershell
 Clear-ADSyncToolsOnPremisesAttribute [-Id] <String> [[-onPremisesDistinguishedName]] [[-onPremisesDomainName]] [[-onPremisesImmutableId]] 
[[-onPremisesObjectIdentifier]] [[-onPremisesSamAccountName]] [[-onPremisesSecurityIdentifier]] [[-onPremisesUserPrincipalName]] [<CommonParameters>] 
```

#### By BodyParameter

```powershell
 Clear-ADSyncToolsOnPremisesAttribute [-Id] <String> [-BodyParameter] <String> [<CommonParameters>] 
```

#### By All

```powershell
 Clear-ADSyncToolsOnPremisesAttribute [-Id] <String> [-All] [<CommonParameters>] 
```

#### Example 1

Clear only onPremisesImmutableId attribute

```powershell
 Clear-ADSyncToolsOnPremisesAttribute -Id '12345678-90ab-cd12-3456-7890abcd1234' -onPremisesImmutableId
```

#### Example 2

Clear on-premises attributes based on a json parameter body (-BodyParameter)

```powershell
$jsonBody = @'
{ 
  "onPremisesDistinguishedName": null, 
  "onPremisesDomainName": null, 
  "onPremisesImmutableId": null, 
  "onPremisesObjectIdentifier": null, 
  "onPremisesSamAccountName": null, 
  "onPremisesSecurityIdentifier": null, 
  "onPremisesUserPrincipalName": null 
} 
'@ 

Clear-ADSyncToolsOnPremisesAttribute -Id $userId -BodyParameter $jsonBody

```

## Set-ADSyncToolsOnPremisesAttribute

Sets on-premises attributes for a Cloud-Only user in Entra ID.

This operation requires Microsoft Graph PowerShell SDK, preauthenticated with `Connect-MgGraph -Scopes "User.ReadWrite.All, User-OnPremisesSyncBehavior.ReadWrite.All"`

Important

Before updating on‑premises attributes for Entra ID users in production, back up the user’s on‑premises properties so that you can roll back the operation if needed.

You can back up all the current values with the following command:

```powershell
Get-ADSyncToolsOnPremisesAttribute | Export-Csv backupOnpremisesAttributes.csv -Delimiter ';' 
```

This function can be used to set any of the following on-premises attributes:

- onPremisesDistinguishedName
- onPremisesDomainName
- onPremisesImmutableId
- onPremisesObjectIdentifier \*
- sonPremisesSamAccountName
- onPremisesSecurityIdentifier \*\*
- onPremisesUserPrincipalName

    \* System-generated attribute. Clearing it is supported, but setting a specific value can fail depending on service behavior.

    \*\* Must have the correct Security Identifier format, for example: "S-1-5-21-1234567890-0987654321-1234567890-1111"

### SYNTAX

```powershell
Set-ADSyncToolsOnPremisesAttribute [-Id] <String> [[-onPremisesDistinguishedName] <String>] [[-onPremisesDomainName] <String>] [[-onPremisesImmutableId] <String>] [[-onPremisesSamAccountName] <String>] [[-onPremisesSecurityIdentifier] <String>] [[-onPremisesUserPrincipalName] <String>] [<CommonParameters>] 
```

#### By BodyParameter

```powershell
Set-ADSyncToolsOnPremisesAttribute [-Id] <String> [-BodyParameter] <String> [<CommonParameters>] 
```

### EXAMPLES

#### Example 1

Set only onPremisesImmutableId (pipelining)

```powershell
'User1@Contoso.com' | Set-ADSyncToolsOnPremisesAttribute -onPremisesImmutableId 'nofCJe0gZk6D8J4gRgrt+A==' 
```

#### Example 2

Set on-premises attributes based on a json parameter body (-BodyParameter)

```powershell
$jsonBody = @' 
{ 
  "onPremisesDistinguishedName": "User1@Contoso.com", 
  "onPremisesDomainName": 'Contoso.com', 
  "onPremisesImmutableId": 'nofCJe0gZk6D8J4gRgrt+A==', 
  "onPremisesSamAccountName": 'User1', 
  "onPremisesSecurityIdentifier": "S-1-5-21-4097605469-3104078553-1111111111-1111", 
  "onPremisesUserPrincipalName": "User1@Contoso.com" 
}
'@
Set-ADSyncToolsOnPremisesAttribute -Id '11111111-2222-3333-4444-555555555555' -BodyParameter $jsonBody
```

Note

You can use `-Verbose` with any command to show additional details as to what the function is doing.