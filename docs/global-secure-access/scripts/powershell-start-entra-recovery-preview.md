---
layout: Conceptual
title: PowerShell sample - Preview a Microsoft Entra recovery for Global Secure Access objects | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/scripts/powershell-start-entra-recovery-preview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Create a non-destructive Microsoft Entra recovery preview job scoped to directory objects that affect Global Secure Access.
ms.topic: sample
ms.date: 2026-06-17T00:00:00.0000000Z
ms.reviewer: tdetzner
ai-usage: ai-assisted
locale: en-us
document_id: fc5fdb4e-0d8c-6a63-3183-34593c1f2c2f
document_version_independent_id: fc5fdb4e-0d8c-6a63-3183-34593c1f2c2f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/scripts/powershell-start-entra-recovery-preview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/scripts/powershell-start-entra-recovery-preview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/scripts/powershell-start-entra-recovery-preview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bffd3061-61dd-c2f2-81fa-ec57537097c1
---

# PowerShell sample - Preview a Microsoft Entra recovery for Global Secure Access objects | Microsoft Learn

This script creates a non-destructive Microsoft Entra recovery preview job against a selected snapshot. Use the preview output to review what a recovery would change before you start a recovery job.

The Microsoft Entra Backup and Recovery APIs are in Microsoft Graph beta. Only one preview or recovery job can run per tenant at a time.

## Prerequisites

- PowerShell 7.0 or later.
- Install the modules listed in the script's `.NOTES` block.
- Use only permissions and roles that your organization has approved for the task.

## Script

```powershell
<#
.SYNOPSIS
    Creates a scoped Microsoft Entra recovery preview job for GSA-related objects.
.DESCRIPTION
    Creates a recoveryPreviewJob against a chosen tenant snapshot, scoped to
    entity types that affect Global Secure Access: Conditional Access policies,
    named locations, applications, and service principals. The preview job is a
    non-destructive dry run.

    After the job reaches status 'succeeded', call the getChanges function
    against the returned PreviewJobUri to enumerate the objects and property
    changes that a recovery would apply.

    Use Get-GsaEntraSnapshot.ps1 to retrieve available SnapshotId values.
.PARAMETER SnapshotId
    Snapshot ID from the output of Get-GsaEntraSnapshot.ps1.
.PARAMETER EntityTypes
    Directory object types to include in the preview scope. Defaults to the
    GSA-relevant set.
.PARAMETER TenantId
    Target Microsoft Entra tenant ID.
.PARAMETER UseManagedIdentity
    Authenticate using the current managed identity. Use in Azure Automation.
.PARAMETER ClientId
    App registration client ID. Required with CertificateThumbprint.
.PARAMETER CertificateThumbprint
    Certificate thumbprint for service principal authentication.
.EXAMPLE
    .\Start-GsaEntraRecoveryPreview.ps1 -SnapshotId "MjAyNi0w..." -UseManagedIdentity
.NOTES
    Required Graph permissions:
        EntraBackup.ReadWrite.Preview (delegated only)
    Required Entra role:
        Entra Backup Administrator
    Minimum module versions:
        Microsoft.Graph.Authentication 2.x
    Beta API: subject to change per Microsoft Graph versioning policy.
    Only one preview or recovery job can run per tenant at a time.
    Reference: https://learn.microsoft.com/en-us/graph/api/resources/entrarecoveryservices-recoverypreviewjob?view=graph-rest-beta
    Author: GSA Operations
#>

[CmdletBinding(DefaultParameterSetName = 'Interactive')]
[OutputType([pscustomobject])]
param(
    [Parameter(Mandatory)]
    [string]$SnapshotId,

    [ValidateSet('conditionalAccessPolicy', 'namedLocationPolicy', 'application', 'servicePrincipal', 'group', 'user', 'appRoleAssignment', 'oAuth2PermissionGrant', 'authenticationMethodPolicy', 'authorizationPolicy', 'authenticationStrengthPolicy')]
    [string[]]$EntityTypes = @('conditionalAccessPolicy', 'namedLocationPolicy', 'application', 'servicePrincipal'),

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
        default            { Connect-MgGraph -TenantId $TenantId -Scopes 'EntraBackup.ReadWrite.Preview' -NoWelcome | Out-Null }
    }
    Write-Verbose "Connected to Microsoft Graph."
} catch {
    throw "Failed to authenticate to Microsoft Graph: $_"
}

# Build scoped preview job payload
$body = @{
    filteringCriteria = @{
        '@odata.type' = '#microsoft.graph.entraRecoveryServices.recoveryJobEntityNamesFilter'
        entityTypes   = $EntityTypes
    }
} | ConvertTo-Json -Depth 5

# Create preview job
try {
    $uri      = "https://graph.microsoft.com/beta/directory/recovery/snapshots/$SnapshotId/recoveryPreviewJobs"
    $response = Invoke-MgGraphRequest -Method POST -Uri $uri -Body $body -ContentType 'application/json' -ResponseHeadersVariable headers -StatusCodeVariable status
    if ($status -ne 202) {
        throw "Unexpected status code $status when creating preview job."
    }
} catch {
    throw "Failed to create recovery preview job. Verify the Microsoft Entra Backup Administrator role and EntraBackup.ReadWrite.Preview permission. Error: $_"
}

$jobUrl = $headers.Location | Select-Object -First 1
if (-not $jobUrl) {
    Write-Warning "No Location header returned. Inspect the response manually."
    return
}

[PSCustomObject]@{
    SnapshotId     = $SnapshotId
    EntityTypes    = $EntityTypes
    PreviewJobUri  = $jobUrl
    CreatedAt      = (Get-Date)
    NextSteps      = "Poll PreviewJobUri until status=succeeded, then call {PreviewJobUri}/getChanges"
}
```