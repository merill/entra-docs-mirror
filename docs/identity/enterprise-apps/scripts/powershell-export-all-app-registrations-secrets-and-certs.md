---
layout: Conceptual
title: 'PowerShell sample: Export secrets and certificates for app registrations - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/scripts/powershell-export-all-app-registrations-secrets-and-certs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: PowerShell example that exports all secrets and certificates for the specified app registrations in your Microsoft Entra tenant.
ms.custom: 
ai-usage: ai-assisted
ms.topic: sample
ms.date: 2025-01-23T00:00:00.0000000Z
ms.reviewer: mifarca
locale: en-us
document_id: 25bc9172-4cc4-5664-d033-206421f76f0b
document_version_independent_id: fcd3096f-fd10-f871-03da-59c2cebe1cd0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/scripts/powershell-export-all-app-registrations-secrets-and-certs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/scripts/powershell-export-all-app-registrations-secrets-and-certs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/scripts/powershell-export-all-app-registrations-secrets-and-certs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ab4bf348-4e85-32c2-0b33-dac391949317
---

# PowerShell sample: Export secrets and certificates for app registrations - Microsoft Entra ID | Microsoft Learn

This PowerShell script example exports all secrets and certificates for the specified app registrations from your directory into a CSV file.

If you don't have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

This sample requires the [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation) SDK module.

## Sample script

```powershell
<#################################################################################
DISCLAIMER:

This is not an official PowerShell Script. We designed it specifically for the situation you have
encountered right now.

Please do not modify or change any preset parameters.

Please note that we will not be able to support the script if it's changed or altered in any way
or used in a different situation for other means.

This code-sample is provided "AS IS" without warranty of any kind, either expressed or implied,
including but not limited to the implied warranties of merchantability and/or fitness for a
particular purpose.

This sample is not supported under any Microsoft standard support program or service.

Microsoft further disclaims all implied warranties including, without limitation, any implied
warranties of merchantability or of fitness for a particular purpose.

The entire risk arising out of the use or performance of the sample and documentation remains with
you.

In no event shall Microsoft, its authors, or anyone else involved in the creation, production, or
delivery of the script be liable for any damages whatsoever (including, without limitation, damages
for loss of business profits, business interruption, loss of business information, or other
pecuniary loss) arising out of the use of or inability to use the sample or documentation, even if
Microsoft has been advised of the possibility of such damages.
#################################################################################>

Connect-MgGraph -Scopes 'Application.Read.All'

$Messages = @{
    DurationNotice = @{
        Info = @(
            'The operation is running and will take longer the more applications the tenant has...'
            'Please wait...'
        ) -join ' '
    }
    Export         = @{
        Info   = 'Where should the CSV file export to?'
        Prompt = 'Enter the full path in the format of <C:\Users\<USER>\Desktop\Users.csv>'
    }
}

Write-Host $Messages.DurationNotice.Info -ForegroundColor yellow

$Applications = Get-MgApplication -All

$Logs = @()

foreach ($App in $Applications) {
    $AppName = $App.DisplayName
    $AppID   = $App.Id
    $ApplID  = $App.AppId

    $AppCreds = Get-MgApplication -ApplicationId $AppID |
        Select-Object PasswordCredentials, KeyCredentials

    $Secrets = $AppCreds.PasswordCredentials
    $Certs   = $AppCreds.KeyCredentials

    ############################################
    $Logs += [PSCustomObject]@{
        'ApplicationName'        = $AppName
        'ApplicationID'          = $ApplID
        'Secret Name'            = $Null
        'Secret Start Date'      = $Null
        'Secret End Date'        = $Null
        'Certificate Name'       = $Null
        'Certificate Start Date' = $Null
        'Certificate End Date'   = $Null
        'Owner'                  = $Null
        'Owner_ObjectID'         = $Null
    }
    ############################################
    foreach ($Secret in $Secrets) {
        $StartDate  = $Secret.StartDateTime
        $EndDate    = $Secret.EndDateTime
        $SecretName = $Secret.DisplayName

        $Owner    = Get-MgApplicationOwner -ApplicationId $App.Id
        $Username = $Owner.AdditionalProperties.userPrincipalName -join ';'
        $OwnerID  = $Owner.Id -join ';'

        if ($null -eq $Owner.AdditionalProperties.userPrincipalName) {
            $Username = @(
                $Owner.AdditionalProperties.displayName
                '**<This is an Application>**'
            ) -join ' '
        }
        if ($null -eq $Owner.AdditionalProperties.displayName) {
            $Username = '<<No Owner>>'
        }

        $Logs += [PSCustomObject]@{
            'ApplicationName'        = $AppName
            'ApplicationID'          = $ApplID
            'Secret Name'            = $SecretName
            'Secret Start Date'      = $StartDate
            'Secret End Date'        = $EndDate
            'Certificate Name'       = $Null
            'Certificate Start Date' = $Null
            'Certificate End Date'   = $Null
            'Owner'                  = $Username
            'Owner_ObjectID'         = $OwnerID
        }
    }

    foreach ($Cert in $Certs) {
        $StartDate = $Cert.StartDateTime
        $EndDate   = $Cert.EndDateTime
        $CertName  = $Cert.DisplayName

        $Owner    = Get-MgApplicationOwner -ApplicationId $App.Id
        $Username = $Owner.AdditionalProperties.userPrincipalName -join ';'
        $OwnerID  = $Owner.Id -join ';'

        if ($null -eq $Owner.AdditionalProperties.userPrincipalName) {
            $Username = @(
                $Owner.AdditionalProperties.displayName
                '**<This is an Application>**'
            ) -join ' '
        }
        if ($null -eq $Owner.AdditionalProperties.displayName) {
            $Username = '<<No Owner>>'
        }

        $Logs += [PSCustomObject]@{
            'ApplicationName'        = $AppName
            'ApplicationID'          = $ApplID
            'Secret Name'            = $Null
            'Certificate Name'       = $CertName
            'Certificate Start Date' = $StartDate
            'Certificate End Date'   = $EndDate
            'Owner'                  = $Username
            'Owner_ObjectID'         = $OwnerID
            'Secret Start Date'      = $Null
            'Secret End Date'        = $Null
        }
    }
}

Write-Host $Messages.Export.Info -ForegroundColor Green
$Path = Read-Host -Prompt $Messages.Export.Prompt
$Logs | Export-Csv $Path -NoTypeInformation -Encoding UTF8
```

## Script explanation

The script can be used directly without any modifications. The admin is asked about the expiration date and whether they would like to see already expired secrets or certificates or not.

The "Add-Member" command is responsible for creating the columns in the CSV file. You can modify the "$Path" variable directly in PowerShell, with a CSV file path, in case you'd prefer the export to be non-interactive.

| Command | Notes |
| --- | --- |
| [Get-MgApplication](/en-us/powershell/module/microsoft.graph.applications/get-mgapplication?view=graph-powershell-1.0&amp;preserve-view=true) | Retrieves an application from your directory. |
| [Get-MgApplicationOwner](/en-us/powershell/module/microsoft.graph.applications/get-mgapplicationowner?view=graph-powershell-1.0&amp;preserve-view=true) | Retrieves the owners of an application from your directory. |