---
layout: Landing
title: Microsoft Entra Domain Services documentation - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/
summary: Learn how to use Microsoft Entra Domain Services to provide Kerberos or NTLM authentication to applications or join Azure VMs to a managed domain.
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to use Microsoft Entra Domain Services to provide Kerberos or NTLM authentication to applications or join Azure VMs to a managed domain.
ms.topic: landing-page
ms.collection: collection
ms.date: 2023-09-23T00:00:00.0000000Z
locale: en-us
document_id: 0666b0fc-8a3a-b59e-2789-1c096115bb18
document_version_independent_id: 13e8c2d1-71ae-eb34-1f70-dfaa3830946b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/index.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: landing
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/index
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/index.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4d4bef3e-a3cb-4f71-8e5c-7267f9468993
---

# Microsoft Entra Domain Services documentation

Learn how to use Microsoft Entra Domain Services to provide Kerberos or NTLM authentication to applications or join Azure VMs to a managed domain.

## About Microsoft Entra Domain Services

### Overview

- [What is Microsoft Entra Domain Services?](overview)
- [Compare identity solutions](compare-identity-solutions)

### Concept

- [How does synchronization work?](synchronization)
- [FAQs](faqs)

## Get started

### Deploy

- [Create a managed domain](tutorial-create-instance)

### Tutorial

- [Domain-join a Windows Server VM](join-windows-vm)
- [Install management tools](tutorial-create-management-vm)

## Configure

### Tutorial

- [Configure secure LDAP](tutorial-configure-ldaps)

### How-To Guide

- [Enable password hash synchronization](tutorial-configure-password-hash-sync)
- [Create an organizational unit (OU)](create-ou)
- [Configure Kerberos Constrained Delegation](deploy-kcd)
- [Secure managed domain](secure-your-domain)

## Manage

### How-To Guide

- [Administer group policy](manage-group-policy)
- [Manage DNS](manage-dns)
- [Check health status](check-health)
- [Configure email notifications](notifications)
- [Enable security audits](security-audit-events)
- [Restore group policy from backup](group-policy)

## Domain-join VMs

### Tutorial

- [Windows Server](join-windows-vm)

### How-To Guide

- [Ubuntu Server](join-ubuntu-linux-vm)
- [Red Hat Enterprise Linux](join-rhel-linux-vm)
- [SUSE Linux Enterprise](join-suse-linux-vm)

## Troubleshoot

### How-To Guide

- [Common issues](troubleshoot)
- [Common alert messages](troubleshoot-alerts)
- [Network security group issues](alert-nsg)
- [Secure LDAP issues](alert-ldaps)