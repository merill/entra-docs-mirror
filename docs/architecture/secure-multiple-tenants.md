---
layout: Conceptual
title: Resource isolation with multiple tenants to secure with Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/secure-multiple-tenants
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Introduction to resource isolation with multiple tenants in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2022-07-05T00:00:00.0000000Z
ms.reviewer: gasinh
ms.subservice: architecture
locale: en-us
document_id: 4ca77e3f-dd92-78a5-e5c9-cd34e56383c9
document_version_independent_id: fadbbd04-975d-b1b5-5935-65f29602e8d6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/secure-multiple-tenants.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/secure-multiple-tenants
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/secure-multiple-tenants.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 43fd4c77-bd60-2115-923f-d63f9f9f0116
---

# Resource isolation with multiple tenants to secure with Microsoft Entra ID - Microsoft Entra | Microsoft Learn

There are specific scenarios when delegating administration in a single tenant boundary doesn't meet your needs. In this section, there are requirements that may drive you to create a multi-tenant architecture. Multi-tenant organizations might span two or more Microsoft Entra tenants. This can result in unique cross-tenant collaboration and management requirements. Multi-tenant architectures increase management overhead and complexity and should be used with caution. We recommend using a single tenant if your needs can be met with that architecture. For more detailed information, see [Multi-tenant user management](multi-tenant-user-management-introduction).

A separate tenant creates a new boundary, and therefore decoupled management of Microsoft Entra directory roles, directory objects, Conditional Access policies, Azure resource groups, Azure management groups, and other controls as described in previous sections.

A separate tenant is useful for an organization's IT department to validate tenant-wide changes in Microsoft services such as, Intune, Microsoft Entra Connect, or a hybrid authentication configuration while protecting an organization's users and resources. This includes testing service configurations that might have tenant-wide effects and can't be scoped to a subset of users in the production tenant.

Deploying a non-production environment in a separate tenant might be necessary during development of custom applications that can change data of production user objects with MS Graph or similar APIs (for example, applications that are granted Directory.ReadWrite.All, or similar wide scope).

Note

Microsoft Entra Connect synchronization to multiple tenants, which might be useful when deploying a non-production environment in a separate tenant. For more information, see [Microsoft Entra Connect: Supported topologies](../identity/hybrid/connect/plan-connect-topologies).

## Outcomes

In addition to the outcomes achieved with a single tenant architecture as described previously, organizations can fully decouple the resource and tenant interactions:

### Resource separation

- **Visibility** - Resources in a separate tenant can't be discovered or enumerated by users and administrators in other tenants. Similarly, usage reports and audit logs are contained within the new tenant boundary. This separation of visibility allows organizations to manage resources needed for confidential projects.
- **Object footprint** - Applications that write to Microsoft Entra ID and/or other Microsoft Online services through Microsoft Graph or other management interfaces can operate in a separate object space. This enables development teams to perform tests during the software development lifecycle without affecting other tenants.
- **Quotas** - Consumption of tenant-wide [Azure Quotas and Limits](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits) is separated from that of the other tenants.

### Configuration separation

A new tenant provides a separate set of tenant-wide settings that can accommodate resources and trusting applications that have requirements that need different configurations at the tenant level. Additionally, a new tenant provides a new set of Microsoft Online services such as Office 365.

### Administrative separation

A new tenant boundary involves a separate set of Microsoft Entra directory roles, which enables you to configure different sets of administrators.

## Common usage

The following diagram illustrates a common usage for resource isolation in multiple tenants: a pre-production or "sandbox" environment that requires more separation than can be achieved with delegated administration in a single tenant.

![Diagram that shows common usage scenario.](media/secure-multiple-tenants/multiple-tenant-common-scenario.png)

Contoso is an organization that augmented their corporate tenant architecture with a pre-production tenant called ContosoSandbox.com. The sandbox tenant is used to support ongoing development of enterprise solutions that write to Microsoft Entra ID and Microsoft 365 using Microsoft Graph. These solutions are deployed in the corporate tenant.

The sandbox tenant is brought online to prevent those applications under development from impacting production systems either directly or indirectly, by consuming tenant resources and affecting quotas, or throttling.

Developers require access to the sandbox tenant during the development lifecycle, ideally with self-service access requiring additional permissions that are restricted in the production environment. Examples of these additional permissions might include creating, deleting, and updating user accounts, registering applications, provisioning and deprovisioning Azure resources, and changes to policies or overall configuration of the environment.

In this example, Contoso uses [Microsoft Entra B2B Collaboration](../external-id/what-is-b2b) to provision users from the corporate tenant to enable users that can manage and access resources in applications in the sandbox tenant without managing multiple credentials. This capability is primarily oriented to cross-organization collaboration scenarios. However, enterprises with multiple tenants like Contoso can use this capability to avoid additional credential lifecycle administration and user experience complexities.

Use [External Identities cross-tenant access](../external-id/cross-tenant-access-settings-b2b-collaboration) settings to manage how you collaborate with other Microsoft Entra organizations through B2B collaboration. These settings determine both the level of inbound access users in external Microsoft Entra organizations have to your resources, and the level of outbound access your users have to external organizations. They also let you trust multifactor authentication (MFA) and device claims ([compliant claims and Microsoft Entra hybrid joined claims](../identity/conditional-access/policy-alt-all-users-compliant-hybrid-or-mfa)) from other Microsoft Entra organizations. For details and planning considerations, see [Cross-tenant access in Microsoft Entra External ID](../external-id/cross-tenant-access-overview).

Another approach could have been to utilize the capabilities of Microsoft Entra Connect to sync the same on-premises Microsoft Entra credentials to multiple tenants, keeping the same password but differentiating on the users UPN domain.

## Multi-tenant resource isolation

With a new tenant, you have a separate set of administrators. Organizations can choose to use corporate identities through [Microsoft Entra B2B collaboration](../external-id/what-is-b2b). Similarly, organizations can implement [Azure Lighthouse](/en-us/azure/lighthouse/overview) for cross-tenant management of Azure resources so that non-production Azure subscriptions are managed by identities in the production counterpart. Azure Lighthouse can't be used to manage services outside of Azure, such as Microsoft Intune. For Managed Service Providers (MSPs), [Microsoft 365 Lighthouse](/en-us/microsoft-365/lighthouse/m365-lighthouse-overview?view=o365-worldwide&amp;preserve-view=true) is an admin portal that helps secure and manage devices, data, and users at scale for small- and medium-sized business (SMB) customers who are using Microsoft 365 Business Premium, Microsoft 365 E3, or Windows 365 Business.

This will allow users to continue to use their corporate credentials, while achieving the benefits of separation.

Microsoft Entra B2B collaboration in sandbox tenants should be configured to allow only identities from the corporate environment to be onboarded using Azure B2B [allow/deny lists](../external-id/allow-deny-list). For tenants that you do want to allow for B2B consider using External Identities cross-tenant access settings for cross tenant multifactor authentication\Device trust.

Important

Multi-tenant architectures with external identity access enabled provide only resource isolation, but don't enable identity isolation. Resource isolation using Microsoft Entra B2B collaboration and Azure Lighthouse don't mitigate risks related to identities.

If the sandbox environment shares identities with the corporate environment, the following scenarios are applicable to the sandbox tenant:

- A malicious actor that compromises a user, a device, or hybrid infrastructure in the corporate tenant, and is invited into the sandbox tenant, might gain access to the sandbox tenant's apps and resources.
- An operational error (for example, user account deletion or credential revocation) in the corporate tenant might affect the access of an invited user into the sandbox tenant.

You must do the risk analysis and potentially consider identity isolation through multiple tenants for business-critical resources that require a highly defensive approach. Azure Privileged Identity Management can help mitigate some of the risks by imposing extra security for accessing business critical tenants and resources.

### Directory objects

The tenant you use to isolate resources may contain the same types of objects, Azure resources, and trusting applications as your primary tenant. You may need to provision the following object types:

**Users and groups**: Identities needed by solution engineering teams, such as:

- Sandbox environment administrators.
- Technical owners of applications.
- Line-of-business application developers.
- Test end-user accounts.

These identities might be provisioned for:

- Employees who come with their corporate account through [Microsoft Entra B2B collaboration](../external-id/what-is-b2b).
- Employees who need local accounts for administration, emergency administrative access, or other technical reasons.

Customers who have or require non-production Active Directory on-premises can also synchronize their on-premises identities to the sandbox tenant if needed by the underlying resources and applications.

**Devices**: The non-production tenant contains a reduced number of devices to the extent that are needed in the solution engineering cycle:

- Administration workstations
- Non-production computers and mobile devices needed for development, testing, and documentation

### Applications

Microsoft Entra integrated applications: Application objects and service principals for:

- Test instances of the applications that are deployed in production (for example, applications that write to Microsoft Entra ID and Microsoft online services).
- Infrastructure services to manage and maintain the non-production tenant, potentially a subset of the solutions available in the corporate tenant.

Microsoft Online Services:

- Typically, the team that owns the Microsoft Online Services in production should be the one owning the non-production instance of those services.
- Administrators of non-production test environments shouldn't be provisioning Microsoft Online Services unless those services are specifically being tested. This avoids inappropriate use of Microsoft services, for example setting up production SharePoint sites in a test environment.
- Similarly, provisioning of Microsoft Online services that can be initiated by end users (also known as ad-hoc subscriptions) should be locked down. For more information, see [What is self-service sign-up for Microsoft Entra ID?](../identity/users/directory-self-service-signup).
- Generally, all non-essential license features should be disabled for the tenant using group-based licensing. This should be done by the same team that manages licenses in the production tenant, to avoid misconfiguration by developers who might not know the effect of enabling licensed features.

### Azure resources

Any Azure resources needed by trusting applications may also be deployed. For example, databases, virtual machines, containers, Azure functions, and so on. For your sandbox environment, you must weigh the cost savings of using less-expensive SKUs for products and services with the less security features available.

The RBAC model for access control should still be employed in a non-production environment in case changes are replicated to production after tests have concluded. Failure to do so allows security flaws in the non-production environment to propagate to your production tenant.

## Resource and identity isolation with multiple tenants

### Isolation outcomes

There are limited situations where resource isolation can't meet your requirements. You can isolate both resources and identities in a multi-tenant architecture by disabling all cross-tenant collaboration capabilities and effectively building a separate identity boundary. This approach is a defense against operational errors and compromise of user identities, devices, or hybrid infrastructure in corporate tenants.

### Isolation common usage

A separate identity boundary is typically used for business-critical applications and resources such as customer-facing services. In this scenario, Fabrikam has decided to create a separate tenant for their customer-facing SaaS product to avoid the risk of employee identity compromise affecting their SaaS customers. The diagram above illustrates the boundary between Fabrikam and FabrikamSaaS. The FabrikamSaaS tenant contains the environments used for applications that are offered to customers as part of Fabrikam's business model.

### Isolation of directory objects

The directory objects in FabrikamSaas are as follows:

Users and groups: Identities needed by solution IT teams, customer support staff, or other necessary personnel are created within the SaaS tenant. To preserve isolation, only local accounts are used, and Microsoft Entra B2B collaboration isn't enabled.

Azure AD B2C directory objects: If the tenant environments are accessed by customers, it may contain an Azure AD B2C tenant and its associated identity objects. Subscriptions that hold these directories are good candidates for an isolated consumer-facing environment.

Devices: This tenant contains a reduced number of devices; only those that are needed to run customer-facing solutions:

- Secure administration workstations.
- Support personnel workstations (this can include engineers who are "on call" as described above).

### Isolation of applications

**Microsoft Entra integrated applications**: Application objects and service principals for:

- Production applications (for example, multi-tenant application definitions).
- Infrastructure services to manage and maintain the customer-facing environment.

**Azure Resources**: Hosts the IaaS, PaaS and SaaS resources of the customer-facing production instances.