---
layout: Conceptual
title: Microsoft Entra ID and PCI-DSS Requirement 1 - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/pci-requirement-1
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Learn PCI-DSS defined approach requirements for installing and maintaining network security controls
ms.service: entra
ms.subservice: standards
ms.topic: how-to
ms.reviewer: martinco, jricketts
author: janicericketts
ms.author: jricketts
ms.date: 2023-04-18T00:00:00.0000000Z
ms.custom: it-pro
ms.collection: 
locale: en-us
document_id: 14bbcdb2-387e-0353-3f90-193b8a1e3141
document_version_independent_id: c6e2fce7-f202-1d7f-5cd0-a0ec53b3f8f1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/pci-requirement-1.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/pci-requirement-1
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/pci-requirement-1.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 09516003-0174-173e-54cb-30c0e2d563fd
---

# Microsoft Entra ID and PCI-DSS Requirement 1 - Microsoft Entra | Microsoft Learn

**Requirement 1: Install and Maintain Network Security Controls** **Defined approach requirements**

## 1.1 Processes and mechanisms for installing and maintaining network security controls are defined and understood.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **1.1.1** All security policies and operational procedures that are identified in Requirement 1 are:  Documented  Kept up to date  In use  Known to all affected parties | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |
| **1.1.2** Roles and responsibilities for performing activities in Requirement 1 are documented, assigned, and understood | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |

## 1.2 Network security controls (NSCs) are configured and maintained.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **1.2.1** Configuration standards for NSC rulesets are:  Defined  Implemented  Maintained | Integrate access technologies such as VPN, remote desktop, and network access points with Microsoft Entra ID for authentication and authorization, if the access technologies support modern authentication. Ensure NSC standards, which pertain to identity-related controls, include definition of Conditional Access policies, application assignment, access reviews, group management, credential policies, etc. [Microsoft Entra operations reference guide](../architecture/ops-guide-intro) |
| **1.2.2** All changes to network connections and to configurations of NSCs are approved and managed in accordance with the change control process defined at Requirement 6.5.1 | Not applicable to Microsoft Entra ID. |
| **1.2.3** An accurate network diagram(s) is maintained that shows all connections between the cardholder data environment (CDE) and other networks, including any wireless networks. | Not applicable to Microsoft Entra ID. |
| **1.2.4** An accurate data-flow diagram(s) is maintained that meets the following:  Shows all account data flows across systems and networks.  Updated as needed upon changes to the environment. | Not applicable to Microsoft Entra ID. |
| **1.2.5** All services, protocols, and ports allowed are identified, approved, and have a defined business need | Not applicable to Microsoft Entra ID. |
| **1.2.6** Security features are defined and implemented for all services, protocols, and ports in use and considered insecure, such that risk is mitigated. | Not applicable to Microsoft Entra ID. |
| **1.2.7** Configurations of NSCs are reviewed at least once every six months to confirm they're relevant and effective. | Use Microsoft Entra access reviews to automate group-membership reviews and applications, such as VPN appliances, which align to network security controls in your CDE. [What are access reviews?](../id-governance/access-reviews-overview) |
| **1.2.8** Configuration files for NSCs are:  Secured from unauthorized access  Kept consistent with active network configurations | Not applicable to Microsoft Entra ID. |

## 1.3 Network access to and from the cardholder data environment is restricted.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **1.3.1** Inbound traffic to the CDE is restricted as follows:  To only traffic that is necessary.  All other traffic is specifically denied | Use Microsoft Entra ID to configure named locations to create Conditional Access policies. Calculate user and sign-in risk. Microsoft recommends customers populate and maintain the CDE IP addresses using network locations. Use them to define Conditional Access policy requirements. [Using the location condition in a Conditional Access policy](../identity/conditional-access/concept-assignment-network) |
| **1.3.2** Outbound traffic from the CDE is restricted as follows:  To only traffic that is necessary.  All other traffic is specifically denied | For NSC design, include Conditional Access policies for applications to allow access to CDE IP addresses.  Emergency access or remote access to establish connectivity to CDE, such as virtual private network (VPN) appliances, captive portals, might need policies to prevent unintended lockout. [Using the location condition in a Conditional Access policy](../identity/conditional-access/concept-assignment-network)[Manage emergency access accounts in Microsoft Entra ID](../identity/role-based-access-control/security-emergency-access) |
| **1.3.3** NSCs are installed between all wireless networks and the CDE, regardless of whether the wireless network is a CDE, such that:  All wireless traffic from wireless networks into the CDE is denied by default.  Only wireless traffic with an authorized business purpose is allowed into the CDE. | For NSC design, include Conditional Access policies for applications to allow access to CDE IP addresses.  Emergency access or remote access to establish connectivity to CDE, such as virtual private network (VPN) appliances, captive portals, might need policies to prevent unintended lockout. [Using the location condition in a Conditional Access policy](../identity/conditional-access/concept-assignment-network)[Manage emergency access accounts in Microsoft Entra ID](../identity/role-based-access-control/security-emergency-access) |

## 1.4 Network connections between trusted and untrusted networks are controlled.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **1.4.1** NSCs are implemented between trusted and untrusted networks. | Not applicable to Microsoft Entra ID. |
| **1.4.2** Inbound traffic from untrusted networks to trusted networks is restricted to:  Communications with system components that are authorized to provide publicly accessible services, protocols, and ports.  Stateful responses to communications initiated by system components in a trusted network.  All other traffic is denied. | Not applicable to Microsoft Entra ID. |
| **1.4.3** Anti-spoofing measures are implemented to detect and block forged source IP addresses from entering the trusted network. | Not applicable to Microsoft Entra ID. |
| **1.4.4** System components that store cardholder data are not directly accessible from untrusted networks. | In addition to controls in the networking layer, applications in the CDE using Microsoft Entra ID can use Conditional Access policies. Restrict access to applications based on location. [Using network location in a Conditional Access policy](../identity/conditional-access/concept-assignment-network) |
| **1.4.5** The disclosure of internal IP addresses and routing information is limited to only authorized parties. | Not applicable to Microsoft Entra ID. |

## 1.5 Risks to the CDE from computing devices that are able to connect to both untrusted networks and the CDE are mitigated.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **1.5.1** Security controls are implemented on any computing devices, including company- and employee-owned devices, that connect to both untrusted networks (including the Internet) and the CDE as follows:  Specific configuration settings are defined to prevent threats being introduced into the entity’s network.  Security controls are actively running.  Security controls are not alterable by users of the computing devices unless specifically documented and authorized by management on a case-by-case basis for a limited period. | Deploy Conditional Access policies that require device compliance. [Use compliance policies to set rules for devices you manage with Intune](/en-us/mem/intune/protect/device-compliance-get-started) Integrate device compliance state with anti-malware solutions. [Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune](/en-us/mem/intune/protect/advanced-threat-protection)[Mobile Threat Defense integration with Intune](/en-us/mem/intune/protect/mobile-threat-defense) |