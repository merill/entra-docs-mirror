---
layout: Conceptual
title: Configure Microsoft Entra HIPAA audit control safeguards - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/hipaa-audit-controls
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Guidance on how to configure Microsoft Entra HIPAA audit control safeguards
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, jricketts
ms.date: 2023-04-13T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 82ebca5f-1ad6-6096-cbed-1e5d26320b3a
document_version_independent_id: 66a9061b-9bc9-0f45-c24e-799819a91afd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/hipaa-audit-controls.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/hipaa-audit-controls
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/hipaa-audit-controls.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
platformId: 19eef470-7899-261a-4777-31d33a48eb8a
---

# Configure Microsoft Entra HIPAA audit control safeguards - Microsoft Entra | Microsoft Learn

Microsoft Entra ID meets identity-related practice requirements for implementing Health Insurance Portability and Accountability Act of 1996 (HIPAA) safeguards. To be HIPAA compliant, implement the safeguards using this guidance, with other needed configurations or processes.

For the audit controls:

- Establish data governance for personal data storage.
- Identify and label sensitive data.
- Configure audit collection and secure log data.
- Configure data loss prevention.
- Enable information protection.

For safeguard:

- Determine where Protected Health Information (PHI) data is stored.
- Identify and mitigate any risks for data that is stored.

This article provides relevant HIPAA safeguard wording, followed by a table with Microsoft recommendations and guidance to help achieve HIPAA compliance.

## Audit controls

The following content is safeguard guidance from HIPAA. Find Microsoft recommendations to meet safeguard implementation requirements.

**HIPAA safeguard - audit controls**

`Implement hardware, software, and/or procedural mechanisms that record and examine activity in information systems that contain or use electronic protected health information.`

| Recommendation | Action |
| --- | --- |
| Enable Microsoft Purview | [Microsoft Purview](/en-us/purview/purview) helps to manage and monitor data by providing data governance. Using Purview helps to minimize compliance risks and meet regulatory requirements.Microsoft Purview in the governance portal provides a [unified data governance](/en-us/microsoft-365/compliance/manage-data-governance) service that helps you manage your on-premises, multicloud and Software-as-service (SaaS) data.Microsoft Purview is a framework, a suite of products that work together to provide visualization of sensitive data lifecycle protection for data, and data loss prevention. |
| Enable Microsoft Sentinel | [Microsoft Sentinel](/en-us/azure/sentinel/overview) provides security information and event management (SIEM) and security orchestration, automation, and response (SOAR) solutions. Microsoft Sentinel collects audit logs and uses built-in AI to help analyze large volumes of data. SIEM enables an organization to detect incidents that could go undetected. |
| Configure Azure Monitor | [Use Azure Monitor Logs](/en-us/azure/azure-monitor/logs/data-security) collects and organizes logs, expanding to cloud and hybrid environments. It provides recommendations on key areas on how to protect resources combined with Azure trust center. |
| Enable logging and monitoring | [Logging and monitoring](/en-us/security/benchmark/azure/security-control-logging-monitoring) are essential to securing an environment. The data supports investigations and helps detect potential threats by identifying unusual patterns. Enable logging and monitoring of services to reduce the risk of unauthorized access.We recommend you monitor [Microsoft Entra activity logs](../identity/monitoring-health/howto-access-activity-logs). |
| Scan environment for electronic protected health information (ePHI) data | [Microsoft Purview](/en-us/azure/purview/overview) can be enabled in audit mode to scan what ePHI is sitting in the data estate and the resources that being used to store that data. This capability helps in establishing data classification and labeling based on the sensitivity of the data. |
| Create a data loss prevention (DLP) policy | DLP policies help establish processes to ensure that sensitive data isn't lost, misused, or accessed by unauthorized users. It prevents data breaches and exfiltration.[Microsoft Purview DLP](/en-us/microsoft-365/compliance/dlp-policy-reference) examines email messages, navigate to the Microsoft Purview portal to review the polices and customize them for your organization. |
| Enable monitoring through Azure Policy | [Azure Policy](/en-us/azure/governance/policy/overview) helps to enforce organizational standards, and enables the ability to assess the state of compliance across an environment. This approach ensures consistency, regulatory compliance and monitoring providing security recommendations through [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction) |
| Assess device management requirements | [Microsoft Intune](/en-us/mem/intune/) can be used to provide mobile device management (MDM) and mobile application management (MAM). Microsoft Intune provides control over company and personal devices. Capabilities include managing how devices can be used and enforcing policies that give you direct control over mobile applications. |
| Application protection | Microsoft Intune can help establish a [data protection framework](/en-us/mem/intune/apps/app-protection-policy) that covers the Microsoft 365 office applications, and incorporating them across devices. App protection policies ensure that organizational data remains safe and contained in the app on both personal (BYOD) to corporate owned devices. |
| Configure insider risk management | Microsoft Purview [Insider Risk Management](/en-us/microsoft-365/compliance/insider-risk-management-solution-overview) correlates signals to identify potential malicious or inadvertent insider risks, such as IP theft, data leakage, and security violations. Insider Risk Management enables you to create policies to manage security and compliance. This capability is built upon the principle of privacy by design, users are pseudonymized by default, and role-based access controls and audit logs are in place to help ensure user-level privacy. |
| Configure communication compliance | Microsoft Purview [Communication Compliance](/en-us/microsoft-365/compliance/communication-compliance-solution-overview) provides the tools to help organizations detect regulatory compliance such as compliance for Securities and Exchange Commission (SEC) or Financial Industry Regulatory Authority (FINRA) standards. The tool monitors for business conduct violations such as sensitive or confidential information, harassing or threatening language, and sharing of adult content. This capability is built with privacy by design, usernames are pseudonymized by default, role-based access controls are built in, investigators are opted in by an admin, and audit logs are in place to help ensure user-level privacy. |

## Safeguard controls

The following content provides the safeguard controls guidance from HIPAA. Find Microsoft recommendations to meet HIPAA compliance.

**HIPAA - safeguard**

`Conduct an accurate and thorough safeguard of the potential risks and vulnerabilities to the confidentiality, integrity, and availability of electronic protected health information held by the covered entity.`

| Recommendation | Action |
| --- | --- |
| Scan environment for ePHI data | [Microsoft Purview](/en-us/purview/governance-solutions-overview) can be enabled in audit mode to scan what ePHI is sitting in the data estate, and the resources that are being used to store that data. This information helps in establishing data classification and labeling the sensitivity of the data.In addition, using [Content Explorer](/en-us/purview/data-classification-content-explorer) provides visibility into where the sensitive data is located. This information helps start the labeling journey from manually applying labeling or labeling recommendations on the client-side to service-side autolabeling. |
| Enable Priva to safeguard Microsoft 365 data | [Microsoft Priva](/en-us/privacy/priva/priva-overview) evaluate ePHI data stored in Microsoft 365, scanning, and evaluating for sensitive information. |
| Enable Azure Security benchmark | [Microsoft cloud security benchmark](/en-us/security/benchmark/azure/introduction) provides control for data protection across Azure services and provides a baseline for implementation for services that store ePHI. Audit mode provides those recommendations and remediation steps to secure the environment. |
| Enable Defender Vulnerability Management | [Microsoft Defender Vulnerability management](/en-us/azure/defender-for-cloud/remediate-vulnerability-findings-vm) is a built-in module in **Microsoft Defender for Endpoint**. The module helps you identify and discover vulnerabilities and misconfigurations in real-time. The module also helps you prioritize presenting the findings in a dashboard, and reports across devices, VMs and databases. |

## Learn more

- [Zero Trust Pillar: Devices, Data, Application, Visibility, Automation and Orchestration](/en-us/security/zero-trust/zero-trust-overview)
- [Zero Trust Pillar: Data, Visibility, Automation and Orchestration](/en-us/security/zero-trust/zero-trust-overview)