---
layout: Conceptual
title: Configure CMMC Level 2 Identification and Authentication (IA) controls - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/configure-cmmc-level-2-identification-and-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Learn how to configure Microsoft Entra ID to meet CMMC Level 2 Identification and authorization requirements.
ms.service: entra
ms.subservice: standards
ms.topic: concept-article
ms.date: 2023-01-03T00:00:00.0000000Z
author: janicericketts
ms.author: jricketts
ms.reviewer: jricketts
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done
locale: en-us
document_id: 14c66071-e64b-a2cc-b77d-9a2178186b42
document_version_independent_id: e8fbf140-e67d-0660-8239-1ade2fa11231
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/configure-cmmc-level-2-identification-and-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/configure-cmmc-level-2-identification-and-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/configure-cmmc-level-2-identification-and-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: c0a51cba-1b7d-c069-f1bd-d10ef345fe94
---

# Configure CMMC Level 2 Identification and Authentication (IA) controls - Microsoft Entra | Microsoft Learn

Microsoft Entra ID helps you meet identity-related practice requirements in each Cybersecurity Maturity Model Certification (CMMC) level. To complete other configurations or processes to be compliant with CMMC V2.0 level 2 requirements, is the responsibility of companies performing work with, and on behalf of, the US Dept. of Defense (DoD).

CMMC Level 2 has 13 domains that have one or more practices related to identity. The domains are:

- Access Control (AC)
- Audit & Accountability (AU)
- Configuration Management (CM)
- Identification & Authentication (IA)
- Incident Response (IR)
- Maintenance (MA)
- Media Protection (MP)
- Personnel Security (PS)
- Physical Protection (PE)
- Risk Assessment (RA)
- Security Assessment (CA)
- System and Communications Protection (SC)
- System and Information Integrity (SI)

The remainder of this article provides guidance for the Identification and Authorization (IA) domain. There's a table with links to content that provides step-by-step guidance to accomplish the practice.

## Identification & Authentication

The following table provides a list of practice statement and objectives, and Microsoft Entra guidance and recommendations to enable you to meet these requirements with Microsoft Entra ID.

| CMMC practice statement and objectives | Microsoft Entra guidance and recommendations |
| --- | --- |
| IA.L2-3.5.3**Practice statement:** Use multifactor authentication for local and network access to privileged accounts and for network access to non-privileged accounts. **Objectives:**Determine if:[a.] privileged accounts are identified;[b.] multifactor authentication is implemented for local access to privileged accounts;[c.] multifactor authentication is implemented for network access to privileged accounts; and[d.] multifactor authentication is implemented for network access to non-privileged accounts. | The following items are definitions for the terms used for this control area:- **Local Access** - Access to an organizational information system by a user (or process acting on behalf of a user) communicating through a direct connection without the use of a network.<br>- **Network Access** - Access to an information system by a user (or a process acting on behalf of a user) communicating through a network (for example, local area network, wide area network, Internet).<br>- **Privileged User** - A user that's authorized (and therefore, trusted) to perform security-relevant functions that ordinary users aren't authorized to perform.Breaking down the previous requirement means:<br>- All users are required MFA for network/remote access.<br>- Only privileged users are required MFA for local access. If regular user accounts have administrative rights only on their computers, they're not a “privileged account” and don't require MFA for local access. You're responsible for configuring Conditional Access to require multifactor authentication. Enable Microsoft Entra authentication methods that meet AAL2 and higher.[Grant controls in Conditional Access policy](../identity/conditional-access/concept-conditional-access-grant)[Achieve NIST authenticator assurance levels with Microsoft Entra ID](nist-overview)[Authentication methods and features](../identity/authentication/overview-authentication) |
| IA.L2-3.5.4**Practice statement:** Employ replay-resistant authentication mechanisms for network access to privileged and non-privileged accounts.**Objectives:**Determine if:[a.] replay-resistant authentication mechanisms are implemented for network account access to privileged and non-privileged accounts. | All Microsoft Entra authentication methods at AAL2 and above are replay resistant.[Achieve NIST authenticator assurance levels with Microsoft Entra ID](nist-overview) |
| IA.L2-3.5.5**Practice statement:** Prevent reuse of identifiers for a defined period.**Objectives:**Determine if:[a.] a period within which identifiers can't be reused is defined; and[b.] reuse of identifiers is prevented within the defined period. | All user, group, device object globally unique identifiers (GUIDs) are guaranteed unique and non-reusable for the lifetime of the Microsoft Entra tenant.[user resource type - Microsoft Graph v1.0](/en-us/graph/api/resources/user?view=graph-rest-1.0&amp;preserve-view=true)[group resource type - Microsoft Graph v1.0](/en-us/graph/api/resources/group?view=graph-rest-1.0&amp;preserve-view=true)[device resource type - Microsoft Graph v1.0](/en-us/graph/api/resources/device?view=graph-rest-1.0&amp;preserve-view=true) |
| IA.L2-3.5.6**Practice statement:** Disable identifiers after a defined period of inactivity.**Objectives:**Determine if:[a.] a period of inactivity after which an identifier is disabled is defined; and[b.] identifiers are disabled after the defined period of inactivity. | Implement account management automation with Microsoft Graph and Microsoft Graph PowerShell SDK. Use Microsoft Graph to monitor sign-in activity and Microsoft Graph PowerShell SDK to take action on accounts within the required time frame.**Determine inactivity**[Manage inactive user accounts in Microsoft Entra ID](../identity/monitoring-health/howto-manage-inactive-user-accounts)[Manage stale devices in Microsoft Entra ID](../identity/devices/manage-stale-devices)**Remove or disable accounts**[Working with users in Microsoft Graph](/en-us/graph/api/resources/user)[Get a user](/en-us/graph/api/user-get?tabs=http)[Update user](/en-us/graph/api/user-update?tabs=http)[Delete a user](/en-us/graph/api/user-delete?tabs=http)**Work with devices in Microsoft Graph**[Get device](/en-us/graph/api/device-get?tabs=http)[Update device](/en-us/graph/api/device-update?tabs=http)[Delete device](/en-us/graph/api/device-delete?tabs=http)**[Use the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/overview)**[Get-MgUser](/en-us/powershell/module/microsoft.graph.users/get-mguser)[Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser)[Get-MgDevice](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdevice)[Update-MgDevice](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/update-mgdevice) |
| IA.L2-3.5.7**Practice statement:** **Objectives:** Enforce a minimum password complexity and change of characters when new passwords are created.Determine if:[a.] password complexity requirements are defined;[b.] password change of character requirements are defined;[c.] minimum password complexity requirements as defined are enforced when new passwords are created; and[d.] minimum password change of character requirements as defined are enforced when new passwords are created.IA.L2-3.5.8**Practice statement:** Prohibit password reuse for a specified number of generations.**Objectives:**Determine if:[a.] the number of generations during which a password cannot be reused is specified; and[b.] reuse of passwords is prohibited during the specified number of generations. | We **strongly encourage** passwordless strategies. This control is only applicable to password authenticators, so removing passwords as an available authenticator renders this control not applicable.Per NIST SP 800-63 B Section 5.1.1: Maintain a list of commonly used, expected, or compromised passwords.With Microsoft Entra password protection, default global banned password lists are automatically applied to all users in a Microsoft Entra tenant. To support your business and security needs, you can define entries in a custom banned password list. When users change or reset their passwords, these banned password lists are checked to enforce the use of strong passwords.For customers that require strict password character change, password reuse and complexity requirements use hybrid accounts configured with Password-Hash-Sync. This action ensures the passwords synchronized to Microsoft Entra ID inherit the restrictions configured in Active Directory password policies. Further protect on-premises passwords by configuring on-premises Microsoft Entra Password Protection for Active Directory Domain Services.[NIST Special Publication 800-63 B](https://pages.nist.gov/800-63-3/sp800-63b.html)[NIST Special Publication 800-53 Revision 5 (IA-5 - Control enhancement (1)](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf)[Eliminate bad passwords using Microsoft Entra password protection](../identity/authentication/concept-password-ban-bad)[What is password hash synchronization with Microsoft Entra ID?](../identity/hybrid/connect/whatis-phs) |
| IA.L2-3.5.9**Practice statement:** Allow temporary password use for system logons with an immediate change to a permanent password.**Objectives:**Determine if:[a.] an immediate change to a permanent password is required when a temporary password is used for system sign-on. | A Microsoft Entra user initial password is a temporary single use password that once successfully used is immediately required to be changed to a permanent password. Microsoft strongly encourages the adoption of passwordless authentication methods. Users can bootstrap Passwordless authentication methods using Temporary Access Pass (TAP). TAP is a time and use limited passcode issued by an admin that satisfies strong authentication requirements. Use of passwordless authentication along with the time and use limited TAP completely eliminates the use of passwords (and their reuse).[Add or delete users](../fundamentals/how-to-create-delete-users)[Configure a Temporary Access Pass in Microsoft Entra ID to register Passwordless authentication methods](../identity/authentication/howto-authentication-temporary-access-pass)[Passwordless authentication](../identity/authentication/concept-authentication-passkeys-fido2) |
| IA.L2-3.5.10**Practice statement:** Store and transmit only cryptographically protected passwords.**Objectives:**Determine if:[a.] passwords are cryptographically protected in storage; and[b.] passwords are cryptographically protected in transit. | **Secret Encryption at Rest**:In addition to disk level encryption, when at rest, secrets stored in the directory are encrypted using the Distributed Key Manager(DKM). The encryption keys are stored in Microsoft Entra core store and in turn are encrypted with a scale unit key. The key is stored in a container that is protected with directory ACLs, for highest privileged users and specific services. The symmetric key is typically rotated every six months. Access to the environment is further protected with operational controls and physical security.**Encryption in Transit**:To assure data security, Directory Data in Microsoft Entra ID is signed and encrypted while in transit between data centers within a scale unit. The data is encrypted and unencrypted by the Microsoft Entra core store tier, which resides inside secured server hosting areas of the associated Microsoft data centers.Customer-facing web services are secured with the Transport Layer Security (TLS) protocol.For more information, [download](https://azure.microsoft.com/resources/azure-active-directory-data-security-considerations/)*Data Protection Considerations - Data Security*. On page 15, there are more details.[Demystifying Password Hash Sync (microsoft.com)](https://www.microsoft.com/security/blog/2019/05/30/demystifying-password-hash-sync/)[Microsoft Entra Data Security Considerations](https://aka.ms/aaddatawhitepaper) |
| IA.L2-3.5.11**Practice statement:** Obscure feedback of authentication information.**Objectives:**Determine if:[a.] authentication information is obscured during the authentication process. | By default, Microsoft Entra ID obscures all authenticator feedback. |

### Next steps

- [Configure Microsoft Entra ID for CMMC compliance](configure-for-cmmc-compliance)
- [Configure CMMC Level 1 controls](configure-cmmc-level-1-controls)
- [Configure CMMC Level 2 Access Control (AC) controls](configure-cmmc-level-2-access-control)
- [Configure CMMC Level 2 additional controls](configure-cmmc-level-2-additional-controls)