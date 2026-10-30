---
layout: Conceptual
title: Silent install Microsoft Entra private network connector - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-register-connector-powershell
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Create a PowerShell script for unattended installation and registration of the Microsoft Entra private network connector for bulk deployments or servers without a UI.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 32f92666-005c-2440-db8c-5f95536ca031
document_version_independent_id: 32f92666-005c-2440-db8c-5f95536ca031
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-register-connector-powershell.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-register-connector-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-register-connector-powershell.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d1362980-0cc5-ab4f-1a28-8edeb911cc5f
---

# Silent install Microsoft Entra private network connector - Global Secure Access | Microsoft Learn

## Overview

This article helps you create a Windows PowerShell script that enables unattended installation and registration for your Microsoft Entra private network connector.

Unattended installation is useful when you want to:

- Install the connector on Windows servers that don't have user interface enabled, or that you can't access with Remote Desktop.
- Install and register many connectors at once.
- Integrate the connector installation and registration as part of another procedure.
- Create a standard server image that contains the connector bits but isn't registered.

For the [private network connector](concept-connectors) to work, you must register it with Microsoft Entra ID. Registration is done in the user interface when you install the connector, but you can use PowerShell to automate the process.

There are two steps for an unattended installation. First, install the connector. Second, register the connector with Microsoft Entra ID.

Important

If you are installing the connector for the Microsoft Azure Government cloud, review the [prerequisites](../identity/hybrid/connect/reference-connect-government-cloud#allow-access-to-urls) and [installation steps](../identity/hybrid/connect/reference-connect-government-cloud#install-the-agent-for-the-azure-government-cloud). The Microsoft Azure Government cloud requires enabling access to a different set of URLs and an additional parameter to run the installation.

## Install the connector

Use the following steps to install the connector without registering it:

1. Open a command prompt.
2. Run the following command, the `/q` flag means quiet installation. A quiet installation doesn't prompt you to accept the End-User License Agreement.

    ```
    MicrosoftEntraPrivateNetworkConnectorInstaller.exe REGISTERCONNECTOR="false" /q
    ```

## Register the connector with Microsoft Entra ID

Register the connector using a token created offline.

### Register the connector using a token created offline

1. Create an offline token using the `AuthenticationContext` class using the values in this code snippet or PowerShell cmdlets:

    **Using C#:**

    ```csharp
    using System;
    using System.Linq;
    using System.Collections.Generic;
    using Microsoft.Identity.Client;
    
    class Program
    {
       #region constants
       /// <summary>
       /// The AAD authentication endpoint uri
       /// </summary>
       static readonly string AadAuthenticationEndpoint = "https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    
       /// <summary>
       /// The application ID of the connector in AAD
       /// </summary>
       static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";
    
       /// <summary>
       /// The AppIdUri of the registration service in AAD
       /// </summary>
       static readonly string RegistrationServiceAppIdUri = "https://proxy.cloudwebappproxy.net/registerapp/user_impersonation";
    
       #endregion
    
       #region private members
       private string token;
       private string tenantID;
       #endregion
    
       public void GetAuthenticationToken()
       {
          IPublicClientApplication clientApp = PublicClientApplicationBuilder
             .Create(ConnectorAppId)
             .WithDefaultRedirectUri() // will automatically use the default Uri for native app
             .WithAuthority(AadAuthenticationEndpoint)
             .Build();
    
          AuthenticationResult authResult = null;
    
          IAccount account = null;
    
          IEnumerable<string> scopes = new string[] { RegistrationServiceAppIdUri };
    
          try
          {
          authResult = await clientApp.AcquireTokenSilent(scopes, account).ExecuteAsync();
          }
          catch (MsalUiRequiredException ex)
          {
          authResult = await clientApp.AcquireTokenInteractive(scopes).ExecuteAsync();
          }
    
          if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
          {
          Trace.TraceError("Authentication result, token or tenant id returned are null");
          throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
          }
    
          token = authResult.AccessToken;
          tenantID = authResult.TenantId;
       }
    }
    ```

    **Using PowerShell:**

    ```powershell
    # Loading DLLs
    
    Find-PackageProvider -Name NuGet| Install-PackageProvider -Force
    Register-PackageSource -Name nuget.org -Location https://www.nuget.org/api/v2 -ProviderName NuGet
    Install-Package Microsoft.IdentityModel.Abstractions  -ProviderName Nuget -RequiredVersion 6.22.0.0 
    Install-Module Microsoft.Identity.Client
    
    add-type -path "C:\Program Files\PackageManagement\NuGet\Packages\Microsoft.IdentityModel.Abstractions.6.22.0\lib\net461\Microsoft.IdentityModel.Abstractions.dll"
    add-type -path "C:\Program Files\WindowsPowerShell\Modules\Microsoft.Identity.Client\4.53.0\Microsoft.Identity.Client.dll"
    
    # The AAD authentication endpoint uri
    
    $authority = "https://login.microsoftonline.com/common/oauth2/v2.0/authorize"
    
    #The application ID of the connector in AAD
    
    $connectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";
    
    #The AppIdUri of the registration service in AAD
    $registrationServiceAppIdUri = "https://proxy.cloudwebappproxy.net/registerapp/user_impersonation"
    
    # Define the resources and scopes you want to call
    
    $scopes = New-Object System.Collections.ObjectModel.Collection["string"] 
    
    $scopes.Add($registrationServiceAppIdUri)
    
    $app = [Microsoft.Identity.Client.PublicClientApplicationBuilder]::Create($connectorAppId).WithAuthority($authority).WithDefaultRedirectUri().Build()
    
    [Microsoft.Identity.Client.IAccount] $account = $null
    
    # Acquiring the token
    
    $authResult = $null
    
    $authResult = $app.AcquireTokenInteractive($scopes).WithAccount($account).ExecuteAsync().ConfigureAwait($false).GetAwaiter().GetResult()
    
    # Check AuthN result
    If (($authResult) -and ($authResult.AccessToken) -and ($authResult.TenantId)) {
    
       $token = $authResult.AccessToken
       $tenantId = $authResult.TenantId
    
       Write-Output "Success: Authentication result returned."
    }
    Else {
    
       Write-Output "Error: Authentication result, token or tenant id returned with null."
    
    } 
    ```
2. Once you have the token, create a `SecureString` using the token:

    ```powershell
    $SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force
    ```
3. Run the following Windows PowerShell command, replacing `<tenant GUID>` with your directory ID. The `RegisterConnector.ps1` script is located in the connector installation folder (by default, `C:\Program Files\Microsoft Entra private network connector\`). If you're running the command from a different directory, provide the full path to the script.

    ```powershell
    .\RegisterConnector.ps1 `
        -modulePath "C:\Program Files\Microsoft Entra private network connector\Modules\" `
        -moduleName "MicrosoftEntraPrivateNetworkConnectorPSModule" `
        -Authenticationmode Token `
        -Token $SecureToken `
        -TenantId <tenant GUID> `
        -Feature ApplicationProxy
    ```
4. Store the script or code in a secure location as it contains sensitive credential information.