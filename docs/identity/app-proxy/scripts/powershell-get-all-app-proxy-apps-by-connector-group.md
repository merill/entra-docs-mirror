---
layout: Conceptual
title: List Microsoft Entra private network connector groups for apps - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/scripts/powershell-get-all-app-proxy-apps-by-connector-group
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: PowerShell example that lists all Microsoft Entra private network connector groups with the assigned applications.
ms.custom: 
ms.topic: sample
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: ashishj
ai-usage: ai-assisted
locale: en-us
document_id: 885962c3-89c0-319a-b9fd-84f50d490925
document_version_independent_id: 8fbf93ab-7fdf-13e5-7b64-c0e0e7a8cb7c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/scripts/powershell-get-all-app-proxy-apps-by-connector-group.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/scripts/powershell-get-all-app-proxy-apps-by-connector-group
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/scripts/powershell-get-all-app-proxy-apps-by-connector-group.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 69bdecdb-d1e4-4062-47f7-09172a15ea76
---

# List Microsoft Entra private network connector groups for apps - Microsoft Entra ID | Microsoft Learn

## Overview

The PowerShell script example lists information about all Microsoft Entra private network connector groups with the assigned applications.

If you don't have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

The sample requires the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer.

## Sample script

```powershell
# This sample script gets all Microsoft Entra private network connector groups with the assigned applications.
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

Write-Host "Reading service principals. This operation might take longer..." -BackgroundColor "Black" -ForegroundColor "Green" 

$aadapServPrinc = Get-MgBetaServicePrincipal -Top 100000 | where-object {$_.Tags -Contains "WindowsAzureActiveDirectoryOnPremApp"}

Write-Host "Reading Microsoft Entra applications. This operation might take longer..." -BackgroundColor "Black" -ForegroundColor "Green"

$allApps = Get-MgBetaApplication -Top 100000

Write-Host "Reading application. This operation might take longer..." -BackgroundColor "Black" -ForegroundColor "Green"

$aadapApp = $aadapServPrinc | ForEach-Object {$allApps.AppId -match $_.AppId}
 
Write-Host "Reading connector groups. This operation might take longer..." -BackgroundColor "Black" -ForegroundColor "Green"

$aadapConnectorGroups= Get-MgBetaOnPremisePublishingProfileConnectorGroup -OnPremisesPublishingProfileId "applicationProxy" -Top 100000 

Write-Host "Displaying connector groups and assigned applications..." -BackgroundColor "Black" -ForegroundColor "Green"
Write-Host " "

foreach ($item in $aadapConnectorGroups)
 {
  
   If ($item.ConnectorGroupType -eq "applicationProxy")
    {  
        "Connector group: " + $item.Name + " (Id: " + $item.Id+ ") - Region: " + $item.Region;
          
        $assignedApps= Get-MgBetaOnPremisePublishingProfileConnectorGroupApplication -ConnectorGroupId $item.Id -OnPremisesPublishingProfileId "applicationProxy";
    
        " "; 

        foreach ($item2 in $assignedApps)
         {
           
           $Item2.DisplayName + " (AppId: " + $item2.AppId+ ")"
         } 
    
    " ";
       
    }
           
 }   

Write-Host ("")
Write-Host ("Finished.") -BackgroundColor "Black" -ForegroundColor "Green"
Write-Host "To disconnect from Microsoft Graph, please use the Disconnect-MgGraph cmdlet." 
```

## Script explanation

| Command | Notes |
| --- | --- |
| [Connect-MgGraph](/en-us/powershell/module/microsoft.graph.authentication/connect-mggraph) | Connects to Microsoft Graph |
| [Get-MgBetaServicePrincipal](/en-us/powershell/module/microsoft.graph.applications/get-mgserviceprincipal) | Gets a service principal |
| [Get-MgBetaApplication](/en-us/powershell/module/microsoft.graph.beta.applications/get-mgbetaapplication) | Gets an Enterprise Application |
| [Get-MgBetaOnPremisePublishingProfileConnectorGroup](/en-us/powershell/module/microsoft.graph.beta.applications/get-mgbetaonpremisepublishingprofileconnectorgroup) | Gets a connector group |
| [Get-MgBetaOnPremisePublishingProfileConnectorGroupApplication](/en-us/powershell/module/microsoft.graph.beta.applications/get-mgbetaonpremisepublishingprofileconnectorgroupapplication) | Gets applications assigned to a connector group |