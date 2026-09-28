---
layout: Conceptual
title: PowerShell sample - List Microsoft Entra Backup and Recovery snapshots for Global Secure Access recovery | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/scripts/powershell-get-entra-snapshot
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: List Microsoft Entra Backup and Recovery snapshots that can help recover directory objects used by Global Secure Access.
ms.topic: sample
ms.date: 2026-06-17T00:00:00.0000000Z
ms.reviewer: tdetzner
ai-usage: ai-assisted
locale: en-us
document_id: 8fb32e6e-3eab-bd30-7d2f-aab6126ceeeb
document_version_independent_id: 8fb32e6e-3eab-bd30-7d2f-aab6126ceeeb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/scripts/powershell-get-entra-snapshot.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/scripts/powershell-get-entra-snapshot
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/scripts/powershell-get-entra-snapshot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
platformId: 220d90c6-e151-f3f2-1d38-8609c3a63262
---

# PowerShell sample - List Microsoft Entra Backup and Recovery snapshots for Global Secure Access recovery | Microsoft Learn

This script lists Microsoft Entra Backup and Recovery snapshots for the tenant. Use the latest snapshot ID as input to the recovery preview script before you execute a recovery.

The Microsoft Entra Backup and Recovery APIs are in Microsoft Graph beta. Validate permissions and behavior in your tenant before you depend on these APIs in an operations process.

## Prerequisites

- PowerShell 7.0 or later.
- Install the modules listed in the script's `.NOTES` block.
- Use only permissions and roles that your organization has approved for the task.

## Script

```powershell
<#
.SYNOPSIS
    Lists Microsoft Entra Backup and Recovery snapshots for the tenant.
.DESCRIPTION
    Queries the Microsoft Entra Backup and Recovery service (beta) for available
    tenant snapshots. Microsoft Entra automatically creates one snapshot per day
    and retains up to five. Use the returned snapshot IDs as input to
    Start-GsaEntraRecoveryPreview.ps1.

    Output is PowerShell objects suitable for pipeline use. The latest snapshot
    (by creation date) is highlighted in the Latest property.
.PARAMETER TenantId
    Target Microsoft Entra tenant ID. Omit when running under managed identity
    in the same tenant.
.PARAMETER ClientId
    App registration client ID. Required with CertificateThumbprint.
.PARAMETER CertificateThumbprint
    Certificate thumbprint for service principal authentication.
.PARAMETER UseManagedIdentity
    Authenticate using the current managed identity. Use in Azure Automation.
.EXAMPLE
    .\Get-GsaEntraSnapshot.ps1 -UseManagedIdentity
.EXAMPLE
    .\Get-GsaEntraSnapshot.ps1 -TenantId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" -ClientId "yyyy" -CertificateThumbprint "ZZZZ"
.NOTES
    Required Graph permissions:
        EntraBackup.Read.All (application or delegated)
    Required Entra role:
        Entra Backup Reader
    Minimum module versions:
        Microsoft.Graph.Authentication 2.x
    Beta API: subject to change per Microsoft Graph versioning policy.
    Reference: https://learn.microsoft.com/en-us/graph/api/resources/entrarecoveryservices-backup-recovery-overview?view=graph-rest-beta
    Author: GSA Operations
#>

[CmdletBinding(DefaultParameterSetName = 'Interactive')]
[OutputType([pscustomobject])]
param(
    [Parameter(ParameterSetName = 'ServicePrincipal', Mandatory)]
    [Parameter(ParameterSetName = 'Interactive')]
    [string]$TenantId,

    [Parameter(ParameterSetName = 'ServicePrincipal', Mandatory)]
    [string]$ClientId,

    [Parameter(ParameterSetName = 'ServicePrincipal', Mandatory)]
    [string]$CertificateThumbprint,

    [Parameter(ParameterSetName = 'ManagedIdentity', Mandatory)]
    [switch]$UseManagedIdentity
)

$ErrorActionPreference = 'Stop'

# Authenticate
try {
    switch ($PSCmdlet.ParameterSetName) {
        'ManagedIdentity'  { Connect-MgGraph -Identity -NoWelcome | Out-Null }
        'ServicePrincipal' { Connect-MgGraph -TenantId $TenantId -ClientId $ClientId -CertificateThumbprint $CertificateThumbprint -NoWelcome | Out-Null }
        default            { Connect-MgGraph -TenantId $TenantId -Scopes 'EntraBackup.Read.All' -NoWelcome | Out-Null }
    }
    Write-Verbose "Connected to Microsoft Graph."
} catch {
    throw "Failed to authenticate to Microsoft Graph: $_"
}

# List snapshots
try {
    $uri      = 'https://graph.microsoft.com/beta/directory/recovery/snapshots'
    $response = Invoke-MgGraphRequest -Method GET -Uri $uri
    $snapshots = @($response.value)
} catch {
    throw "Failed to retrieve snapshots. Verify the Entra Backup Reader role and EntraBackup.Read.All permission. Error: $_"
}

if ($snapshots.Count -eq 0) {
    Write-Warning "No snapshots returned. Confirm Microsoft Entra Backup and Recovery is enabled for this tenant."
    return
}

$latestId = ($snapshots | Sort-Object createdDateTime -Descending | Select-Object -First 1).id

foreach ($snapshot in $snapshots) {
    [PSCustomObject]@{
        SnapshotId       = $snapshot.id
        CreatedDateTime  = [datetime]$snapshot.createdDateTime
        ChangedObjects   = $snapshot.totalChangedObjectCount
        Latest           = ($snapshot.id -eq $latestId)
    }
}
```