---
layout: Conceptual
title: PowerShell sample - List all Microsoft Entra private network connector groups - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/scripts/powershell-get-all-connectors
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: PowerShell example that lists all Microsoft Entra private network connector groups and connectors in your directory.
ms.custom: 
ms.topic: sample
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: ashishj
ai-usage: ai-assisted
locale: en-us
document_id: d175b48a-7910-10dd-05fe-8ab31dc76200
document_version_independent_id: d2c39813-85e6-dce0-5b80-cd0d8e9ec778
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/scripts/powershell-get-all-connectors.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/scripts/powershell-get-all-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/scripts/powershell-get-all-connectors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 5990bcdd-6fff-de9e-1d25-65569c89b92d
---

# PowerShell sample - List all Microsoft Entra private network connector groups - Microsoft Entra ID | Microsoft Learn

## Overview

The PowerShell script example lists all Microsoft Entra private network connector groups and connectors in your directory.

If you don't have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

This sample requires the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer.

## Sample script

```powershell
# This sample script gets all Microsoft Entra private network connector groups with the included connectors.
#
# Version 1.0
#
# This script requires PowerShell 5.1 (x64) or beyond and one of the following modules:
#
# Microsoft.Graph.Beta ver 2.10 or newer
#
# Before you begin:
#    
#    Required Microsoft Entra role at least Application Administrator or Application Developer 
#    or appropriate custom permissions as documented https://learn.microsoft.com/azure/active-directory/roles/custom-enterprise-app-permissions
#
# 

Import-Module Microsoft.Graph.Beta.Applications

Connect-MgGraph -Scope Directory.Read.All -NoWelcome

Write-Host "Reading Microsoft Entra private network connector groups. This operation might take longer..." -BackgroundColor "Black" -ForegroundColor "Green"

$aadapConnectorGroups= Get-MgBetaOnPremisePublishingProfileConnectorGroup -OnPremisesPublishingProfileId "applicationProxy" -Top 100000 

$countAssignedApps, $CountOfConnectorGroups = 0

foreach ($item in $aadapConnectorGroups) {
   
     If ($item.ConnectorGroupType -eq "applicationProxy") {

     Write-Host "Connector group: " $item.Name, "(Id:" $item.Id ")" -BackgroundColor "Black" -ForegroundColor "White" 
     Write-Host "Region: " $item.Region
     
     Write-Host " "

     $connectors = Get-MgBetaOnPremisePublishingProfileConnectorGroupMember -ConnectorGroupId $item.Id -OnPremisesPublishingProfileId "applicationProxy" 

     $connectors | ft

     " ";

     $CountOfConnectorGroups = $CountOfConnectorGroups + 1

     }
}  

Write-Host ("")
Write-Host ("Number of Microsoft Entra private network connector Groups: $CountOfConnectorGroups")
Write-Host ("")
Write-Host ("Finished.") -BackgroundColor "Black" -ForegroundColor "Green"
Write-Host "To disconnect from Microsoft Graph, please use the Disconnect-MgGraph cmdlet."
```

## Script explanation

| Command | Notes |
| --- | --- |
| [Connect-MgGraph](/en-us/powershell/module/microsoft.graph.authentication/connect-mggraph) | Connects to Microsoft Graph |
| [Get-MgBetaOnPremisePublishingProfileConnectorGroup](/en-us/powershell/module/microsoft.graph.beta.applications/get-mgbetaonpremisepublishingprofileconnectorgroup) | Gets a connector group |
| [Get-MgBetaOnPremisePublishingProfileConnectorGroupMember](/en-us/powershell/module/microsoft.graph.beta.applications/get-mgbetaonpremisepublishingprofileconnectorgroupmember) | Gets the members of a connector group |