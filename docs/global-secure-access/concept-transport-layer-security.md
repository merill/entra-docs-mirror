---
layout: Conceptual
title: What is Transport Layer Security Inspection? - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-transport-layer-security
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: This article provides an overview of the Transport Layer Security (TLS) inspection process and how it increases security between two communicating parties.
ms.topic: concept-article
ms.date: 2026-08-28T00:00:00.0000000Z
ms.reviewer: teresayao
locale: en-us
document_id: 8e206f12-f03a-8b1e-7293-d992593a0895
document_version_independent_id: 8e206f12-f03a-8b1e-7293-d992593a0895
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-transport-layer-security.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-transport-layer-security
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-transport-layer-security.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
platformId: b89c36ce-301e-53b6-0ee7-e032c39e32c0
---

# What is Transport Layer Security Inspection? - Global Secure Access | Microsoft Learn

The Transport Layer Security (TLS) protocol uses certificates at the transport layer to ensure the privacy, integrity, and authenticity of data exchanged between two communicating parties. While TLS secures legitimate traffic, malicious traffic like malware and data leakage attacks can still hide behind encryption. The Microsoft Entra Internet Access TLS inspection capability provides visibility into encrypted traffic by making content available for enhanced protection, such as malware detection, data loss prevention, prompt inspection, and other advanced security controls. This article gives an overview of the TLS inspection process.

## The TLS inspection process

When you enable TLS inspection, Global Secure Access decrypts HTTPS requests at the service edge. Advanced security controls, such as full URL filtering and file scan policies, are evaluated. If no security control blocks the request, Global Secure Access re-encrypts and forwards the request to the destination.

To enable TLS inspection, follow these steps:

1. Generate a certificate signing request (CSR) in the Global Secure Access portal and sign the CSR using your organization's root or intermediate certificate authority.
2. Upload the signed certificate to the portal.

Global Secure Access uses a two-tier certificate architecture. The customer-signed intermediate certificate is the first tier and is used to create a second short-lived intermediate certificate, which dynamically generates leaf certificates for TLS termination. TLS inspection establishes two separate TLS connections:

- One from the client browser to a Global Secure Access service edge
- One from Global Secure Access to the destination server

Global Secure Access uses leaf certificates during TLS handshakes between client devices and the service. To ensure successful handshakes, install your root certificate authority and the intermediate certificate authority (if used to sign the CSR) in the trusted certificate store on all client devices.

[![Diagram that shows the Transport Layer Security (TLS) inspection process.](media/concept-transport-layer-security/inspection-process-diagram.png)](media/concept-transport-layer-security/inspection-process-diagram-expanded.png#lightbox)

Traffic logs include four TLS-related metadata fields that help you understand how TLS policies are applied:

- *TlsAction*: Bypassed or Intercepted
- *TlsPolicyId*: The unique identifier of the applied TLS policy
- *TlsPolicyName*: The readable name of the TLS policy for easier reference
- *TlsStatus*: Success or Failure

To get started with TLS inspection, see [Configure Transport Layer Security Policies](how-to-transport-layer-security).

Note

TLS inspection is a prerequisite for capturing Generative AI prompt content and Model Context Protocol (MCP) payloads on end-user devices. For more information, see [Generative AI Insights in Global Secure Access](concept-generative-ai-insights).

## Supported ciphers

| List of supported ciphers |
| --- |
| ECDHE-ECDSA-AES128-GCM-SHA256 |
| ECDHE-ECDSA-CHACHA20-POLY1305 |
| ECDHE-RSA-AES128-GCM-SHA256 |
| ECDHE-RSA-CHACHA20-POLY1305 |
| ECDHE-ECDSA-AES128-SHA |
| ECDHE-RSA-AES128-SHA |
| AES128-GCM-SHA256 |
| AES128-SHA |
| ECDHE-ECDSA-AES256-GCM-SHA384 |
| ECDHE-RSA-AES256-GCM-SHA384 |
| ECDHE-ECDSA-AES256-SHA |
| ECDHE-RSA-AES256-SHA |
| AES256-GCM-SHA384 |
| AES256-SHA |

## Known limitations

TLS inspection has the following known limitations:

- TLS inspection supports up to 100 policies, 1,000 rules, and 8,000 destinations.
- Make sure each certificate signing request (CSR) you generate has a unique certificate name and isn't reused. The signed certificate must stay valid for at least six months.
- You can use only one active certificate at a time.
- TLS inspection doesn't support HTTP/2 negotiation. Most sites automatically fall back to HTTP/1.1 and continue to work, but sites that require HTTP/2 won't load if TLS inspection is enabled. Add a custom TLS bypass rule to allow access to HTTP/2-only sites.
- TLS inspection doesn't follow Authority Information Access (AIA) and Online Certificate Status Protocol (OCSP) links when validating destination certificates.

## Mobile platform

- Many mobile applications implement certificate pinning, which prevents successful TLS inspection, resulting in handshake failures or loss of functionality. To reduce risk, enable TLS inspection in a test environment first and validate that critical applications are compatible. For apps that rely on certificate pinning, configure TLS inspection custom rules to bypass these destinations using domain-based or category-based rules.