---
layout: Conceptual
title: PowerShell sample - Get the auth token for registering your Microsoft Entra private network connector through Azure, AWS, or GCP Marketplaces | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/scripts/powershell-get-token
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: PowerShell example that gets the auth token for registering your Microsoft Entra private network connector through Azure, AWS, or GCP Marketplaces.
ms.topic: sample
ms.date: 2026-03-16T00:00:00.0000000Z
ms.reviewer: katabish
locale: en-us
document_id: a682c533-35ea-0090-0a50-875ba7fae668
document_version_independent_id: a682c533-35ea-0090-0a50-875ba7fae668
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/scripts/powershell-get-token.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/scripts/powershell-get-token
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/scripts/powershell-get-token.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1d393655-fce0-d2dd-a34d-3c445bce1a14
---

# PowerShell sample - Get the auth token for registering your Microsoft Entra private network connector through Azure, AWS, or GCP Marketplaces | Microsoft Learn

## Overview

The PowerShell script helps you get the auth token for registering your Microsoft Entra private network connector through [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftcorporation1687208452115.entraprivatenetworkconnector?tab=overview), [AWS Marketplace](https://aws.amazon.com/marketplace/pp/prodview-cgpbjiaphamuc), or [GCP Marketplace](https://console.cloud.google.com/marketplace/product/ciem-entra/entraprivatenetworkconnector?hl=en).

If you don't have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

Note

We recommend that you use the Azure Az PowerShell module to interact with Azure. See [Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) to get started. To learn how to migrate to the Az PowerShell module, see [Migrate Azure PowerShell from AzureRM to Az](/en-us/powershell/azure/migrate-from-azurerm-to-az).

The sample requires the [Microsoft Graph Beta PowerShell module](/en-us/powershell/microsoftgraph/installation) 2.10 or newer.

## Important considerations

- Run the PowerShell script as an Administrator from an elevated PowerShell ISE.
- Don't run the script on a Windows computer where the private network connector is already installed.
- Make sure there's no `C:\temp` folder on the machine. If you have some files stored in a `C:\temp` folder, move them before you run the script.
- After the script runs successfully, the access token is available at `C:\token.txt`.

## Sample script

```powershell
# This sample script lets you obtain the Auth Token that you can use for registering the Entra private network connector through Marketplace.
#
# Version 1.2
#
# This script requires following 
#    - PowerShell 5.1 (x64) or beyond
#    - Module: MicrosoftEntraPrivateNetworkConnectorPSModule 
#
# The script will get the module as result of Entra Private Network Connector Installation and quiet Registration (/q flag). A quiet installation doesn't prompt you to accept the End-User License Agreement.
# This script will uninstall the Entra Private Network Connector once the required modules are downloaded. 
#
# Before you begin:
#    
# - Make sure you are running PowerShell as an Administrator
# - You are on Windows Machine which is not running the Entra Private Network Connector already. If you already have a connector installed, quiet registration step below will fail. 
# - Make sure there is no C:\temp folder on the machine. If you have some files stored, please move those before running the script 

# Make sure ExecutionPolicy is set to Unrestricted
Set-ExecutionPolicy UnRestricted -Force

# The script will use a temp folder on C Drive. First it will remove the folder and create a new folder to ensure its empty.
$tempPath = "C:\temp"
$tokenPath = "C:\token.txt"

# Check if the folder exists
if (Test-Path -Path $tempPath) {
    Write-Host "Your C Drive has existing temp folder that is being deleted"
    Remove-Item -Path $tempPath -Recurse -Force
} 

# Creating C:\temp folder
New-Item -ItemType Directory -Path $tempPath -Force | Out-Null

# Copy Required Dlls 
Write-Host "Downloading Entra Private Network Connector Installer..."
Invoke-WebRequest https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/DownloadConnectorInstaller -OutFile "$tempPath\MicrosoftEntraPrivateNetworkConnectorInstaller.exe"

# Set the prompt path to C:\temp
Set-Location -Path $tempPath

# Quiet Registration of the Connector. This step will provide the required Module for acquiring the token. 
# At the end of this step, you should see 2 folders under C:\Program Files. 1) Microsoft Entra private network connector 2) Microsoft Entra private network connector updater
# These folders contains the required modules needed for getting the token. 
Write-Host "Installing connector (quiet mode)..."
Start-Process -FilePath ".\MicrosoftEntraPrivateNetworkConnectorInstaller.exe" -ArgumentList "REGISTERCONNECTOR=`"false`"", "/q" -Wait

# Wait 60 seconds for installation to complete
Write-Host "Waiting for installation to complete..."
Start-Sleep -Seconds 60

$folderPath = "C:\Program Files\Microsoft Entra private network connector\Modules\MicrosoftEntraPrivateNetworkConnectorPSModule"

# Check if the Module exists
if (Test-Path -Path $folderPath) {
    Write-Host "The Module is successfully made available at path: $folderPath"
    
    # Set the prompt path to C:\Program Files\Microsoft Entra private network connector\Modules\MicrosoftEntraPrivateNetworkConnectorPSModule
    Set-Location -Path "C:\Program Files\Microsoft Entra private network connector\Modules\MicrosoftEntraPrivateNetworkConnectorPSModule"

    # Import Module 
    Import-Module ..\MicrosoftEntraPrivateNetworkConnectorPSModule -ErrorAction Stop

    # Load MSAL  
    Add-Type -Path .\Microsoft.Identity.Client.dll

    # The AAD authentication endpoint uri
    $authority = "https://login.microsoftonline.com/common/oauth2/v2.0/authorize"

    # The application ID of the connector in AAD. Use the Connector AppId below
    $connectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489"

    # The AppIdUri of the registration service in AAD
    $registrationServiceAppIdUri = "https://proxy.cloudwebappproxy.net/registerapp/user_impersonation"

    # Define the resources and scopes you want to call
    $scopes = New-Object System.Collections.ObjectModel.Collection["string"]
    $scopes.Add($registrationServiceAppIdUri)

    $app = [Microsoft.Identity.Client.PublicClientApplicationBuilder]::Create($connectorAppId).WithAuthority($authority).WithDefaultRedirectUri().Build()

    [Microsoft.Identity.Client.IAccount] $account = $null

    # Acquiring the token
    Write-Host "Acquiring authentication token (interactive login required)..."
    $authResult = $null
    $authResult = $app.AcquireTokenInteractive($scopes).WithAccount($account).ExecuteAsync().ConfigureAwait($false).GetAwaiter().GetResult()

    # Check AuthN result
    If (($authResult) -and ($authResult.AccessToken) -and ($authResult.TenantId)) {
        $token = $authResult.AccessToken
        $tenantId = $authResult.TenantId
        
        $accessToken = $token

        New-Item -ItemType File -Path $tokenPath -Force | Out-Null
        Set-Content -Path $tokenPath -Value "$accessToken"
        
        Write-Host "Token successfully acquired and saved to $tokenPath"

        # Set the prompt path to C: 
        Set-Location -Path "C:\"

        # Uninstall the Connector from your machine.
        # You can do so programmatically (below) or manually by double clicking C:\temp\MicrosoftEntraPrivateNetworkConnectorInstaller.exe and choose Uninstall. 
        # Note that if the Connector service is not uninstalled properly, next iteration can fail on this machine.
        Write-Host "Uninstalling connector..."
        Start-Process -FilePath "$tempPath\MicrosoftEntraPrivateNetworkConnectorInstaller.exe" -ArgumentList "/uninstall", "/quiet" -Wait

        # Wait 60 seconds
        Write-Host "Waiting for uninstallation to complete..."
        Start-Sleep -Seconds 60

        # Delete the related files
        Write-Host "Cleaning up files..."
        if (Test-Path -Path $tempPath) {
            try {
                Remove-Item -Path $tempPath -Recurse -Force
            } catch {
                Write-Warning "Could not fully remove '$tempPath': $_"
            }
        }
        if (Test-Path -Path "C:\Program Files\Microsoft Entra private network connector") {
            try {
                Remove-Item -Path "C:\Program Files\Microsoft Entra private network connector" -Recurse -Force
            } catch {
                Write-Warning "Could not fully remove 'Microsoft Entra private network connector' folder: $_"
            }
        }
        if (Test-Path -Path "C:\Program Files\Microsoft Entra private network connector updater") {
            try {
                Remove-Item -Path "C:\Program Files\Microsoft Entra private network connector updater" -Recurse -Force
            } catch {
                Write-Warning "Could not fully remove 'Microsoft Entra private network connector updater' folder: $_"
            }
        }

        Write-Output "Access Token that you acquired is available in $tokenPath."
        Write-Output "Please ensure no additional spaces are introduced when copying token to marketplace input form. Introducing spaces can change the token and can cause failures"

    }
    else {
        Write-Error "Authentication failed: result, access token, or tenant ID was null. No token has been saved. Please re-run the script and complete the interactive login."
        Set-Location -Path "C:\"
        return
    }
}
else {
    Write-Host "The required module is not made available at path: $folderPath"
    Write-Host "This could be related to left over state from previous installation of connector on this machine."
    Write-Host "You can try to go to c:\temp\ and double click the MicrosoftEntraPrivateNetworkConnectorInstaller.exe file. Click Uninstall if visible. This can clean the state."
    Write-Host "If you don't have .exe file, you can download it from https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/DownloadConnectorInstaller and double click it to Uninstall"
    Write-Host "Try Again after the state is clean"
    return
}
```