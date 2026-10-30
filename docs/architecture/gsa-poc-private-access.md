---
layout: Conceptual
title: Microsoft Global Secure Access Proof-of-Concept Guidance - Configure Microsoft Entra Private Access - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/gsa-poc-private-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: global-secure-access
manager: martinco
description: Learn how to deploy and test Microsoft Global Secure Access as a proof of concept with Microsoft Entra Private Access.
ms.topic: concept-article
ms.date: 2025-01-22T00:00:00.0000000Z
locale: en-us
document_id: 6673e9c0-5d05-6bb8-fe17-3c515dc12cdb
document_version_independent_id: 6673e9c0-5d05-6bb8-fe17-3c515dc12cdb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/gsa-poc-private-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/gsa-poc-private-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/gsa-poc-private-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3f43f51a-ce26-4377-97f4-9f6799ff4a24
---

# Microsoft Global Secure Access Proof-of-Concept Guidance - Configure Microsoft Entra Private Access - Microsoft Entra | Microsoft Learn

The proof-of-concept (PoC) guidance in this series of articles helps you to learn, deploy, and test Microsoft Global Secure Access with Microsoft Entra Internet Access, Microsoft Entra Private Access, and the Microsoft traffic profile.

Detailed guidance begins with [Introduction to Microsoft Global Secure Access proof-of-concept guidance](gsa-poc-guidance-intro) and continues after this article with [Configure Microsoft Entra Internet Access](gsa-poc-internet-access).

This article helps you to test Microsoft Entra Private Access and configure at least one private network connector. For detailed guidance, see [How to configure connectors for Microsoft Entra Private Access](../global-secure-access/how-to-configure-connectors).

## Install the Microsoft Entra private network connector

[Install and configure](../global-secure-access/how-to-configure-connectors#install-and-register-a-connector) the [latest version](../global-secure-access/reference-version-history) of the Microsoft Entra private network connector from the Microsoft Entra admin center.

## Configure use cases

Configure and test your Microsoft Entra Private Access use cases. The following sections provide example use cases with specific guidance.

### Replace VPN

You can use VPN replacement to open Microsoft Entra Private Access for traffic destined to all private network locations for all users. Follow these steps to seamlessly transition from full network access to Zero Trust network access:

1. [Configure Quick Access for Global Secure Access](../global-secure-access/how-to-configure-quick-access).
2. [Add private Domain Name System (DNS) suffixes](../global-secure-access/how-to-configure-quick-access#add-private-dns-suffixes).
3. [Manage user and group assignment to an application](../identity/enterprise-apps/assign-user-or-group-access-portal).
4. [Apply Conditional Access policies to Microsoft Entra Private Access apps](../global-secure-access/how-to-target-resource-private-access-apps).

### Provide access to specific apps

If your goal is to move to a Zero Trust posture, configure per-app access to all your apps. This scenario can be a daunting undertaking because many companies don't have a full inventory of all IP addresses and fully qualified domain names (FQDNs) that users access on the private network.

To move to per-app access, configure Global Secure Access applications with app segments that limit access to specific IP addresses, IP ranges, FQDNs, protocols, and ports. You can create these configurations manually or by using tools such as PowerShell and App Discovery. Ensure that your Global Secure Access application includes in its app segments all IPs, ports, and protocols that the application uses.

Note

Any Global Secure Access applications with app segments that overlap with Quick Access take precedence. In other words, Global Secure Access doesn't route any traffic to those destinations over Quick Access. To avoid service disruption, assign users correctly to your Global Secure Access applications. If you need a slower onboarding to a Zero Trust posture, consider moving subsets of IP ranges and ports rather than entire enterprise applications at one time.

These articles provide detailed guidance:

- [Configure per-app access by using Global Secure Access applications](../global-secure-access/how-to-configure-per-app-access)
- [Application discovery (preview) for Global Secure Access](../global-secure-access/how-to-application-discovery)

### Use Kerberos SSO to Active Directory resources

Microsoft Entra Private Access uses Kerberos to provide single sign-on (SSO) for on-premises resources. You can use cloud Kerberos trust in Windows Hello for Business to allow SSO for users. To enable this scenario, you must publish your domain controllers and DNS suffixes in Microsoft Entra Private Access. For detailed guidance, see [Use Kerberos for single sign-on (SSO) with Microsoft Entra Private Access](../global-secure-access/how-to-configure-kerberos-sso).

### Protect privileged access with PIM

You can use [Microsoft Entra Privileged Identity Management (PIM)](../id-governance/privileged-identity-management/pim-configure) to control access to specific critical resources. This feature adds an extra layer of security to enforce just-in-time (JIT) privileged access on top of private access.

To configure Microsoft Entra Private Access to use PIM, configure and assign groups, activate privileged access, and follow compliance guidance. For details, refer to [Secure private application access with Privileged Identity Management (PIM) and Global Secure Access](../global-secure-access/how-to-configure-global-access-with-pim).

### Use PowerShell to manage Microsoft Entra Private Access

Several Global Secure Access commands are available in the Microsoft Entra PowerShell module. For detailed guidance, refer to [Install the Microsoft Entra PowerShell module](/en-us/powershell/entra-powershell/installation).

### Protect on-premises resources

To help protect on-premises resources like domain controllers by enabling multifactor authentication (MFA), see [Microsoft Entra Private Access for on-premises users](https://techcommunity.microsoft.com/blog/identity/microsoft-entra-private-access-for-on-prem-users/3905450).

### Coexist with a partner

When customers deploy the 3P solution, they might want to use Microsoft Entra Private Access while using other solutions for internet access. For guidance, see [Partner ecosystem overview](../global-secure-access/partner-ecosystems-overview).

## Troubleshoot

If you have problems with your PoC, these articles can help you with troubleshooting, logging, and monitoring:

- [Global Secure Access FAQ](../global-secure-access/resource-faq)
- [Troubleshoot problems installing the Microsoft Entra private network connector](../global-secure-access/troubleshoot-connectors)
- [Troubleshoot the Global Secure Access client: Diagnostics](../global-secure-access/troubleshoot-global-secure-access-client-advanced-diagnostics)
- [Troubleshoot the Global Secure Access client: Health check tab](../global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check)
- [Troubleshoot a Distributed File System issue with Global Secure Access](../global-secure-access/troubleshoot-distributed-file-system)
- [Global Secure Access logs and monitoring](../global-secure-access/concept-global-secure-access-logs-monitoring)
- [How to use workbooks with Global Secure Access](../global-secure-access/how-to-use-workbooks)