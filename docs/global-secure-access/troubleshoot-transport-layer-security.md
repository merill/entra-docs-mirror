---
layout: Conceptual
title: Troubleshoot Transport Layer Security inspection errors - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-transport-layer-security
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to troubleshoot and resolve Transport Layer Security (TLS) inspection errors in Global Secure Access.
ms.topic: troubleshooting-known-issue
ms.reviewer: teresayao
ms.date: 2026-08-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 9c4b1ce3-306b-7301-7053-a12aa6c31935
document_version_independent_id: 9c4b1ce3-306b-7301-7053-a12aa6c31935
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/troubleshoot-transport-layer-security.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/troubleshoot-transport-layer-security
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/troubleshoot-transport-layer-security.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/089c8ba6-d135-43ff-bfaf-b8197fb72fb9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/32516e21-6665-416f-be21-413febe47d91
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0bc05bfa-7b15-b70b-6f55-0c0d2677a68c
---

# Troubleshoot Transport Layer Security inspection errors - Global Secure Access | Microsoft Learn

This article explains common troubleshooting scenarios when deploying a Transport Layer Security (TLS) inspection policy.

## Certificate problem: unable to get the local issuer certificate

This error occurs because developer tools like Git and Python don't use the operating system's certificate store by default. Instead, they maintain their own certificate stores and don't recognize the TLS inspection certificate.

### Troubleshooting for Git

You can direct Git to use Windows' certificate store:

`git config --global http.sslbackend schannel`

Alternatively, you can append a custom TLS inspection root certificate to Git's Certificate Authority bundle so Git trusts your internal certificate authority.

```PowerShell
$certPath = "./myTLSInspectionRootCA.crt"
$gitCAPath = git config --get http.sslcainfo
if ($gitCAPath) {
    Get-Content $certPath | Add-Content -Path $gitCAPath
    Write-Host "Certificate appended to Git CA bundle"
} else {
    Write-Host "Git CA bundle path not found"
}
```

### Troubleshooting for Python

Python-based tools, such as Azure CLI, fail without the correct certificate authority. You can install `pip-system-certs` so Python trusts the Windows certificate store:

#### Azure CLI

```powershell
"C:\Program Files\Microsoft SDKs\Azure\CLI2\python.exe" -m pip install pip-system-certs
```

#### System Python

```bash
python -m pip install pip-system-certs
```

Alternatively, you can append a custom TLS inspection root certificate to Python’s CA bundle so Python trusts your internal certificate authority.

```powershell
$certPath = "./myTLSInspectionRootCA.crt"
$pythonCertPath = python -c "import certifi; print(certifi.where())"
Get-Content $certPath | Add-Content -Path $pythonCertPath
Write-Host "Certificate appended to Python's CA bundle"
```

### Troubleshooting for Docker

Docker containers might fail TLS connections when the TLS inspection certificate isn't trusted. Add your certificate to Docker's trusted certificates list by adding these commands to your Dockerfile:

#### Debian or Ubuntu-based images

```dockerfile
COPY myTLSInspectionRootCA.crt /usr/local/share/ca-certificates/
RUN update-ca-certificates
```

#### Alpine-based images

```dockerfile
COPY myTLSInspectionRootCA.crt /usr/local/share/ca-certificates/
RUN apk update && apk add ca-certificates && update-ca-certificates
```

### Troubleshooting for Node

Node.js doesn't use the operating system's certificate store by default. You can configure Node.js to use the system certificate store using one of the following methods:

#### Command Line

Use the `--use-system-ca` flag when running your application. Replace `<your-app>.js` with your application's entry point (for example, `index.js` or `server.js`):

```bash
node --use-system-ca <your-app>.js
```

#### Environment Variable (single session)

Set the variable inline for a single command:

```bash
NODE_USE_SYSTEM_CA=1 node <your-app>.js
```

#### Environment Variable (all Node.js apps)

To apply the setting permanently for all Node.js applications, set `NODE_USE_SYSTEM_CA` as a persistent environment variable.

For the current user:

```powershell
setx NODE_USE_SYSTEM_CA 1
```

For all users on the machine (requires administrator privileges):

```powershell
setx NODE_USE_SYSTEM_CA 1 /M
```

After running either command, restart any open terminals for the change to take effect. All Node.js processes will then use the system certificate store automatically.

## Applications don't work on mobile platforms

Mobile applications might fail when TLS inspection is enabled due to certificate pinning, which restricts applications to trust only specific certificates.

### Troubleshooting steps

Create a TLS bypass rule to exclude the application's destination FQDNs from TLS inspection. For detailed steps, see [Configure Transport Layer Security inspection policies](how-to-transport-layer-security).

## An internal certificate already exists

For preview customers with a legacy TLS configuration, when creating a Certificate Signing Request (CSR), you might see this error: `Cannot create external certificate, an internal certificate already exists for tenant.`

### Troubleshooting steps

To resolve this issue:

1. Sign in to the Microsoft Entra admin center with [custom TLS inspection settings](https://aka.ms/tlspreview-portal) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Settings** &gt; **Session management**.
3. Select the **TLS Inspection** tab.
4. Select and delete the Certificate URL.
5. Select **Save**.