---
layout: Conceptual
title: PowerShell sample - Assign user to a Microsoft Entra application proxy app - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/scripts/powershell-assign-user-to-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: PowerShell example that assigns a user to a Microsoft Entra application proxy application.
ms.custom: 
ms.topic: sample
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: ashishj
ai-usage: ai-assisted
locale: en-us
document_id: 09071013-5d8c-b37e-93b6-5eb8d084018c
document_version_independent_id: 1ded8a28-2e76-4c2b-f2bc-ad0eddf1cc53
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/scripts/powershell-assign-user-to-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/scripts/powershell-assign-user-to-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/scripts/powershell-assign-user-to-app.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c12e63e0-33a8-fda4-c7b5-c9e58be27d41
---

# PowerShell sample - Assign user to a Microsoft Entra application proxy app - Microsoft Entra ID | Microsoft Learn

## Overview

The PowerShell script example assigns a user to a specific Microsoft Entra application proxy application.

If you don't have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

The sample requires the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer.

## Sample script

```powershell
#  This sample script assigns a user to a specific Microsoft Entra application proxy application.
#
#  Tip: You can identify the parameters by using the following PS commands:
#    ServicePrincipalObjectId - Get-MgBetaServicePrincipal -Filter "DisplayName eq '<displayname of the app>'" 
#    UserObjectId - Get-MgBetaUser -ConsistencyLevel eventual -Count userCount -Search '"DisplayName:<name of the user>"'"
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
[string] $ServicePrincipalObjectId = "null",
[parameter(Mandatory=$true)]
[string] $UserObjectId = "null"
)

$servicePrincipalObjectId = $ServicePrincipalObjectId
$userObjectId = $UserObjectId

If (($servicePrincipalObjectId -eq "null") -or ($userObjectId -eq "null")) {

    Write-Host "Parameter is missing." -BackgroundColor "Black" -ForegroundColor "Green"
    Write-Host " "
    Write-Host ".\assign-user-to-app.ps1 -ServicePrincipalObjectId <ObjectId of the Microsoft Entra application proxy application service principal> -UserObjectId <ObjectId of the User>" -BackgroundColor "Black" -ForegroundColor "Green"
    Write-Host " "
    Write-Host "Hints:" -BackgroundColor "Black" -ForegroundColor "Green"
    Write-Host "You can easily identify the parameters by using the following PS commands:" -BackgroundColor "Black" -ForegroundColor "Green"
    Write-Host " "
    Write-Host "ServicePrincipalObjectId - Get-MgBetaServicePrincipal -Filter "DisplayName eq '<displayname of the app>'" " -BackgroundColor "Black" -ForegroundColor "Green"
    Write-Host "UserObjectId - Get-MgBetaUser -ConsistencyLevel eventual -Count userCount -Search '"DisplayName:<name of the user>"'" -BackgroundColor "Black" -ForegroundColor "Green"

    Exit
}

Import-Module Microsoft.Graph.Beta.Applications

Connect-MgGraph -Scope Directory.ReadWrite.All -NoWelcome

New-MgBetaUserAppRoleAssignment -UserId $userObjectId -PrincipalId $userObjectId -ResourceId $servicePrincipalObjectId -AppRoleId "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"

Write-Host ("")
Write-Host ("Finished.") -BackgroundColor "Black" -ForegroundColor "Green"
Write-Host ("")
Write-Host "To disconnect from Microsoft Graph, please use the Disconnect-MgGraph cmdlet."

```

## Script explanation

| Command | Notes |
| --- | --- |
| [Connect-MgGraph](/en-us/powershell/module/microsoft.graph.authentication/connect-mggraph) | Connects to Microsoft Graph |
| [New-MgBetaUserAppRoleAssignment](/en-us/powershell/module/microsoft.graph.beta.applications/new-mgbetauserapproleassignment) | Assigns an app role to the user |