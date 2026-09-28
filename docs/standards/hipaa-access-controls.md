---
layout: Conceptual
title: Configure Microsoft Entra HIPAA access control safeguards - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/hipaa-access-controls
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Guidance on how to configure Microsoft Entra HIPAA access control safeguards
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, jricketts
ms.date: 2023-04-13T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 771cb845-292d-64d9-60b0-6cb3a4463cc3
document_version_independent_id: ff91e0c3-1b53-62a2-e732-a6088772045a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/hipaa-access-controls.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/hipaa-access-controls
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/hipaa-access-controls.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 60160d65-0832-4b93-c497-bd95bba3d2fa
---

# Configure Microsoft Entra HIPAA access control safeguards - Microsoft Entra | Microsoft Learn

Microsoft Entra ID meets identity-related practice requirements for implementing Health Insurance Portability and Accountability Act of 1996 (HIPAA) safeguards. To be HIPAA compliant, implement the safeguards using this guidance. You might need to modify other configurations or processes.

To understand the **User Identification Safeguard**, we recommend you research and set objectives that enable you to:

- Ensure IDs are unique to everyone that needs to connect to the domain.
- Establish a Joiner, Mover, and Leaver (JML) process.
- Enabler auditing for identity tracking.

For the **Authorized Access Control Safeguard**, set objectives so that:

- System access is limited to authorized users.
- Authorized users are identified.
- Access to personal data is limited to authorized users.

For the **Emergency Access Procedure Safeguard**:

- Ensure high availability of core services.
- Eliminate single points of failure.
- Establish a disaster recovery plan.
- Ensure backups of high-risk data.
- Establish and maintain emergency access accounts.

For the **Automatic Logoff Safeguard**:

- Establish a procedure that terminates an electronic session after a predetermined time of inactivity.
- Configure and implement an automatic sign out policy.

## Unique user identification

The following table has access control safeguards from the HIPAA guidance for unique user identification. Find Microsoft recommendations to meet safeguard implementation requirements.

**HIPAA safeguard - unique user identification**

`Assign a unique name and/or number for identifying and tracking user identity.`

| Recommendation | Action |
| --- | --- |
| Set up hybrid to utilize Microsoft Entra ID | [Microsoft Entra Connect](../identity/hybrid/connect/how-to-connect-install-express) integrates on-premises directories with Microsoft Entra ID, supporting the use of single identities to access on-premises applications and cloud services such as Microsoft 365. It orchestrates synchronization between Active Directory (AD) and Microsoft Entra ID. To get started with Microsoft Entra Connect review the prerequisites, making note of the server requirements and how to prepare your Microsoft Entra tenant for management.[Microsoft Entra Connect sync](/en-us/azure/active-directory/cloud-sync/tutorial-pilot-aadc-aadccp) is a provisioning agent that is managed on the cloud. The provisioning agent supports synchronizing to Microsoft Entra ID from a multi-forest disconnected AD environment. Lightweight agents are installed and can be used with Microsoft Entra Connect.We recommend you use **Password Hash Sync** to help reduce the number of passwords and protect against leaked credential detection. |
| Provision user accounts | [Microsoft Entra ID](../fundamentals/how-to-create-delete-users) is a cloud-based identity and access management service that provides single sign-on, multi-factor authentication and Conditional Access to guard against security attacks. To create a user account, sign in into the Microsoft Entra admin center as a **User Admin** and create a new account by navigating to [All users](../fundamentals/how-to-create-delete-users) in the menu.  Microsoft Entra ID provides support for automated user provisioning for systems and applications. Capabilities include creating, updating, and deleting a user account. Automated provisioning creates new accounts in the right systems for new people when they join a team in an organization, and automated deprovisioning deactivates accounts when people leave the team. Configure provisioning by navigating to the Microsoft Entra admin center and selecting [enterprise applications](../identity/app-provisioning/configure-automatic-user-provisioning-portal) to add and manage the app settings. |
| HR-driven provisioning | [Integrating Microsoft Entra account provisioning](../identity/app-provisioning/plan-cloud-hr-provision) within a Human Resources (HR) system reduces the risk of excessive access and access no longer required. The HR system becomes the start-of-authority, for newly created accounts, extending the capabilities to account deprovisioning. Automation manages the identity lifecycle and reduces the risk of over-provisioning. This approach follows the security best practice of providing least privilege access. |
| Create lifecycle workflows | [Lifecycle workflows](../id-governance/understanding-lifecycle-workflows) provide identity governance for automating the joiner/mover/leaver (JML) lifecycle. Lifecycle workflows centralize the workflow process by either using the [built-in templates](../id-governance/lifecycle-workflow-templates) or creating your own custom workflows. this practice helps reduce or potentially remove manual tasks for organizational JML strategy requirements. Within the Azure portal, navigate to **ID Governance** in the Microsoft Entra menu to review or configure tasks that fit within your organizational requirements. |
| Manage privileged identities | [Microsoft Entra Privileged Identity Management (PIM)](../id-governance/privileged-identity-management/pim-configure) enables management, control, and the ability to monitor access. You provide access when it's needed, on a time-based and approval-based role activation. This approach limits the risk of excessive, unnecessary, or misused access permissions. |
| Monitoring and alerting | [Microsoft Entra ID Protection](../id-protection/overview-identity-protection) provides a consolidated view into risk events and potential vulnerabilities that could affect an organization’s identities. Enabling the protection applies the existing Microsoft Entra anomaly detection capabilities and introduces risk event types that detect anomalies in real-time. Through the Microsoft Entra admin center, you can sign-in, audit, and review provisioning logs.The logs can be [downloaded, archived, and streamed](../identity/monitoring-health/howto-download-logs) to your security information and event management (SIEM) tool. Microsoft Entra logs can be located in the monitoring section of the Microsoft Entra menu. The logs can also be sent to [Azure Monitor](../identity/monitoring-health/concept-log-monitoring-integration-options-considerations) using an Azure log analytics workspace where you can set up alerting on the connected data.  Microsoft Entra ID uniquely identifies users via the [ID property](/en-us/graph/api/resources/user?view=graph-rest-1.0&amp;preserve-view=true) on the respective directory object. This approach enables you to filter for specific identities in the log files. |

## Authorized access control

The following table has HIPAA guidance for access control safeguards for authorized access control. Find Microsoft recommendations to meet safeguard implementation requirements.

**HIPAA safeguard - authorized access control**

`Person or entity authentication, implement procedures to verify that a person or entity seeking access to electronic protected health information is the one claimed.`

| Recommendation | Action |
| --- | --- |
| Enable multi-factor authentication (MFA) | [MFA in Microsoft Entra ID](../identity/authentication/concept-mfa-howitworks) protects identities by adding another layer of security. The extra layer authentication is effective in helping prevent unauthorized access. Using an MFA approach enables you to require more validation of sign in credentials during the authentication process. Examples include setting up the [Authenticator app](https://support.microsoft.com/account-billing/set-up-an-authenticator-app-as-a-two-step-verification-method-2db39828-15e1-4614-b825-6e2b524e7c95) for one-click verification, or enabling [passwordless authentication](../identity/authentication/concept-authentication-passkeys-fido2). |
| Enable Conditional Access policies | [Conditional Access](../identity/conditional-access/concept-conditional-access-policies) policies help organizations restrict access to approved applications. Microsoft Entra analyses signals from either the user, device, or the location to automate decisions and enforce organizational policies for access to resources and data. |
| Enable role-based access control (RBAC) | [RBAC](../identity/role-based-access-control/custom-overview) provides security on an enterprise level with the concept of separation of duties. RBAC enables you to adjust and review permissions to protect confidentiality, privacy and access management to resources and sensitive data along with the systems.Microsoft Entra ID provides support for [built-in roles](../identity/role-based-access-control/permissions-reference), which is a fixed set of permissions that can't be modified. You can also create your own [custom roles](../identity/role-based-access-control/custom-create) where you can add a preset list. |
| Enable attribute-based access control (ABAC) | [ABAC](/en-us/azure/role-based-access-control/conditions-overview) defines access based on attributes associated with security principles, resources, and environment. It provides fine-grained access control and reduces the number of role assignments. The use of ABAC can be scoped to the content within the dedicated Azure storage. |
| Configure user groups access in SharePoint | [SharePoint groups](/en-us/sharepoint/dev/general-development/authorization-users-groups-and-the-object-model-in-sharepoint) are a collection of users. The permissions are scoped to the site collection level for access to the content. Application of this constraint can be scoped to service accounts that require data flow access between applications. |

## Emergency access procedure

The following table has HIPAA guidance access control safeguards for emergency access procedures. Find Microsoft recommendations to meet safeguard implementation requirements.

**HIPAA safeguard - emergency access procedure**

`Establish (and implement as needed) procedures and policies for obtaining necessary electronic protected health information during an emergency or occurrence.`

| Recommendation | Action |
| --- | --- |
| Use Azure Recovery Services | [Azure Backups](/en-us/azure/backup/backup-architecture) provide the support required to back up vital and sensitive data. Coverage includes storage/databases and cloud infrastructure, along with on-premises windows devices to the cloud. Establish [backup policies](/en-us/azure/backup/backup-architecture#backup-policy-essentials) to address backup and recovery process risks. Ensure data is safely stored and can be retrieved with minimal downtime. Azure Site Recovery provides near-constant data replication to ensure copies of are in sync. Initial steps prior to setting up the service are to determine the recovery point objective (RPO) and recovery time objective (RTO) to support your organizational requirements. |
| Ensure resiliency | [Resiliency](/en-us/azure/architecture/framework/resiliency/overview) helps to maintain service levels when there's disruption to business operations and core IT services. The capability spans services, data, Microsoft Entra ID, and Active Directory considerations. Determining a strategic [resiliency plan](/en-us/azure/architecture/checklist/resiliency-per-service) to include what systems and data rely on Microsoft Entra and hybrid environments. [Microsoft 365 resiliency](/en-us/compliance/assurance/assurance-sharepoint-onedrive-data-resiliency) covering the core services, which include Exchange, SharePoint, and OneDrive to protect against data corruption and applying resiliency data points to protect ePHI content. |
| Create break glass accounts | Establishing an emergency or a [break glass account](../identity/role-based-access-control/security-emergency-access) ensures that system and services can still be accessed in unforeseen circumstances, such as network failures or other reasons for administrative access loss. We recommend you don't associate this account with an [individual user](../identity/authentication/concept-authentication-passkeys-fido2) or account. |

## Workstation security - automatic logoff

The following table has HIPAA guidance on the automatic logoff safeguard. Find Microsoft recommendations to meet safeguard implementation requirements.

**HIPAA safeguard - automatic logoff**

`Implement electronic procedures that terminate an electronic session after a predetermined time of inactivity.| Create a policy and procedure to determine the length of time that a user is allowed to stay logged on, after a predetermined period of inactivity.`

| Recommendation | Action |
| --- | --- |
| Create group policy | Support for devices not migrated to Microsoft Entra ID and managed by Intune, [Group Policy (GPO)](/en-us/entra/identity/domain-services/manage-group-policy) can enforce sign out, or lock screen time for devices on AD, or in hybrid environments. |
| Assess device management requirements | [Microsoft Intune](/en-us/mem/intune/fundamentals/what-is-intune) provides mobile device management (MDM) and mobile application management (MAM). It provides control over company and personal devices. You can manage device usage and enforce policies to control mobile applications. |
| Device Conditional Access policy | Implement device lock by using a Conditional Access policy to restrict access to [compliant](../identity/conditional-access/concept-conditional-access-grant) or Microsoft Entra hybrid joined devices. Configure [policy settings](../identity/conditional-access/concept-conditional-access-grant#require-hybrid-azure-ad-joined-device).For unmanaged devices, configure the [Sign-In Frequency](../identity/conditional-access/howto-conditional-access-session-lifetime) setting to force users to reauthenticate. |
| Configure session time out for Microsoft 365 | Review the [session timeouts](/en-us/microsoft-365/admin/manage/idle-session-timeout-web-apps) for Microsoft 365 applications and services, to amend any prolonged timeouts. |
| Configure session time out for Azure portal | Review the [session timeouts for Azure portal session](/en-us/azure/azure-portal/set-preferences), by implementing a timeout due to inactivity it helps to protect resources from unauthorized access. |
| Review application access sessions | [Continuous access evaluation](../identity/conditional-access/concept-continuous-access-evaluation) policies can deny or grant access to applications. If the sign-in is successful, the user is given an access token that is valid for one (1) hour. Once the access token expires the client is directed back to Microsoft Entra ID, conditions are reevaluated, and the token is refreshed for another hour. |

## Learn more

- [Zero Trust Pillar: Identity, Devices](/en-us/security/zero-trust/zero-trust-overview)
- [Zero Trust Pillar: Identity, Data](/en-us/security/zero-trust/zero-trust-overview)
- [Zero Trust Pillar: Devices, Identity, Application](/en-us/security/zero-trust/zero-trust-overview)