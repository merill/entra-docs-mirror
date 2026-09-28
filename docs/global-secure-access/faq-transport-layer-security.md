---
layout: FAQ
title: Transport Layer Security Inspection Frequently Asked Questions - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/faq-transport-layer-security
summary: >
  <p>This article answers frequently asked questions about Transport Layer Security inspection.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Get answers to common questions about Transport Layer Security (TLS) inspection.
ms.topic: faq
ms.date: 2025-05-28T00:00:00.0000000Z
locale: en-us
document_id: c71d8d4e-caf1-36cb-2c79-9e566241f9e8
document_version_independent_id: c71d8d4e-caf1-36cb-2c79-9e566241f9e8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/faq-transport-layer-security.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/faq-transport-layer-security
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/faq-transport-layer-security.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: a55b9038-528a-36c4-f123-8ec22c798fd7
---

# Transport Layer Security Inspection Frequently Asked Questions - Global Secure Access | Microsoft Learn

This article answers frequently asked questions about Transport Layer Security inspection.

## What is Transport Layer Security (TLS) inspection?

TLS inspection decrypts and analyzes encrypted network traffic to help organizations detect threats, enforce security policies, and prevent data exfiltration. With the majority of internet traffic now encrypted, TLS inspection provides visibility into data flows that would otherwise be opaque to security tools. TLS inspection enables enterprises to apply advanced protections such as content filtering without compromising the confidentiality of legitimate communications.

## How does TLS inspection work?

TLS inspection enables organizations to analyze encrypted network traffic by decrypting it for security inspection and re-encrypting it before forwarding it to its destination. To implement TLS inspection effectively, consider the following operational best practices:

- Communicate clearly with users: Before enabling TLS inspection in a production environment, ensure users are informed about how encrypted traffic is handled. Many organizations choose to provide a Terms of Use (ToU) or similar notice.
- Select a certificate authority: Choose a root or intermediate certificate authority to sign the Certificate Signing Request (CSR) created by Global Secure Access for TLS inspection.
- Define a TLS policy: Configure a TLS inspection policy that aligns with your organization's security and operational requirements.
- Configure Conditional Access: Create a Conditional Access policy and associate it with the Global Secure Access security profile linked to the TLS policy.
- Distribute the trusted certificate: Ensure the selected certificate authority is installed on all client devices to establish trust and enable seamless TLS inspection.

## What are the cryptographic algorithms supported when generating Certificates for TLS inspection?

Global Secure Access currently supports SHA-256, SHA-384, and SHA-512 for the signing certificates.

## How do I Sign CSR Using the Active Directory Certificate Services (AD CS)

TLS inspection requires an intermediate certificate authority, ensure you are using the Subordinate CA template. To sign CSR generated from TLS settings, you may use AD CS web enrollment UI or use the certreq command-line tool.

```cmd
certreq -submit -attrib "CertificateTemplate:SubCA" "C:\pathtoyourCSR\tlsca.csr" "tlsca.cer"
```

## What is certificate pinning, and how does it affect TLS inspection?

Certificate pinning is a security mechanism that restricts an application's TLS connections to a specific set of trusted certificates or public keys. Certificate pinning ensures that the application only communicates with servers presenting those exact credentials, even if other certificates are valid and trusted by the system. This technique helps defend against man-in-the-middle (MITM) attacks by preventing unauthorized interception of encrypted traffic. However, it also interferes with network security tools that rely on TLS inspection, which works by decrypting and re-encrypting traffic using an intermediary certificate.

## How should I handle applications that use certificate pinning?

The connection fails if TLS inspection terminates traffic from applications that use certificate pinning. To ensure your applications work as expected, use a [custom TLS bypass rule](how-to-transport-layer-security) to bypass TLS inspection only for these applications.

## What destinations are included in the system bypass?

System bypass list includes known destinations that use certificate pinning or have other incompatibilities with TLS inspection. These destinations are automatically excluded from TLS inspection to ensure proper functionality. The system bypass list is regularly updated to include new destinations as they are identified. A few examples of destinations in the system bypass list include:

- Adobe CRS
- AplusPC UCC Regions
- App Center
- Apple ESS Push Services
- Azure Diagnostics
- Azure IoT Hub
- Azure Management
- Azure WAN Listener
- Centanet
- Central Plaza e-Order
- Cisco Umbrella Proxy
- DocuSign
- Dropbox
- e-Szigno
- Global Secure Access Diagnostics
- Guardz Device Agent
- iCloud
- Likr Load Balancer
- MediaTek
- Microsigner
- Microsoft Graph
- Microsoft Login Services
- Microsoft Office 365
- O2 Moje Login
- OpenSpace Solutions
- Power BI External
- Signal
- TeamViewer
- Visual Studio Telemetry
- Webex
- WhatsApp
- Windows Update
- ZDX Cloud
- Zscaler Beta
- Zscaler Two
- Zoom

## Is TLS 1.3 supported?

Microsoft Entra TLS inspection enables TLS 1.2 and TLS 1.3 by default. The highest mutually supported version is selected for the session, from the client to Global Secure Access and from Global Secure Access to the destinations. Microsoft Entra doesn't support TLS 1.3 with Encrypted Client Hello (ECH) because the Server Name Indication (SNI) is encrypted, which prevents Global Secure Access from creating the corresponding leaf certificates for TLS termination.

## What happens if I have legacy applications using less secure TLS versions, such as TLS 1.1?

We recommend bypassing TLS inspection for these destinations. TLS 1.2 is the minimum recommended version because older versions, like TLS 1.1 and TLS 1.0, aren't secure and are vulnerable to attacks. When possible, move these applications to support TLS 1.2 or higher.

## Do you use hardware security modules (HSM) to protect keys?

We use software-protected keys. Global Secure Access intermediate certificate keys are stored in memory to dynamically generate leaf certificates for websites. While these keys aren't protected by an HSM, access to our servers is highly restricted, and we use strict security controls to safeguard key access and system integrity.

## What other Global Secure Access features have dependencies on TLS inspection?

Content-based security controls have dependencies on TLS inspection, including URL filtering, Content policies, Prompt policies, and enabling partner security solutions.