---
layout: Conceptual
title: 'Microsoft Entra Connect: Migrate groups from one forest to another - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-migrate-groups
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes the steps needed to successfully migrate groups from one forest to another for Microsoft Entra Connect.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 09f38b6b-f87a-121d-873a-c3473af2e626
document_version_independent_id: 1dc80eb3-ae22-dc8a-5e7a-1aaf53a2ba87
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-migrate-groups.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-migrate-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-migrate-groups.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: f492db12-64be-9b8a-a14d-3300c0c9fbe1
---

# Microsoft Entra Connect: Migrate groups from one forest to another - Microsoft Entra ID | Microsoft Learn

This article describes how to migrate groups from one forest to another so that the migrated group objects match the existing objects in the cloud.

## Prerequisites

- Microsoft Entra Connect version 1.5.18.0 or later
- Source anchor attribute set to `mS-DS-ConsistencyGuid`

## Migrate groups

Starting in version 1.5.18.0, Microsoft Entra Connect supports the use of the `mS-DS-ConsistencyGuid` attribute for groups. If you choose `mS-DS-ConsistencyGuid` as the source anchor attribute and the value is populated in Active Directory, Microsoft Entra Connect uses the value of `mS-DS-ConsistencyGuid` as the `immutableId`. Otherwise, it falls back to using `objectGUID`. But note that Microsoft Entra Connect doesn't write the value back to the `mS-DS-ConsistencyGuid` attribute in Active Directory.

During a cross-forest move, when a group object is moving from one forest (say F1) to another forest (say F2), you need to copy either the `mS-DS-ConsistencyGuid` value (if it's present) or the `objectGUID` value from the object in forest F1 to the `mS-DS-ConsistencyGuid` attribute of the object in F2.

Use the following scripts as a guide to learn how to migrate a single group from one forest to another. You can also use these scripts as a guide for the migration of multiple groups. The scripts use the forest name F1 for the source forest and F2 for the destination forest.

First, we get the `objectGUID` and `mS-DS-ConsistencyGuid` of the group object in forest F1. These attributes are exported to a CSV file.

```
<#
DESCRIPTION
============
This script will take DN of a group as input.
It then copies the objectGUID and mS-DS-ConsistencyGuid values along with other attributes of the given group to a CSV file.

This CSV file can then be used as input to the Export-Group script.
#>
Param(
       [ValidateNotNullOrEmpty()]
       [string]
       $dn,

       [ValidateNotNullOrEmpty()]
       [string]
       $outputCsv
)

$defaultProperties = @('samAccountName', 'distinguishedName', 'objectGUID', 'mS-DS-ConsistencyGuid')
$group  = Get-ADGroup -Filter "DistinguishedName -eq '$dn'" -Properties $defaultProperties -ErrorAction Stop
$results = @()
if ($group -eq $null)
{
       Write-Error "Group not found"
}
else
{
       $objectGUIDValue = [GUID]$group.'objectGUID'
       $mSDSConsistencyGuidValue = "N/A"
       if ($group.'mS-DS-ConsistencyGuid' -ne $null)
       {
              $mSDSConsistencyGuidValue = [GUID]$group.'mS-DS-ConsistencyGuid'
       }
       $adgroup = New-Object -TypeName PSObject
       $adgroup | Add-Member -MemberType NoteProperty -Name samAccountName -Value $($group.'samAccountName')
       $adgroup | Add-Member -MemberType NoteProperty -Name distinguishedName -Value $($group.'distinguishedName')
       $adgroup | Add-Member -MemberType NoteProperty -Name objectGUID -Value $($objectGUIDValue)
       $adgroup | Add-Member -MemberType NoteProperty -Name mS-DS-ConsistencyGuid -Value $($mSDSConsistencyGuidValue)
       $results += $adgroup
}

Write-Host "Exporting group to output file"
$results | Export-Csv "$outputCsv" -NoTypeInformation

```

Next, we use the generated output CSV file to stamp the `mS-DS-ConsistencyGuid` attribute on the target object in forest F2:

```
<#
DESCRIPTION
============
This script will take DN of a group as input and the CSV file that was generated by the Import-Group script.
It copies either the objectGUID or the mS-DS-ConsistencyGuid value from the CSV file to the given object.

#>
Param(
       [ValidateNotNullOrEmpty()]
       [string]
       $dn,

       [ValidateNotNullOrEmpty()]
       [string]
       $inputCsv
)

$group  = Get-ADGroup -Filter "DistinguishedName -eq '$dn'" -ErrorAction Stop
if ($group -eq $null)
{
       Write-Error "Group not found"
}

$csvFile = Import-Csv -Path $inputCsv -ErrorAction Stop
$msDSConsistencyGuid = $csvFile.'mS-DS-ConsistencyGuid'
$objectGuid = [GUID] $csvFile.'objectGUID'
$targetGuid = $msDSConsistencyGuid

if ($msDSConsistencyGuid -eq "N/A")
{
       $targetGuid = $objectGuid
}

Set-ADGroup -Identity $dn -Replace @{'mS-DS-ConsistencyGuid'=$targetGuid} -ErrorAction Stop

```