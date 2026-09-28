---
layout: Conceptual
title: Configure CMMC Level 1 controls - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/configure-cmmc-level-1-controls
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Learn how to configure Microsoft Entra identities to meet CMMC Level 1 requirements.
ms.service: entra
ms.subservice: standards
ms.topic: concept-article
ms.date: 2023-01-03T00:00:00.0000000Z
author: janicericketts
ms.author: jricketts
ms.reviewer: jricketts
ms.custom: it-pro
locale: en-us
document_id: d7899c85-e10f-8a99-6000-16d6d2918024
document_version_independent_id: 594494c7-56c6-4d6d-6a52-3ef0fd039b93
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/configure-cmmc-level-1-controls.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/configure-cmmc-level-1-controls
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/configure-cmmc-level-1-controls.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 95937850-c5f8-35f5-db56-68b1188a0d69
---

# Configure CMMC Level 1 controls - Microsoft Entra | Microsoft Learn

Microsoft Entra ID meets identity-related practice requirements in each Cybersecurity Maturity Model Certification (CMMC) level. To be compliant with requirements in CMMC, it's the responsibility of companies performing work with, and on behalf of, the US Dept. of Defense (DoD) to complete other configurations or processes. In CMMC Level 1, there are three domains that have one or more practices related to identity:

- Access Control (AC)
- Identification and Authentication (IA)
- System and Information integrity (SI)

Learn more:

- DoD CMMC website - [Cybersecurity Maturity Model Certification Overview](https://dodcio.defense.gov/CMMC/about/)
- Microsoft Download Center - [Microsoft Product Placemat for CMMC Level 3 (preview)](https://www.microsoft.com/download/details.aspx?id=102536)

The remainder of this content is organized by domain and associated practices. For each domain, there's a table with links to content that provides step-by-step guidance to accomplish the practice.

## Access Control domain

The following table provides a list of practice statement and objectives, and Microsoft Entra guidance and recommendations to enable you to meet these requirements with Microsoft Entra ID.

| CMMC practice statement and objectives | Microsoft Entra guidance and recommendations |
| --- | --- |
| AC.L1-3.1.1**Practice statement:** Limit information system access to authorized users, processes acting on behalf of authorized users, or devices (including other information systems).**Objectives:**Determine if:[a.] authorized users are identified;[b.] processes acting on behalf of authorized users are identified;[c.] devices (and other systems) authorized to connect to the system are identified;[d.] system access is limited to authorized users;[e.] system access is limited to processes acting on behalf of authorized users; and[f.] system access is limited to authorized devices (including other systems). | You're responsible for setting up Microsoft Entra accounts, which is accomplished from external HR systems, on-premises Active Directory, or directly in the cloud. You configure Conditional Access to only grant access from a known (Registered/Managed) device. In addition, apply the concept of least privilege when granting application permissions. Where possible, use delegated permission. Set up users- [Plan cloud HR application to Microsoft Entra user provisioning](../identity/app-provisioning/plan-cloud-hr-provision)<br>- [Microsoft Entra Connect Sync: Understand and customize synchronization](../identity/hybrid/connect/how-to-connect-sync-whatis)<br>- [Add or delete users – Microsoft Entra ID](../fundamentals/how-to-create-delete-users)Set up devices<br>- [What is device identity in Microsoft Entra ID](../identity/devices/overview)Configure applications<br>- [QuickStart: Register an app in the Microsoft identity platform](../identity-platform/quickstart-register-app)<br>- [Microsoft identity platform scopes, permissions, & consent](../identity-platform/permissions-consent-overview)<br>- [Securing service principals in Microsoft Entra ID](../architecture/service-accounts-principal)Conditional Access<br>- [What is Conditional Access in Microsoft Entra ID](../identity/conditional-access/overview)<br>- [Conditional Access require managed device](../identity/conditional-access/concept-conditional-access-grant) |
| AC.L1-3.1.2**Practice statement:** Limit information system access to the types of transactions and functions that authorized users are permitted to execute.**Objectives:**Determine if:[a.] the types of transactions and functions that authorized users are permitted to execute are defined; and[b.] system access is limited to the defined types of transactions and functions for authorized users. | You're responsible for configuring access controls such as Role Based Access Controls (RBAC) with built-in or custom roles. Use role assignable groups to manage role assignments for multiple users requiring same access. Configure Attribute Based Access Controls (ABAC) with default or custom security attributes. The objective is to granularly control access to resources protected with Microsoft Entra ID.Set up RBAC- [Overview of role-based access control in Active Directory](../identity/role-based-access-control/custom-overview)[Microsoft Entra built-in roles](../identity/role-based-access-control/permissions-reference)<br>- [Create a custom role in Microsoft Entra ID](../identity/role-based-access-control/custom-create)Set up ABAC<br>- [What is Azure attribute-based access control (Azure ABAC)](/en-us/azure/role-based-access-control/conditions-overview)<br>- [What are custom security attributes in Microsoft Entra ID?](../fundamentals/custom-security-attributes-overview)Configure groups for role assignment<br>- [Use Microsoft Entra groups to manage role assignments](../identity/role-based-access-control/groups-concept) |
| AC.L1-3.1.20**Practice statement:** Verify and control/limit connections to and use of external information systems.**Objectives:**Determine if:[a.] connections to external systems are identified;[b.] the use of external systems is identified;[c.] connections to external systems are verified;[d.] the use of external systems is verified;[e.] connections to external systems are controlled and or limited; and[f.] the use of external systems is controlled and or limited. | You're responsible for configuring Conditional Access policies using device controls and or network locations to control and or limit connections and use of external systems. Configure Terms of Use (TOU) for recorded user acknowledgment of terms and conditions for use of external systems for access.Set up Conditional Access as required- [What is Conditional Access?](../identity/conditional-access/overview)<br>- [Require managed devices for cloud app access with Conditional Access](../identity/conditional-access/concept-conditional-access-grant)<br>- [Require device to be marked as compliant](../identity/conditional-access/concept-conditional-access-grant)<br>- [Conditional Access: Filter for devices](../identity/conditional-access/concept-condition-filters-for-devices)Use Conditional Access to block access<br>- [Conditional Access - Block access by location](../identity/conditional-access/policy-block-by-location)Configure terms of use<br>- [Terms of use](../identity/conditional-access/terms-of-use)<br>- [Conditional Access require terms of use](../identity/conditional-access/policy-all-users-require-terms-of-use) |
| AC.L1-3.1.22**Practice statement:** Control information posted or processed on publicly accessible information systems.**Objectives:**Determine if:[a.] individuals authorized to post or process information on publicly accessible systems are identified;[b.] procedures to ensure FCI isn't posted or processed on publicly accessible systems are identified;[c.] a review process is in place prior to posting of any content to publicly accessible systems; and[d.] content on publicly accessible systems is reviewed to ensure that it doesn't include federal contract information (FCI). | You're responsible for configuring Privileged Identity Management (PIM) to manage access to systems where posted information is publicly accessible. Require approvals with justification prior to role assignment in PIM. Configure Terms of Use (TOU) for systems where posted information is publicly accessible for recorded acknowledgment of terms and conditions for posting of publicly accessible information.Plan PIM deployment- [What is Privileged Identity Management?](../id-governance/privileged-identity-management/pim-configure)<br>- [Plan a Privileged Identity Management deployment](../id-governance/privileged-identity-management/pim-deployment-plan)Configure terms of use<br>- [Terms of use](../identity/conditional-access/terms-of-use)<br>- [Conditional Access require terms of use](../identity/conditional-access/policy-all-users-require-terms-of-use)<br>- [Configure Microsoft Entra role settings in PIM - Require Justification](../id-governance/privileged-identity-management/pim-how-to-change-default-settings) |

## Identification and Authentication (IA) domain

The following table provides a list of practice statement and objectives, and Microsoft Entra guidance and recommendations to enable you to meet these requirements with Microsoft Entra ID.

| CMMC practice statement and objectives | Microsoft Entra guidance and recommendations |
| --- | --- |
| IA.L1-3.5.1**Practice statement:** Identify information system users, processes acting on behalf of users, or devices.**Objectives:**Determine if:[a.] system users are identified;[b.] processes acting on behalf of users are identified; and[c.] devices accessing the system are identified. | Microsoft Entra ID uniquely identifies users, processes (service principal/workload identities), and devices via the ID property on the respective directory objects. You can filter log files to help with your assessment using the following links. Use the following reference to meet assessment objectives.Filtering logs by user properties- [User resource type: ID Property](/en-us/graph/api/resources/user?view=graph-rest-1.0&amp;preserve-view=true)Filtering logs by service properties<br>- [ServicePrincipal resource type: ID Property](/en-us/graph/api/resources/serviceprincipal?view=graph-rest-1.0&amp;preserve-view=true)Filtering logs by device properties<br>- [Device resource type: ID Property](/en-us/graph/api/resources/device?view=graph-rest-1.0&amp;preserve-view=true) |
| IA.L1-3.5.2**Practice statement:** Authenticate (or verify) the identities of those users, processes, or devices, as a prerequisite to allowing access to organizational information systems.**Objectives:**Determine if:[a.] the identity of each user is authenticated or verified as a prerequisite to system access;[b.] the identity of each process acting on behalf of a user is authenticated or verified as a prerequisite to system access; and[c.] the identity of each device accessing or connecting to the system is authenticated or verified as a prerequisite to system access. | Microsoft Entra ID uniquely authenticates or verifies each user, process acting on behalf of user, or device as a prerequisite to system access. Use the following reference to meet assessment objectives.Set up user accounts- [What is Microsoft Entra authentication?](../identity/authentication/overview-authentication)[Configure Microsoft Entra ID to meet NIST authenticator assurance levels](nist-overview)Set up service principal accounts<br>- [Service principal authentication](../architecture/service-accounts-principal)Set up device accounts<br>- [What is a device identity?](../identity/devices/overview)<br>- [How it works: Device registration](../identity/devices/device-registration-how-it-works)<br>- [What is a Primary Refresh Token?](../identity/devices/concept-primary-refresh-token)<br>- What does the PRT contain |

## System and Information Integrity (SI) domain

The following table provides a list of practice statement and objectives, and Microsoft Entra guidance and recommendations to enable you to meet these requirements with Microsoft Entra ID.

| CMMC practice statement | Microsoft Entra guidance and recommendations |
| --- | --- |
| SI.L1-3.14.1 - Identify, report, and correct information and information system flaws in a timely manner.SI.L1-3.14.2 - Provide protection from malicious code at appropriate locations in organizational information systems.SI.L1-3.14.4 - Update malicious code protection mechanisms when new releases are available.SI.L1-3.14.5 - Perform periodic scans of the information system and real-time scans of files from external sources as files are downloaded, opened, or executed. | **Consolidated Guidance for legacy managed devices**Configure Conditional Access to require Microsoft Entra hybrid joined device. For devices joined to an on-premises AD, it's assumed that the control over these devices is enforced using management solutions such as Configuration Manager or group policy (GP). Because there's no method for Microsoft Entra ID to determine whether any of these methods has been applied to a device, requiring a Microsoft Entra hybrid joined device is a relatively weak mechanism to require a managed device. The administrator judges whether the methods applied to your on-premises domain-joined devices are strong enough to constitute a managed device, if the device is also a Microsoft Entra hybrid joined device.**Consolidated guidance for cloud-managed (or co-management) devices**Configure Conditional Access to require a device to be marked as compliant, the strongest form to request a managed device. This option requires device registration with Microsoft Entra ID, and indicated as compliant by Intune or a third-party mobile device management (MDM) system that manages Windows 10 devices via Microsoft Entra integration. |

### Next steps

- [Configure Microsoft Entra ID for CMMC compliance](configure-for-cmmc-compliance)
- [Configure CMMC Level 2 Access Control (AC) controls](configure-cmmc-level-2-access-control)
- [Configure CMMC Level 2 Identification and Authentication (IA) controls](configure-cmmc-level-2-identification-and-authentication)
- [Configure CMMC Level 2 additional controls](configure-cmmc-level-2-additional-controls)