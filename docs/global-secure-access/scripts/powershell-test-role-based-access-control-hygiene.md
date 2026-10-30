---
layout: Conceptual
title: PowerShell sample - Check Microsoft Entra Global Secure Access role assignment reviews | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/scripts/powershell-test-role-based-access-control-hygiene
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Check Global Secure Access-related administrator role assignments and identify accounts that need quarterly review.
ms.topic: sample
ms.date: 2026-06-17T00:00:00.0000000Z
ms.reviewer: tdetzner
ai-usage: ai-assisted
locale: en-us
document_id: 6b1ebbd8-31c2-ef8f-ead6-da29dfceff6f
document_version_independent_id: 6b1ebbd8-31c2-ef8f-ead6-da29dfceff6f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/scripts/powershell-test-role-based-access-control-hygiene.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/scripts/powershell-test-role-based-access-control-hygiene
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/scripts/powershell-test-role-based-access-control-hygiene.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3adac954-7023-7e79-c4bf-b93b82ce1f88
---

# PowerShell sample - Check Microsoft Entra Global Secure Access role assignment reviews | Microsoft Learn

This script queries Microsoft Graph for directory role assignments relevant to Global Secure Access administration. It compares those assignments with a review log and identifies accounts that need quarterly review.

The script name uses RBAC as an abbreviation for role-based access control.

The script dot-sources `_GsaOpsHelpers.ps1`, so place the helper file in the same folder before you run this sample.

## Prerequisites

- PowerShell 7.0 or later.
- Install the modules listed in the script's `.NOTES` block.
- Use only permissions and roles that your organization approves for the task.

## Script

```powershell
<#
.SYNOPSIS
    Checks Global Secure Access role assignments and identifies accounts that need review.
.DESCRIPTION
    Queries Microsoft Graph for directory role assignments relevant to Global Secure Access
    administration. Compares the last review date (stored in a review log file) against the
    current quarter boundary. Sends an alert email via Microsoft Graph when accounts
    are found.

    Run this script weekly as an Azure Automation runbook or scheduled task.
.PARAMETER ReviewLogPath
    Path to the JSON file tracking last-reviewed dates per account. If running in Azure
    Automation, use an Azure Storage blob or Automation variable.
.PARAMETER AlertRecipient
    Email address to receive the alert when accounts need review.
.PARAMETER SenderId
    UserId or UPN of the mailbox used to send alert emails (requires Mail.Send permission).
.EXAMPLE
    .\Test-GsaRbacHygiene.ps1 -ReviewLogPath "C:\GsaOps\rbac-review-log.json" -AlertRecipient "gsa-ops@contoso.com" -SenderId "gsa-automation@contoso.com"
.NOTES
    Required permissions: RoleManagement.Read.Directory, Mail.Send
    Minimum module versions: Microsoft.Graph.Authentication 2.x, Microsoft.Graph.Identity.DirectoryManagement 2.x, Microsoft.Graph.Users.Actions 2.x
    Requires PowerShell 7.0 or later (uses `ConvertFrom-Json -AsHashtable`).
    Dot-sources scripts/automation/_GsaOpsHelpers.ps1 for shared auth and email helpers.
    Author: GSA Operations
#>

[CmdletBinding()]
[OutputType([pscustomobject])]
param(
    [Parameter(Mandatory)]
    [string]$ReviewLogPath,

    [string]$AlertRecipient,

    [string]$SenderId,

    [string]$TenantId,

    [string]$SubscriptionId,

    [switch]$SkipEmail
)

$ErrorActionPreference = 'Stop'

# Load shared helpers (Connect-GsaRuntime, Send-GsaAlertEmail)
. "$PSScriptRoot\_GsaOpsHelpers.ps1"

# Global Secure Access-related directory roles
$GSA_ROLE_NAMES = @(
    "Global Secure Access Administrator",
    "Security Administrator",
    "Conditional Access Administrator",
    "Network Administrator",
    "Global Administrator"
)

# Ensure Microsoft Graph context is available (throws on failure)
Connect-GsaRuntime -Service Graph -TenantId $TenantId -SubscriptionId $SubscriptionId

# Get current quarter boundary
$now = Get-Date
$quarterStart = Get-Date -Year $now.Year -Month ([Math]::Floor(($now.Month - 1) / 3) * 3 + 1) -Day 1

# Load review log
$reviewLog = @{}
if (Test-Path $ReviewLogPath) {
    $reviewLog = Get-Content $ReviewLogPath -Raw | ConvertFrom-Json -AsHashtable
    Write-Verbose "Loaded review log with $($reviewLog.Count) entries."
} else {
    Write-Warning "No review log found at $ReviewLogPath. All accounts will be marked for review."
}

# Query role assignments for GSA-related roles
$overdueAccounts = [System.Collections.Generic.List[PSCustomObject]]::new()

try {
    $directoryRoles = Get-MgDirectoryRole -All -ErrorAction Stop
} catch {
    Write-Error "Failed to retrieve directory roles. Error: $_"
    return
}

foreach ($role in $directoryRoles) {
    if ($role.DisplayName -notin $GSA_ROLE_NAMES) { continue }

    try {
        $members = Get-MgDirectoryRoleMember -DirectoryRoleId $role.Id -All -ErrorAction Stop
    } catch {
        Write-Error "Failed to retrieve members of role '$($role.DisplayName)'. Error: $_"
        continue
    }

    foreach ($member in $members) {
        $upn = $member.AdditionalProperties["userPrincipalName"]
        if (-not $upn) { continue }

        $lastReviewed = $null
        if ($reviewLog.ContainsKey($upn)) {
            $lastReviewed = [datetime]$reviewLog[$upn]
        }

        if (-not $lastReviewed -or $lastReviewed -lt $quarterStart) {
            $overdueAccounts.Add([PSCustomObject]@{
                UserPrincipalName = $upn
                RoleName          = $role.DisplayName
                LastReviewed      = if ($lastReviewed) { $lastReviewed.ToString("yyyy-MM-dd") } else { "Never" }
                QuarterStart      = $quarterStart.ToString("yyyy-MM-dd")
            })
        }
    }
}

# Output results
if ($overdueAccounts.Count -eq 0) {
    Write-Verbose "All Global Secure Access administrator account reviews are current for this quarter."
    [PSCustomObject]@{
        Status        = "Compliant"
        CheckedAt     = $now
        OverdueCount  = 0
    }
    return
}

Write-Warning "$($overdueAccounts.Count) Global Secure Access administrator account(s) need quarterly review."
$overdueAccounts | Format-Table -AutoSize | Out-String | Write-Verbose

# Update review log — add newly discovered accounts without overwriting existing review dates
$allDiscoveredUpns = $overdueAccounts | ForEach-Object { $_.UserPrincipalName } | Select-Object -Unique
foreach ($upn in $allDiscoveredUpns) {
    if (-not $reviewLog.ContainsKey($upn)) {
        $reviewLog[$upn] = $null
    }
}
$reviewLog | ConvertTo-Json -Depth 2 | Set-Content -Path $ReviewLogPath -Encoding UTF8
Write-Verbose "Review log updated at $ReviewLogPath with $($reviewLog.Count) entries."

# Build and send alert email (unless -SkipEmail)
if ($SkipEmail) {
    Write-Verbose "Skipping alert email (-SkipEmail specified)."
} elseif (-not $SenderId -or -not $AlertRecipient) {
    Write-Warning "Skipping alert email — -SenderId and -AlertRecipient are required when -SkipEmail is not set."
} else {
    $tableRows = ($overdueAccounts | ForEach-Object {
        "<tr><td>$($_.UserPrincipalName)</td><td>$($_.RoleName)</td><td>$($_.LastReviewed)</td></tr>"
    }) -join "`n"

    $emailBody = @"
<h2>Global Secure Access role assignment review alert</h2>
<p><strong>$($overdueAccounts.Count)</strong> administrator account(s) with Global Secure Access-related roles need review because their last review date is earlier than <strong>$($quarterStart.ToString("yyyy-MM-dd"))</strong>.</p>
<table border="1" cellpadding="5" cellspacing="0">
<tr><th>Account</th><th>Role</th><th>Last Reviewed</th></tr>
$tableRows
</table>
<p><strong>Action required:</strong> Review each account's access, confirm the assignment is still needed, and update the review log.</p>
"@

    try {
        Send-GsaAlertEmail `
            -SenderId  $SenderId `
            -Recipient $AlertRecipient `
            -Subject   "Global Secure Access role assignment review alert - $($overdueAccounts.Count) account(s)" `
            -HtmlBody  $emailBody
    } catch {
        Write-Warning "Alert email failed (non-fatal): $_"
    }
}

# Return summary object
[PSCustomObject]@{
    Status        = "NonCompliant"
    CheckedAt     = $now
    OverdueCount  = $overdueAccounts.Count
    OverdueAccounts = $overdueAccounts
}
```