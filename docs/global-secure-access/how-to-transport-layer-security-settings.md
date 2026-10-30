---
layout: Conceptual
title: Configure TLS inspection with your own certificate - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-transport-layer-security-settings
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to bring your own certificate authority for Transport Layer Security inspection.
ms.topic: how-to
ms.reviewer: teresayao
ms.date: 2026-08-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: f4033ce5-3523-5143-e098-93dc2b3864ee
document_version_independent_id: f4033ce5-3523-5143-e098-93dc2b3864ee
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-transport-layer-security-settings.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-transport-layer-security-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-transport-layer-security-settings.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 1a1f45a9-f497-6512-8f8a-f2010c500560
---

# Configure TLS inspection with your own certificate - Global Secure Access | Microsoft Learn

Transport Layer Security (TLS) inspection in Microsoft Entra Internet Access uses a two-tier intermediate certificate model to issue dynamically generated leaf certificates for decrypting traffic. This bring your own certificate (BYOC) option lets you use your organization's public key infrastructure (PKI) to sign the certificate authority (CA) that serves as the Global Secure Access intermediate CA.

This article explains how to create a certificate signing request (CSR), sign it with your CA, and upload the signed certificate. If you don't want to operate your own CA for TLS inspection, see [Configure TLS inspection with a Microsoft-managed certificate](how-to-transport-layer-security-settings-managed-certificate).

## Prerequisites

To complete the steps in this process, you must have the following prerequisites in place:

- A PKI service to sign the CSR and generate an intermediate certificate for TLS inspection. For testing scenarios, you can also use a self-signed root certificate created with OpenSSL.
- A trial license for Microsoft Entra Internet Access.
- [Global Secure Access prerequisites](how-to-configure-web-content-filtering).

## Create a CSR and upload your signed certificate

To create a CSR and upload the signed certificate for TLS termination:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as a [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Secure** &gt; **TLS inspection policies**.
3. Switch to the **TLS inspection settings** tab.
4. Select **+ Create certificate** to start generating a certificate signing request.
5. In the **Create certificate** pane, fill in the following fields:

    - **Certificate name**: This name appears in the certificate hierarchy when viewed in a browser. It must be unique, contain no spaces, and be no more than 12 characters long. You can't reuse a previous certificate name, even after you delete the certificate.
    - **Common name** (CN): Enter a common name that identifies the intermediate certificate, for example, `Contoso TLS ICA`.
    - **Organizational Unit** (OU): Enter an organization name, for example, `Contoso IT`.
6. Select **Create CSR**. The `.csr` file is saved to your default download folder.

    [![Screenshot of the Create certificate pane with fields filled and the Create CSR button highlighted.](media/how-to-transport-layer-security-settings/create-certificate.png)](media/how-to-transport-layer-security-settings/create-certificate.png#lightbox)
7. Sign the CSR using your PKI service. Make sure **Server Auth** is in Extended Key Usage and `certificate authority (CA)=true`, `keyCertSign,cRLSign`, `basicConstraints=critical,CA:TRUE`, and `pathLenConstraint = 1` are in Basic Extension. Save the signed certificate in `.pem` format. If you're testing with a self-signed certificate, follow the instructions to use OpenSSL to sign the CSR.
8. Select **+ Upload certificate**.
9. In the **Upload certificate** form, upload the `certificate.pem` and `chain.pem` files.
10. Select **Upload signed certificate**.

    [![Screenshot of Upload certificate form with example certificate and chain certificate files in the upload fields.](media/how-to-transport-layer-security-settings/upload-certificate.png)](media/how-to-transport-layer-security-settings/upload-certificate.png#lightbox)
11. The uploaded certificate defaults to **Disabled** status. Set the status to **Enabled**. You can have one enabled certificate.

    [![Screenshot of the TLS inspection settings tab showing certificate status is Enabled.](media/how-to-transport-layer-security-settings/status-active.png)](media/how-to-transport-layer-security-settings/status-active.png#lightbox)

## Test with a self-signed root certificate authority using OpenSSL

For **testing purposes only**, use a self-signed root certificate authority (CA) that you create with OpenSSL to sign the CSR.

1. If you don't already have one, first create an *openssl.cnf* file with this configuration:

    ```ini
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
    basicConstraints = critical, CA:true
    keyUsage = critical, digitalSignature, cRLSign, keyCertSign
    extendedKeyUsage = serverAuth
    
    [ server_ext ]
    subjectKeyIdentifier = hash
    authorityKeyIdentifier = keyid:always,issuer
    basicConstraints = critical, CA:false
    keyUsage = critical, digitalSignature
    extendedKeyUsage = serverAuth
    ```
2. Create a new root certificate authority and private key using the following *openssl.cnf* config file:

    ```console
    openssl req -x509 -new -nodes -newkey rsa:4096 -keyout rootCAchain.key -sha256 -days 370 -out rootCAchain.pem -subj "/C=US/ST=US/O=Self Signed/CN=Self Signed Root CA" -config openssl.cnf -extensions rootCA_ext
    ```
3. Sign the CSR using the following command:

    ```console
    openssl x509 -req -in <CSR file> -CA rootCAchain.pem -CAkey rootCAchain.key -CAcreateserial -out signedcertificate.pem -days 370 -sha256 -extfile openssl.cnf -extensions signedCA_ext
    ```
4. Upload `signedcertificate.pem` and `rootCAchain.pem` according to the steps in Create a CSR and upload your signed certificate.

## Configure TLS inspection in Microsoft Entra Internet Access

The following video shows how to configure TLS inspection in Microsoft Entra Internet Access using a self-signed certificate created with OpenSSL. It also shows how to build TLS inspection policies, configure security profiles, apply web content filtering, enforce Conditional Access policies, create custom block pages, and implement threat intelligence policies.

## PowerShell examples

For examples that configure a certificate authority for TLS inspection using Active Directory Certificate Services (AD CS) or OpenSSL, see:

- [Create TLS certificates using AD CS](scripts/powershell-active-directory-certificate-service)
- [Create a TLS certificate using OpenSSL](scripts/powershell-open-secure-sockets-layer)