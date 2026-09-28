---
layout: Conceptual
title: Microsoft Entra ID and PCI-DSS Requirement 5 - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/pci-requirement-5
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Learn PCI-DSS defined approach requirements for protecting all systems and networks from malicious software
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
document_id: 9e2b7bb1-5353-cf4f-5a59-a97ad11bc77e
document_version_independent_id: f7fc67f4-f1d1-14e3-d378-f9e49c19724d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/pci-requirement-5.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/pci-requirement-5
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/pci-requirement-5.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ca3e3e74-9d3b-209e-e73e-2a7c61f8b05a
---

# Microsoft Entra ID and PCI-DSS Requirement 5 - Microsoft Entra | Microsoft Learn

**Requirement 5: Protect All Systems and Networks from Malicious Software** **Defined approach requirements**

## 5.1 Processes and mechanisms for protecting all systems and networks from malicious software are defined and understood.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **5.1.1** All security policies and operational procedures that are identified in Requirement 5 are:  Documented  Kept up to date  In use  Known to all affected parties | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |
| **5.1.2** Roles and responsibilities for performing activities in Requirement 5 are documented, assigned, and understood. | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |

## 5.2 Malicious software (malware) is prevented, or detected and addressed.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **5.2.1** An anti-malware solution(s) is deployed on all system components, except for those system components identified in periodic evaluations per Requirement 5.2.3 that concludes the system components aren't at risk from malware. | Deploy Conditional Access policies that require device compliance. [Use compliance policies to set rules for devices you manage with Intune](/en-us/mem/intune/protect/device-compliance-get-started) Integrate device compliance state with anti-malware solutions. [Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune](/en-us/mem/intune/protect/advanced-threat-protection)[Mobile Threat Defense integration with Intune](/en-us/mem/intune/protect/mobile-threat-defense) |
| **5.2.2** The deployed anti-malware solution(s):  Detects all known types of malware. Removes, blocks, or contains all known types of malware. | Not applicable to Microsoft Entra ID. |
| **5.2.3** Any system components that aren't at risk for malware are evaluated periodically to include the following:  A documented list of all system components not at risk for malware.  Identification and evaluation of evolving malware threats for those system components.  Confirmation whether such system components continue to not require anti-malware protection. | Not applicable to Microsoft Entra ID. |
| **5.2.3.1** The frequency of periodic evaluations of system components identified as not at risk for malware is defined in the entity’s targeted risk analysis, which is performed according to all elements specified in Requirement 12.3.1. | Not applicable to Microsoft Entra ID. |

## 5.3 Anti-malware mechanisms and processes are active, maintained, and monitored.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **5.3.1** The anti-malware solution(s) is kept current via automatic updates. | Not applicable to Microsoft Entra ID. |
| **5.3.2** The anti-malware solution(s):  Performs periodic scans and active or real-time scans. OR  Performs continuous behavioral analysis of systems or processes. | Not applicable to Microsoft Entra ID. |
| **5.3.2.1** If periodic malware scans are performed to meet Requirement 5.3.2, the frequency of scans is defined in the entity’s targeted risk analysis, which is performed according to all elements specified in Requirement 12.3.1. | Not applicable to Microsoft Entra ID. |
| **5.3.3** For removable electronic media, the anti-malware solution(s):  Performs automatic scans of when the media is inserted, connected, or logically mounted,  OR  Performs continuous behavioral analysis of systems or processes when the media is inserted, connected, or logically mounted. | Not applicable to Microsoft Entra ID. |
| **5.3.4** Audit logs for the anti-malware solution(s) are enabled and retained in accordance with Requirement 10.5.1. | Not applicable to Microsoft Entra ID. |
| **5.3.5** Anti-malware mechanisms can't be disabled or altered by users, unless specifically documented, and authorized by management on a case-by-case basis for a limited time period. | Not applicable to Microsoft Entra ID. |

## 5.4 Anti-phishing mechanisms protect users against phishing attacks.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **5.4.1** Processes and automated mechanisms are in place to detect and protect personnel against phishing attacks. | Configure Microsoft Entra ID to use phishing-resistant credentials. [Implementation considerations for phishing-resistant MFA](memo-22-09-multi-factor-authentication) Use controls in Conditional Access to require authentication with phishing-resistant credentials. [Conditional Access authentication strength](../identity/authentication/concept-authentication-strengths) Guidance herein relates to identity and access management configuration. To mitigate phishing attacks, deploy workload capabilities, such as in Microsoft 365. [Anti-phishing protection in Microsoft 365](/en-us/microsoft-365/security/office-365-security/anti-phishing-protection-about?view=o365-worldwide&amp;preserve-view=true) |