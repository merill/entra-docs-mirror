---
layout: Conceptual
title: Microsoft Entra security operations for Privileged Identity Management - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/security-operations-privileged-identity-management
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Establish baselines and use Microsoft Entra Privileged Identity Management (PIM) to monitor and alert on issues with accounts governed by PIM.
ms.topic: concept-article
ms.date: 2022-09-06T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
ms.subservice: architecture
locale: en-us
document_id: 9bd9dc46-b9d6-ea38-e7b2-a6dd9fb51016
document_version_independent_id: 3bf3da69-65f1-399e-dbe4-f6133af42a08
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/security-operations-privileged-identity-management.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/security-operations-privileged-identity-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/security-operations-privileged-identity-management.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: bb3976a4-b8b7-b091-08ab-47f9bc54ba48
---

# Microsoft Entra security operations for Privileged Identity Management - Microsoft Entra | Microsoft Learn

The security of business assets depends on the integrity of the privileged accounts that administer your IT systems. Cyber-attackers use credential theft attacks to target admin accounts and other privileged access accounts to try gaining access to sensitive data.

For cloud services, prevention and response are the joint responsibilities of the cloud service provider and the customer.

Traditionally, organizational security has focused on the entry and exit points of a network as the security perimeter. However, SaaS apps and personal devices have made this approach less effective. In Microsoft Entra ID, we replace the network security perimeter with authentication in your organization's identity layer. As users are assigned to privileged administrative roles, their access must be protected in on-premises, cloud, and hybrid environments.

You're entirely responsible for all layers of security for your on-premises IT environment. When you use Azure cloud services, prevention and response are joint responsibilities of Microsoft as the cloud service provider and you as the customer.

- For more information on the shared responsibility model, see [Shared responsibility in the cloud](/en-us/azure/security/fundamentals/shared-responsibility).
- For more information on securing access for privileged users, see [Securing Privileged access for hybrid and cloud deployments in Microsoft Entra ID](../identity/role-based-access-control/security-planning).
- For a wide range of videos, how-to guides, and content of key concepts for privileged identity, visit [Privileged Identity Management documentation](../id-governance/privileged-identity-management/).

Privileged Identity Management (PIM) is a Microsoft Entra service that enables you to manage, control, and monitor access to important resources in your organization. These resources include resources in Microsoft Entra ID, Azure, and other Microsoft Online Services such as Microsoft 365 or Microsoft Intune. You can use PIM to help mitigate the following risks:

- Identify and minimize the number of people who have access to secure information and resources.
- Detect excessive, unnecessary, or misused access permissions on sensitive resources.
- Reduce the chances of a malicious actor getting access to secured information or resources.
- Reduce the possibility of an unauthorized user inadvertently impacting sensitive resources.

Use this article provides guidance to set baselines, audit sign-ins, and usage of privileged accounts. Use the source audit log source to help maintain privileged account integrity.

## Where to look

The log files you use for investigation and monitoring are:

- [Microsoft Entra audit logs](../identity/monitoring-health/concept-audit-logs)
- [Sign-in logs](../identity/monitoring-health/concept-sign-ins)
- [Microsoft 365 Audit logs](/en-us/microsoft-365/compliance/auditing-solutions-overview)
- [Azure Key Vault logs](/en-us/azure/key-vault/general/logging?tabs=Vault)

In the Azure portal, view the Microsoft Entra audit logs and download them as comma-separated value (CSV) or JavaScript Object Notation (JSON) files. The Azure portal has several ways to integrate Microsoft Entra logs with other tools to automate monitoring and alerting:

- [**Microsoft Sentinel**](/en-us/azure/sentinel/overview) – enables intelligent security analytics at the enterprise level by providing security information and event management (SIEM) capabilities.
- **[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure)** - Sigma is an evolving open standard for writing rules and templates that automated management tools can use to parse log files. Where Sigma templates exist for our recommended search criteria, we've added a link to the Sigma repo. The Sigma templates aren't written, tested, and managed by Microsoft. Rather, the repo and templates are created and collected by the worldwide IT security community.
- [**Azure Monitor**](/en-us/azure/azure-monitor/overview) – enables automated monitoring and alerting of various conditions. Can create or use workbooks to combine data from different sources.
- [**Azure Event Hubs**](/en-us/azure/event-hubs/event-hubs-about)**integrated with a SIEM**- [Microsoft Entra logs can be integrated to other SIEMs](../identity/monitoring-health/howto-stream-logs-to-event-hub) such as Splunk, ArcSight, QRadar, and Sumo Logic via the Azure Event Hubs integration.
- [**Microsoft Defender for Cloud Apps**](/en-us/cloud-app-security/what-is-cloud-app-security) – enables you to discover and manage apps, govern across apps and resources, and check your cloud apps’ compliance.
- **[Securing workload identities with Microsoft Entra ID Protection](../id-protection/concept-workload-identity-risk)** - Used to detect risk on workload identities across sign-in behavior and offline indicators of compromise.

The rest of this article has recommendations to set a baseline to monitor and alert on, with a tier model. Links to pre-built solutions appear after the table. You can build alerts using the preceding tools. The content is organized into the following areas:

- Baselines
- Microsoft Entra role assignment
- Microsoft Entra role alert settings
- Azure resource role assignment
- Access management for Azure resources
- Elevated access to manage Azure subscriptions

## Baselines

The following are recommended baseline settings:

| What to monitor | Risk level | Recommendation | Roles | Notes |
| --- | --- | --- | --- | --- |
| Microsoft Entra roles assignment | High | Require justification for activation. Require approval to activate. Set two-level approver process. On activation, require Microsoft Entra multifactor authentication. Set maximum elevation duration to 8 hrs. | Security Administrator, Privileged Role Administrator, Global Administrator | A Privileged Role Administrator can customize PIM in their Microsoft Entra organization, including changing the experience for users activating an eligible role assignment. |
| Azure Resource Role Configuration | High | Require justification for activation. Require approval to activate. Set two-level approver process. On activation, require Microsoft Entra multifactor authentication. Set maximum elevation duration to 8 hrs. | Owner, User Access Administrator | Investigate immediately if not a planned change. This setting might enable attacker access to Azure subscriptions in your environment. |

## Privileged Identity Management Alerts

Privileged Identity Management (PIM) generates alerts when there's suspicious or unsafe activity in your Microsoft Entra organization. When an alert is generated, it appears in the Privileged Identity Management dashboard. You can also configure an email notification or send to your SIEM via GraphAPI. Because these alerts focus specifically on administrative roles, you should monitor closely for any alerts.

| What to monitor | Risk Level | Where | Filter/sub-filter UX | Notes |
| --- | --- | --- | --- | --- |
| [Roles are being assigned outside of Privileged Identity Management](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | High | Privileged Identity Management, Alerts | [Roles are being assigned outside of Privileged Identity Management](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | [How to configure security alerts](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| [Potential stale accounts in a privileged role](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | Medium | Privileged Identity Management, Alerts | [Potential stale accounts in a privileged role](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | [How to configure security alerts](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| [Administrators aren't using their privileged roles](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | Low | Privileged Identity Management, Alerts | [Administrators aren't using their privileged roles](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | [How to configure security alerts](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| [Roles don't require multifactor authentication for activation](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | Low | Privileged Identity Management, Alerts | [Roles don't require multifactor authentication for activation](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | [How to configure security alerts](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| [The organization doesn't have Microsoft Entra ID P2 or Microsoft Entra ID Governance](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | Low | Privileged Identity Management, Alerts | [The organization doesn't have Microsoft Entra ID P2 or Microsoft Entra ID Governance](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | [How to configure security alerts](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| [There are too many Global Administrators](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | Low | Privileged Identity Management, Alerts | [There are too many Global Administrators](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | [How to configure security alerts](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| [Roles are being activated too frequently](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | Low | Privileged Identity Management, Alerts | [Roles are being activated too frequently](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts) | [How to configure security alerts](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts#security-alerts)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

## Microsoft Entra roles assignment

A Privileged Role Administrator can customize PIM in their Microsoft Entra organization, which includes changing the user experience of activating an eligible role assignment:

- Prevent bad actor to remove Microsoft Entra multifactor authentication requirements to activate privileged access.
- Prevent malicious users bypass justification and approval of activating privileged access.

| What to monitor | Risk level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| Alert on Add changes to privileged account permissions | High | Microsoft Entra audit logs | Category = Role Management-and-Activity Type – Add eligible member (permanent) -and-Activity Type – Add eligible member (eligible) -and-Status = Success/failure-and-Modified properties = Role.DisplayName | Monitor and always alert for any changes to Privileged Role Administrator and Global Administrator. This can be an indication an attacker is trying to gain privilege to modify role assignment settings. If you don’t have a defined threshold, alert on 4 in 60 minutes for users and 2 in 60 minutes for privileged accounts.[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Alert on bulk deletion changes to privileged account permissions | High | Microsoft Entra audit logs | Category = Role Management-and-Activity Type – Remove eligible member (permanent) -and-Activity Type – Remove eligible member (eligible) -and-Status = Success/failure-and-Modified properties = Role.DisplayName | Investigate immediately if not a planned change. This setting could enable an attacker access to Azure subscriptions in your environment.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/BulkChangestoPrivilegedAccountPermissions.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Changes to PIM settings | High | Microsoft Entra audit log | Service = PIM-and-Category = Role Management-and-Activity Type = Update role setting in PIM-and-Status Reason = MFA on activation disabled (example) | Monitor and always alert for any changes to Privileged Role Administrator and Global Administrator. This can be an indication an attacker has access to modify role assignment settings. One of these actions could reduce the security of the PIM elevation and make it easier for attackers to acquire a privileged account.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/ChangestoPIMSettings.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Approvals and deny elevation | High | Microsoft Entra audit log | Service = Access Review-and-Category = UserManagement-and-Activity Type = Request Approved/Denied-and-Initiated actor = UPN | All elevations should be monitored. Log all elevations to give a clear indication of timeline for an attack.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/AuditLogs/PIMElevationRequestRejected.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |
| Alert setting changes to disabled. | High | Microsoft Entra audit logs | Service =PIM-and-Category = Role Management-and-Activity Type = Disable PIM Alert-and-Status = Success /Failure | Always alert. Helps detect bad actor removing alerts associated with Microsoft Entra multifactor authentication requirements to activate privileged access. Helps detect suspicious or unsafe activity.[Microsoft Sentinel template](https://github.com/Azure/Azure-Sentinel/blob/master/Detections/SecurityAlert/DetectPIMAlertDisablingActivity.yaml)[Sigma rules](https://github.com/SigmaHQ/sigma/tree/master/rules/cloud/azure) |

For more information on identifying role setting changes in the Microsoft Entra audit log, see [View audit history for Microsoft Entra roles in Privileged Identity Management](../id-governance/privileged-identity-management/pim-how-to-use-audit-log).

## Azure resource role assignment

Monitoring Azure resource role assignments allows visibility into activity and activations for resources roles. These assignments might be misused to create an attack surface to a resource. As you monitor for this type of activity, you're trying to detect:

- Query role assignments at specific resources
- Role assignments for all child resources
- All active and eligible role assignment changes

| What to monitor | Risk level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| Audit Alert Resource Audit log for Privileged account activities | High | In PIM, under Azure Resources, Resource Audit | Action: Add eligible member to role in PIM completed (time bound) -and-Primary Target -and-Type User-and-Status = Succeeded | Always alert. Helps detect bad actor adding eligible roles to manage all resources in Azure. |
| Audit Alert Resource Audit for Disable Alert | Medium | In PIM, under Azure Resources, Resource Audit | Action: Disable Alert-and-Primary Target: Too many owners assigned to a resource-and-Status = Succeeded | Helps detect bad actor disabling alerts, in the Alerts pane, which can bypass malicious activity being investigated |
| Audit Alert Resource Audit for Disable Alert | Medium | In PIM, under Azure Resources, Resource Audit | Action: Disable Alert-and-Primary Target: Too many permanent owners assigned to a resource-and-Status = Succeeded | Prevent bad actor from disable alerts, in the Alerts pane, which can bypass malicious activity being investigated |
| Audit Alert Resource Audit for Disable Alert | Medium | In PIM, under Azure Resources, Resource Audit | Action: Disable Alert-and-Primary Target Duplicate role created-and-Status = Succeeded | Prevent bad actor from disable alerts, from the Alerts pane, which can bypass malicious activity being investigated |

For more information on configuring alerts and auditing Azure resource roles, see:

- [Configure security alerts for Azure resource roles in Privileged Identity Management](../id-governance/privileged-identity-management/pim-resource-roles-configure-alerts)
- [View audit report for Azure resource roles in Privileged Identity Management (PIM)](../id-governance/privileged-identity-management/azure-pim-resource-rbac)

## Access management for Azure resources and subscriptions

Users or group members assigned the Owner or User Access Administrator subscriptions roles, and Microsoft Entra Global Administrators who enabled subscription management in Microsoft Entra ID, have Resource Administrator permissions by default. The administrators assign roles, configure role settings, and review access using Privileged Identity Management (PIM) for Azure resources.

A user who has Resource administrator permissions can manage PIM for Resources. Monitor for and mitigate this introduced risk: the capability can be used to allow bad actors privileged access to Azure subscription resources, such as virtual machines (VMs) or storage accounts.

| What to monitor | Risk level | Where | Filter/sub-filter | Notes |
| --- | --- | --- | --- | --- |
| Elevations | High | Microsoft Entra ID, under Manage, Properties | Periodically review setting.Access management for Azure resources | Global Administrators can elevate by enabling Access management for Azure resources.Verify bad actors haven't gained permissions to assign roles in all Azure subscriptions and management groups associated with Active Directory. |

For more information, see [Assign Azure resource roles in Privileged Identity Management](../id-governance/privileged-identity-management/pim-resource-roles-assign-roles)