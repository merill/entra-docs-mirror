---
layout: Conceptual
title: PowerShell sample - Microsoft Entra application proxy apps with no certificate - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/scripts/powershell-get-all-custom-domain-no-cert
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: PowerShell example that lists all Microsoft Entra application proxy applications that are using custom domains but don't have a valid TLS/SSL certificate uploaded.
ms.custom: 
ms.topic: sample
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: ashishj
ai-usage: ai-assisted
locale: en-us
document_id: 7b4973d8-4a3d-5b32-7101-c2dbb7ee43d2
document_version_independent_id: 86d9f399-bc5e-7778-1570-27bba7894b81
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/scripts/powershell-get-all-custom-domain-no-cert.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/scripts/powershell-get-all-custom-domain-no-cert
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/scripts/powershell-get-all-custom-domain-no-cert.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 6f4cd3fc-6d6b-a040-4b82-7e446ad3d903
---

# PowerShell sample - Microsoft Entra application proxy apps with no certificate - Microsoft Entra ID | Microsoft Learn

## Overview

The PowerShell script example lists all Microsoft Entra application proxy apps that are using custom domains that don't have a valid TLS/SSL certificate uploaded.

If you don't have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

The sample requires the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer.

## Sample script

```powershell
# This sample script gets all Microsoft Entra application proxy applications using custom domain with no uploaded certificate.
#
# Version 1.0
#
# This script requires PowerShell 5.1 (x64) and one of the following modules:
#
# Microsoft.Graph ver 2.10 or newer
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

$allApps = Get-MgBetaServicePrincipal -Top 100000 | where-object {$_.Tags -Contains "WindowsAzureActiveDirectoryOnPremApp"}

$numberofAadapApps = 0

Write-Host " "
Write-Host "Displaying custom domain Microsoft Entra application proxy applications with no uploaded certificates..." -BackgroundColor "Black" -ForegroundColor "Green"
Write-Host " "

foreach ($item in $allApps) {

 $aadapApp, $aadapAppConf, $aadapAppConf1 = $null, $null, $null
 
 $aadapAppId =  Get-MgBetaApplication -Top 100000 | where-object {$_.AppId -eq $item.AppId}
 $aadapAppConf = Get-MgBetaApplication -ApplicationId $aadapAppId.Id -ErrorAction SilentlyContinue -select OnPremisesPublishing | select OnPremisesPublishing -expand OnPremisesPublishing 
 $aadapAppConf1 = Get-MgBetaApplication -ApplicationId $aadapAppId.Id -ErrorAction SilentlyContinue -select OnPremisesPublishing | select OnPremisesPublishing -expand OnPremisesPublishing `
  | select verifiedCustomDomainCertificatesMetadata -expand verifiedCustomDomainCertificatesMetadata 

  if (($aadapAppConf -ne $null) -and ($aadapAppConf.ExternalUrl -notmatch ".msappproxy.net")) {
   
   if ($aadapAppConf1.VerifiedCustomDomainCertificatesMetadata.Thumbprint.Length -eq 0) {
  
     Write-Host $item.DisplayName"(AppId: " $item.AppId ", ObjId:" $item.Id")" -BackgroundColor "Black" -ForegroundColor "White"
     Write-Host
     Write-Host "External Url: " $aadapAppConf.ExternalUrl
     Write-Host "Internal Url: " $aadapAppConf.InternalUrl
     Write-Host "Pre-authentication: " $aadapAppConf.ExternalAuthenticationType
     Write-Host
  
     $numberofAadapApps = $numberofAadapApps + 1              
    }
  
   }
  
}

Write-Host
Write-Host "Number of the custom domain Microsoft Entra application proxy applications with no uploaded certificate: " $numberofAadapApps -BackgroundColor "Black" -ForegroundColor "White"
Write-Host ("")

Write-Host
Write-Host "Finished." -BackgroundColor "Black" -ForegroundColor "Green"
Write-Host "To disconnect from Microsoft Graph, please use the Disconnect-MgGraph cmdlet."
```

## Script explanation

| Command | Notes |
| --- | --- |
| [Connect-MgGraph](/en-us/powershell/module/microsoft.graph.authentication/connect-mggraph) | Connects to Microsoft Graph |
| [Get-MgBetaServicePrincipal](/en-us/powershell/module/microsoft.graph.applications/get-mgserviceprincipal) | Gets a service principal |
| [Get-MgBetaApplication](/en-us/powershell/module/microsoft.graph.beta.applications/get-mgbetaapplication) | Gets an Enterprise Application |