---
layout: Conceptual
title: PowerShell Sample - Create a TLS Certificate Using Active Directory Certificate Services | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/scripts/powershell-active-directory-certificate-service
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Use this PowerShell script to create a TLS certificate using Active Directory Certificate Services (ADCS) in a test environment.
ms.topic: sample
ms.date: 2025-09-09T00:00:00.0000000Z
ms.reviewer: teresayao
locale: en-us
document_id: 96fbee5e-86cd-dbc5-257b-17c3f0082264
document_version_independent_id: 96fbee5e-86cd-dbc5-257b-17c3f0082264
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/scripts/powershell-active-directory-certificate-service.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/scripts/powershell-active-directory-certificate-service
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/scripts/powershell-active-directory-certificate-service.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 6d0dc6e1-8481-e083-6830-b73af9ace800
---

# PowerShell Sample - Create a TLS Certificate Using Active Directory Certificate Services | Microsoft Learn

This script automates generating and signing Transport Layer Security (TLS) certificates using Active Directory Certificate Services (ADCS). It creates a certificate signing request (CSR) using the TLS inspection graph API. The script then submits the certificate to ADCS for signing, retrieves the signed certificate, and uploads the certificate and chain to TLS inspection settings.

## Generate and sign TLS certificates

```powershell
# This script requires the following:
#    - PowerShell 5.1 (x64) or later
#    - Module: Microsoft.Graph.Beta
#
# Before you begin:
#    
# - Make sure you're running PowerShell as an administrator
# - Make sure you run: Install-Module Microsoft.Graph.Beta -AllowClobber -Force
# - Make sure you have ADCS configured with a SubCA template and you have "<CAHostName>\<CACommonName>"
# Ensure Microsoft.Graph.Beta module is available

# Import module

Import-Module Microsoft.Graph.Beta.NetworkAccess

# Connect to Microsoft Graph (handles token for you)
Connect-MgGraph -Scopes "NetworkAccess.ReadWrite.All" -NoWelcome

# Modify the following with your own settings before running the script:
# Name of the certificate (letters and numbers only and within 12 characters)
$name = "TLSiCAName"
# Common Name (CN) for the certificate
$commonName = "Contoso TLS Demo"
# Organization Name (O) for the certificate
$organizationName = "Contoso"
#ADCS settings
# Make sure you have ADCS configured with a SubCA template and you have "<CAHostName>\<CACommonName>"
$Template = "SubCA"
$CAConfig="<CACommonName> of your ADCS server"

# Check if the External Certificate Authority Certificates already exists
try {
    $response = Get-MgBetaNetworkAccessTlExternalCertificateAuthorityCertificate
    if ($response.Count -gt 0) 
    {
     Write-Host "A certificate for TLS inspection already exists." exit 1
    } 
}
catch {
    Write-Error "Graph SDK call to check on the list of certificates failed: $($_.Exception.Message)"
}

# Create the certificate signing request (CSR)

$paramscsr = @{"@odata.type" = "#microsoft.graph.networkaccess.externalCertificateAuthorityCertificate"name = $namecommonName =  $commonNameorganizationName = $organizationName
}
$createResponse = $null
try {
    $createResponse = New-MgBetaNetworkAccessTlExternalCertificateAuthorityCertificate -BodyParameter $paramscsr -ErrorAction Stop
} catch {
    Write-Error "Failed to create certificate signing request: $($_.Exception.Message)"
    exit 1
}

# Save CSR to file
$csr = $createResponse.CertificateSigningRequest
$CsrPath = "$name.csr"
Set-Content -Path $CsrPath -Value $csr -Encoding ascii
Write-Host "CSR saved to $CsrPath"

# The unique identifier of the created certificate, used for uploading the signed certificate and chain
$certId = $createResponse.Id

# Certificate and chain file names
$signedCert = "TlsDemoCert.pem"
$chainContent = "TlsDemoCertChain.pem"

# Submit CSR to ADCS to sign, using subordinate CA template, retrieve Request ID
$submitOutput = certreq -submit -attrib "CertificateTemplate:$Template" -config $CAConfig $CsrPath $signedCert
if (-not (Test-Path $signedCert)) {
    Write-Error "Certificate was not issued. Check CA or template permissions."
    exit 1
}
Write-Host "Certificate issued and saved to $signedCert"

# Extract Request ID from output
$requestId = ($submitOutput | Select-String -Pattern 'RequestId:\s*(\d+)' | ForEach-Object { 
    if ($_.Matches.Count -gt 0) { $_.Matches[0].Groups[1].Value }
})
if (-not $requestId) {
    Write-Error "Could not determine Request ID from certreq output."
    exit 1
}
Write-Host "Request ID: $requestId"

# Retrieve certificate in pem and chain in p7b format
$tempP7B ="tempchain.p7b"
$tempPem ="tempcert.pem"
Write-Host "Retrieving full certificate chain..."
certreq -retrieve -config $CAConfig $requestId $tempPem $tempP7B 
if (-not (Test-Path $tempP7B )) {
    Write-Error "Failed to retrieve certificate chain."
    exit 1
}
# Read the .p7b file as bytes
$p7bBytes = [System.IO.File]::ReadAllBytes($tempP7B)
# Create a certificate collection and import the .p7b content
$certCollection = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2Collection
$certCollection.Import($p7bBytes)
# Sort certificates from intermediate to root (based on Issuer/Subject)
# Initialize PEM block array
$pemBlocks = @()
# Loop through each certificate and convert to PEM format
foreach ($cert in $certCollection) {
    $base64 = [System.Convert]::ToBase64String($cert.RawData, 'InsertLineBreaks')
    $pem = "-----BEGIN CERTIFICATE-----`n$base64`n-----END CERTIFICATE-----"
    $pemBlocks += $pem
}
# Save all PEM blocks to a single file
$pemBlocks -join "`n" | Set-Content -Path $chainContent -Encoding ascii
Write-Host "Certificate chain saved to $chainContent"

# Read certificate and chain
if (-not (Test-Path $tempPem) -or ((Get-Content -Path $tempPem -Raw).Trim().Length -eq 0)) {
    Write-Error "The certificate file $tempPem does not exist or is empty. Aborting upload."
    exit 1
}
$paramsupload = @{
certificate = Get-Content -Path $tempPem -Raw
chain       = Get-Content -Path $chainContent -Raw
}
# Upload the signed certificate and its chain to Microsoft Graph using the SDK cmdlet.
# -ExternalCertificateAuthorityCertificateId: The unique ID of the certificate request previously created.
# -BodyParameter: A hashtable containing the PEM-encoded certificate and chain as required by the API.
#   }

try {
    Update-MgBetaNetworkAccessTlExternalCertificateAuthorityCertificate -ExternalCertificateAuthorityCertificateId $certId -BodyParameter $paramsupload
} catch {
    Write-Error "Failed to upload certificate and chain: $($_.Exception.Message)"
    exit 1
}
Write-Host "Your TLS certificate is created and uploaded successfully."

# Delete temp files other than the signed certificate and chain.
Remove-Item $CsrPath, $tempP7B, $tempPem -ErrorAction SilentlyContinue
```