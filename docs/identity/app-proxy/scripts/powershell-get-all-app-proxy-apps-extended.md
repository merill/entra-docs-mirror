---
layout: Conceptual
title: PowerShell sample - List extended info for Microsoft Entra application proxy apps - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/scripts/powershell-get-all-app-proxy-apps-extended
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: PowerShell example that lists all Microsoft Entra application proxy applications along with the application ID (AppId), name (DisplayName), external URL (ExternalUrl), internal URL (InternalUrl), and authentication type (ExternalAuthenticationType).
ms.custom: 
ms.topic: sample
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: ashishj
ai-usage: ai-assisted
locale: en-us
document_id: c4548fbf-74c9-eb00-c500-512ca44e847b
document_version_independent_id: f5226110-5836-af4a-f111-4063c84f99e9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/scripts/powershell-get-all-app-proxy-apps-extended.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/scripts/powershell-get-all-app-proxy-apps-extended
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/scripts/powershell-get-all-app-proxy-apps-extended.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: d8429d46-b39d-fbed-fc9c-7d288f9ce088
---

# PowerShell sample - List extended info for Microsoft Entra application proxy apps - Microsoft Entra ID | Microsoft Learn

## Overview

The PowerShell script example lists information about all Microsoft Entra application proxy applications, including the application ID (AppId), name (DisplayName), external URL (ExternalUrl), internal URL (InternalUrl), authentication type (ExternalAuthenticationType), single sign-on (SSO) mode and further settings.

Changing the value of the `$ssoMode` variable enables a filtered output by SSO mode. Further details are documented in the script.

If you don't have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

The sample requires the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer.

## Sample script

```powershell
# This sample script enumerates all Microsoft Entra application proxy applications with configuration details
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

$ssoMode = "All"

# Change $ssoMode to filter the output based on the configured SSO type
# All                           - all Microsoft Entra application proxy apps (no filter)
# none                          - Microsoft Entra application proxy apps configured with no SSO, SAML, Linked, Password
# OnPremisesKerberos            - Microsoft Entra application proxy apps configured with Windows Integrated SSO (Kerberos Constrained Delegation)
# aadHeaderBased                - Microsoft Entra Native Header-based authentication
# pingHeaderBased               - Microsoft Entra Ping Header-based authentication
# oAuthToken                    - Microsoft Entra OAuth-based SSO

Import-Module Microsoft.Graph.Beta.Applications

Connect-MgGraph -Scope Directory.Read.All -NoWelcome

Write-Host "Reading service principals. This operation might take longer..." -BackgroundColor "Black" -ForegroundColor "Green" 

$aadapServPrinc = Get-MgBetaServicePrincipal -Top 100000 | where-object {$_.Tags -Contains "WindowsAzureActiveDirectoryOnPremApp"}

Write-Host "Reading Microsoft Entra applications. This operation might take longer..." -BackgroundColor "Black" -ForegroundColor "Green"

$allApps = Get-MgBetaApplication -Top 100000

Write-Host "Filtering Microsoft Entra application proxy applications. This operation might take longer..." -BackgroundColor "Black" -ForegroundColor "Green"

$aadapApp = $null

foreach ($item in $aadapServPrinc) {
   foreach ($item2 in $allApps) {
    
     if ($item.AppId -eq $item2.AppId) {[array]$aadapApp += $item2}

    }
}

$numberofAadapApps, $numberofFilteredAadapApps = 0, 0

Write-Host "Displaying all Microsoft Entra application proxy applications with configuration details..." -BackgroundColor "Black" -ForegroundColor "Green"
Write-Host "SSO mode filter: " $ssoMode -BackgroundColor "Black" -ForegroundColor "Green"
Write-Host " "

foreach ($item in $aadapApp) {
 
 $aadapAppConf, $aadapAppConf1, $aadapAppConf2, $aadapAppConf3, $aadapAppConf4 = $null, $null, $null, $null, $null

 $aadapAppConf = Get-MgBetaApplication -ApplicationId $item.Id -ErrorAction SilentlyContinue -select OnPremisesPublishing | select OnPremisesPublishing -expand OnPremisesPublishing 
 $aadapAppConf1 = Get-MgBetaApplication -ApplicationId $item.Id -ErrorAction SilentlyContinue -select OnPremisesPublishing | select OnPremisesPublishing -expand OnPremisesPublishing `
  | select singleSignOnSettings -expand SingleSignOnSettings 
 $aadapAppConf2 = Get-MgBetaApplication -ApplicationId $item.Id -ErrorAction SilentlyContinue -select OnPremisesPublishing | select OnPremisesPublishing -expand OnPremisesPublishing `
  | select verifiedCustomDomainCertificatesMetadata -expand verifiedCustomDomainCertificatesMetadata 
 $aadapAppConf3 = Get-MgBetaApplication -ApplicationId $item.Id -ErrorAction SilentlyContinue -select OnPremisesPublishing | select OnPremisesPublishing -expand OnPremisesPublishing | select OnPremisesApplicationSegments -expand OnPremisesApplicationSegments
 $aadapAppConf4 = Get-MgBetaApplication -ApplicationId $item.Id -ErrorAction SilentlyContinue -select OnPremisesPublishing | select OnPremisesPublishing -expand OnPremisesPublishing `
  | select singleSignOnSettings -expand SingleSignOnSettings | select KerberosSignOnSettings -expand KerberosSignOnSettings 

    if ($aadapAppConf -ne $null) {
   
      if ($ssoMode -eq "All" -Or $aadapAppConf1.SingleSignOnSettings.SingleSignOnMode -eq $ssoMode) {
    
        Write-Host $Item.DisplayName " (AppId: " $item.AppId  " / ObjectId: " $item.Id ")" -BackgroundColor "Black" -ForegroundColor "White"    

        Write-Host " "

        Write-Host "External Url: " $aadapAppConf.ExternalUrl
        Write-Host "Internal Url: " $aadapAppConf.InternalUrl
        Write-Host "Pre authentication type: " $aadapAppConf.ExternalAuthenticationType
        Write-Host " "
        Write-Host "SSO mode: " $aadapAppConf1.SingleSignOnSettings.SingleSignOnMode

      If ($aadapAppConf1.SingleSignOnMode -eq "OnPremisesKerberos") {

        Write-Host "Service Principal Name (SPN): " $aadapAppConf4.KerberosServicePrincipalName
        Write-Host "Username Mapping Attribute: " $aadapAppConf4.KerberosSignOnMappingAttributeType
      
        }
      
        Write-Host " "
        Write-Host "Backend Application Timeout: " $aadapAppConf.ApplicationServerTimeout
        Write-Host "Translate URLs in Headers: " $aadapAppConf.IsTranslateHostHeaderEnabled
        Write-Host "Translate URLs in Application Body: " $aadapAppConf.IsTranslateLinksInBodyEnabled
        Write-Host "Use HTTP-Only Cookie: " $aadapAppConf.IsHttpOnlyCookieEnabled
        Write-Host "Use Secure Cookie: " $aadapAppConf.IsSecureCookieEnabled
        Write-Host "Use Persistent Cookie: " $aadapAppConf.IsPersistentCookieEnabled
        Write-Host "Backend Certification Validation: " $aadapAppConf.IsBackendCertificateValidationEnabled

      If ($aadapAppConf3.Count -gt 0) { Write-Host "Complex App."}
      
      If ($aadapAppConf2.VerifiedCustomDomainCertificatesMetadata.Thumbprint.Length -ne 0) {
       
        Write-Host " "
        Write-Host "SSL Certificate details:"
        Write-Host "Certificate SubjectName: " $aadapAppConf2.VerifiedCustomDomainCertificatesMetadata.SubjectName
        Write-Host "Certificate Issuer: " $aadapAppConf2.VerifiedCustomDomainCertificatesMetadata.Issuer
        Write-Host "Certificate Thumbprint: " $aadapAppConf2.VerifiedCustomDomainCertificatesMetadata.Thumbprint
        Write-Host "Valid from: " $aadapAppConf2.VerifiedCustomDomainCertificatesMetadata.IssueDate
        Write-Host "Valid to: " $aadapAppConf2.VerifiedCustomDomainCertificatesMetadata.ExpiryDate
       
       } 

      $numberofFilteredAadapApps = $numberofFilteredAadapApps + 1
      
        Write-Host
      }

      $numberofAadapApps = $numberofAadapApps + 1          

     }
}

Write-Host "Number of the Microsoft Entra application proxy Applications: " $numberofAadapApps
Write-Host "Number of the filtered Microsoft Entra application proxy Applications: " $numberofFilteredAadapApps
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