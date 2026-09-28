---
layout: Conceptual
title: 'Microsoft Entra Connect: TLS 1.2 enforcement for Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-tls-enforcement
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to force your Microsoft Entra Connect server to use only Transport Layer Security (TLS) 1.2.
ms.topic: reference
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 7cf85204-f66d-66f8-5d16-27a5a184e4f4
document_version_independent_id: 970014f2-d475-5c5f-58ac-49faa45252a3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/reference-connect-tls-enforcement.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/reference-connect-tls-enforcement
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/reference-connect-tls-enforcement.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1795d33d-8703-3ff9-75e9-b44f518ab0dd
---

# Microsoft Entra Connect: TLS 1.2 enforcement for Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn

Important

This requirement only applies to versions 2.3.20.0 through to 2.4.129.0. Entra Connect version 2.4.131.0 and higher do not require TLS enforcement before installation or upgrade.

Transport Layer Security (TLS) protocol version 1.2 is a cryptography protocol that is designed to provide secure communications. The TLS protocol aims primarily to provide privacy and data integrity. TLS has gone through many iterations, with version 1.2 being defined in [RFC 5246](https://tools.ietf.org/html/rfc5246). Microsoft Entra Connect version 1.2.65.0 and later now fully support using only TLS 1.2 for communications with Azure. This article provides information about how to force your Microsoft Entra Connect server to use only TLS 1.2.

## Update the registry

In order to force the Microsoft Entra Connect server to only use TLS 1.2, the registry of the Windows server must be updated. Set the following registry keys on the Microsoft Entra Connect server.

Important

After you've updated the registry, you must restart the Windows server for the changes to take effect.

### Enable TLS 1.2

- [HKEY\_LOCAL\_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
    - "SystemDefaultTlsVersions"=dword:00000001
    - "SchUseStrongCrypto"=dword:0000001
- [HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
    - "SystemDefaultTlsVersions"=dword:00000001
    - "SchUseStrongCrypto"=dword:00000001
- [HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server]
    - "Enabled"=dword:00000001
- [HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server]
    - "DisabledByDefault"=dword:00000000
- [HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client]
    - "Enabled"=dword:00000001
- [HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client]
    - "DisabledByDefault"=dword:00000000

### PowerShell script to check TLS 1.2

You can use the following PowerShell script to check the current TLS 1.2 settings on your Microsoft Entra Connect server.

```powershell

Function Get-ADSyncToolsTls12RegValue
{
    [CmdletBinding()]
    Param
    (
        # Registry Path
        [Parameter(Mandatory=$true,
                   Position=0)]
        [string]
        $RegPath,

        # Registry Name
        [Parameter(Mandatory=$true,
                   Position=1)]
        [string]
        $RegName
    )
    $regItem = Get-ItemProperty -Path $RegPath -Name $RegName -ErrorAction Ignore
    $output = "" | select Path,Name,Value
    $output.Path = $RegPath
    $output.Name = $RegName

    If ($regItem -eq $null)
    {
        $output.Value = "Not Found"
    }
    Else
    {
        $output.Value = $regItem.$RegName
    }
    $output
}

$regSettings = @()
$regKey = 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319'
$regSettings += Get-ADSyncToolsTls12RegValue $regKey 'SystemDefaultTlsVersions'
$regSettings += Get-ADSyncToolsTls12RegValue $regKey 'SchUseStrongCrypto'

$regKey = 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319'
$regSettings += Get-ADSyncToolsTls12RegValue $regKey 'SystemDefaultTlsVersions'
$regSettings += Get-ADSyncToolsTls12RegValue $regKey 'SchUseStrongCrypto'

$regKey = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'
$regSettings += Get-ADSyncToolsTls12RegValue $regKey 'Enabled'
$regSettings += Get-ADSyncToolsTls12RegValue $regKey 'DisabledByDefault'

$regKey = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'
$regSettings += Get-ADSyncToolsTls12RegValue $regKey 'Enabled'
$regSettings += Get-ADSyncToolsTls12RegValue $regKey 'DisabledByDefault'

$regSettings

```

Example Output showing proper TLS1.2 configuration:

![image](https://user-images.githubusercontent.com/38323403/138769930-2cdd290b-8f18-4f52-8a80-c12e5f8a56ba.png)

### PowerShell script to enable TLS 1.2

You can use the following PowerShell script to enable TLS 1.2 on your Microsoft Entra Connect server.

```powershell

If (-Not (Test-Path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319'))
{
    New-Item 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -Force | Out-Null
}
New-ItemProperty -Path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -Name 'SystemDefaultTlsVersions' -Value '1' -PropertyType 'DWord' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -Name 'SchUseStrongCrypto' -Value '1' -PropertyType 'DWord' -Force | Out-Null

If (-Not (Test-Path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319'))
{
    New-Item 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -Force | Out-Null
}
New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -Name 'SystemDefaultTlsVersions' -Value '1' -PropertyType 'DWord' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -Name 'SchUseStrongCrypto' -Value '1' -PropertyType 'DWord' -Force | Out-Null

If (-Not (Test-Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'))
{
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force | Out-Null
}
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Name 'Enabled' -Value '1' -PropertyType 'DWord' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Name 'DisabledByDefault' -Value '0' -PropertyType 'DWord' -Force | Out-Null

If (-Not (Test-Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'))
{
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force | Out-Null
}
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Name 'Enabled' -Value '1' -PropertyType 'DWord' -Force | Out-Null
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Name 'DisabledByDefault' -Value '0' -PropertyType 'DWord' -Force | Out-Null

Write-Host 'TLS 1.2 has been enabled. You must restart the Windows Server for the changes to take affect.' -ForegroundColor Cyan

```