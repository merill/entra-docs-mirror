---
layout: Conceptual
title: PowerShell sample - Recover from Global Secure Access break glass scenario | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/scripts/powershell-break-glass-recovery
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: PowerShell examples that re-enable any Conditional Access policies that were disabled in a break glass scenario.
ms.topic: sample
ms.date: 2026-03-16T00:00:00.0000000Z
locale: en-us
document_id: 61249227-3f3c-0f11-faa0-fc65ed875c76
document_version_independent_id: 61249227-3f3c-0f11-faa0-fc65ed875c76
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/scripts/powershell-break-glass-recovery.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/scripts/powershell-break-glass-recovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/scripts/powershell-break-glass-recovery.md
cmProducts: []
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: db9f2de9-a7e6-0aa2-4b7b-997083ec7608
---

# PowerShell sample - Recover from Global Secure Access break glass scenario | Microsoft Learn

## Overview

After an outage is resolved, you need to make a fast and accurate recovery from a [break glass](powershell-break-glass) operation.

The following script helps you quickly regain the security value of [Global Secure Access](../overview-what-is-global-secure-access) and [Compliant Network](../how-to-compliant-network) for your users.

## Implement break glass recovery

The PowerShell script enables all forwarding profiles and Conditional Access policies using the compliant network condition that were disabled in the [break glass](powershell-break-glass) script.

The sample requires the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer.

```powershell
# recoveryscript.ps1 enables any Conditional Access policies using the Compliant Network condition that were disabled in a breakglass scenario. 
# This script is the recovery method once the GSA service is back up after running .\gsabreakglass.ps1
#
# Version 1.0
#
# This script requires following 
#    - PowerShell 5.1 (x64) or beyond
#    - Module: Microsoft.Graph.Beta
#
#
# Before you begin:
#    
# - Make sure you are running PowerShell as an Administrator
# - Make sure your Administrator persona is an leveraging an Entra ID emergency access admin account, not subject to Microsoft Entra Internet Access Compliant Network policy, as described in https://learn.microsoft.com/entra/identity/role-based-access-control/security-emergency-access.
# - Make sure you run: Install-Module Microsoft.Graph.Beta -AllowClobber -Force
Import-Module Microsoft.Graph.Beta.Identity.SignIns
Connect-MgGraph -Scopes "Policy.Read.All,Policy.ReadWrite.ConditionalAccess"

$result = @()
$timeRun = Get-Date
$result += "Script was run at $($timeRun)`n"
# Enable Traffic Profiles
$disabledForwardingProfiles = Get-Content -Path "C:\BreakGlass\DisabledForwardingProfiles.txt"
if ($disabledForwardingProfiles.Count -gt 2) {$disabledForwardingProfiles = $disabledForwardingProfiles[1..($disabledForwardingProfiles.Count - 2)]foreach ($profile in $disabledForwardingProfiles){	$profile = $profile -split ','	$body = @{ state = "enabled" } | ConvertTo-Json	$check = Invoke-MgGraphRequest -Method PATCH -Uri "https://graph.microsoft.com/beta/networkaccess/forwardingprofiles/$($profile[1])" -Body $body -ContentType "application/json"	if ($check.state -eq "enabled") {		$profileContent = "{0},{1},{2}`n" -f $profile.name, $profile.id, $profile.lastModifiedDateTime		$result += $profileContent		Write-Host "$($profile[0]) is now enabled."	} else {		Write-Host "$($profile[0]) can't be enabled."	}}
$path = "C:\BreakGlass\RecoveredForwardingProfiles.txt"if (Test-Path $path){	$result | Out-File -FilePath $path} else {	New-Item -Force -Path $path -Type File	$result | Out-File -FilePath $path}Write-Host "`nResults have been exported to C:\BreakGlass\RecoveredForwardingProfiles.txt`n"
} else {Write-Host "There are no Forwarding Profiles to recover."
}

# Enable Compliant Network Conditional Access policies
$result = @()
$result += "Script was run at $($timeRun)"
$count = 0
$reportOnlyOutput = Get-Content -Path "C:\BreakGlass\ReportOnlyCompliantNetworkCAPolicies.txt"
if ($reportOnlyOutput.Count -le 3){Write-Host "There are no Conditional Access policies to recover. Exiting script."exit
}
$policiesToRecover = $reportOnlyOutput[2..($reportOnlyOutput.Count - 2)]
$result += "Total count of Compliant Network Conditional Access policies to recover: $($policiesToRecover.Count)"

# Based on admin input, either view or recover the list of policies disabled in the breakglass scenario.
$action = Read-Host "`nDo you want to recover all affected Conditional Access policies (type 'recover') or just view them (type 'view')?"
if ($action -eq "view") {
    $result += "Total count of policies to revert: $($policiesToRecover.Count)"
    foreach ($policy in $policiesToRecover) 
    {
        $policyFields = $policiesToRecover -split ','
        $policyId = $policyFields[1]
        $current = Get-MgBetaIdentityConditionalAccessPolicy -ConditionalAccessPolicyId $policyId
        $currentState = $current.state
        $currentTime = Get-Date
        $policyContent = "{0},{1},{2},{3},{4},{5},{6}" -f $policyFields[0], $policyId, $policyFields[2], $policyFields[3], "State Before Recovery: $($policyFields[4])", "State During Recovery: $($currentState) at $($currentTime)", "State After Recovery: enabled)"
        $result += $policyContent
    }
    $path = "C:\BreakGlass\ViewCompliantNetworkCAPoliciesToRecover.txt"
    if (Test-Path $path)
    {
        $result | Out-File -FilePath $path
    } else {
        New-Item -Force -Path $path -Type File	$result | Out-File -FilePath $path
    }
    Write-Host "Results have been exported to C:\BreakGlass\ViewCompliantNetworkCAPoliciesToRecover.txt"
} elseif ($action -eq "recover") {
    foreach ($policy in $policiesToRecover) 
    {
        $policyFields = $policiesToRecover -split ','
        $policyId = $policyFields[1]
        $params = @{
            state = "enabled"
        }
        $preRecovery = Get-MgBetaIdentityConditionalAccessPolicy -ConditionalAccessPolicyId $policyId
        $preRecoveryState = $preRecovery.state
        $preRecoveryTime = Get-Date
        Update-MgBetaIdentityConditionalAccessPolicy -ConditionalAccessPolicyId $policyId -BodyParameter $params
        
        $postRecoveryTime = Get-Date
        $postRecovery = Get-MgBetaIdentityConditionalAccessPolicy -ConditionalAccessPolicyId $policyId
        $postRecoveryState = $postRecovery.state
        
        if ($postRecoveryState -eq "enabled") 
        {
            $policyContent = "{0},{1},{2},{3},{4},{5},{6}" -f $policyFields[0], $policyId, $policyFields[2], $policyFields[3], "State $($policyFields[4])", "State During Breakglass: $($preRecoveryState) at $($preRecoveryTime)", "State After Recovery: $($postRecoveryState) at $($postRecoveryTime)"
            $result += $policyContent
            $count++		Write-Host "Policy with ID $($policyId) is now Enabled"
        } else {
            Write-Host "Policy with ID $($policy.id) could not be enabled"
        }
    }
    $result += "Number of policies recovered: $($count)"
    $path = "C:\BreakGlass\RecoveredCompliantNetworkCAPolicies.txt"
    if (Test-Path $path)
    {
        $result | Out-File -FilePath $path
    } else {
        New-Item -Force -Path $path -Type File	$result | Out-File -FilePath $path
    }
    Write-Host "`nResults have been exported to C:\BreakGlass\RecoveredCompliantNetworkCAPolicies.txt`n"
}
```