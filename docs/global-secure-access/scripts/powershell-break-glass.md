---
layout: Conceptual
title: PowerShell sample - Disable traffic forwarding and disable Conditional Access policies using the compliant network condition in a break glass scenario | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/scripts/powershell-break-glass
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: PowerShell examples for use in a Microsoft Entra Internet Access break glass scenario.
ms.topic: sample
ms.date: 2026-03-16T00:00:00.0000000Z
locale: en-us
document_id: b9c89ece-339f-aad1-e56e-2993ef4a5d7b
document_version_independent_id: b9c89ece-339f-aad1-e56e-2993ef4a5d7b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/scripts/powershell-break-glass.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/scripts/powershell-break-glass
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/scripts/powershell-break-glass.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 81101c5b-96c6-470a-9b90-bdf27e11d08b
---

# PowerShell sample - Disable traffic forwarding and disable Conditional Access policies using the compliant network condition in a break glass scenario | Microsoft Learn

## Overview

In the event of an outage or connectivity failure to Microsoft Entra Internet Access, your users remain protected. However, you might want to perform a "break glass" operation: Temporarily disabling traffic forwarding profiles and disabling the Compliant Network condition policies can help your users regain access to their Microsoft apps in favor of productivity.

The following sample script helps you quickly disable traffic forwarding and switch your Conditional Access policies using the [Compliant Network](../how-to-compliant-network) condition into Report-Only mode.

## List and disable Conditional Access policies using the Compliant Network condition in a break glass scenario

The PowerShell script effectively disables any Conditional Access policies that use the Compliant Network condition. In an emergency situation, use this script to temporarily regain access for your users.

The sample requires the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer.

```powershell
# gsabreakglass.ps1 places the Compliant Network Conditional Access Policies for a given tenant using Microsoft Entra Internet Access into Report-Only mode.
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
Connect-MgGraph -Scopes "Policy.Read.All,Policy.ReadWrite.ConditionalAccess,NetworkAccess.ReadWrite.All"

$result = @()
$timeRun = Get-Date
$result += "Script was run at $($timeRun)"
$count = 0
# Search for any Conditional Access policies leveraging the Compliant Network condition.
$allCAPolicies = Get-MgBetaIdentityConditionalAccessPolicy
$allCompliantNetworkCAPolicies = @()
foreach ($policy in $allCAPolicies) 
{
    if ($policy.conditions.locations.excludeLocations -Contains "3d46dbda-8382-466a-856d-eb00cbc6b910" -or $policy.conditions.locations.includeLocations -Contains "3d46dbda-8382-466a-856d-eb00cbc6b910") 
    {
        $allCompliantNetworkCAPolicies += $policy
    }
}
$compliantNetworkCount = $allCompliantNetworkCAPolicies.Count
$result += "Total count of Compliant Network Conditional Access policies: $($compliantNetworkCount)"
# List + Save the list of Compliant Network Conditional Access policies to the C:\BreakGlass folder for use in .\breakglass.ps1
foreach ($policy in $allCompliantNetworkCAPolicies)
{
    $current = Get-MgBetaIdentityConditionalAccessPolicy -ConditionalAccessPolicyId $policy.id
    $currentState = $current.state
    $currentTime = Get-Date
    $policyContent = "{0},{1},{2},{3},{4}" -f $policy.displayName, $policy.id, "Current State: $($currentState) at $($currentTime)", $policy.CreatedDateTime, $policy.ModifiedDateTime
    $result += $policyContentWrite-Host "Conditional Access Policy with ID: $($policy.id) (state: $($current.state)) uses the Compliant Network Condition. Policy name: $($policy.displayName)"
}
$result += " "
$path = "C:\BreakGlass\ListCompliantNetworkCAPolicies.txt"
if (Test-Path $path)
{
    $result | Out-File -FilePath $path
} else {
    New-Item -Force -Path $path -Type File$result | Out-File -FilePath $path
}
Write-Host "`nList of Compliant NW policies has been exported to C:\BreakGlass\ListCompliantNetworkCAPolicies.txt`n"

$result = @()
$timeRun = Get-Date
$result += "Script was run at $($timeRun)"
$count = 0
$result += "Total count of Compliant Network Conditional Access policies: $($allCompliantNetworkCAPolicies.Count)"
# Based on admin input, disable either all or some Conditional Access policies leveraging the Compliant Network Condition.
$action = Read-Host "Do you want to put all enabled compliant network Conditional Access policies in Report-Only mode (type 'all') or just specific policy IDs (type 'ids')?"
if ($action -eq "all") 
{
    foreach ($policy in $allCompliantNetworkCAPolicies) 
    {
        if ($policy) 
        {
            #only BreakGlass if policy is already enabled
            if ($policy.state -eq "enabled")
            {
                $params = @{
                    state = "enabledForReportingButNotEnforced"
                }
                $current = Get-MgBetaIdentityConditionalAccessPolicy -ConditionalAccessPolicyId $policy.id
                $currentState = $current.state
                $currentTime = Get-Date
                Update-MgBetaIdentityConditionalAccessPolicy -ConditionalAccessPolicyId $policy.id -BodyParameter $params
                
                $updatedTime = Get-Date
                $check = Get-MgBetaIdentityConditionalAccessPolicy -ConditionalAccessPolicyId $policy.id
                $updatedState = $check.state
                
                if ($updatedState -eq "enabledForReportingButNotEnforced") 
                {
                    $policyContent = "{0},{1},{2},{3},{4},{5}" -f $policy.displayName, $policy.id, $policy.CreatedDateTime, $policy.ModifiedDateTime, "Before BreakGlass: $($currentState) at $($currentTime)", "After BreakGlass: $($updatedState) at $($updatedTime)"
                    $result += $policyContent
                    $count++				Write-Host "Policy with ID $($policy.id) is now in Report-Only mode"
                } else {
                    Write-Host "Policy with ID $($policy.id) could not be put in Report-Only mode"
                }
            } else {
                Write-Host "Policy with ID $($policy.id) is already Disabled or Report-Only."
            }
        } else {
            Write-Host "Policy with ID $($policy.id) was not found."
        }
    }
} elseif ($action -eq "ids") {
    $policyIds = Read-Host "Enter the IDs of the policies you want to put in Report-Only mode (separated by commas)"
    $policyIds = $policyIds -split ","
   
    foreach ($id in $policyIds) 
    {
        $policy = $allCompliantNetworkCAPolicies | Where-Object { $_.id -eq $id }
        if ($policy) 
        {
            if ($policy.state -eq "enabled")
            {
                $params = @{
                state = "enabledForReportingButNotEnforced"
                }
                $current = Get-MgBetaIdentityConditionalAccessPolicy -ConditionalAccessPolicyId $policy.id
                $currentState = $current.state
                $currentTime = Get-Date
                Update-MgBetaIdentityConditionalAccessPolicy -ConditionalAccessPolicyId $policy.id -BodyParameter $params
                
                $updatedTime = Get-Date
                $check = Get-MgBetaIdentityConditionalAccessPolicy -ConditionalAccessPolicyId $policy.id
                $updatedState = $check.state
                
                if ($updatedState -eq "enabledForReportingButNotEnforced") 
                {
                    $policyContent = "{0},{1},{2},{3},{4},{5}" -f $policy.displayName, $policy.id, $policy.CreatedDateTime, $policy.ModifiedDateTime, "Before BreakGlass: $($currentState) at $($currentTime)", "After BreakGlass: $($updatedState) at $($updatedTime)"
                    $result += $policyContent
                    $count++
                    Write-Host "Policy with ID $($policy.id) is now in Report-Only mode."
                } else {
                    Write-Host "Policy with ID $($policy.id) could not be put in Report-Only mode"
                }
            } else {
                Write-Host "Policy with ID $($policy.id) is already Disabled or Report-Only."
            }
        } else {
            Write-Host "Policy with ID $id not found."
        }
    }
} else {
    Write-Host "Invalid action. Please type 'all' or 'ids'."
}
# Save the list of Compliant Network Conditional Access policies that were moved to Report-Only mode to the C:\BreakGlass folder for use in .\breakglass.ps1
$result += "Number of policies placed in Report-Only mode: $($count)"
$path = "C:\BreakGlass\ReportOnlyCompliantNetworkCAPolicies.txt"
if (Test-Path $path)
{
    $result | Out-File -FilePath $path
} else {
    New-Item -Force -Path $path -Type File$result | Out-File -FilePath $path
}
Write-Host "`nCA policy disablement results have been exported to C:\BreakGlass\ReportOnlyCompliantNetworkCAPolicies.txt`n"

# Disable Traffic Profiles
$forwardingResult = @()
$timeRun = Get-Date
$result = "Script was run at $($timeRun)`n"

$forwardingProfiles = Invoke-MgGraphRequest -Method GET -Uri "https://graph.microsoft.com/beta/networkaccess/forwardingprofiles"
foreach ($profile in $forwardingProfiles.value)
{if ($profile.state -eq "enabled") {	$body = @{ state = "disabled" } | ConvertTo-Json	$check = Invoke-MgGraphRequest -Method PATCH -Uri "https://graph.microsoft.com/beta/networkaccess/forwardingprofiles/$($profile.id)" -Body $body -ContentType "application/json"	if ($check.state -eq "disabled") {		$profileContent = "{0},{1},{2}`n" -f $profile.name, $profile.id, $profile.lastModifiedDateTime		$result += $profileContent		Write-Host "$($profile.name) is now disabled."	} else {		Write-Host "$($profile.name) can't be disabled."	}} else{	Write-Host "$($profile.name) is already disabled."}
}

# Save the list of disabled Forwarding profiles to C:\BreakGlass folder
$path = "C:\BreakGlass\DisabledForwardingProfiles.txt"
if (Test-Path $path)
{
    $result | Out-File -FilePath $path
} else {
    New-Item -Force -Path $path -Type File$result | Out-File -FilePath $path
}
Write-Host "`nDisabled Forwarding Profiles have been exported to C:\BreakGlass\DisabledForwardingProfiles.txt`n"
```