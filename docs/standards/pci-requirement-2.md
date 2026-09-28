---
layout: Conceptual
title: Microsoft Entra ID and PCI-DSS Requirement 2 - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/pci-requirement-2
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Learn PCI-DSS defined approach requirements for applying secure configurations to all system components
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, jricketts
ms.date: 2023-04-18T00:00:00.0000000Z
ms.custom: it-pro
ms.collection: 
locale: en-us
document_id: 42fa8815-353c-2574-a4a6-be0c4710a3d6
document_version_independent_id: 45b1a30d-18b1-b444-b038-69b28db1e4e5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/pci-requirement-2.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/pci-requirement-2
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/pci-requirement-2.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 84da2dd8-5c97-334f-0323-225dec4d4aff
---

# Microsoft Entra ID and PCI-DSS Requirement 2 - Microsoft Entra | Microsoft Learn

**Requirement 2: Apply Secure Configurations to All System Components** **Defined approach requirements**

## 2.1 Processes and mechanisms for applying secure configurations to all system components are defined and understood.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **2.1.1** All security policies and operational procedures that are identified in Requirement 2 are:  Documented  Kept up to date  In use Known to all affected parties | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |
| **2.1.2** Roles and responsibilities for performing activities in Requirement 2 are documented, assigned, and understood. | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |

## 2.2 System components are configured and managed securely.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **2.2.1** Configuration standards are developed, implemented, and maintained to:  Cover all system components.  Address all known security vulnerabilities. Be consistent with industry-accepted system hardening standards or vendor hardening recommendations.  Be updated as new vulnerability issues are identified, as defined in Requirement 6.3.1.  Be applied when new systems are configured and verified as in place before or immediately after a system component is connected to a production environment. | See, [Microsoft Entra security operations guide](../architecture/security-operations-introduction) |
| **2.2.2** Vendor default accounts are managed as follows:  If the vendor default account(s) will be used, the default password is changed per Requirement 8.3.6.  If the vendor default account(s) will not be used, the account is removed or disabled. | Not applicable to Microsoft Entra ID. |
| **2.2.3** Primary functions requiring different security levels are managed as follows:  Only one primary function exists on a system component,  OR  Primary functions with differing security levels that exist on the same system component are isolated from each other, OR  Primary functions with differing security levels on the same system component are all secured to the level required by the function with the highest security need. | Learn about determining least-privileged roles. [Least privileged roles by task in Microsoft Entra ID](../identity/role-based-access-control/delegate-by-task) |
| **2.2.4** Only necessary services, protocols, daemons, and functions are enabled, and all unnecessary functionality is removed or disabled. | Review Microsoft Entra settings and disable unused features. [Five steps to securing your identity infrastructure](/en-us/azure/security/fundamentals/steps-secure-identity)[Microsoft Entra security operations guide](../architecture/security-operations-introduction) |
| **2.2.5** If any insecure services, protocols, or daemons are present:  Business justification is documented.  Additional security features are documented and implemented that reduce the risk of using insecure services, protocols, or daemons. | Review Microsoft Entra settings and disable unused features. [Five steps to securing your identity infrastructure](/en-us/azure/security/fundamentals/steps-secure-identity)[Microsoft Entra security operations guide](../architecture/security-operations-introduction) |
| **2.2.6** System security parameters are configured to prevent misuse. | Review Microsoft Entra settings and disable unused features. [Five steps to securing your identity infrastructure](/en-us/azure/security/fundamentals/steps-secure-identity)[Microsoft Entra security operations guide](../architecture/security-operations-introduction) |
| **2.2.7** All nonconsole administrative access is encrypted using strong cryptography. | Microsoft Entra ID interfaces, such the management portal, Microsoft Graph, and PowerShell, are encrypted in transit using TLS. [Enable support for TLS 1.2 in your environment for Microsoft Entra TLS 1.1 and 1.0 deprecation](/en-us/troubleshoot/azure/active-directory/enable-support-tls-environment?tabs=azure-monitor) |

## 2.3 Wireless environments are configured and managed securely.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **2.3.1** For wireless environments connected to the CDE or transmitting account data, all wireless vendor defaults are changed at installation or are confirmed to be secure, including but not limited to:  Default wireless encryption keys  Passwords on wireless access points  SNMP defaults  Any other security-related wireless vendor defaults | If your organization integrates network access points with Microsoft Entra ID for authentication, see [Requirement 1: Install and Maintain Network Security Controls](pci-requirement-1). |
| **2.3.2** For wireless environments connected to the CDE or transmitting account data, wireless encryption keys are changed as follows:  Whenever personnel with knowledge of the key leave the company or the role for which the knowledge was necessary.  Whenever a key is suspected of or known to be compromised. | Not applicable to Microsoft Entra ID. |