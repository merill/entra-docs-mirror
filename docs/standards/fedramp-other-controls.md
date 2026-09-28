---
layout: Conceptual
title: Configure additional controls to meet FedRAMP High Impact level - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/fedramp-other-controls
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Detailed guidance on how to configure additional controls to meet FedRAMP High Impact levels.
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, gasinh
ms.date: 2023-05-23T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 9ba23972-cd4e-1968-a673-65f27493c313
document_version_independent_id: 53ec869a-314c-9031-5166-f4af2c21bba7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/fedramp-other-controls.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/fedramp-other-controls
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/fedramp-other-controls.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/54918a83-0404-4863-9c91-715186c1f582
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b26f5f7a-0913-4a95-8337-ed7543902f2d
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 63381a2b-dd53-dbb2-2022-775ada7483f9
---

# Configure additional controls to meet FedRAMP High Impact level - Microsoft Entra | Microsoft Learn

The following list of controls (and control enhancements) might require configuration in your Microsoft Entra tenant.

Each row in the following tables provides prescriptive guidance. This guidance helps you in developing your organization's response to any shared responsibilities regarding the control or control enhancement.

## Audit and accountability

The guidance in the following table pertains to:

- AU-2 Audit events
- AU-3 Content of audit
- AU-6 Audit review, analysis, and reporting

| FedRAMP Control ID and description | Microsoft Entra guidance and recommendations |
| --- | --- |
| **AU-2 Audit Events** **The organization:** **(a.)** Determines that the information system is capable of auditing the following events: [*FedRAMP Assignment: [Successful and unsuccessful account logon events, account management events, object access, policy change, privilege functions, process tracking, and system events. For Web applications: all administrator activity, authentication checks, authorization checks, data deletions, data access, data changes, and permission changes*];**(b.)** Coordinates the security audit function with other organizational entities requiring audit-related information to enhance mutual support and to help guide the selection of auditable events;**(c.)** Provides a rationale for why the auditable events are deemed to be adequate to support after-the-fact investigations of security incidents; and**(d.)** Determines that the following events are to be audited in the information system: [*FedRAMP Assignment: organization-defined subset of the auditable events defined in AU-2 a. to be audited continually for each identified event*].**AU-2 Additional FedRAMP Requirements and Guidance:** **Requirement:** Coordination between service provider and consumer shall be documented and accepted by the JAB/AO.**AU-3 Content and Audit Records**The information system generates audit records containing information that establishes what type of event occurred, when the event occurred, where the event occurred, the source of the event, the outcome of the event, and the identity of any individuals or subjects associated with the event.**AU-3(1)**The information system generates audit records containing the following additional information: [*FedRAMP Assignment: organization-defined additional, more detailed information*].**AU-3 (1) Additional FedRAMP Requirements and Guidance:** **Requirement:** The service provider defines audit record types [*FedRAMP Assignment: session, connection, transaction, or activity duration; for client-server transactions, the number of bytes received and bytes sent; additional informational messages to diagnose or identify the event; characteristics that describe or identify the object or resource being acted upon; individual identities of group account users; full-text of privileged commands*]. The audit record types are approved and accepted by the JAB/AO.**Guidance:** For client-server transactions, the number of bytes sent and received gives bidirectional transfer information that can be helpful during an investigation or inquiry.**AU-3(2)**The information system provides centralized management and configuration of the content to be captured in audit records generated by [*FedRAMP Assignment: all network, data storage, and computing devices*]. | Ensure the system is capable of auditing events defined in AU-2 Part a. Coordinate with other entities within the organization's subset of auditable events to support after-the-fact investigations. Implement centralized management of audit records.<br>All account lifecycle operations (account creation, modification, enabling, disabling, and removal actions) are audited within the Microsoft Entra audit logs. All authentication and authorization events are audited within Microsoft Entra sign-in logs, and any detected risks are audited in the Microsoft Entra ID Protection logs. You can stream each of these logs directly into a security information and event management (SIEM) solution such as Microsoft Sentinel. Alternatively, use Azure Event Hubs to integrate logs with third-party SIEM solutions.<br><br>Audit events<br>- [Audit activity reports in the Microsoft Entra admin center](../identity/monitoring-health/concept-audit-logs)<br>- [Sign-in activity reports in the Microsoft Entra admin center](../identity/monitoring-health/concept-sign-ins)<br>- [How To: Investigate risk](../id-protection/howto-identity-protection-investigate-risk)<br>SIEM integrations<br>- [Microsoft Sentinel : Connect data from Microsoft Entra ID](/en-us/azure/sentinel/connect-azure-active-directory)<br>- [Stream to Azure event hub and other SIEMs](../identity/monitoring-health/howto-stream-logs-to-event-hub) |
| **AU-6 Audit Review, Analysis, and Reporting** **The organization:** **(a.)** Reviews and analyzes information system audit records [*FedRAMP Assignment: at least weekly*] for indications of [*Assignment: organization-defined inappropriate or unusual activity*]; and**(b.)** Reports findings to [*Assignment: organization-defined personnel or roles*].**AU-6 Additional FedRAMP Requirements and Guidance:** **Requirement:** Coordination between service provider and consumer shall be documented and accepted by the Authorizing Official. In multi-tenant environments, capability and means for providing review, analysis, and reporting to consumer for data pertaining to consumer shall be documented.**AU-6(1)**The organization employs automated mechanisms to integrate audit review, analysis, and reporting processes to support organizational processes for investigation and response to suspicious activities.**AU-6(3)**The organization analyzes and correlates audit records across different repositories to gain organization-wide situational awareness.**AU-6(4)**The information system provides the capability to centrally review and analyze audit records from multiple components within the system.**AU-6(5)**The organization integrates analysis of audit records with analysis of [*FedRAMP Selection (one or more): vulnerability scanning information; performance data; information system monitoring information; penetration test data;* [*Assignment: organization-defined data/information collected from other sources*]] to further enhance the ability to identify inappropriate or unusual activity.**AU-6(6)**The organization correlates information from audit records with information obtained from monitoring physical access to further enhance the ability to identify suspicious, inappropriate, unusual, or malevolent activity.**AU-6 Additional FedRAMP Requirements and Guidance:** **Requirement:** Coordination between service provider and consumer shall be documented and accepted by the JAB/AO.**AU-6(7)**The organization specifies the permitted actions for each [FedRAMP Selection (one or more): information system process; role; user] associated with the review, analysis, and reporting of audit information.**AU-6(10)**The organization adjusts the level of audit review, analysis, and reporting within the information system when there is a change in risk based on law enforcement information, intelligence information, or other credible sources of information. | Review and analyze audit records at least once each week to identify inappropriate or unusual activity, and report findings to appropriate personnel. <br>The preceding guidance provided for AU-02 and AU-03 allows for weekly review of audit records and reporting to appropriate personnel. You can't meet these requirements by using only Microsoft Entra ID. You must also use a SIEM solution such as Microsoft Sentinel. For more information, see [What is Microsoft Sentinel?](/en-us/azure/sentinel/overview). |

## Incident response

The guidance in the following table pertains to:

- IR-4 Incident handling
- IR-5 Incident monitoring

| FedRAMP Control ID and description | Microsoft Entra guidance and recommendations |
| --- | --- |
| **IR-4 Incident Handling** **The organization:** **(a.)** Implements an incident handling capability for security incidents that includes preparation, detection and analysis, containment, eradication, and recovery;**(b.)** Coordinates incident handling activities with contingency planning activities; and**(c.)** Incorporates lessons learned from ongoing incident handling activities into incident response procedures, training, and testing/exercises, and implements the resulting changes accordingly.**IR-4 Additional FedRAMP Requirements and Guidance:** **Requirement:** The service provider ensures that individuals conducting incident handling meet personnel security requirements commensurate with the criticality/sensitivity of the information being processed, stored, and transmitted by the information system.**IR-04(1)**The organization employs automated mechanisms to support the incident handling process.**IR-04(2)**The organization includes dynamic reconfiguration of [*FedRAMP Assignment: all network, data storage, and computing devices*] as part of the incident response capability.**IR-04(3)**The organization identifies [*Assignment: organization-defined classes of incidents*] and [*Assignment: organization-defined actions to take in response to classes of incident*] to ensure continuation of organizational missions and business functions.**IR-04(4)**The organization correlates incident information and individual incident responses to achieve an organization-wide perspective on incident awareness and response.**IR-04(6)**The organization implements incident handling capability for insider threats.**IR-04(8)**The organization implements incident handling capability for insider threats.The organization coordinates with [*FedRAMP Assignment: external organizations including consumer incident responders and network defenders and the appropriate consumer incident response team (CIRT)/ Computer Emergency Response Team (CERT) (such as US-CERT, DoD CERT, IC CERT)*] to correlate and share [*Assignment: organization-defined incident information*] to achieve a cross- organization perspective on incident awareness and more effective incident responses.**IR-05 Incident Monitoring**The organization tracks and documents information system security incidents.**IR-05(1)**The organization employs automated mechanisms to assist in the tracking of security incidents and in the collection and analysis of incident information. | Implement incident handling and monitoring capabilities. This includes Automated Incident Handling, Dynamic Reconfiguration, Continuity of Operations, Information Correlation, Insider Threats, Correlation with External Organizations, and Incident Monitoring and Automated Tracking. <br>The audit logs record all configuration changes. Authentication and authorization events are audited within the sign-in logs, and any detected risks are audited in the Microsoft Entra ID Protection logs. You can stream each of these logs directly into a SIEM solution, such as Microsoft Sentinel. Alternatively, use Azure Event Hubs to integrate logs with third-party SIEM solutions. Automate dynamic reconfiguration based on events in the SIEM by using Microsoft Graph PowerShell.<br><br>Audit events<br>- [Audit activity reports in the Microsoft Entra admin center](../identity/monitoring-health/concept-audit-logs)<br>- [Sign-in activity reports in the Microsoft Entra admin center](../identity/monitoring-health/concept-sign-ins)<br>- [How To: Investigate risk](../id-protection/howto-identity-protection-investigate-risk)<br>SIEM integrations<br>- [Microsoft Sentinel : Connect data from Microsoft Entra ID](/en-us/azure/sentinel/connect-azure-active-directory)<br>- [Stream to Azure event hub and other SIEMs](../identity/monitoring-health/howto-stream-logs-to-event-hub) |

## Personnel security

The guidance in the following table pertains to:

- PS-4 Personnel termination

| FedRAMP Control ID and description | Microsoft Entra guidance and recommendations |
| --- | --- |
| **PS-4 Personnel Termination**The organization, upon termination of individual employment:**(a.)** Disables information system access within [*FedRAMP Assignment: eight (8) hours*];**(b.)** Terminates/revokes any authenticators/credentials associated with the individual;**(c.)** Conducts exit interviews that include a discussion of [*Assignment: organization-defined information security topics*];**(d.)** Retrieves all security-related organizational information system-related property;**(e.)** Retains access to organizational information and information systems formerly controlled by terminated individual; and**(f.)** Notifies [*Assignment: organization-defined personnel or roles*] within [*Assignment: organization-defined time period*].**PS-4(2)**The organization employs automated mechanisms to notify [*FedRAMP Assignment: access control personnel responsible for disabling access to the system*] upon termination of an individual. | Automatically notify personnel responsible for disabling access to the system. <br>Disable accounts and revoke all associated authenticators and credentials within 8 hours. <br><br>Configure provisioning (including disablement upon termination) of accounts in Microsoft Entra ID from external HR systems, on-premises Active Directory, or directly in the cloud. Terminate all system access by revoking existing sessions. <br><br>Account provisioning<br>- See detailed guidance in AC-02. <br>Revoke all associated authenticators<br>- [Revoke user access in an emergency in Microsoft Entra ID](../identity/users/users-revoke-access) |

## System and information integrity

The guidance in the following table pertains to:

- SI-4 Information system monitoring

| FedRAMP Control ID and description | Microsoft Entra guidance and recommendations |
| --- | --- |
| **SI-4 Information System Monitoring** **The organization:** **(a.)** Monitors the information system to detect:**(1.)** Attacks and indicators of potential attacks in accordance with [*Assignment: organization-defined monitoring objectives*]; and**(2.)** Unauthorized local, network, and remote connections;**(b.)** Identifies unauthorized use of the information system through [*Assignment: organization-defined techniques and methods*];**(c.)** Deploys monitoring devices (i) strategically within the information system to collect organization-determined essential information; and (ii) at ad hoc locations within the system to track specific types of transactions of interest to the organization;**(d.)** Protects information obtained from intrusion-monitoring tools from unauthorized access, modification, and deletion;**(e.)** Heightens the level of information system monitoring activity whenever there is an indication of increased risk to organizational operations and assets, individuals, other organizations, or the Nation based on law enforcement information, intelligence information, or other credible sources of information;**(f.)** Obtains legal opinion with regard to information system monitoring activities in accordance with applicable federal laws, Executive Orders, directives, policies, or regulations; and**(d.)** Provides [*Assignment: organization-defined information system monitoring information*] to [*Assignment: organization-defined personnel or roles] [Selection (one or more): as needed; [Assignment: organization-defined frequency]*].**SI-4 Additional FedRAMP Requirements and Guidance:** **Guidance:** See US-CERT Incident Response Reporting Guidelines.**SI-04(1)** The organization connects and configures individual intrusion detection tools into an information system-wide intrusion detection system. | Implement information system-wide monitoring, and the intrusion detection system. <br>Include all Microsoft Entra logs (Audit, Sign-in, ID Protection) within the information system monitoring solution. <br><br>Stream Microsoft Entra logs into a SIEM solution (see IA-04). |