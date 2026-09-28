---
layout: Conceptual
title: Troubleshoot secure LDAP in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/tshoot-ldaps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to troubleshoot secure LDAP (LDAPS) for a Microsoft Entra Domain Services managed domain
ms.assetid: 445c60da-e115-447b-841d-96739975bdf6
ms.topic: troubleshooting
ms.date: 2025-02-19T00:00:00.0000000Z
locale: en-us
document_id: 4680b98d-19f1-9501-37a9-4f7b6ada69d7
document_version_independent_id: e36c68c0-74c3-54a1-25e0-908511e8575c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/tshoot-ldaps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/tshoot-ldaps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/tshoot-ldaps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d3b6a66a-f953-3345-249e-62bca2e5e178
---

# Troubleshoot secure LDAP in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

Applications and services that use lightweight directory access protocol (LDAP) to communicate with Microsoft Entra Domain Services can be [configured to use secure LDAP](tutorial-configure-ldaps). An appropriate certificate and required network ports must be open for secure LDAP to work correctly.

This article helps you troubleshoot issues with secure LDAP access in Microsoft Entra Domain Services.

## Common connection issues

If you have trouble connecting to a Microsoft Entra Domain Services managed domain using secure LDAP, review the following troubleshooting steps. After each troubleshooting step, try to connect to the managed domain again:

- The issuer chain of the secure LDAP certificate must be trusted on the client. You can add the Root certification authority (CA) to the trusted root certificate store on the client to establish the trust.
    - Make sure you [export and apply the certificate to client computers](tutorial-configure-ldaps#export-a-certificate-for-client-computers).
- Verify the secure LDAP certificate for your managed domain has the DNS name in the *Subject* or the *Subject Alternative Names*attribute.
    - Review the [secure LDAP certificate requirements](tutorial-configure-ldaps#create-a-certificate-for-secure-ldap) and create a replacement certificate if needed.
- Verify that the LDAP client, such as *ldp.exe*connects to the secure LDAP endpoint using a DNS name, not the IP address.
    - The certificate applied to the managed domain doesn't include the IP addresses of the service, only the DNS names.
- Check the DNS name the LDAP client connects to. It must resolve to the public IP address for secure LDAP on the managed domain.
    - If the DNS name resolves to the internal IP address, update the DNS record to resolve to the external IP address.
- For external connectivity, the network security group must include a rule that allows the traffic to TCP port 636 from the internet.
    - If you can connect to the managed domain using secure LDAP from resources directly connected to the virtual network but not external connections, make sure you [create a network security group rule to allow secure LDAP traffic](tutorial-configure-ldaps#lock-down-secure-ldap-access-over-the-internet).