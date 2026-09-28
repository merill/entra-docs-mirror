---
layout: Conceptual
title: PowerShell sample - Verify Microsoft Entra Global Secure Access configuration backup compliance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/scripts/powershell-test-backup-compliance
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Verify that your Global Secure Access configuration backup runbook ran successfully. Send an alert when the runbook fails or misses a scheduled run.
ms.topic: sample
ms.date: 2026-06-17T00:00:00.0000000Z
ms.reviewer: tdetzner
ai-usage: ai-assisted
locale: en-us
document_id: d5c53bc8-d32d-152c-51aa-e956a95ffd61
document_version_independent_id: d5c53bc8-d32d-152c-51aa-e956a95ffd61
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/scripts/powershell-test-backup-compliance.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/scripts/powershell-test-backup-compliance
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/scripts/powershell-test-backup-compliance.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: aec4352d-c71c-05ae-a979-dbd0c8eeaff2
---

# PowerShell sample - Verify Microsoft Entra Global Secure Access configuration backup compliance | Microsoft Learn

This script checks recent Azure Automation jobs for your Global Secure Access configuration backup runbook. It returns a compliance summary and can send an alert email when the backup job fails or no job ran during the expected schedule.

The script dot-sources `_GsaOpsHelpers.ps1`, so place the helper file in the same folder before you run this sample.

## Prerequisites

- PowerShell 7.0 or later.
- Install the modules listed in the script's `.NOTES` block.
- Use only permissions and roles that your organization has approved for the task.

## Script

```powershell
<#
.SYNOPSIS
    Monitors GSA configuration backup job results and alerts on failures.
.DESCRIPTION
    Queries Azure Automation for the status of GSA backup runbook jobs over a
    configurable lookback window. If any jobs failed or no jobs ran during the
    expected schedule, sends an alert email via Microsoft Graph.

    Run this script daily as a secondary watchdog runbook in the same (or a
    different) Automation Account.
.PARAMETER AutomationAccountName
    Name of the Azure Automation Account running the backup runbooks.
.PARAMETER ResourceGroupName
    Resource group containing the Automation Account.
.PARAMETER BackupRunbookName
    Name of the runbook that performs GSA configuration backups.
.PARAMETER LookbackHours
    Number of hours to look back for completed jobs. Default: 26 (covers a
    daily schedule with 2-hour buffer).
.PARAMETER AlertRecipient
    Email address to receive failure alerts.
.PARAMETER SenderId
    UserId or UPN of the mailbox used to send alert emails.
.EXAMPLE
    .\Test-GsaBackupCompliance.ps1 -AutomationAccountName "gsa-automation" -ResourceGroupName "gsa-ops-rg" -BackupRunbookName "Export-GsaConfiguration" -AlertRecipient "gsa-ops@contoso.com" -SenderId "gsa-automation@contoso.com"
.NOTES
    Required permissions: Azure — Automation Job Operator on the Automation Account; Graph — Mail.Send
    Minimum module versions: Az.Accounts 2.x, Az.Automation 1.x, Microsoft.Graph.Authentication 2.x, Microsoft.Graph.Users.Actions 2.x
    Dot-sources scripts/automation/_GsaOpsHelpers.ps1 for shared auth and email helpers.
    Author: GSA Operations
#>

[CmdletBinding()]
[OutputType([pscustomobject])]
param(
    [Parameter(Mandatory)]
    [string]$AutomationAccountName,

    [Parameter(Mandatory)]
    [string]$ResourceGroupName,

    [Parameter(Mandatory)]
    [string]$BackupRunbookName,

    [int]$LookbackHours = 26,

    [string]$AlertRecipient,

    [string]$SenderId,

    [string]$TenantId,

    [string]$SubscriptionId,

    [switch]$SkipEmail
)

$ErrorActionPreference = 'Stop'

# Load shared helpers (Connect-GsaRuntime, Send-GsaAlertEmail)
. "$PSScriptRoot\_GsaOpsHelpers.ps1"

# Ensure Az and Graph contexts are available (throws on failure)
Connect-GsaRuntime -Service Both -TenantId $TenantId -SubscriptionId $SubscriptionId

# Query recent backup jobs
$cutoff = (Get-Date).AddHours(-$LookbackHours)

try {
    $jobs = Get-AzAutomationJob `
        -AutomationAccountName $AutomationAccountName `
        -ResourceGroupName $ResourceGroupName `
        -RunbookName $BackupRunbookName `
        -ErrorAction Stop |
        Where-Object { $_.CreationTime -ge $cutoff }
} catch {
    Write-Error "Failed to query Automation jobs. Error: $_"
    return
}

# Evaluate results
$failedJobs = $jobs | Where-Object { $_.Status -eq 'Failed' }
$noJobsRan = $jobs.Count -eq 0

if (-not $noJobsRan -and $failedJobs.Count -eq 0) {
    Write-Verbose "All $($jobs.Count) backup job(s) in the last $LookbackHours hours completed successfully."
    [PSCustomObject]@{
        Status      = "Compliant"
        CheckedAt   = (Get-Date)
        TotalJobs   = $jobs.Count
        FailedJobs  = 0
    }
    return
}

# Build alert details
$alertReason = if ($noJobsRan) {
    "No backup jobs ran in the last $LookbackHours hours. The scheduled backup may be misconfigured or the Automation Account may be stopped."
} else {
    "$($failedJobs.Count) of $($jobs.Count) backup job(s) failed in the last $LookbackHours hours."
}

$jobDetails = ""
if ($failedJobs.Count -gt 0) {
    $tableRows = ($failedJobs | ForEach-Object {
        "<tr><td>$($_.JobId)</td><td>$($_.Status)</td><td>$($_.CreationTime.ToString('yyyy-MM-dd HH:mm'))</td><td>$($_.Exception)</td></tr>"
    }) -join "`n"
    $jobDetails = @"
<table border="1" cellpadding="5" cellspacing="0">
<tr><th>Job ID</th><th>Status</th><th>Started</th><th>Error</th></tr>
$tableRows
</table>
"@
}

$emailBody = @"
<h2>GSA Backup Compliance Alert</h2>
<p>$alertReason</p>
$jobDetails
<p><strong>Action required:</strong></p>
<ol>
<li>Check the Automation Account <strong>$AutomationAccountName</strong> in resource group <strong>$ResourceGroupName</strong>.</li>
<li>Review the failed job output for error details.</li>
<li>Run the backup manually: <code>Start-AzAutomationRunbook -Name '$BackupRunbookName' -AutomationAccountName '$AutomationAccountName' -ResourceGroupName '$ResourceGroupName'</code></li>
<li>Verify the backup file was created in your backup storage location.</li>
<li>Fix the root cause (expired credentials, API throttling, storage quota) and confirm the next scheduled run succeeds.</li>
</ol>
"@

if ($SkipEmail) {
    Write-Verbose "Skipping alert email (-SkipEmail specified)."
} elseif (-not $SenderId -or -not $AlertRecipient) {
    Write-Warning "Skipping alert email — -SenderId and -AlertRecipient are required when -SkipEmail is not set."
} else {
    try {
        Send-GsaAlertEmail `
            -SenderId  $SenderId `
            -Recipient $AlertRecipient `
            -Subject   "GSA Backup Alert — $alertReason" `
            -HtmlBody  $emailBody
    } catch {
        Write-Warning "Alert email failed (non-fatal): $_"
    }
}

# Return summary
[PSCustomObject]@{
    Status      = "NonCompliant"
    CheckedAt   = (Get-Date)
    TotalJobs   = $jobs.Count
    FailedJobs  = $failedJobs.Count
    Reason      = $alertReason
}
```