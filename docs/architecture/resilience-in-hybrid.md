---
layout: Conceptual
title: Build more resilient hybrid authentication in Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-in-hybrid
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: A guide for architects and IT administrators on building a resilient hybrid infrastructure.
ms.topic: concept-article
ms.date: 2022-11-16T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: ceb73aa3-30c9-4ee6-f612-726e7fcab9c6
document_version_independent_id: 25d263e2-ec9b-c010-9d0a-6d7f48c9a323
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-in-hybrid.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-in-hybrid
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-in-hybrid.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 92b3602c-4427-bca7-00fa-b7c05447a8a3
---

# Build more resilient hybrid authentication in Microsoft Entra ID - Microsoft Entra | Microsoft Learn

A hybrid infrastructure includes both cloud and on premises components. Hybrid authentication allows users to access cloud-based resources with their identities originating on premises, or to access on-premises resources with cloud-based identities.

- Cloud components include Microsoft Entra ID, Azure resources and services, your organization's cloud-based apps, and SaaS applications.
- on premises components include on premises applications, resources like SQL databases, and an identity provider like Windows Server Active Directory.

Important

As you plan for resilience in your hybrid infrastructure, it's key to minimize dependencies and single points of failure. On premises and cloud connectivity disruption can occur for many reasons, including hardware failure, power outages, natural disasters, and malware attacks.

Microsoft offers multiple mechanisms for hybrid authentication for applications connected to Microsoft Entra. If your organization has been relying upon Active Directory passwords and pass-through authentication or federation to authenticate users, we recommend that you implement password hash synchronization, if possible.

- [Password hash synchronization (PHS)](../identity/hybrid/connect/whatis-phs) uses Microsoft Entra Connect to sync the identity and a hash-of-the-hash of the password from Windows Server AD to Microsoft Entra ID. It enables users to sign in to Microsoft Entra to access cloud-based resources with the same password as it set in Active Directory. PHS has dependencies on AD only during synchronization, not during authentication.
- [Pass-through Authentication (PTA)](../identity/hybrid/connect/how-to-connect-pta) redirects users to Microsoft Entra ID for sign-in. Then, the username and password are validated against Active Directory on premises through an agent that is deployed in the corporate network. PTA has a footprint of its Microsoft Entra PTA agents that reside on servers on premises. Those servers must be reachable during authentication and must be able to reach a domain controller.
- [Federation](../identity/hybrid/connect/whatis-fed) customers deploy a federation service such as Active Directory Federation Services (AD FS) as an identity provider. Microsoft Entra ID redirects users to authenticate to the identity provider federation service, then validates the SAML assertion produced by the federation service. The user must be able to connect to the identity provider, and the identity provider may also rely upon Active Directory.
- [Microsoft Entra certificate-based authentication(CBA)](../identity/authentication/concept-certificate-based-authentication) enables Microsoft Entra to authenticate users using X.509 certificates issued by an Enterprise Public Key Infrastructure (PKI) stored in Active Directory, Microsoft Entra ID, or both. Using Microsoft Entra CBA, customers can simplify and reduce dependencies on on-premises components by eliminating the need for Active Directory Federation Services (AD FS).

You may be using one or more of these methods in your organization. For more information, see [Choose the right authentication method for your Microsoft Entra hybrid identity solution](../identity/hybrid/connect/choose-ad-authn). This article contains a decision tree that can help you decide on your methodology.

## Password hash synchronization

The simplest and most resilient hybrid authentication option for Microsoft Entra ID is [Password Hash Synchronization](../identity/hybrid/connect/whatis-phs). It doesn't have any on premises identity infrastructure dependency when processing authentication requests. After identities with password hashes are synchronized to Microsoft Entra ID, users can authenticate to Microsoft Entra and cloud resources with no dependency on the on-premises identity components.

![Architecture diagram of PHS](media/resilience-in-hybrid/admin-resilience-password-hash-sync.png)

If you choose this authentication option, you won't experience disruption for access to Microsoft Entra and other cloud resources when on premises identity components become unavailable.

### How do I implement PHS?

To implement PHS, see the following resources:

- [Implement password hash synchronization with Microsoft Entra Connect](../identity/hybrid/connect/how-to-connect-password-hash-synchronization)
- [Enable password hash synchronization](../identity/hybrid/connect/how-to-connect-password-hash-synchronization)

If your requirements are such that you can't use PHS, use Pass-through Authentication.

## Pass-through Authentication

Pass-through Authentication has a dependency on authentication agents that reside on premises on servers. A persistent connection, or service bus, is present between Microsoft Entra ID and the on-premises PTA agents. The firewall, servers hosting the authentication agents, and the on-premises Windows Server Active Directory (or other identity provider) are all potential failure points.

![Architecture diagram of PTA](media/resilience-in-hybrid/admin-resilience-pass-through-authentication.png)

### How do I implement PTA?

To implement Pass-through Authentication, see the following resources.

- [How Pass-through Authentication works](../identity/hybrid/connect/how-to-connect-pta-how-it-works)
- [Pass-through Authentication security deep dive](../identity/hybrid/connect/how-to-connect-pta-security-deep-dive)
- [Install Microsoft Entra pass-through authentication](../identity/hybrid/connect/how-to-connect-pta-quick-start)
- If you're using PTA, define a [highly available topology](../identity/hybrid/connect/how-to-connect-pta-quick-start).

## Federation

Federation involves the creation of a trust relationship between Microsoft Entra ID and the federation service, which includes the exchange of endpoints, token signing certificates, and other metadata. When a request comes to Microsoft Entra ID, it reads the configuration and redirects the user to the endpoints configured. At that point, the user interacts with the federation service, which issues a SAML assertion that is validated by Microsoft Entra ID.

The following diagram shows a topology of an enterprise AD FS deployment that includes redundant federation and web application proxy servers across multiple on premises data centers. This configuration relies on enterprise networking infrastructure components like DNS, Network Load Balancing with geo-affinity capabilities, and firewalls. All on premises components and connections are susceptible to failure. Visit the [AD FS Capacity Planning Documentation](/en-us/windows-server/identity/ad-fs/design/planning-for-ad-fs-server-capacity) for more information.

Note

Federation has a high number of on premises dependencies. While this diagram shows AD FS, other on premises identity providers are subject to similar design considerations to achieve high availability, scalability, and fail over.

![Architecture diagram of federation](media/resilience-in-hybrid/admin-resilience-federation.png)

### How do I implement federation?

If you're implementing a federated authentication strategy or want to make it more resilient, see the following resources.

- [What is federated authentication](../identity/hybrid/connect/whatis-fed)
- [How federation works](../identity/hybrid/connect/how-to-connect-fed-whatis)
- [Microsoft Entra federation compatibility list](../identity/hybrid/connect/how-to-connect-fed-compatibility)
- Follow the [AD FS capacity planning documentation](/en-us/windows-server/identity/ad-fs/design/planning-for-ad-fs-server-capacity)
- [Deploying AD FS in Azure IaaS](/en-us/windows-server/identity/ad-fs/deployment/how-to-connect-fed-azure-adfs)
- [Enable PHS](../identity/hybrid/connect/tutorial-phs-backup) along with your federation

## Related architecture resources

For more architecture and deployment guidance related to hybrid identity, see:

- [Microsoft Entra deployment plans](deployment-plans) — deployment guidance for authentication, apps, devices, and hybrid scenarios
- [Microsoft Entra architecture overview](architecture) — service design, scalability, continuous availability, and datacenter architecture
- [Identity and access management architecture in Azure](/en-us/azure/architecture/identity/identity-start-here) — reference architectures, baseline implementations, and design guidance for hybrid identity
- [Integrate on-premises AD with Microsoft Entra ID](/en-us/azure/architecture/reference-architectures/identity/azure-ad) — full reference architecture with downloadable Visio diagrams
- [Choose the right authentication method](../identity/hybrid/connect/choose-ad-authn) — authentication decision tree for hybrid identity solutions
- [Data residency for Microsoft Entra ID](../fundamentals/data-residency) — data storage locations, sovereign clouds, and environment constraints