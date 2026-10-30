---
layout: Conceptual
title: PowerShell sample - Move Microsoft Entra application proxy apps to another group - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/scripts/powershell-move-all-apps-to-connector-group
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Microsoft Entra application proxy PowerShell example used to move all applications currently assigned to a connector group to a different connector group.
ms.custom: 
ms.topic: sample
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: ashishj
ai-usage: ai-assisted
locale: en-us
document_id: 2337982f-b184-2c55-5b77-e73afb3d1cee
document_version_independent_id: eb3f79aa-b23d-7319-965f-6b47ce16ffbc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/scripts/powershell-move-all-apps-to-connector-group.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/scripts/powershell-move-all-apps-to-connector-group
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/scripts/powershell-move-all-apps-to-connector-group.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 6f46c342-b208-3b07-c6a3-378e3137b221
---

# PowerShell sample - Move Microsoft Entra application proxy apps to another group - Microsoft Entra ID | Microsoft Learn

## Overview

The PowerShell script example moves all Microsoft Entra application proxy applications currently assigned to a connector group to a different connector group.

If you don't have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

The sample requires the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer.

## Sample script

```powershell
# This sample script moves all Microsoft Entra application proxy applications assigned to a specific connector group to another connector group.
#
# .\move-all-apps-to-a-connector-group.ps1 -CurrentConnectorGroupId <ObjectId of the current connector group> -NewConnectorGroupId <ObjectId of the new connector group>
#
# Version 1.0
#
# This script requires PowerShell 5.1 (x64) or beyond and one of the following modules:
#
# Microsoft.Graph.Beta ver 2.10 or newer
#
# Before you begin:
#    
#    Required Microsoft Entra role at least Application Administrator
#    or appropriate custom permissions as documented https://learn.microsoft.com/azure/active-directory/roles/custom-enterprise-app-permissions
#
# 

param(
[parameter(Mandatory=$true)]
[string] $CurrentConnectorGroupId = "null", 
[parameter(Mandatory=$true)]
[string] $NewConnectorGroupId = "null"
)

$currentGroupId = $CurrentConnectorGroupId
$newGroupId = $NewConnectorGroupId
$connectorAssignedApp = $null

If (($currentGroupId -eq "null") -or ($newGroupId -eq "null")) {

    Write-Host "Parameter is missing." -BackgroundColor "Black" -ForegroundColor "Green"
    Write-Host " "
    Write-Host ".\move-all-apps-to-a-connector-group.ps1 -CurrentConnectorGroupId <ObjectId of the current connector group> -NewConnectorGroupId <ObjectId of the new connector group>" -BackgroundColor "Black" -ForegroundColor "Green"
    Write-Host " "

    Exit
}

Import-Module Microsoft.Graph.Beta.Applications

Connect-MgGraph -Scope Directory.ReadWrite.All -NoWelcome

Try {
$temp = Get-MgBetaOnPremisePublishingProfileConnectorGroup -OnPremisesPublishingProfileId "applicationProxy" -ConnectorGroupId $currentGroupId
$temp = Get-MgBetaOnPremisePublishingProfileConnectorGroup -OnPremisesPublishingProfileId "applicationProxy" -ConnectorGroupId $newGroupId
}

Catch {
    Write-Host "Possibly, one of the parameters is incorrect." -BackgroundColor "Black" -ForegroundColor "Red"
    Write-Host " "

    Exit
}

Write-Host "Reading service principals. This operation might take longer..." -BackgroundColor "Black" -ForegroundColor "Green" 

$aadapServPrinc = Get-MgBetaServicePrincipal -Top 100000 | where-object {$_.Tags -Contains "WindowsAzureActiveDirectoryOnPremApp"}

Write-Host "Displaying Microsoft Entra application proxy applications moved from the connector Id :",$currentGroupId," to: ",$newGroupId -BackgroundColor "Black" -ForegroundColor "Green"
Write-Host " "

$connectorAssignedApp = Get-MgBetaOnPremisePublishingProfileConnectorGroupApplication -OnPremisesPublishingProfileId "applicationProxy" -ConnectorGroupId $CurrentConnectorGroupId;
$movedApps, $notmovedApps = 0, 0

 foreach ($item in $connectorAssignedApp) {

    if ($item.AppId -in ($aadapServPrinc.AppId)) {
               
     $item.DisplayName + " (AppId: " + $item.AppId + ")"
     
     $params = @{
      "@odata.id" = "https://graph.microsoft.com/beta/onPremisesPublishingProfiles/applicationProxy/connectorGroups/$NewConnectorGroupId"
       }
      
        Set-MgBetaApplicationConnectorGroupByRef -ApplicationId $item.Id -BodyParameter $params 

        $movedApps = $movedApps + 1
     }
     else
     {
      $notmovedApps = $notmovedApps + 1
     }      
} 

Write-Host ("")
Write-Host ("$movedApps apps has been moved to the new connector.") -BackgroundColor "Black" -ForegroundColor "Green"
Write-Host ("$notmovedApps apps could not be moved to the new connector. Finished.") -BackgroundColor "Black" -ForegroundColor "Green"
Write-Host ("")
Write-Host "To disconnect from Microsoft Graph, please use the Disconnect-MgGraph cmdlet."
Write-Host ("")
```

## Script explanation

| Command | Notes |
| --- | --- |
| [Connect-MgGraph](/en-us/powershell/module/microsoft.graph.authentication/connect-mggraph) | Connects to Microsoft Graph |
| [Get-MgBetaServicePrincipal](/en-us/powershell/module/microsoft.graph.applications/get-mgserviceprincipal) | Gets a service principal |
| [Get-MgBetaOnPremisePublishingProfileConnectorGroup](/en-us/powershell/module/microsoft.graph.beta.applications/get-mgbetaapplication) | Gets an Enterprise Application |
| [Get-MgBetaOnPremisePublishingProfileConnectorGroupApplication](/en-us/powershell/module/microsoft.graph.beta.applications/get-mgbetaonpremisepublishingprofileconnectorgroupapplication) | Lists applications assigned to a connector group |
| [Set-MgBetaApplicationConnectorGroupByRef](/en-us/powershell/module/microsoft.graph.beta.applications/set-mgbetaapplicationconnectorgroupbyref) | Assigns an application to the connector group |