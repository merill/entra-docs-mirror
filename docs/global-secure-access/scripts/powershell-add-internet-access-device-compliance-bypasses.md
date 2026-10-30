---
layout: Conceptual
title: PowerShell sample - Add Intune device compliance bypasses to Global Secure Access Internet Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/scripts/powershell-add-internet-access-device-compliance-bypasses
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: PowerShell example that adds Intune-related endpoints to the Global Secure Access Internet Access custom bypass policy to mitigate device compliance issues.
ms.topic: sample
ms.date: 2025-06-06T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 905af996-37dd-12ba-d385-2346f97212ff
document_version_independent_id: 905af996-37dd-12ba-d385-2346f97212ff
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/scripts/powershell-add-internet-access-device-compliance-bypasses.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/scripts/powershell-add-internet-access-device-compliance-bypasses
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/scripts/powershell-add-internet-access-device-compliance-bypasses.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 0b41b22c-785d-0098-8b59-07dff2abb517
---

# PowerShell sample - Add Intune device compliance bypasses to Global Secure Access Internet Access | Microsoft Learn

## Overview

The [Universal Conditional Access documentation](/en-us/entra/global-secure-access/concept-universal-conditional-access#known-tunnel-authorization-limitations) notes that Global Secure Access has tunnel authorization limitations. This means that you can block access to a forwarding profile in Conditional Access and inadvertently lock users out from accessing anything on their machine.

The way to mitigate this issue is bypassing [Network endpoints for Microsoft Intune](/en-us/mem/intune/fundamentals/intune-endpoints). This PowerShell script adds Intune-related endpoints to the Global Secure Access Internet Access (IA) custom bypass policy. This helps mitigate device compliance issues and supports scenarios such as AzVPN side-by-side deployments.

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
# add-ia-bypasses.ps1 adds intune-related endpoints to GSA IA custom bypass to mitigate the device-compliance related Chicken and Egg Problem.
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
$intunerule = [PSCustomObject]@{
    name = "Network Endpoints for Microsoft Intune"
    action = "bypass"
    destinations = @()
    ruleType = "fqdn"
    ports = @("80", "443")
    protocol = "tcp"
    '@odata.type' = "#microsoft.graph.networkaccess.internetAccessForwardingRule"
}
$intunedomains = @("*.manage.microsoft.com","manage.microsoft.com","EnterpriseEnrollment.manage.microsoft.com","*.do.dsp.mp.microsoft.com","*.dl.delivery.mp.microsoft.com","*.emdl.ws.microsoft.com","kv801.prod.do.dsp.mp.microsoft.com","geo.prod.do.dsp.mp.microsoft.com","emdl.ws.microsoft.com","2.dl.delivery.mp.microsoft.com","bg.v4.emdl.ws.microsoft.com","swda01-mscdn.manage.microsoft.com","swda02-mscdn.manage.microsoft.com","swdb01-mscdn.manage.microsoft.com","swdb02-mscdn.manage.microsoft.com","swdc01-mscdn.manage.microsoft.com","swdc02-mscdn.manage.microsoft.com","swdd01-mscdn.manage.microsoft.com","swdd02-mscdn.manage.microsoft.com","swdin01-mscdn.manage.microsoft.com","swdin02-mscdn.manage.microsoft.com","account.live.com","login.live.com","config.edge.skype.com","go.microsoft.com","*.windowsupdate.com","*.dl.delivery.mp.microsoft.com","*.prod.do.dsp.mp.microsoft.com","emdl.ws.microsoft.com","*.delivery.mp.microsoft.com","*.update.microsoft.com","tsfe.trafficshaping.dsp.mp.microsoft.com","time.windows.com","clientconfig.passport.net","windowsphone.com","*.s-microsoft.com","c.s-microsoft.com","ekop.intel.com","ekcert.spserv.microsoft.com","ftpm.amd.com","lgmsapeweu.blob.core.windows.net","*.support.services.microsoft.com","remoteassistance.support.services.microsoft.com","rdprelayv3eastusprod-0.support.services.microsoft.com","*.trouter.skype.com","remoteassistanceprodacs.communication.azure.com","edge.skype.com","aadcdn.msftauth.net","aadcdn.msauth.net","alcdn.msauth.net","wcpstatic.microsoft.com","*.aria.microsoft.com","browser.pipe.aria.microsoft.com","*.events.data.microsoft.com","v10.events.data.microsoft.com","*.monitor.azure.com","js.monitor.azure.com","edge.microsoft.com","*.trouter.communication.microsoft.com","go.trouter.communication.microsoft.com","*.trouter.teams.microsoft.com","trouter2-usce-1-a.trouter.teams.microsoft.com","api.flightproxy.skype.com","ecs.communication.microsoft.com","remotehelp.microsoft.com","trouter-azsc-usea-0-a.trouter.skype.com","*.webpubsub.azure.com","AMSUA0101-RemoteAssistService-pubsub.webpubsub.azure.com","remoteassistanceweb-gcc.usgov.communication.azure.us","gcc.remotehelp.microsoft.com","gcc.relay.remotehelp.microsoft.com","*.gov.teams.microsoft.us","*.notify.windows.com","*.wns.windows.com","sinwns1011421.wns.windows.com","sin.notify.windows.com","*.do.dsp.mp.microsoft.com","*.dl.delivery.mp.microsoft.com","*.emdl.ws.microsoft.com","kv801.prod.do.dsp.mp.microsoft.com","geo.prod.do.dsp.mp.microsoft.com","emdl.ws.microsoft.com","2.dl.delivery.mp.microsoft.com","bg.v4.emdl.ws.microsoft.com","itunes.apple.com","*.itunes.apple.com","*.mzstatic.com","*.phobos.apple.com","phobos.itunes-apple.com.akadns.net","5-courier.push.apple.com","phobos.apple.com","ocsp.apple.com","ax.itunes.apple.com","ax.itunes.apple.com.edgesuite.net","s.mzstatic.com","a1165.phobos.apple.com","intunecdnpeasd.azureedge.net","login.microsoftonline.com","graph.windows.net","*.officeconfig.msocdn.com","config.office.com","enterpriseregistration.windows.net","naprodimedatapri.azureedge.net","naprodimedatasec.azureedge.net","naprodimedatahotfix.azureedge.net","euprodimedatapri.azureedge.net","euprodimedatasec.azureedge.net","euprodimedatahotfix.azureedge.net","approdimedatapri.azureedge.net","approdimedatasec.azureedge.net","approdimedatahotfix.azureedge.net","*.azureedge.net","graph.microsoft.com","displaycatalog.mp.microsoft.com","purchase.md.mp.microsoft.com","licensing.mp.microsoft.com","storeedgefd.dsx.mp.microsoft.com","intunemaape1.eus.attest.azure.net","intunemaape2.eus2.attest.azure.net","intunemaape3.cus.attest.azure.net","intunemaape4.wus.attest.azure.net","intunemaape5.scus.attest.azure.net","intunemaape6.ncus.attest.azure.net","intunemaape7.neu.attest.azure.net","intunemaape8.neu.attest.azure.net","intunemaape9.neu.attest.azure.net","intunemaape10.weu.attest.azure.net","intunemaape11.weu.attest.azure.net","intunemaape12.weu.attest.azure.net","intunemaape13.jpe.attest.azure.net","intunemaape17.jpe.attest.azure.net","intunemaape18.jpe.attest.azure.net","intunemaape19.jpe.attest.azure.net","*.dm.microsoft.com","*.events.data.microsoft.com"
)
foreach ($intunedomain in $intunedomains) {$fqdn = [PSCustomObject]@{   '@odata.type' = "#microsoft.graph.networkaccess.fqdn"   value = $intunedomain}$intunerule.destinations += $fqdn
}
$body = $intunerule | ConvertTo-Json
Invoke-MgGraphRequest -Method POST -Uri "https://graph.microsoft.com/beta/networkaccess/forwardingPolicies('$($custombypass)')/policyRules" -Body $body -ContentType "application/json"
```