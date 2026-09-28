---
layout: Conceptual
title: Compare Microsoft directory-based services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/compare-identity-solutions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: In this overview, you compare the different identity offerings for Active Directory Domain Services, Microsoft Entra ID, and Microsoft Entra Domain Services.
ms.topic: overview
ms.date: 2025-06-30T00:00:00.0000000Z
locale: en-us
document_id: 9ff64a31-7310-b2e8-28ba-690790b9b00d
document_version_independent_id: bd83c309-bd2b-6211-8d86-6d9713822c2b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/compare-identity-solutions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/compare-identity-solutions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/compare-identity-solutions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 45a37710-9738-feb1-7673-2a506b1be3df
---

# Compare Microsoft directory-based services - Microsoft Entra ID | Microsoft Learn

To provide applications, services, or devices access to a central identity, there are three common ways to use Active Directory-based services in Azure. This choice in identity solutions gives you the flexibility to use the most appropriate directory for your organization's needs. For example, if you mostly manage cloud-only users that run mobile devices, it may not make sense to build and run your own Active Directory Domain Services (AD DS) identity solution. Instead, you could just use Microsoft Entra ID.

Although the three Active Directory-based identity solutions share a common name and technology, they're designed to provide services that meet different customer demands. At high level, these identity solutions and feature sets are:

- **Active Directory Domain Services (AD DS)**- Enterprise-ready lightweight directory access protocol (LDAP) server that provides key features such as identity and authentication, computer object management, group policy, and trusts.
    - AD DS is a central component in many organizations with an on-premises IT environment, and provides core user account authentication and computer management features.
    - For more information, see [Active Directory Domain Services overview in the Windows Server documentation](/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview).
- **Microsoft Entra ID**- Cloud-based identity and mobile device management that provides user account and authentication services for resources such as Microsoft 365, the Microsoft Entra admin center, or SaaS applications.
    - Microsoft Entra ID can be synchronized with an on-premises AD DS environment to provide a single identity to users that works natively in the cloud.
    - For more information about Microsoft Entra ID, see [What is Microsoft Entra ID?](/en-us/azure/active-directory/fundamentals/whatis)
- **Microsoft Entra Domain Services**- Provides managed domain services with a subset of fully compatible traditional AD DS features such as domain join, group policy, LDAP, and Kerberos / NTLM authentication.
    - Domain Services integrates with Microsoft Entra ID, which itself can synchronize with an on-premises AD DS environment. This ability extends central identity use cases to traditional web applications that run in Azure as part of a lift-and-shift strategy.
    - To learn more about synchronization with Microsoft Entra ID and on-premises, see [How objects and credentials are synchronized in a managed domain](synchronization).

This overview article compares and contrasts how these identity solutions can work together, or would be used independently, depending on the needs of your organization.

## Domain Services and self-managed AD DS

If you have applications and services that need access to traditional authentication mechanisms such as Kerberos or NTLM, there are two ways to provide Active Directory Domain Services in the cloud:

- A *managed domain* that you create using Microsoft Entra Domain Services. Microsoft creates and manages the required resources.
- A *self-managed* domain that you create and configure using traditional resources such as virtual machines (VMs), Windows Server guest OS, and Active Directory Domain Services (AD DS). You then continue to administer these resources.

With Domain Services, the core service components are deployed and maintained for you by Microsoft as a *managed* domain experience. You don't deploy, manage, patch, and secure the AD DS infrastructure for components like the VMs, Windows Server OS, or domain controllers (DCs).

Domain Services provides a smaller subset of features to traditional self-managed AD DS environment, which reduces some of the design and management complexity. For example, there are no AD forests, domain, sites, and replication links to design and maintain. You can still [create forest trusts between Domain Services and on-premises environments](tutorial-create-forest-trust).

For applications and services that run in the cloud and need access to traditional authentication mechanisms such as Kerberos or NTLM, Domain Services provides a managed domain experience with the minimal amount of administrative overhead. For more information, see [Management concepts for user accounts, passwords, and administration in Domain Services](administration-concepts).

When you deploy and run a self-managed AD DS environment, you have to maintain all of the associated infrastructure and directory components. There's additional maintenance overhead with a self-managed AD DS environment, but you're then able to do additional tasks such as extend the schema or create forest trusts.

Common deployment models for a self-managed AD DS environment that provides identity to applications and services in the cloud include the following:

- **Standalone cloud-only AD DS** - Azure VMs are configured as domain controllers and a separate, cloud-only AD DS environment is created. This AD DS environment doesn't integrate with an on-premises AD DS environment. A different set of credentials is used to sign in and administer VMs in the cloud.
- **Extend on-premises domain to Azure**- An Azure virtual network connects to an on-premises network using a VPN / ExpressRoute connection. Azure VMs connect to this Azure virtual network, which lets them domain-join to the on-premises AD DS environment.
    - An alternative is to create Azure VMs and promote them as replica domain controllers from the on-premises AD DS domain. These domain controllers replicate over a VPN / ExpressRoute connection to the on-premises AD DS environment. The on-premises AD DS domain is effectively extended into Azure.

The following table outlines some of the features you may need for your organization, and the differences between a managed domain or a self-managed AD DS domain:

| **Feature** | **Managed domain** | **Self-managed AD DS** |
| --- | --- | --- |
| **Managed service** | **✓** | **✕** |
| **Secure deployments** | **✓** | Administrator secures the deployment |
| **DNS server** | **✓** (managed service) | **✓** |
| **Domain or Enterprise administrator privileges** | **✕** | **✓** |
| **Domain join** | **✓** | **✓** |
| **Domain authentication using NTLM and Kerberos** | **✓** | **✓** |
| **Kerberos constrained delegation** | Resource-based | Resource-based & account-based |
| **Custom OU structure** | **✓** | **✓** |
| **Group Policy** | **✓** | **✓** |
| **Schema extensions** | **✕** | **✓** |
| **AD domain / forest trusts** | **✓** (Requires Enterprise SKU) | **✓** |
| **Secure LDAP (LDAPS)** | **✓** | **✓** |
| **LDAP read** | **✓** | **✓** |
| **LDAP write** | **✓** (within the managed domain) | **✓** |
| **Geo-distributed deployments** | **✓** | **✓** |

## Domain Services and Microsoft Entra ID

Microsoft Entra ID lets you manage the identity of devices used by the organization and control access to corporate resources from those devices. Users can also register their personal device (a bring-your-own (BYO) model) with Microsoft Entra ID, which provides the device with an identity. Microsoft Entra ID then authenticates the device when a user signs in to Microsoft Entra ID and uses the device to access secured resources. The device can be managed using Mobile Device Management (MDM) software like Microsoft Intune. This management ability lets you restrict access to sensitive resources to managed and policy-compliant devices.

Traditional computers and laptops can also join to Microsoft Entra ID. This mechanism offers the same benefits of registering a personal device with Microsoft Entra ID, such as to allow users to sign in to the device using their corporate credentials.

Microsoft Entra joined devices give you the following benefits:

- Single-sign-on (SSO) to applications secured by Microsoft Entra ID.
- Enterprise policy-compliant roaming of user settings across devices.
- Access to the Windows Store for Business using corporate credentials.
- Windows Hello for Business.
- Restricted access to apps and resources from devices compliant with corporate policy.

Devices can be joined to Microsoft Entra ID with or without a hybrid deployment that includes an on-premises AD DS environment. The following table outlines common device ownership models and how they would typically be joined to a domain:

| **Type of device** | **Device platforms** | **Mechanism** |
| --- | --- | --- |
| Personal devices | Windows 10, iOS, Android, macOS | Microsoft Entra registered |
| Organization-owned device not joined to on-premises AD DS | Windows 10 | Microsoft Entra joined |
| Organization-owned device joined to an on-premises AD DS | Windows 10 | Microsoft Entra hybrid joined |

On a Microsoft Entra joined or registered device, user authentication happens using modern OAuth / OpenID Connect based protocols. These protocols are designed to work over the internet, so are great for mobile scenarios where users access corporate resources from anywhere.

With Domain Services-joined devices, applications can use the Kerberos and NTLM protocols for authentication, so can support legacy applications migrated to run on Azure VMs as part of a lift-and-shift strategy. The following table outlines differences in how the devices are represented and can authenticate themselves against the directory:

| **Aspect** | **Microsoft Entra joined** | **Domain Services-joined** |
| --- | --- | --- |
| Device controlled by | Microsoft Entra ID | Domain Services managed domain |
| Representation in the directory | Device objects in the Microsoft Entra directory | Computer objects in the Domain Services managed domain |
| Authentication | OAuth / OpenID Connect based protocols | Kerberos and NTLM protocols |
| Management | Mobile Device Management (MDM) software like Intune | Group Policy |
| Networking | Works over the internet | Must be connected to, or peered with, the virtual network where the managed domain is deployed |
| Great for... | End-user mobile or desktop devices | Server VMs deployed in Azure |

If on-premises AD DS and Microsoft Entra ID are configured for federated authentication using AD FS, then there's no (current/valid) password hash available in Azure DS. Microsoft Entra user accounts created before fed auth was implemented might have an old password hash but this likely doesn't match a hash of their on-premises password. As a result, Domain Services won't be able to validate the users credentials