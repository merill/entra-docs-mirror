---
layout: Conceptual
title: Automate identity provisioning to applications introduction - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/automate-provisioning-to-applications-introduction
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn to design solutions to automatically provision identities in hybrid environments to provide application access.
ms.topic: overview
ms.date: 2022-09-23T00:00:00.0000000Z
ms.custom:
- it-pro
- kr2b-contr-experiment
ms.subservice: architecture
locale: en-us
document_id: a63225a3-cf68-02c6-38a0-04323fe5ed4b
document_version_independent_id: 0dd9eb81-1095-8b1e-ea02-fa5d85fec31c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/automate-provisioning-to-applications-introduction.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/automate-provisioning-to-applications-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/automate-provisioning-to-applications-introduction.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: f6f2b407-62c8-abbe-7421-dc2dfac9d874
---

# Automate identity provisioning to applications introduction - Microsoft Entra | Microsoft Learn

The article helps architects, Microsoft partners, and IT professionals with information addressing identity [provisioning](https://www.gartner.com/en/information-technology/glossary/user-provisioning) needs in their organizations, or the organizations they're working with. The content focuses on automating user provisioning for access to applications across all systems in your organization.

Employees in an organization rely on many applications to perform their work. These applications often require IT admins or application owners to provision accounts before an employee can start accessing them. Organizations also need to manage the lifecycle of these accounts and keep them up to date with the latest information and remove accounts when users don't require them anymore.

The Microsoft Entra provisioning service automates your identity lifecycle and keeps identities in sync across trusted source systems (like HR systems) and applications that users need access to. It enables you to bring users into Microsoft Entra ID and provision them into the various applications that they require. The provisioning capabilities are foundational building blocks that enable rich governance and lifecycle workflows. For [hybrid](../identity/hybrid/whatis-hybrid-identity) scenarios, the Microsoft Entra agent model connects to on-premises or infrastructure as a service (IaaS) systems, and includes components such as the Microsoft Entra provisioning agent, Microsoft Identity Manager (MIM), and Microsoft Entra Connect.

Thousands of organizations are running Microsoft Entra cloud-hosted services, with its hybrid components delivered on-premises, for provisioning scenarios. Microsoft invests in cloud-hosted and on-premises functionality, including MIM and Microsoft Entra Connect Sync, to help organizations provision users in their connected systems and applications. This article focuses on how organizations can use Microsoft Entra ID to address their provisioning needs and make clear which technology is most right for each scenario.

![Typical deployment of MIM](media/automate-user-provisioning-to-applications-introduction/typical-mim-deployment.png)

Use the following table to find content specific to your scenario. For example, if you want employee and contractor identities management from an HR system to Active Directory Domain Services (AD DS) or Microsoft Entra ID, follow the link to *Connect identities with your system of record*.

| What | From | To | Read |
| --- | --- | --- | --- |
| Employees and contractors | HR systems | Microsoft Windows Server Active Directory and Microsoft Entra ID | [Connect identities with your system of record](automate-provisioning-to-applications-solutions) |
| Existing Microsoft Windows Server Active Directory users and groups | AD DS | Microsoft Entra ID | [Synchronize identities between Microsoft Entra ID and Active Directory](automate-provisioning-to-applications-solutions) |
| Users, groups | Microsoft Entra ID | software as a service (SaaS) and on-premises apps | [Automate provisioning to non-Microsoft applications](../id-governance/entitlement-management-organization) |
| Access rights | Microsoft Entra ID Governance | SaaS and on-premises apps | [Entitlement management](../id-governance/entitlement-management-overview) |
| Existing users and groups | Microsoft Windows Server Active Directory, SaaS and on-premises apps | Identity governance (so I can review them) | [Microsoft Entra access reviews](../id-governance/access-reviews-overview) |
| Non-employee users (with approval) | Other cloud directories | SaaS and on-premises apps | [Connected organizations](../id-governance/entitlement-management-organization) |
| Users, groups | Microsoft Entra ID | Managed Microsoft Windows Server Active Directory domain | [Microsoft Entra Domain Services](https://azure.microsoft.com/services/active-directory-ds/) |

## Example topologies

Organizations vary greatly in the applications and infrastructure that they rely on to run their business. Some organizations have all their infrastructure in the cloud, relying solely on SaaS applications, while others have invested deeply in on-premises infrastructure over several years. The three topologies below depict how Microsoft can meet the needs of a cloud only customer, hybrid customer with basic provisioning requirements, and a hybrid customer with advanced provisioning requirements.

### Cloud only

In this example, the organization has a cloud HR system such as Workday or SuccessFactors, uses Microsoft 365 for collaboration, and SaaS apps such as ServiceNow and Zoom.

![Cloud only deployment](media/automate-user-provisioning-to-applications-introduction/cloud-only-identity-management.png)

1. The Microsoft Entra provisioning service imports users from the cloud HR system and creates an account in Microsoft Entra ID, based on business rules that the organization defines.
2. The user complete sets up the suitable authentication methods, such as the authenticator app, Fast Identity Online 2 (FIDO2)/Windows Hello for Business (WHfB) keys via [Temporary Access Pass](../identity/authentication/howto-authentication-temporary-access-pass) and then signs into Teams. This Temporary Access Pass was automatically generated for the user through Microsoft Entra lifecycle workflows.
3. The Microsoft Entra provisioning service creates accounts in the various applications that the user needs, such as ServiceNow and Zoom. The user can request the necessary devices they need and start chatting with their teams.

### Hybrid-basic

In this example, the organization has a mix of cloud and on-premises infrastructure. In addition to the systems mentioned above, the organization relies on SaaS applications and on-premises applications that are both Microsoft Windows Server Active Directory integrated and non-Microsoft Windows Server Active Directory integrated.

![Hybrid deployment model](media/automate-user-provisioning-to-applications-introduction/hybrid-basic.png)

1. The Microsoft Entra provisioning service imports the user from Workday and creates an account in AD DS, enabling the user to access Microsoft Windows Server Active Directory-integrated applications.
2. Microsoft Entra Connect cloud sync provisions the user into Microsoft Entra ID, which enables the user to access SharePoint in Microsoft 365 and their OneDrive files.
3. The Microsoft Entra provisioning service detects a new account was created in Microsoft Entra ID. It then creates accounts in the SaaS and on-premises applications the user needs access to.

### Hybrid-advanced

In this example, the organization has users spread across multiple on-premises HR systems and cloud HR. They have large groups and device synchronization requirements.

![Advanced hybrid deployment model](media/automate-user-provisioning-to-applications-introduction/hybrid-advanced.png)

1. MIM imports user information from each HR stem. MIM determines which users are needed for those employees in different directories. MIM provisions those identities in AD DS.
2. Microsoft Entra Connect Sync then synchronizes those users and groups to Microsoft Entra ID and provides users access to their resources.