---
layout: Conceptual
title: Microsoft Entra feature availability in Azure for US Government - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/feature-availability
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn which Microsoft Entra features are available in Azure for US Government.
ms.topic: reference
ms.date: 2026-01-15T00:00:00.0000000Z
ms.reviewer: mattsmith
locale: en-us
document_id: baec6c51-15ff-186e-de34-ed72e7cdd0d9
document_version_independent_id: 4a23e043-6f7f-d07f-ab66-70d66b571b88
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/feature-availability.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/feature-availability
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/feature-availability.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: bfe24308-3542-6da6-02ba-295629dcdb80
---

# Microsoft Entra feature availability in Azure for US Government - Microsoft Entra ID | Microsoft Learn

This following tables list Microsoft Entra feature availability in Azure for US Government.

## Microsoft Entra ID

| Service | Feature | Availability |
| --- | --- | --- |
| **Authentication, single sign-on, and MFA** | Cloud authentication (Pass-through authentication, password hash synchronization) | ✅ |
|  | Federated authentication (Active Directory Federation Services or federation with other identity providers) | ✅ |
|  | Single sign-on (SSO) unlimited | ✅ |
|  | Multifactor authentication (MFA) | ✅ |
|  | Passwordless (Windows Hello for Business, Microsoft Authenticator, FIDO2 security key integrations) | ✅ |
|  | Certificate-based authentication | ✅ |
|  | Service-level agreement | ✅ |
| **Applications access** | SaaS apps with modern authentication (Microsoft Entra application gallery apps, SAML, and OAUTH 2.0) | ✅ |
|  | Group assignment to applications | ✅ |
|  | Cloud app discovery (Microsoft Defender for Cloud Apps) | ✅ |
|  | Application Proxy for on-premises, header-based, and Integrated Windows Authentication | ✅ |
|  | Secure hybrid access partnerships (Kerberos, NTLM, LDAP, RDP, and SSH authentication) | ✅ |
| **Authorization and Conditional Access** | Role-based access control (RBAC) | ✅ |
|  | Conditional Access | ✅ |
|  | SharePoint limited access | ✅ |
|  | Session lifetime management | ✅ |
|  | ID Protection (vulnerabilities, risky accounts, risk event investigation, SIEM connectivity) | See Microsoft Entra ID Protection. |
| **Administration and hybrid identity** | User and group management | ✅ |
|  | Group Source of Authority (SOA) | ✅ |
|  | Advanced group management (Dynamic groups, naming policies, expiration, default classification) | ✅ |
|  | Directory synchronization—Microsoft Entra Connect (sync and cloud sync) | ✅ |
|  | Microsoft Entra Connect Health reporting | ✅ |
|  | Delegated administration—built-in roles | ✅ |
|  | Global password protection and management – cloud-only users | ✅ |
|  | Global password protection and management – custom banned passwords, users synchronized from on-premises Active Directory | ✅ |
|  | Microsoft Identity Manager user client access license (CAL) | ✅ |
| **End-user self-service** | Application launch portal (My Apps) | ✅ |
|  | User application collections in My Apps | ✅ |
|  | Self-service account management portal (My Account) | ✅ |
|  | Self-service password change for cloud users | ✅ |
|  | Self-service password reset/change/unlock with on-premises write-back | ✅ |
|  | Self-service sign-in activity search and reporting | ✅ |
|  | Self-service group management (My Groups) | ✅ |
|  | Self-service entitlement management (My Access) | ✅ |
| **Identity governance** | Automated user provisioning to apps | ✅ |
|  | Automated group provisioning to apps | ✅ |
|  | HR-driven provisioning | Partial. See HR-provisioning apps. |
|  | Terms of use | ✅ |
|  | Access reviews | ✅ |
|  | Entitlement management | ✅ |
|  | Privileged Identity Management (PIM) | ✅ |
|  | Lifecycle workflows, in Microsoft Entra ID Governance | ✅ |
| **Event logging and reporting** | Basic security and usage reports | ✅ |
|  | Advanced security and usage reports | ✅ |
|  | ID Protection: vulnerabilities and risky accounts | ✅ |
|  | ID Protection: risk events investigation, SIEM connectivity | ✅ |
| **Frontline workers** | SMS sign-in | ✅ |
|  | Shared device sign-out | Enterprise state roaming for Windows 10 devices isn't available. |
|  | Delegated user management portal (My Staff) | ❌ |

## Microsoft Entra ID Protection

| Risk Detection | Availability |
| --- | --- |
| Leaked credentials (Microsoft Account Compromise Exchange) | ✅ |
| Microsoft Entra threat intelligence | ❌ |
| Anonymous IP address | ✅ |
| Atypical travel | ✅ |
| Anomalous Token | ✅ |
| Token Issuer Anomaly | ✅ |
| Malware linked IP address | ✅ |
| Suspicious browser | ✅ |
| Unfamiliar sign-in properties | ✅ |
| Admin confirmed user compromised | ✅ |
| Malicious IP address | ✅ |
| Suspicious inbox manipulation rules | ✅ |
| Password spray | ✅ |
| Impossible travel | ✅ |
| New country | ✅ |
| Activity from anonymous IP address | ✅ |
| Suspicious inbox forwarding | ✅ |
| Additional risk detected | ✅ |

## HR provisioning apps

| HR-provisioning app | Availability |
| --- | --- |
| Workday to Microsoft Entra user provisioning | ✅ |
| Workday Writeback | ✅ |
| SuccessFactors to Microsoft Entra user provisioning | ✅ |
| SuccessFactors to Writeback | ✅ |
| API-driven inbound provisioning | ✅ |
| Provisioning agent configuration and registration with Azure for US Government tenant | ✅ |

## Other Microsoft Entra products

[Microsoft Entra ID Governance](../../id-governance/licensing-fundamentals) is available in the US Government community cloud (GCC), GCC-High, and Department of Defense cloud environments. [Microsoft Entra Workload Identities Premium edition](../../workload-id/workload-identities-faqs#is-the-workload-id-premium-plan-available-on-azure-government-clouds) is available in Azure for US government.