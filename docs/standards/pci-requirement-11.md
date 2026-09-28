---
layout: Conceptual
title: Microsoft Entra ID and PCI-DSS Requirement 11 - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/pci-requirement-11
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Learn PCI-DSS defined approach requirements for regular testing of security and network security
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
document_id: 29729038-6ac6-1022-c498-d1669099c748
document_version_independent_id: 45cfe138-0306-aef6-7c0d-6b66add74eed
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/pci-requirement-11.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/pci-requirement-11
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/pci-requirement-11.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 82f9486b-c379-16b3-ce4f-4ab7715b78cf
---

# Microsoft Entra ID and PCI-DSS Requirement 11 - Microsoft Entra | Microsoft Learn

**Requirement 11: Test Security of Systems and Networks Regularly** **Defined approach requirements**

## 11.1 Processes and mechanisms for regularly testing security of systems and networks are defined and understood.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **11.1.1** All security policies and operational procedures that are identified in Requirement 11 are:  Documented  Kept up to date  In use  Known to all affected parties | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |
| **11.1.2** Roles and responsibilities for performing activities in Requirement 11 are documented, assigned, and understood. | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |

## 11.2 Wireless access points are identified and monitored, and unauthorized wireless access points are addressed.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **11.2.1** Authorized and unauthorized wireless access points are managed as follows:  The presence of wireless (Wi-Fi) access points is tested for.  All authorized and unauthorized wireless access points are detected and identified.  Testing, detection, and identification occurs at least once every three months.  If automated monitoring is used, personnel are notified via generated alerts. | If your organization integrates network access points with Microsoft Entra ID for authentication, see [Requirement 1: Install and Maintain Network Security Controls](pci-requirement-1) |
| **11.2.2** An inventory of authorized wireless access points is maintained, including a documented business justification. | Not applicable to Microsoft Entra ID. |

## 11.3 External and internal vulnerabilities are regularly identified, prioritized, and addressed.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **11.3.1** Internal vulnerability scans are performed as follows:  At least once every three months.  High-risk and critical vulnerabilities (per the entity’s vulnerability risk rankings defined at Requirement 6.3.1) are resolved.  Rescans are performed that confirm all high-risk and critical vulnerabilities (as noted) have been resolved.  Scan tool is kept up to date with latest vulnerability information.  Scans are performed by qualified personnel and organizational independence of the tester exists. | Include servers that support Microsoft Entra hybrid capabilities. For example, Microsoft Entra Connect, Application proxy connectors, etc. as part of internal vulnerability scans.  Organizations using federated authentication: review and address federation system infrastructure vulnerabilities. [What is federation with Microsoft Entra ID?](../identity/hybrid/connect/whatis-fed) Review and mitigate risk detections reported by Microsoft Entra ID Protection. Integrate the signals with a SIEM solution to integrate more with remediation workflows or automation. [Risk types and detection](../id-protection/concept-identity-protection-risks) Run the Microsoft Entra assessment tool regularly and address findings. [`AzureADAssessment`](https://github.com/AzureAD/AzureADAssessment)[Security operations for infrastructure](../architecture/security-operations-infrastructure)[Integrate Microsoft Entra logs with Azure Monitor logs](../identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs) |
| **11.3.1.1** All other applicable vulnerabilities (those not ranked as high-risk or critical per the entity’s vulnerability risk rankings defined at Requirement 6.3.1) are managed as follows:  Addressed based on the risk defined in the entity’s targeted risk analysis, which is performed according to all elements specified in Requirement 12.3.1.  Rescans are conducted as needed. | Include servers that support Microsoft Entra hybrid capabilities. For example, Microsoft Entra Connect, Application proxy connectors, etc. as part of internal vulnerability scans.  Organizations using federated authentication: review and address federation system infrastructure vulnerabilities. [What is federation with Microsoft Entra ID?](../identity/hybrid/connect/whatis-fed) Review and mitigate risk detections reported by Microsoft Entra ID Protection. Integrate the signals with a SIEM solution to integrate more with remediation workflows or automation. [Risk types and detection](../id-protection/concept-identity-protection-risks) Run the Microsoft Entra assessment tool regularly and address findings. [`AzureAD/AzureADAssessment`](https://github.com/AzureAD/AzureADAssessment)[Security operations for infrastructure](../architecture/security-operations-infrastructure)[Integrate Microsoft Entra logs with Azure Monitor logs](../identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs) |
| **11.3.1.2** Internal vulnerability scans are performed via authenticated scanning as follows:  Systems that are unable to accept credentials for authenticated scanning are documented.  Sufficient privileges are used for those systems that accept credentials for scanning.  If accounts used for authenticated scanning can be used for interactive login, they're managed in accordance with Requirement 8.2.2. | Include servers that support Microsoft Entra hybrid capabilities. For example, Microsoft Entra Connect, Application proxy connectors, etc. as part of internal vulnerability scans.  Organizations using federated authentication: review and address federation system infrastructure vulnerabilities. [What is federation with Microsoft Entra ID?](../identity/hybrid/connect/whatis-fed) Review and mitigate risk detections reported by Microsoft Entra ID Protection. Integrate the signals with a SIEM solution to integrate more with remediation workflows or automation. [Risk types and detection](../id-protection/concept-identity-protection-risks) Run the Microsoft Entra assessment tool regularly and address findings. [`AzureADAssessment`](https://github.com/AzureAD/AzureADAssessment)[Security operations for infrastructure](../architecture/security-operations-infrastructure)[Integrate Microsoft Entra logs with Azure Monitor logs](../identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs) |
| **11.3.1.3** Internal vulnerability scans are performed after any significant change as follows:  High-risk and critical vulnerabilities (per the entity’s vulnerability risk rankings defined at Requirement 6.3.1) are resolved.  Rescans are conducted as needed.  Scans are performed by qualified personnel and organizational independence of the tester exists (not required to be a Qualified Security Assessor (QSA) or Approved Scanning Vendor (ASV)). | Include servers that support Microsoft Entra hybrid capabilities. For example, Microsoft Entra Connect, Application proxy connectors, etc. as part of internal vulnerability scans.  Organizations using federated authentication: review and address federation system infrastructure vulnerabilities. [What is federation with Microsoft Entra ID?](../identity/hybrid/connect/whatis-fed) Review and mitigate risk detections reported by Microsoft Entra ID Protection. Integrate the signals with a SIEM solution to integrate more with remediation workflows or automation. [Risk types and detection](../id-protection/concept-identity-protection-risks) Run the Microsoft Entra assessment tool regularly and address findings. [`AzureADAssessment`](https://github.com/AzureAD/AzureADAssessment)[Security operations for infrastructure](../architecture/security-operations-infrastructure)[Integrate Microsoft Entra logs with Azure Monitor logs](../identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs) |
| **11.3.2** External vulnerability scans are performed as follows:  At least once every three months.  By a PCI SSC ASV.  Vulnerabilities are resolved and ASV Program Guide requirements for a passing scan are met.  Rescans are performed as needed to confirm that vulnerabilities are resolved per the ASV Program Guide requirements for a passing scan. | Not applicable to Microsoft Entra ID. |
| **11.3.2.1** External vulnerability scans are performed after any significant change as follows:  Vulnerabilities that are scored 4.0 or higher by the CVSS are resolved.  Rescans are conducted as needed.  Scans are performed by qualified personnel and organizational independence of the tester exists (not required to be a QSA or ASV). | Not applicable to Microsoft Entra ID. |

## 11.4 External and internal penetration testing is regularly performed, and exploitable vulnerabilities and security weaknesses are corrected.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **11.4.1** A penetration testing methodology is defined, documented, and implemented by the entity, and includes:  Industry-accepted penetration testing approaches.  Coverage for the entire cardholder data environment (CDE) perimeter and critical systems.  Testing from both inside and outside the network.  Testing to validate any segmentation and scope-reduction controls.  Application-layer penetration testing to identify, at a minimum, the vulnerabilities listed in Requirement 6.2.4.  Network-layer penetration tests that encompass all components that support network functions and operating systems.  Review and consideration of threats and vulnerabilities experienced in the last 12 months.  Documented approach to assessing and addressing the risk posed by exploitable vulnerabilities and security weaknesses found during penetration testing.  Retention of penetration testing results and remediation activities results for at least 12 months. | [Penetration Testing Rules of Engagement, Microsoft Cloud](https://www.microsoft.com/msrc/pentest-rules-of-engagement) |
| **11.4.2** Internal penetration testing is performed:  Per the entity’s defined methodology.  At least once every 12 months.  After any significant infrastructure or application upgrade or change.  By a qualified internal resource or qualified external third-party.  Organizational independence of the tester exists (not required to be a QSA or ASV). | [Penetration Testing Rules of Engagement, Microsoft Cloud](https://www.microsoft.com/msrc/pentest-rules-of-engagement) |
| **11.4.3** External penetration testing is performed:  Per the entity’s defined methodology.  At least once every 12 months.  After any significant infrastructure or application upgrade or change.  By a qualified internal resource or qualified external third party.  Organizational independence of the tester exists (not required to be a QSA or ASV). | [Penetration Testing Rules of Engagement, Microsoft Cloud](https://www.microsoft.com/msrc/pentest-rules-of-engagement) |
| **11.4.4** Exploitable vulnerabilities and security weaknesses found during penetration testing are corrected as follows:  In accordance with the entity’s assessment of the risk posed by the security issue as defined in Requirement 6.3.1.  Penetration testing is repeated to verify the corrections. | [Penetration Testing Rules of Engagement, Microsoft Cloud](https://www.microsoft.com/msrc/pentest-rules-of-engagement) |
| **11.4.5** If segmentation is used to isolate the CDE from other networks, penetration tests are performed on segmentation controls as follows:  At least once every 12 months and after any changes to segmentation controls/methods.  Covering all segmentation controls/methods in use.  According to the entity’s defined penetration testing methodology.  Confirming that the segmentation controls/methods are operational and effective, and isolate the CDE from all out-of-scope systems.  Confirming effectiveness of any use of isolation to separate systems with differing security levels (see Requirement 2.2.3).  Performed by a qualified internal resource or qualified external third party.  Organizational independence of the tester exists (not required to be a QSA or ASV). | Not applicable to Microsoft Entra ID. |
| **11.4.6***Additional requirement for service providers only*: If segmentation is used to isolate the CDE from other networks, penetration tests are performed on segmentation controls as follows:  At least once every six months and after any changes to segmentation controls/methods.  Covering all segmentation controls/methods in use.  According to the entity’s defined penetration testing methodology.  Confirming that the segmentation controls/methods are operational and effective, and isolate the CDE from all out-of-scope systems.  Confirming effectiveness of any use of isolation to separate systems with differing security levels (see Requirement 2.2.3).  Performed by a qualified internal resource or qualified external third party.  Organizational independence of the tester exists (not required to be a QSA or ASV). | Not applicable to Microsoft Entra ID. |
| **11.4.7***Additional requirement for multi-tenant service providers only*: Multi-tenant service providers support their customers for external penetration testing per Requirement 11.4.3 and 11.4.4. | [Penetration Testing Rules of Engagement, Microsoft Cloud](https://www.microsoft.com/msrc/pentest-rules-of-engagement) |

## 11.5 Network intrusions and unexpected file changes are detected and responded to.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **11.5.1** Intrusion-detection and/or intrusion-prevention techniques are used to detect and/or prevent intrusions into the network as follows:  All traffic is monitored at the perimeter of the CDE.  All traffic is monitored at critical points in the CDE.  Personnel are alerted to suspected compromises.  All intrusion-detection and prevention engines, baselines, and signatures are kept up to date. | Not applicable to Microsoft Entra ID. |
| **11.5.1.1***Additional requirement for service providers only*: Intrusion-detection and/or intrusion-prevention techniques detect, alert on/prevent, and address covert malware communication channels. | Not applicable to Microsoft Entra ID. |
| **11.5.2** A change-detection mechanism (for example, file integrity monitoring tools) is deployed as follows:  To alert personnel to unauthorized modification (including changes, additions, and deletions) of critical files.  To perform critical file comparisons at least once weekly. | Not applicable to Microsoft Entra ID. |

## 11.6 Unauthorized changes on payment pages are detected and responded to.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **11.6.1** A change- and tamper-detection mechanism is deployed as follows:  To alert personnel to unauthorized modification (including indicators of compromise, changes, additions, and deletions) to the HTTP headers and the contents of payment pages as received by the consumer browser.  The mechanism is configured to evaluate the received HTTP header and payment page.  The mechanism functions are performed as follows: At least once every seven days  OR  Periodically at the frequency defined in the entity’s targeted risk analysis, which is performed according to all elements | Not applicable to Microsoft Entra ID. |