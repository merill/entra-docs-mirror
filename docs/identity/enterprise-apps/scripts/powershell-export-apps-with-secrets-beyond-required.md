---
layout: Conceptual
title: 'PowerShell sample: Export apps with secrets and certificates expiring beyond the required date - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/scripts/powershell-export-apps-with-secrets-beyond-required
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: PowerShell example that exports all apps with secrets and certificates expiring beyond the required date for the specified apps in your Microsoft Entra tenant.
ms.custom: no-azure-ad-ps-ref
ms.topic: sample
ms.date: 2025-01-23T00:00:00.0000000Z
ms.reviewer: mifarca
locale: en-us
document_id: fd6dc6dd-05c6-c272-e314-ab970040e149
document_version_independent_id: cb6c1d60-f9f5-2fc5-57a1-64476dc1c3fd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/scripts/powershell-export-apps-with-secrets-beyond-required.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/scripts/powershell-export-apps-with-secrets-beyond-required
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/scripts/powershell-export-apps-with-secrets-beyond-required.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7f2594d8-6903-1a39-f6e9-d2157b3405f6
---

# PowerShell sample: Export apps with secrets and certificates expiring beyond the required date - Microsoft Entra ID | Microsoft Learn

This PowerShell script example exports all app registrations' secrets and certificates expiring beyond a required period. It performs this task for the specified apps from your directory. The script runs non-interactively. The output is saved in a CSV file.

If you don't have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

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

$loginURL = 'https://login.microsoftonline.com'
$resource = 'https://graph.microsoft.com'

#PARAMETERS TO CHANGE
$ClientID     = 'App ID'
$ClientSecret = 'APP Secret'
$TenantName   = 'TENANT.onmicrosoft.com'

$Months = 'Number of months'
$Path   = 'add a path here\File.csv'
###################################################################
#Repeating Function to get an Access Token based on the parameters:
function Get-RefreshedToken($LoginURL, $ClientID, $ClientSecret, $TenantName) {
    $RequestParameters = @{
        Method = 'POST'
        Uri    = "$LoginURL/$TenantName/oauth2/v2.0/token"
        Body   = @{
            grant_type    = 'client_credentials'
            client_id     = $ClientID
            client_secret = $ClientSecret
            scope         = 'https://graph.microsoft.com/.default'
        }
    }

    Invoke-RestMethod @RequestParameters
}

#BUILD THE ACCESS TOKEN
$RefreshParameters = @{
    LoginURL     = $loginURL
    ClientID     = $ClientID
    ClientSecret = $ClientSecret
    TenantName   = $TenantName
}
$OAuth    = Get-RefreshedToken @RefreshParameters
$Identity = $OAuth.access_token

##############################################

$HeaderParams = @{
    'Authorization' = "$($OAuth.token_type) $($Identity)"
}
$AppsSecrets = 'https://graph.microsoft.com/v1.0/applications'

$ApplicationsList = Invoke-WebRequest -Headers $HeaderParams -Uri $AppsSecrets -Method GET

$Logs        = @()
$NextCounter = 0

do {
    $ApplicationEvents = $ApplicationsList.Content |
        ConvertFrom-Json |
        Select-Object -ExpandProperty value

    foreach ($ApplicationEvent in $ApplicationEvents) {
        $IDs     = $ApplicationEvent.id
        $AppName = $ApplicationEvent.displayName
        $AppID   = $ApplicationEvent.appId
        $Secrets = $ApplicationEvent.passwordCredentials

        $NextCounter++

        foreach ($Secret in $Secrets) {
            $StartDate       = $Secret.startDateTime
            $EndDate         = $Secret.endDateTime
            $pos             = $StartDate.IndexOf('T')
            $LeftPart        = $StartDate.Substring(0, $pos)
            $Position        = $EndDate.IndexOf('T')
            $LeftPartEnd     = $EndDate.Substring(0, $pos)
            $DateStringStart = [Datetime]::ParseExact($LeftPart, 'yyyy-MM-dd', $null)
            $DateStringEnd   = [Datetime]::ParseExact($LeftPartEnd, 'yyyy-MM-dd', $null)
            $OptimalDate     = $DateStringStart.AddMonths($Months)

            if ($OptimalDate -lt $DateStringEnd) {
                $Log = [PSCustomObject]@{
                    'Application'       = $AppName
                    'AppID'             = $AppID
                    'Secret Start Date' = $DateStringStart
                    'Secret End Date'   = $DateStringEnd
                }

                $OwnerRequestParams = @{
                    Headers = $HeaderParams
                    Uri     = "https://graph.microsoft.com/v1.0/applications/$IDs/owners"
                    Method  = 'GET'
                }
                $ApplicationsOwners = Invoke-WebRequest @OwnerRequestParams

                $Users = $ApplicationsOwners.Content |
                    ConvertFrom-Json |
                    Select-Object -ExpandProperty value

                foreach ($User in $Users) {
                    $Owner = $User.displayname
                    $Log | Add-Member -MemberType NoteProperty -Name  'AppOwner' -Value $Owner
                }

                $Logs += $Log
            }
        }

        If ($NextCounter -eq 100) {
            $OData = $ApplicationsList.Content | ConvertFrom-Json
            $AppsSecrets = $OData.'@odata.nextLink'
            try {
                $ListRequestParams = @{
                    UseBasicParsing = $true
                    Headers         = $HeaderParams
                    Uri             = $AppsSecrets
                    Method          = 'GET'
                    ContentType     = 'application/Json'
                }
                $ApplicationsList = Invoke-WebRequest @ListRequestParams
            } catch {
                $_
            }

            $NextCounter = 0

            Start-Sleep -Seconds 1
        }
    }

} while ($AppsSecrets -ne $null)

$Logs | Export-Csv $Path -NoTypeInformation -Encoding UTF8
```

## Script explanation

This script is working non-interactively. The admin using it needs to change the values in the "#PARAMETERS TO CHANGE" section. They need to enter their own App ID, Application Secret, and Tenant Name. They also need to specify the period for the apps' credentials expiration. Finally, they need to set the path where the CSV is exported.

This script uses the [Client_Credential Oauth Flow](../../../identity-platform/v2-oauth2-client-creds-grant-flow) The function "RefreshToken" builds the access token based on the values of the parameters modified by the admin.

The "Add-Member" command is responsible for creating the columns in the CSV file.

| Command | Notes |
| --- | --- |
| [Invoke-WebRequest](/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest) | Sends HTTP and HTTPS requests to a web page or web service. It parses the response and returns collections of links, images, and other significant HTML elements. |