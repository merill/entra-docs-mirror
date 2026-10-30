---
layout: Conceptual
title: Microsoft Entra ID and PCI-DSS Requirement 10 - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/pci-requirement-10
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Learn PCI-DSS defined approach requirements about logging and monitoring all access to system components and CHD
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
document_id: f347bd8a-b022-acbd-6145-a8440f9aed89
document_version_independent_id: 90da366d-a5c7-438c-2716-506bd3e0b160
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/pci-requirement-10.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/pci-requirement-10
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/pci-requirement-10.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 3607a44b-3f1d-3e92-503e-fe283121a2dc
---

# Microsoft Entra ID and PCI-DSS Requirement 10 - Microsoft Entra | Microsoft Learn

**Requirement 10: Log and Monitor All Access to System Components and Cardholder Data** **Defined approach requirements**

## 10.1 Processes and mechanisms for logging and monitoring all access to system components and cardholder data are defined and documented.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **10.1.1** All security policies and operational procedures that are identified in Requirement 10 are:  Documented  Kept up to date  In use  Known to all affected parties | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |
| **10.1.2** Roles and responsibilities for performing activities in Requirement 10 are documented, assigned, and understood. | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |

## 10.2 Audit logs are implemented to support the detection of anomalies and suspicious activity, and the forensic analysis of events.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **10.2.1** Audit logs are enabled and active for all system components and cardholder data. | Archive Microsoft Entra audit logs to obtain changes to security policies and Microsoft Entra tenant configuration.  Archive Microsoft Entra activity logs in a security information and event management (SIEM) system to learn about usage. [Microsoft Entra activity logs in Azure Monitor](../identity/monitoring-health/concept-log-monitoring-integration-options-considerations) |
| **10.2.1.1** Audit logs capture all individual user access to cardholder data. | Not applicable to Microsoft Entra ID. |
| **10.2.1.2** Audit logs capture all actions taken by any individual with administrative access, including any interactive use of application or system accounts. | Not applicable to Microsoft Entra ID. |
| **10.2.1.3** Audit logs capture all access to audit logs. | In Microsoft Entra ID, you can’t wipe or modify logs. Privileged users can query logs from Microsoft Entra ID. [Least privileged roles by task in Microsoft Entra ID](../identity/role-based-access-control/delegate-by-task) When audit logs are exported to systems such as Azure Log Analytics Workspace, storage accounts, or third-party SIEM systems, monitor them for access. |
| **10.2.1.4** Audit logs capture all invalid logical access attempts. | Microsoft Entra ID generates activity logs when a user attempts to sign in with invalid credentials. It generates activity logs when access is denied due to Conditional Access policies. |
| **10.2.1.5** Audit logs capture all changes to identification and authentication credentials including, but not limited to:  Creation of new accounts  Elevation of privileges  All changes, additions, or deletions to accounts with administrative access | Microsoft Entra ID generates audit logs for the events in this requirement. |
| **10.2.1.6** Audit logs capture the following:  All initialization of new audit logs, and  All starting, stopping, or pausing of the existing audit logs. | Not applicable to Microsoft Entra ID. |
| **10.2.1.7** Audit logs capture all creation and deletion of system-level objects. | Microsoft Entra ID generates audit logs for events in this requirement. |
| **10.2.2** Audit logs record the following details for each auditable event:  User identification.  Type of event.  Date and time.  Success and failure indication.  Origination of event.  Identity or name of affected data, system component, resource, or service (for example, name and protocol). | See, [Audit logs in Microsoft Entra ID](../identity/monitoring-health/concept-audit-logs) |

## 10.3 Audit logs are protected from destruction and unauthorized modifications.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **10.3.1** Read access to audit logs files is limited to those with a job-related need. | Privileged users can query logs from Microsoft Entra ID. [Least privileged roles by task in Microsoft Entra ID](../identity/role-based-access-control/delegate-by-task) |
| **10.3.2** Audit log files are protected to prevent modifications by individuals. | In Microsoft Entra ID, you can’t wipe or modify logs.  When audit logs are exported to systems such as Azure Log Analytics Workspace, storage accounts, or third-party SIEM systems, monitor them for access. |
| **10.3.3** Audit log files, including those for external-facing technologies, are promptly backed up to a secure, central, internal log server(s) or other media that is difficult to modify. | In Microsoft Entra ID, you can’t wipe or modify logs.  When audit logs are exported to systems such as Azure Log Analytics Workspace, storage accounts, or third-party SIEM systems, monitor them for access. |
| **10.3.4** File integrity monitoring or change-detection mechanisms is used on audit logs to ensure that existing log data can't be changed without generating alerts. | In Microsoft Entra ID, you can’t wipe or modify logs.  When audit logs are exported to systems such as Azure Log Analytics Workspace, storage accounts, or third-party SIEM systems, monitor them for access. |

## 10.4 Audit logs are reviewed to identify anomalies or suspicious activity.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **10.4.1** The following audit logs are reviewed at least once daily:  All security events.  Logs of all system components that store, process, or transmit cardholder data (CHD) and/or sensitive authentication data (SAD). Logs of all critical system components.  Logs of all servers and system components that perform security functions (for example, network security controls, intrusion-detection systems/intrusion-prevention systems (IDS/IPS), authentication servers). | Include Microsoft Entra logs in this process. |
| **10.4.1.1** Automated mechanisms are used to perform audit log reviews. | Include Microsoft Entra logs in this process. Configure automated actions and alerting when Microsoft Entra logs are integrated with Azure Monitor. [Deploy Azure Monitor: Alerts and automated actions](/en-us/azure/azure-monitor/best-practices-alerts) |
| **10.4.2** Logs of all other system components (those not specified in Requirement 10.4.1) are reviewed periodically. | Not applicable to Microsoft Entra ID. |
| **10.4.2.1** The frequency of periodic log reviews for all other system components (not defined in Requirement 10.4.1) is defined in the entity’s targeted risk analysis, which is performed according to all elements specified in Requirement 12.3.1 | Not applicable to Microsoft Entra ID. |
| **10.4.3** Exceptions and anomalies identified during the review process are addressed. | Not applicable to Microsoft Entra ID. |

## 10.5 Audit log history is retained and available for analysis.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **10.5.1** Retain audit log history for at least 12 months, with at least the most recent three months immediately available for analysis. | Integrate with Azure Monitor and export the logs for long term archival. [Integrate Microsoft Entra logs with Azure Monitor logs](../identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs) Learn about Microsoft Entra logs data retention policy. [Microsoft Entra data retention](../identity/monitoring-health/reference-reports-data-retention) |

## 10.6 Time-synchronization mechanisms support consistent time settings across all systems.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **10.6.1** System clocks and time are synchronized using time-synchronization technology. | Learn about the time synchronization mechanism in Azure services. [Time synchronization for financial services in Azure](https://azure.microsoft.com/blog/time-synchronization-for-financial-services-in-azure/) |
| **10.6.2** Systems are configured to the correct and consistent time as follows:  One or more designated time servers are in use.  Only the designated central time server(s) receives time from external sources.  Time received from external sources is based on International Atomic Time or Coordinated Universal Time (UTC).  The designated time server(s) accept time updates only from specific industry-accepted external sources.  Where there's more than one designated time server, the time servers peer with one another to keep accurate time.  Internal systems receive time information only from designated central time server(s). | Learn about the time synchronization mechanism in Azure services. [Time synchronization for financial services in Azure](https://azure.microsoft.com/blog/time-synchronization-for-financial-services-in-azure/) |
| **10.6.3** Time synchronization settings and data are protected as follows:  Access to time data is restricted to only personnel with a business need.  Any changes to time settings on critical systems are logged, monitored, and reviewed. | Microsoft Entra ID relies on time synchronization mechanisms in Azure.  Azure procedures synchronize servers and network devices with NTP Stratum 1-time servers synchronized to global positioning system (GPS) satellites. Synchronization occurs every five minutes. Azure ensures service hosts sync time. [Time synchronization for financial services in Azure](https://azure.microsoft.com/blog/time-synchronization-for-financial-services-in-azure/) Hybrid components in Microsoft Entra ID, such as Microsoft Entra Connect servers, interact with on-premises infrastructure. The customer owns time synchronization of on-premises servers. |

## 10.7 Failures of critical security control systems are detected, reported, and responded to promptly.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **10.7.2***Additional requirement for service providers only*: Failures of critical security control systems are detected, alerted, and addressed promptly, including but not limited to failure of the following critical security control systems:  Network security controls  IDS/IPS  File integrity monitoring (FIM)  Anti-malware solutions  Physical access controls  Logical access controls  Audit logging mechanism  Segmentation controls (if used) | Microsoft Entra ID relies on time synchronization mechanisms in Azure.  Azure supports real-time event analysis in its operational environment. Internal Azure infrastructure systems generate near real-time event alerts about potential compromise. |
| **10.7.2** Failures of critical security control systems are detected, alerted, and addressed promptly, including but not limited to failure of the following critical security control systems:  Network security controls  IDS/IP  Change-detection mechanisms  Anti-malware solutions  Physical access controls  Logical access controls  Audit logging mechanisms  Segmentation controls (if used)  Audit log review mechanisms  Automated security testing tools (if used) | See, [Microsoft Entra security operations guide](../architecture/security-operations-introduction) |
| **10.7.3** Failures of any critical security controls systems are responded to promptly, including but not limited to:  Restoring security functions.  Identifying and documenting the duration (date and time from start to end) of the security failure.  Identifying and documenting the cause(s) of failure and documenting required remediation.  Identifying and addressing any security issues that arose during the failure.  Determining whether further actions are required as a result of the security failure.  Implementing controls to prevent the cause of failure from reoccurring.  Resuming monitoring of security controls. | See, [Microsoft Entra security operations guide](../architecture/security-operations-introduction) |