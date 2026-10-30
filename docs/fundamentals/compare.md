---
layout: Conceptual
title: Compare Active Directory to Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/compare
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: This document compares Active Directory Domain Services (AD DS) to Microsoft Entra ID. It outlines key concepts in both identity solutions and explains how it's different or similar.
tags: azuread
ms.topic: concept-article
ms.date: 2022-08-17T00:00:00.0000000Z
ms.reviewer: martinco
locale: en-us
document_id: cecf7a5d-141d-77a6-8cfe-9ff5d6482670
document_version_independent_id: 4cd77fd0-3467-b3a0-2962-a1289655858e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/compare.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/compare
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/compare.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 9565249e-3ee2-ca54-9927-ee9e06757e61
---

# Compare Active Directory to Microsoft Entra ID - Microsoft Entra | Microsoft Learn

Microsoft Entra ID is the next evolution of identity and access management solutions for the cloud. Microsoft introduced Active Directory Domain Services in Windows 2000 to give organizations the ability to manage multiple on-premises infrastructure components and systems using a single identity per user.

Microsoft Entra ID takes this approach to the next level by providing organizations with an Identity as a Service (IDaaS) solution for all their apps across cloud and on-premises.

Most IT administrators are familiar with Active Directory Domain Services concepts. The following table outlines the differences and similarities between Active Directory concepts and Microsoft Entra ID.

| Concept | Windows Server Active Directory | Microsoft Entra ID |
| --- | --- | --- |
| **Users** |  |  |
| Provisioning: users | Organizations create internal users manually or use an in-house or automated provisioning system, such as the Microsoft Identity Manager, to integrate with an HR system. | Existing Microsoft Windows Server Active Directory organizations use [Microsoft Entra Connect](../identity/hybrid/connect/how-to-connect-sync-whatis) to sync identities to the cloud. Microsoft Entra ID adds support to automatically create users from [cloud HR systems](../identity/app-provisioning/what-is-hr-driven-provisioning). Microsoft Entra ID can provision identities in [System for Cross-Domain Identity Management (SCIM) enabled](../identity/app-provisioning/use-scim-to-provision-users-and-groups) software as a service (SaaS) apps to automatically provide apps with the necessary details to allow access for users. |
| Provisioning: external identities | Organizations create external users manually as regular users in a dedicated external Microsoft Windows Server Active Directory forest, resulting in administration overhead to manage the lifecycle of external identities (guest users) | Microsoft Entra ID provides a special class of identity to support external identities. [Microsoft Entra B2B](../external-id/) will manage the link to the external user identity to make sure they are valid. |
| Entitlement management and groups | Administrators make users members of groups. App and resource owners then give groups access to apps or resources. | [Groups](how-to-manage-groups) are also available in Microsoft Entra ID and administrators can also use groups to grant permissions to resources. In Microsoft Entra ID, administrators can assign membership to groups manually or use a query to dynamically include users to a group.  Administrators can use [Entitlement management](../id-governance/entitlement-management-overview) in Microsoft Entra ID to give users access to a collection of apps and resources using workflows and, if necessary, time-based criteria. |
| Admin management | Organizations will use a combination of domains, organizational units, and groups in Microsoft Windows Server Active Directory to delegate administrative rights to manage the directory and resources it controls. | Microsoft Entra ID provides [built-in roles](how-subscriptions-associated-directory) with its Microsoft Entra role-based access control (RBAC) system, with limited support for [creating custom roles](../identity/role-based-access-control/custom-overview) to delegate privileged access to the identity system, the apps, and resources it controls.Managing roles can be enhanced with [Privileged Identity Management (PIM)](../id-governance/privileged-identity-management/pim-configure) to provide just-in-time, time-restricted, or workflow-based access to privileged roles. |
| Credential management | Credentials in Active Directory are based on passwords, certificate authentication, and smart card authentication. Passwords are managed using password policies that are based on password length, expiry, and complexity. | Microsoft Entra ID uses intelligent [password protection](../identity/authentication/concept-password-ban-bad) for cloud and on-premises. Protection includes smart lockout plus blocking common and custom password phrases and substitutions. Microsoft Entra ID significantly boosts security [through multifactor authentication](../identity/authentication/concept-mfa-howitworks) and [passwordless](../identity/authentication/concept-authentication-passkeys-fido2) technologies, like FIDO2. Microsoft Entra ID reduces support costs by providing users a [self-service password reset](../identity/authentication/concept-sspr-howitworks) system. |
| **Apps** |  |  |
| Infrastructure apps | Active Directory forms the basis for many infrastructure on-premises components, for example, DNS, Dynamic Host Configuration Protocol (DHCP), Internet Protocol Security (IPSec), WiFi, NPS, and VPN access | In a new cloud world, Microsoft Entra ID, is the new control plane for accessing apps versus relying on networking controls. When users authenticate, [Conditional Access](../identity/conditional-access/overview) controls which users have access to which apps under required conditions. |
| Traditional and legacy apps | Most on-premises apps use LDAP, Windows-Integrated Authentication (NTLM and Kerberos), or Header-based authentication to control access to users. | Microsoft Entra ID can provide access to these types of on-premises apps using [Microsoft Entra application proxy](/en-us/entra/identity/app-proxy) agents running on-premises. Using this method Microsoft Entra ID can authenticate Active Directory users on-premises using Kerberos while you migrate or need to coexist with legacy apps. |
| SaaS apps | Active Directory doesn't support SaaS apps natively and requires federation system, such as AD FS. | SaaS apps supporting OAuth2, Security Assertion Markup Language (SAML), and WS-\* authentication can be integrated to use Microsoft Entra ID for authentication. |
| Line of business (LOB) apps with modern authentication | Organizations can use AD FS with Active Directory to support LOB apps requiring modern authentication. | LOB apps requiring modern authentication can be configured to use Microsoft Entra ID for authentication. |
| Mid-tier/Daemon services | Services running in on-premises environments normally use Microsoft Windows Server Active Directory service accounts or group Managed Service Accounts (gMSA) to run. These apps will then inherit the permissions of the service account. | Microsoft Entra ID provides [managed identities](../identity/managed-identities-azure-resources/) to run other workloads in the cloud. The lifecycle of these identities is managed by Microsoft Entra ID and is tied to the resource provider and it can't be used for other purposes to gain backdoor access. |
| **Devices** |  |  |
| Mobile | Active Directory doesn't natively support mobile devices without third-party solutions. | Microsoft's mobile device management solution, Microsoft Intune, is integrated with Microsoft Entra ID. Microsoft Intune provides device state information to the identity system to evaluate during authentication. |
| Windows desktops | Active Directory provides the ability to domain join Windows devices to manage them using Group Policy, System Center Configuration Manager, or other third-party solutions. | Windows devices can be [joined to Microsoft Entra ID](../identity/devices/). Conditional Access can check if a device is Microsoft Entra joined as part of the authentication process. Windows devices can also be managed with [Microsoft Intune](/en-us/mem/intune/fundamentals/what-is-intune). In this case, Conditional Access, will consider whether a device is compliant (for example, up-to-date security patches and virus signatures) before allowing access to the apps. |
| Windows servers | Active Directory provides strong management capabilities for on-premises Windows servers using Group Policy or other management solutions. | Windows servers virtual machines in Azure can be managed with [Microsoft Entra Domain Services](../identity/domain-services/). [Managed identities](../identity/managed-identities-azure-resources/) can be used when VMs need access to the identity system directory or resources. |
| Linux/Unix workloads | Active Directory doesn't natively support non-Windows without third-party solutions, although Linux machines can be configured to authenticate with Active Directory as a Kerberos realm. | Linux/Unix VMs can use [managed identities](../identity/managed-identities-azure-resources/) to access the identity system or resources. Some organizations, migrate these workloads to cloud container technologies, which can also use managed identities. |