---
layout: Conceptual
title: PowerShell Sample - Create a TLS Certificate Using OpenSSL | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/scripts/powershell-open-secure-sockets-layer
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Use this PowerShell script to generate and sign Transport Layer Security (TLS) certificates using OpenSSL in a test environment.
ms.topic: sample
ms.date: 2025-09-09T00:00:00.0000000Z
ms.reviewer: teresayao
locale: en-us
document_id: 89cc7154-5156-8c0f-cfc3-1e6db6622b88
document_version_independent_id: 89cc7154-5156-8c0f-cfc3-1e6db6622b88
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/scripts/powershell-open-secure-sockets-layer.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/scripts/powershell-open-secure-sockets-layer
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/scripts/powershell-open-secure-sockets-layer.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7add5261-cb8c-0e03-bf81-8aa84e34b4c0
---

# PowerShell Sample - Create a TLS Certificate Using OpenSSL | Microsoft Learn

This script automates generating and signing Transport Layer Security (TLS) certificates using OpenSSL. It creates a certificate signing request (CSR) using the TLS inspection graph API. The script creates a self-signed root certificate authority using OpenSSL, signs the CSR, and uploads the certificate and chain to TLS inspection settings.

## Prerequisites

- Install OpenSSL for Windows or Linux.

Note

While other tools might be available for certificate management, this sample code in this article uses OpenSSL. OpenSSL is bundled with many Linux distributions, such as Ubuntu.

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
# - Make sure OpenSSL is installed
# - Replace the OpenSSL path below if needed

Import-Module Microsoft.Graph.Beta.NetworkAccess

# Connect to Microsoft Graph
Connect-MgGraph -Scopes "NetworkAccess.ReadWrite.All" -NoWelcome

# Modify the following with your own settings before running the script:
$name = "TLSiDemoCA"
$commonName = "Contoso TLS Demo"
$organizationName = "Contoso"

# Replace with your OpenSSL path
$openSSLPath = "C:\Program Files\OpenSSL-Win64\bin\openssl.exe"

# Generated file names
$rootKey = "TlsDemorootCA.key"
$rootCert = "TlsDemorootCAcert.pem"
$subject = "/C=US/ST=Washington/L=Redmond/O=Contoso/CN=Contoso"
$signedCert = "signedcertificate.pem"
$csrPath = "$name.csr"
$opensslCnfPath = "openssl.cnf"

# Check if External Certificate Authority Certificates already exist
try {
    $response = Get-MgBetaNetworkAccessTlExternalCertificateAuthorityCertificate -ErrorAction Stop
    if ($response.Count -gt 0) {
        Write-Host "A certificate for TLS inspection already exists."
        exit 1
    }
}
catch {
    if ($_.Exception.Message -match "404|NotFound|Tenant TLS Tenant Settings does not exist") {
        Write-Host "TLS inspection tenant settings do not exist yet. Continuing with CSR creation..."
    }
    else {
        Write-Error "The Graph SDK call failed: $($_.Exception.Message)"
        exit 1
    }
}

# Create the certificate signing request (CSR)
$paramscsr = @{
    "@odata.type"    = "#microsoft.graph.networkaccess.externalCertificateAuthorityCertificate"
    name             = $name
    commonName       = $commonName
    organizationName = $organizationName
}

$createResponse = $null
try {
    $createResponse = New-MgBetaNetworkAccessTlExternalCertificateAuthorityCertificate -BodyParameter $paramscsr -ErrorAction Stop
}
catch {
    Write-Error "Failed to create certificate signing request: $($_.Exception.Message)"
    exit 1
}

# Save CSR to file
$csr = $createResponse.CertificateSigningRequest
Set-Content -Path $csrPath -Value $csr -Encoding ASCII
Write-Host "CSR saved to $csrPath"

# Save certificate ID to upload later
$externalCertificateAuthorityCertificateId = $createResponse.Id

# Create OpenSSL config
$opensslCnfContent = @"
[ rootCA_ext ]
subjectKeyIdentifier = hash
authorityKeyIdentifier = keyid:always,issuer
basicConstraints = critical, CA:true
keyUsage = critical, digitalSignature, cRLSign, keyCertSign

[ interCA_ext ]
subjectKeyIdentifier = hash
authorityKeyIdentifier = keyid:always,issuer
basicConstraints = critical, CA:true, pathlen:1
keyUsage = critical, digitalSignature, cRLSign, keyCertSign

[ signedCA_ext ]
subjectKeyIdentifier = hash
authorityKeyIdentifier = keyid:always,issuer
basicConstraints = critical, CA:true, pathlen:1
keyUsage = critical, digitalSignature, cRLSign, keyCertSign
extendedKeyUsage = serverAuth

[ server_ext ]
subjectKeyIdentifier = hash
authorityKeyIdentifier = keyid:always,issuer
basicConstraints = critical, CA:false
keyUsage = critical, digitalSignature
extendedKeyUsage = serverAuth
"@

Set-Content -Path $opensslCnfPath -Value $opensslCnfContent -Encoding ASCII

# Generate Root CA private key and certificate
Write-Host "Generating Root CA key and certificate..."
& $openSSLPath req -x509 -new -nodes -newkey rsa:4096 `
    -keyout $rootKey `
    -sha256 `
    -days 370 `
    -out $rootCert `
    -subj $subject `
    -config $opensslCnfPath `
    -extensions rootCA_ext

if ($LASTEXITCODE -ne 0) {
    Write-Error "Failed to generate the Root CA certificate."
    exit 1
}

# Sign CSR using Root CA
if (Test-Path $csrPath) {
    Write-Host "Signing CSR file $csrPath..."
    & $openSSLPath x509 -req `
        -in $csrPath `
        -CA $rootCert `
        -CAkey $rootKey `
        -CAcreateserial `
        -out $signedCert `
        -days 370 `
        -sha256 `
        -extfile $opensslCnfPath `
        -extensions signedCA_ext

    if ($LASTEXITCODE -ne 0) {
        Write-Error "Failed to sign the CSR."
        exit 1
    }

    Write-Host "Successfully saved signed certificate to $signedCert"
}
else {
    Write-Error "CSR file '$csrPath' not found. Please generate it first."
    exit 1
}

# Optional validation output
Write-Host "`nValidating signed certificate..."
& $openSSLPath x509 -in $signedCert -text -noout

# Read certificate and chain
$paramsupload = @{
    certificate = Get-Content -Path $signedCert -Raw
    chain       = Get-Content -Path $rootCert -Raw
}

# Upload the signed certificate and its chain to Microsoft Graph
try {
    Update-MgBetaNetworkAccessTlExternalCertificateAuthorityCertificate `
        -ExternalCertificateAuthorityCertificateId $externalCertificateAuthorityCertificateId `
        -BodyParameter $paramsupload `
        -ErrorAction Stop
}
catch {
    Write-Error "Failed to upload certificate and chain: $($_.Exception.Message)"
    exit 1
}

Write-Host "Certificate is uploaded successfully via Microsoft Graph SDK."
```