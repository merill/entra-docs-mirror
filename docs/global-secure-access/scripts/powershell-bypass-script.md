---
layout: Conceptual
title: PowerShell sample - Add a custom bypass rule to internet access forwarding profile | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/scripts/powershell-bypass-script
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: PowerShell example that bypasses a certain fqdn or IP from being acquired by the Global Secure Access Client in the Internet Access forwarding profile.
ms.topic: sample
ms.date: 2025-06-06T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 04c8d444-9896-5f60-9f63-a867e4a1ca12
document_version_independent_id: 04c8d444-9896-5f60-9f63-a867e4a1ca12
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/scripts/powershell-bypass-script.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/scripts/powershell-bypass-script
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/scripts/powershell-bypass-script.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 4cea11f9-2c2c-6945-f3f8-b9197a252ee5
---

# PowerShell sample - Add a custom bypass rule to internet access forwarding profile | Microsoft Learn

## Overview

This PowerShell script demonstrates how to programmatically add a custom bypass rule to the Microsoft Entra Internet Access forwarding policy. The script finds the "Custom Bypass" forwarding policy and adds a sample rule to bypass specified domains.

The sample requires the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer.

## Important considerations

- Run the PowerShell script as an Administrator from an elevated PowerShell session.
- Make sure you install the Microsoft.Graph.Beta module: 

    ```powershell
    Install-Module Microsoft.Graph.Beta -AllowClobber -Force
    ```
- The account used for `Connect-MgGraph`must have the following permissions:
    - Policy.Read.All
    - NetworkAccess.ReadWrite.All

## Sample script

```powershell
# bypassscript.ps1 adds sample endpoints to the custom bypass policy in the internet access forwarding profile
# 
# Version 1.0
# 
# This script requires following 
#    - PowerShell 5.1 (x64) or beyond
#    - Module: Microsoft.Graph.Beta
#
# Before you begin:
# - Make sure you are running PowerShell as an Administrator
# - Make sure you run: Install-Module Microsoft.Graph.Beta -AllowClobber -Force
# - Make sure the account used for Connect-MgGraph has the following permissions:
#   - Policy.Read.All
#   - NetworkAccess.ReadWrite.All
# 
if (-not (Get-Module -ListAvailable -Name Microsoft.Graph.Beta.Identity.SignIns)) {
    Write-Host "Module Microsoft.Graph.Beta.Identity.SignIns is not installed. Please install it using: Install-Module Microsoft.Graph.Beta -AllowClobber"
    exit
}
Import-Module Microsoft.Graph.Beta.Identity.SignIns
Connect-MgGraph -Scopes "Policy.Read.All,NetworkAccess.ReadWrite.All"

# Find out custom bypass forwarding policy id
$custombypass = $null
$forwardingpolicies = Invoke-MgGraphRequest -Method GET -Uri "https://graph.microsoft.com/beta/networkaccess/forwardingpolicies"
foreach ($policy in $forwardingpolicies.value) {if ($policy.name -eq "Custom Bypass"){	$custombypass = $policy.id}
}
if ($custombypass -eq $null) {Write-Host "Could not find the IA custom bypass forwarding policy. Exiting."exit
}

# First, Bypass the Intune endpoints
$samplerule = [PSCustomObject]@{
    name = "Sample FQDN bypass rule"
    action = "bypass"
    destinations = @()
    ruleType = "fqdn"
    ports = @("80", "443")
    protocol = "tcp"
    '@odata.type' = "#microsoft.graph.networkaccess.internetAccessForwardingRule"
}
$sampledomains = @("bing.com","*.bing.com"
)

foreach ($sampledomain in $sampledomains) {$fqdn = [PSCustomObject]@{   '@odata.type' = "#microsoft.graph.networkaccess.fqdn"   value = $sampledomain}$samplerule.destinations += $fqdn
}
$body = $samplerule | ConvertTo-Json
Invoke-MgGraphRequest -Method POST -Uri "https://graph.microsoft.com/beta/networkaccess/forwardingPolicies('$($custombypass)')/policyRules" -Body $body -ContentType "application/json"

# Next, Bypass the sample IP-based endpoints
$sampleipbypassrule = [PSCustomObject]@{
    name = "Sample IP bypass rule"
    action = "bypass"
    destinations = @()
    ruleType = "ipSubnet"
    ports = @("80", "443")
    protocol = "tcp"
    '@odata.type' = "#microsoft.graph.networkaccess.internetAccessForwardingRule"
}
$sampleipbypassdomains = @("1.2.3.4/32"
)
foreach ($sampleipbypassdomain in $sampleipbypassdomains) {$ip = [PSCustomObject]@{   '@odata.type' = "#microsoft.graph.networkaccess.ipSubnet"   value = $sampleipbypassdomain}$sampleipbypassrule.destinations += $ip
}
$body = $sampleipbypassrule | ConvertTo-Json
Invoke-MgGraphRequest -Method POST -Uri "https://graph.microsoft.com/beta/networkaccess/forwardingPolicies('$($custombypass)')/policyRules" -Body $body -ContentType "application/json"
```