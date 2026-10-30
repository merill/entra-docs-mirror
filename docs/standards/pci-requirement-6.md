---
layout: Conceptual
title: Microsoft Entra ID and PCI-DSS Requirement 6 - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/pci-requirement-6
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Learn PCI-DSS defined approach requirements about developing and maintaining secure systems and software
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
document_id: ab8ac637-c630-6e22-0d09-9b27dac7f555
document_version_independent_id: b34ae744-359e-9ce9-fb27-ebfb4243dc19
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/pci-requirement-6.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/pci-requirement-6
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/pci-requirement-6.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9a6e41bc-8426-db54-e47a-a65d2dec4f7a
---

# Microsoft Entra ID and PCI-DSS Requirement 6 - Microsoft Entra | Microsoft Learn

**Requirement 6: Develop and Maintain Secure Systems and Software** **Defined approach requirements**

## 6.1 Processes and mechanisms for developing and maintaining secure systems and software are defined and understood.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **6.1.1** All security policies and operational procedures that are identified in Requirement 6 are:  Documented  Kept up to date  In use  Known to all affected parties | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |
| **6.1.2** Roles and responsibilities for performing activities in Requirement 6 are documented, assigned, and understood. | Use the guidance and links herein to produce the documentation to fulfill requirements based on your environment configuration. |

## 6.2 Bespoke and custom software are developed securely.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **6.2.1** Bespoke and custom software are developed securely, as follows:  Based on industry standards and/or best practices for secure development.  In accordance with PCI-DSS (for example, secure authentication and logging).  Incorporating consideration of information security issues during each stage of the software development lifecycle. | Procure and develop applications that use modern authentication protocols, such as OAuth2 and OpenID Connect (OIDC), which integrate with Microsoft Entra ID.  Build software using the Microsoft identity platform. [Microsoft identity platform best practices and recommendations](../identity-platform/identity-platform-integration-checklist) |
| **6.2.2** Software development personnel working on bespoke and custom software are trained at least once every 12 months as follows:  On software security relevant to their job function and development languages.  Including secure software design and secure coding techniques.  Including, if security testing tools are used, how to use the tools for detecting vulnerabilities in software. | Use the following exam to provide proof of proficiency on Microsoft identity platform: [Exam MS-600: Building Applications and Solutions with Microsoft 365 Core Services](/en-us/credentials/certifications/exams/ms-600/) Use the following training to prepare for the exam: [MS-600: Implement Microsoft identity](/en-us/training/paths/m365-identity-associate/) |
| **6.2.3** Bespoke and custom software is reviewed prior to being released into production or to customers, to identify and correct potential coding vulnerabilities, as follows:  Code reviews ensure code is developed according to secure coding guidelines.  Code reviews look for both existing and emerging software vulnerabilities.  Appropriate corrections are implemented prior to release. | Not applicable to Microsoft Entra ID. |
| **6.2.3.1** If manual code reviews are performed for bespoke and custom software prior to release to production, code changes are:  Reviewed by individuals other than the originating code author, and who are knowledgeable about code-review techniques and secure coding practices.  Reviewed and approved by management prior to release. | Not applicable to Microsoft Entra ID. |
| **6.2.4** Software engineering techniques or other methods are defined and in use by software development personnel to prevent or mitigate common software attacks and related vulnerabilities in bespoke and custom software, including but not limited to the following:  Injection attacks, including SQL, LDAP, XPath, or other command, parameter, object, fault, or injection-type flaws.  Attacks on data and data structures, including attempts to manipulate buffers, pointers, input data, or shared data.  Attacks on cryptography usage, including attempts to exploit weak, insecure, or inappropriate cryptographic implementations, algorithms, cipher suites, or modes of operation.  Attacks on business logic, including attempts to abuse or bypass application features and functionalities through the manipulation of APIs, communication protocols and channels, client-side functionality, or other system/application functions and resources. This includes cross-site scripting (XSS) and cross-site request forgery (CSRF).  Attacks on access control mechanisms, including attempts to bypass or abuse identification, authentication, or authorization mechanisms, or attempts to exploit weaknesses in the implementation of such mechanisms.  Attacks via any “high-risk” vulnerabilities identified in the vulnerability identification process, as defined in Requirement 6.3.1. | Not applicable to Microsoft Entra ID. |

## 6.3 Security vulnerabilities are identified and addressed.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **6.3.1** Security vulnerabilities are identified and managed as follows:  New security vulnerabilities are identified using industry-recognized sources for security vulnerability information, including alerts from international and national/regional computer emergency response teams (CERTs).  Vulnerabilities are assigned a risk ranking based on industry best practices and consideration of potential impact.  Risk rankings identify, at a minimum, all vulnerabilities considered to be a high-risk or critical to the environment.  Vulnerabilities for bespoke and custom, and third-party software (for example operating systems and databases) are covered. | Learn about vulnerabilities. [MSRC | Security Updates, Security Update Guide](https://msrc.microsoft.com/update-guide) |
| **6.3.2** An inventory of bespoke and custom software, and third-party software components incorporated into bespoke and custom software is maintained to facilitate vulnerability and patch management. | Generate reports for applications using Microsoft Entra ID for authentication for inventory. [`applicationSignInDetailedSummary` resource type](/en-us/graph/api/resources/applicationsignindetailedsummary?view=graph-rest-beta&amp;viewFallbackFrom=graph-rest-1.0&amp;preserve-view=true)[Applications listed in Enterprise applications](../identity/enterprise-apps/application-list) |
| **6.3.3** All system components are protected from known vulnerabilities by installing applicable security patches/updates as follows:  Critical or high-security patches/updates (identified according to the risk ranking process at Requirement 6.3.1) are installed within one month of release.  All other applicable security patches/updates are installed within an appropriate time frame as determined by the entity (for example, within three months of release). | Not applicable to Microsoft Entra ID. |

## 6.4 Public-facing web applications are protected against attacks.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **6.4.1** For public-facing web applications, new threats and vulnerabilities are addressed on an ongoing basis and these applications are protected against known attacks as follows: Reviewing public-facing web applications via manual or automated application vulnerability security assessment tools or methods as follows:  – At least once every 12 months and after significant changes.  – By an entity that specializes in application security.  – Including, at a minimum, all common software attacks in Requirement 6.2.4.  – All vulnerabilities are ranked in accordance with requirement 6.3.1.  – All vulnerabilities are corrected.  – The application is reevaluated after the corrections  OR  Installing an automated technical solution(s) that continually detect and prevent web-based attacks as follows:  – Installed in front of public-facing web applications to detect and prevent web-based attacks.  – Actively running and up to date as applicable.  – Generating audit logs.  – Configured to either block web-based attacks or generate an alert that is immediately investigated. | Not applicable to Microsoft Entra ID. |
| **6.4.2** For public-facing web applications, an automated technical solution is deployed that continually detects and prevents web-based attacks, with at least the following:  Is installed in front of public-facing web applications and is configured to detect and prevent web-based attacks.  Actively running and up to date as applicable.  Generating audit logs.  Configured to either block web-based attacks or generate an alert that is immediately investigated. | Not applicable to Microsoft Entra ID. |
| **6.4.3** All payment page scripts that are loaded and executed in the consumer’s browser are managed as follows:  A method is implemented to confirm that each script is authorized.  A method is implemented to assure the integrity of each script.  An inventory of all scripts is maintained with written justification as to why each is necessary. | Not applicable to Microsoft Entra ID. |

## 6.5 Changes to all system components are managed securely.

| PCI-DSS Defined approach requirements | Microsoft Entra guidance and recommendations |
| --- | --- |
| **6.5.1** Changes to all system components in the production environment are made according to established procedures that include:  Reason for, and description of, the change.  Documentation of security impact.  Documented change approval by authorized parties.  Testing to verify that the change doesn't adversely impact system security.  For bespoke and custom software changes, all updates are tested for compliance with Requirement 6.2.4 before being deployed into production.  Procedures to address failures and return to a secure state. | Include changes to Microsoft Entra configuration in the change control process. |
| **6.5.2** Upon completion of a significant change, all applicable PCI-DSS requirements are confirmed to be in place on all new or changed systems and networks, and documentation is updated as applicable. | Not applicable to Microsoft Entra ID. |
| **6.5.3** Preproduction environments are separated from production environments and the separation is enforced with access controls. | Approaches to separate preproduction and production environments, based on organizational requirements. [Resource isolation in a single tenant](../architecture/secure-single-tenant)[Resource isolation with multiple tenants](../architecture/secure-multiple-tenants) |
| **6.5.4** Roles and functions are separated between production and preproduction environments to provide accountability such that only reviewed and approved changes are deployed. | Learn about privileged roles and dedicated preproduction tenants. [Best practices for Microsoft Entra roles](../identity/role-based-access-control/best-practices) |
| **6.5.5** Live PANs aren't used in preproduction environments, except where those environments are included in the CDE and protected in accordance with all applicable PCI-DSS requirements. | Not applicable to Microsoft Entra ID. |
| **6.5.6** Test data and test accounts are removed from system components before the system goes into production. | Not applicable to Microsoft Entra ID. |