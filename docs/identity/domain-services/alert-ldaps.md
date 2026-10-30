---
layout: Conceptual
title: Resolve secure LDAP alerts in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/alert-ldaps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to troubleshoot and resolve common alerts with secure LDAP for Microsoft Entra Domain Services.
ms.assetid: 81208c0b-8d41-4f65-be15-42119b1b5957
ms.topic: troubleshooting
ms.date: 2025-01-21T00:00:00.0000000Z
locale: en-us
document_id: 50c54d00-b221-a8a5-2d86-b68dc5026f50
document_version_independent_id: b4de39be-b413-f7e8-f915-29d44367fdb1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/alert-ldaps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/alert-ldaps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/alert-ldaps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 738ad81b-99af-951c-2eee-63d3fa0fe462
---

# Resolve secure LDAP alerts in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

Applications and services that use lightweight directory access protocol (LDAP) to communicate with Microsoft Entra Domain Services can be [configured to use secure LDAP](tutorial-configure-ldaps). An appropriate certificate and required network ports must be open for secure LDAP to work correctly.

This article helps you understand and resolve common alerts with secure LDAP access in Domain Services.

## AADDS101: Secure LDAP network configuration

### Alert message

*Secure LDAP over the internet is enabled for the managed domain. However, access to port 636 is not locked down using a network security group. This may expose user accounts on the managed domain to password brute-force attacks.*

### Resolution

When you enable secure LDAP, it's recommended to create extra rules that restrict inbound LDAPS access to specific IP addresses. These rules protect the managed domain from brute force attacks. To update the network security group to restrict TCP port 636 access for secure LDAP, complete the following steps:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), search for and select **Network security groups**.
2. Choose the network security group associated with your managed domain, such as *AADDS-contoso.com-NSG*, then select **Inbound security rules**
3. Select **+ Add** to create a rule for TCP port 636. If needed, select **Advanced** in the window to create a rule.
4. For the **Source**, choose *IP Addresses* from the drop-down menu. Enter the source IP addresses that you want to grant access for secure LDAP traffic.
5. Choose *Any* as the **Destination**, then enter *636* for **Destination port ranges**.
6. Set the **Protocol** as *TCP* and the **Action** to *Allow*.
7. Specify the priority for the rule, then enter a name such as *RestrictLDAPS*.
8. When ready, select **Add** to create the rule.

The managed domain's health automatically updates itself within two hours and removes the alert.

Tip

TCP port 636 isn't the only rule needed for Domain Services to run smoothly. To learn more, see the [Domain Services Network security groups and required ports](network-considerations#network-security-groups-and-required-ports).

## AADDS502: Secure LDAP certificate expiring

### Alert message

*The secure LDAP certificate for the managed domain will expire on [date]].*

### Resolution

Create a replacement secure LDAP certificate by following the steps to [create a certificate for secure LDAP](tutorial-configure-ldaps#create-a-certificate-for-secure-ldap). Apply the replacement certificate to Domain Services, and distribute the certificate to any clients that connect using secure LDAP.