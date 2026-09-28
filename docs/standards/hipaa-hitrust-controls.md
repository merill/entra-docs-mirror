---
layout: Conceptual
title: Microsoft Entra configuration recommendations for HITRUST controls - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/hipaa-hitrust-controls
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Guidance on navigating details and recommendations for services and features to align with HITRUST controls
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, jricketts
ms.date: 2024-03-19T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 01889989-c35a-3da8-2fcb-af0656c9a6ee
document_version_independent_id: 01889989-c35a-3da8-2fcb-af0656c9a6ee
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/hipaa-hitrust-controls.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/hipaa-hitrust-controls
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/hipaa-hitrust-controls.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/0661002d-4d3e-4257-b5a8-1276befa15d4
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/05df39fb-4203-4146-99d8-5ff1e833520c
platformId: c7e2c585-04d8-373a-5a12-cb239ad8bb87
---

# Microsoft Entra configuration recommendations for HITRUST controls - Microsoft Entra | Microsoft Learn

This article’s guidance helps you navigate details and provides recommendations of services and features in Microsoft Entra ID to support alignment with HITRUST controls. Use the information to help understand the Health Information Trust Alliance (HITRUST) framework, and support your responsibility of ensuring your organization is compliant with the Health Insurance Portability and Accountability Act of 1996 (HIPAA). Assessments involve working with certified HITRUST assessors who are knowledgeable about the framework and are required to help guide you through the process and understand the requirements.

**Acronyms**

The following table lists the acronyms and their spelling in this article.

| Acronym | Spelling |
| --- | --- |
| CE | Covered Entity |
| CSF | Common Security Framework |
| HIPAA | Health Insurance Portability and Accountability Act of 1996 |
| HSR | HIPAA Security Rule |
| HITRUST | Health Information Trust Alliance |
| IAM | Identity and access management |
| IdP | Identity provider |
| ISO | International Organization for Standardization |
| ISMS | Information security management system |
| JEA | Just enough access |
| JML | Join, move, leave |
| MFA | Microsoft Entra multifactor authentication |
| NIST | National Institute of Standards and Technology, US Dept. of Commerce |
| PHI | Protected health information |
| PIM | Privileged Identity Management |
| SSO | Single sign-on |
| TAP | Temporary access pass |

## Health Information Trust Alliance

The HITRUST organization established the Common Security Framework (CSF) to standardize and streamline security and privacy requirements for organizations in the healthcare industry. HITRUST CSF was founded in 2007 to address the complex regulatory environment, security challenges, and privacy concerns that organizations face when handling personal data and protected health information (PHI) data. The CSF consists of 14 control categories comprising 49 control objectives, and 156 control specifics. It was built on the primary principles of International Organization for Standardization (ISO) 27001 and ISO 27002.

The HITRUST MyCSF tool is available in [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/hitrust1666274640786.hitrust?exp=ubp8&amp;tab=Overview). Use it to manage information security risks, data governance, to comply with information protection regulations, also adhere to national and international standards and best practices.

Note

ISO 27001 is a management standard that specifies the requirements for an information security management system (ISMS). ISO 27002 is a set of best practices to select and implement security controls in the ISO 27001 framework.

## HIPAA Security Rule

The [HIPAA Security Rule (HSR)](https://www.hhs.gov/hipaa/for-professionals/security/index.html#:%7E:text=The%20HIPAA%20Security%20Rule%20establishes,maintained%20by%20a%20covered%20entity.) establishes standards to protect an individual’s electronic personal health information created, received, used, or maintained by a Covered Entity (CE), which is a health plan, health care clearinghouse, or healthcare provider. The U.S. Department of Health and Human Services (HHS) manages the HSR. HHS requires administrative, physical, and technical safeguards to ensure the confidentiality, integrity, and security of electronic PHI.

## HITRUST and HIPAA

HITRUST developed the CSF, which includes security and privacy standards to support healthcare regulations. CSF controls and best practices simplify the task of consolidating sources to ensure compliance with federal legislation, HIPAA security, and privacy rules. HITRUST CSF is a certifiable security and privacy framework with controls and requirements to demonstrate HIPAA compliance. Healthcare organizations widely adopted the framework. Use the following table to learn about controls.

| Control category | Control category name |
| --- | --- |
| 0 | Information Security Management Program |
| 1 | Access Control |
| 2 | Human Resource Security |
| 3 | Risk Management |
| 4 | Security Policy |
| 5 | Organization of Information Security |
| 6 | Compliance |
| 7 | Asset Management |
| 8 | Physical and Environmental Security |
| 9 | Communications and Operations Management |
| 10 | Information Systems Acquisition, Development and Maintenance |
| 11 | Information Security Incident Management |
| 12 | Business Continuity Management |
| 13 | Privacy Practices |

Learn more on [Microsoft Azure platform is HITRUST CSF certified](https://azure.microsoft.com/blog/microsoft-azure-achieves-hitrust-csf-certification/), which includes identity and access management:

- [Microsoft Entra ID](../fundamentals/what-is-entra), formerly known as Azure Active Directory
- Rights management with [Microsoft Purview](https://techcommunity.microsoft.com/t5/healthcare-and-life-sciences/microsoft-purview-compliance-score-part-3-hitrust/ba-p/3614103)
- [Microsoft Entra multifactor authentication (MFA)](../identity/authentication/concept-mfa-howitworks)

## Access control categories and recommendations

The following table has the access control category for identity and access management (IAM), and Microsoft Entra recommendations to help meet the control category requirements. Details are from the HITRUST [MyCSF v11](https://hitrustalliance.net/mycsf), which refers to the HIPAA security rule, added to the corresponding control.

| HITRUST control, objective, and HSR | Microsoft Entra guidance and recommendation |
| --- | --- |
| **CSF Control V11**01.b User Registration**Control category**Access Control – User Registration and De-Registration**Control specification**The organization uses a formal user registration and deregistration process to enable assignment of access rights.**Objective name**Authorized Access to Information Systems**HIPAA Security Rule**§ 164.308(a)(3)(ii)(A)§ 164.308(a)(4)(i)§ 164.308(a)(3)(ii)(B)§ 164.308(a)(4)(ii)(C)§ 164.308(a)(4)(ii)(B)§ 164.308(a)(5)(ii)(D)§ 164.312(a)(2)(i)§ 164.312(a)(2)(ii)§ 164.312(d) | [Microsoft Entra ID](../fundamentals/what-is-entra) is an identity platform for verification, [authentication](../identity/authentication/overview-authentication), and credential management when an identity signs in to their device, application, or server. It’s a cloud-based identity and access management service with single sign-on (SSO), MFA, and [Conditional Access](../identity/conditional-access/overview) to guard against security attacks. Authentication ensures only authorized identities gain access to resources and data.[Lifecycle workflows](../id-governance/understanding-lifecycle-workflows) enable identity governance to automate the joiner, mover, leaver (JML) lifecycle. It centralizes the workflow process by using the built-in templates or you create custom workflows. This practice helps reduce, or potentially remove, manual tasks for organizational JML strategy requirements. On the Azure portal, navigate to **ID Governance** in the Microsoft Entra ID menu to review or configure tasks for your organizational requirements.[Microsoft Entra Connect](../identity/hybrid/connect/how-to-connect-install-roadmap) integrates on-premises directories with Microsoft Entra ID, supporting the use of single identities to access on-premises applications and cloud services such as Microsoft 365. It orchestrates synchronization between Active Directory (AD) and Microsoft Entra ID. To get started with Microsoft Entra Connect, review the prerequisites. Note the server requirements and how to prepare your Microsoft Entra tenant for management.[Microsoft Entra Connect Sync](../identity/hybrid/cloud-sync/tutorial-pilot-aadc-aadccp) is a provisioning agent managed on the cloud, which supports synchronization to Microsoft Entra ID from a multi-forest disconnected AD environment. Use the lightweight agents with Microsoft Entra Connect. We recommend password hash sync to help reduce the number of passwords and protect against leaked credential detection. |
| **CSF Control V11**01.c Privilege Management**Control category**Access Control – Privileged Accounts**Control specification**The organization ensures authorized user accounts are registered, tracked, and periodically validated to prevent unauthorized access to information systems**Objective name**Authorized Access to Information Systems**HIPAA Security Rule**§ 164.308(a)(1)(i)§ 164.308(a)(1)(ii)(B)§ 164.308(a)(2)§ 164.308(a)(3)(ii)(B)§ 164.308(a)(3)(ii)(A)§ 164.308(a)(4)(i)§ 164.308(a)(4)(ii)(B)§ 164.308(a)(4)(ii)(C)§ 164.310(a)(2)(ii)§ 164.310(a)(1)§ 164.310(a)(2)(iii)§ 164.312(a)(1) | [Privileged Identity Management (PIM)](../id-governance/privileged-identity-management/pim-configure) is a service in Microsoft Entra ID to manage, control and monitor access to important resources in an organization. It minimizes the number of people with access to secure information to help prevent malicious actors from getting access.PIM has time and approval-based access, to mitigate the risks of excessive, unnecessary, or misused access permissions. It helps identify and analyze privileged accounts to ensure you provide just enough access (JEA) for a user to perform their role.[Monitoring and generating alerts](../id-governance/privileged-identity-management/pim-how-to-configure-security-alerts) prevent suspicious activities, listing the users and roles that trigger the alert, while reducing the risk of unauthorized access. Customize alerts for your organizational security strategy.[Access reviews](../id-governance/access-reviews-overview) enable organizations to manage role assignments and group membership efficiently. Maintain security and compliance by evaluating which accounts have access and ensure access is revoked when needed, thus minimizing the risks from excessive or outdated permissions. |
| **CSF Control V11**0.1d User Password Management**Control category**Access Control - Procedures**Control specification**To ensure authorized user accounts are registered, tracked, and periodically validated to prevent unauthorized access to information systems.**Objective name**Authorized Access to Information Systems**HIPAA Security Rule**§164.308(a)(5)(ii)(D) | [Password management](/en-us/azure/security/fundamentals/identity-management-best-practices) is a critical aspect of security infrastructure. Align with best practices to create a robust security posture, Microsoft Entra ID helps facilitate with a comprehensive strategy support: [SSO](../identity/enterprise-apps/add-application-portal-setup-sso) and [MFA](../identity/authentication/concept-mfa-howitworks) also [passwordless authentication](../identity/authentication/concept-authentication-passkeys-fido2), such as FIDO2 security keys and Windows Hello for Business (WHfB) mitigate user risk and streamline the user authentication experience.Microsoft Entra Password Protection detects, and blocks, known weak passwords. It incorporates password [policies](../identity/authentication/tutorial-configure-custom-password-protection) and has the flexibility to define a custom password list and build a password management strategy to safeguard password use.HITRUST password length and strength requirements align with the National Institute of Standards and Technology [NIST 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html), which includes a minimum of eight characters for a password, or 15 characters for accounts with the most privileged access. Complexity measures include at least one number and/or special character and at least one upper- and lower-case letter for privileged accounts. |
| **CSF Control V11**01.p Secure Log-on Procedures**Control category**Access Control – Secure Logon**Control specification**The organization controls access to information assets using a secure logon procedure.**Objective name**Operating System Access Control**HIPAA Security Rule**§ 164.308(a)(5)(i)§ 164.308(a)(5)(ii)(C)§ 164.308(a)(5)(ii)(D) | Secure sign-in is the process to authenticate an identity securely when they attempt to access a system.**The control focuses on the [operating system](/en-us/azure/governance/policy/samples/hipaa-hitrust-9-2), Microsoft Entra services help strengthen the secure sign in.**[Conditional Access](../identity/conditional-access/overview) policies help organizations restrict access to approved applications, resources, and ensure devices are secure. Microsoft Entra ID analyzes the signals from Conditional Access [policies](../identity/conditional-access/concept-conditional-access-policies) from the identity, location, or device to automate the decision and enforce organizational policies for access to resources and data.[Role-based access control (RBAC)](../identity/role-based-access-control/custom-overview) helps you manage access and managed resources in your organization. RBAC helps implement the principle of least privilege, ensuring users have the permissions they need to perform their tasks. This action minimizes the risk of accidental or intentional misconfiguration.As noted for control 0.1d User Password Management, passwordless authentication uses biometrics because they are difficult to forge, thus providing more secure authentication. |
| **CSF Control V11**01.q User Identification and Authentication**Control category**N/A**Control specification**All users shall have a unique identifier (user ID) for their personal use only, and an authentication technique shall be implemented to substantiate the claimed identity of a user.**Objective name**N/A**HIPAA Security Rule**§ 164.308(a)(5)(ii)(D)§ 164.310(a)(1)§ 164.312(a)(2)(i)§ 164.312(d) | Use [account provisioning](../identity/hybrid/what-is-provisioning) in Microsoft Entra ID to create, update, and manage user accounts. Each user and object are assigned a unique identifier (UID) referred to as the object ID. The UID is a globally unique identifier automatically generated when a user or object is created.Microsoft Entra ID supports [automated user provisioning](../identity/app-provisioning/plan-cloud-hr-provision) for systems and [applications](../identity/app-provisioning/plan-auto-user-provisioning). Automated provisioning creates new accounts in the right systems when people join a team in an organization. Automated deprovisioning deactivates accounts when people leave. |
| **CSF Control V11**01.u Limitation of Connection Time**Control category**Access Control - Secure Logon**Control specification**The organization controls access to information assets using a secure logon procedure.**Objective name**Operating System Access Control**HIPAA Security Rule**§ 164.312(a)(2)(iii) | **The control focuses on the [operating system](/en-us/azure/governance/policy/samples/hipaa-hitrust-9-2), Microsoft Entra services help strengthen the secure sign in.**Secure sign-in is the process to authenticate an identity securely when they attempt to access a system.Microsoft Entra authenticates users and has security features with information about the user and the resource. The information includes the access token, refresh token, and ID token. Configure in accordance with your organizational requirements for application access. Use this guidance predominantly for mobile and desktop clients.Conditional Access policies support configuration settings for web browser [restriction of authenticated sessions](../identity/conditional-access/howto-conditional-access-session-lifetime).Microsoft Entra ID has integrations across operating systems, to provide a better user experience and support for passwordless authentication methods listed:[Platform SSO for macOS](/en-us/mem/intune/configuration/use-enterprise-sso-plug-in-ios-ipados-macos?pivots=all) extends the SSO capabilities for macOS. Users sign in to a Mac using passwordless credentials, or password management validated by Microsoft Entra ID.[Windows passwordless experience](/en-us/windows/security/identity-protection/passwordless-experience/?branch=main&amp;preserve-view=true) promotes an authentication experience without passwords on Microsoft Entra joined devices. Using passwordless authentication reduces vulnerabilities and risks associated with traditional password-based authentication, such as phishing attacks, password reuse, and key logger interception of passwords.[Web sign-in for Windows](/en-us/windows/security/identity-protection/web-sign-in/?tabs=intune&amp;branch=main) is a credential provider that expands the capabilities of web sign-in in Windows 11, covering Windows Hello for Business, temporary access pass (TAP), and federated identities.Azure Virtual Desktop supports [SSO and passwordless authentication](/en-us/azure/virtual-desktop/authentication). With SSO, you can use passwordless authentication and third-party identity providers (IdPs) that federate with Microsoft Entra ID to sign in to your Azure Virtual Desktop resources. It has an SSO experience when authenticating to the session host. It configures the session to provide SSO to Microsoft Entra resources in the session. |