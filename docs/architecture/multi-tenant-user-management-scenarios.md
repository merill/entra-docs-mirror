---
layout: Conceptual
title: Common scenarios for using multitenant user management in Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/multi-tenant-user-management-scenarios
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn about common scenarios where guest accounts can be used to configure user access across Microsoft Entra tenants
ms.topic: concept-article
ms.date: 2024-08-25T00:00:00.0000000Z
ms.custom: it-pro, seodec18, has-azure-ad-ps-ref, azure-ad-ref-level-one-done
ms.subservice: architecture
locale: en-us
document_id: 67954a82-e3c5-e9bb-2ba6-79ae2724bdfd
document_version_independent_id: cbc91c42-e63e-c39b-a2e8-393166cddd92
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/multi-tenant-user-management-scenarios.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/multi-tenant-user-management-scenarios
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/multi-tenant-user-management-scenarios.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: d7caa201-0abb-31ce-bca9-79899514c610
---

# Common scenarios for using multitenant user management in Microsoft Entra ID - Microsoft Entra | Microsoft Learn

This article is the second in a series of articles that provide guidance for configuring and providing user lifecycle management in Microsoft Entra multitenant environments. The following articles in the series provide more information as described.

- [Multitenant user management introduction](multi-tenant-user-management-introduction) is the first in the series of articles that provide guidance for configuring and providing user lifecycle management in Microsoft Entra multitenant environments.
- [Common considerations for multitenant user management](multi-tenant-common-considerations) provides guidance for these considerations: cross-tenant synchronization, directory object, Microsoft Entra Conditional Access, additional access control, and Office 365.
- [Common solutions for multitenant user management](multi-tenant-common-solutions) when single tenancy doesn't work for your scenario, this article provides guidance for these challenges: automatic user lifecycle management and resource allocation across tenants, sharing on-premises apps across tenants.

The guidance helps to you achieve a consistent state of user lifecycle management. Lifecycle management includes provisioning, managing, and deprovisioning users across tenants using the available Azure tools that include [Microsoft Entra B2B collaboration](../external-id/what-is-b2b) (B2B) and [cross-tenant synchronization](../identity/multi-tenant-organizations/cross-tenant-synchronization-overview).

This article describes three scenarios for which you can use multitenant user management features.

- End user-initiated
- Scripted
- Automated

## End user-initiated scenario

In end user-initiated scenarios, resource tenant administrators delegate certain abilities to users in the tenant. Administrators enable end users to invite external users to the tenant, an app, or a resource. You can invite users from the home tenant or they can individually sign up.

For example, a global professional services firm collaborates with subcontractors on projects. Subcontractors (external users) require access to the firm's applications and documents. Firm admins can delegate to its end users the ability to invite subcontractors or configure self-service for subcontractor resource access.

### Provisioning accounts

Here are the most widely used ways to invite end users to access tenant resources.

- [**Application-based invitations.**](../external-id/what-is-b2b) Microsoft applications (such as Teams and SharePoint) can enable external user invitations. Configure B2B invitation settings in both Microsoft Entra B2B and in the relevant applications.
- [**MyApps.**](../identity/enterprise-apps/myapps-overview) Users can invite and assign external users to applications using MyApps. The user account must have [application self-service sign up](../identity/enterprise-apps/manage-self-service-access) approver permissions. Group owners can invite external users to their groups.
- [**Entitlement management.**](../id-governance/entitlement-management-overview) Enable admins or resource owners to create access packages with resources, allowed external organizations, external user expiration, and access policies. Publish access packages to enable external user self-service sign-up for resource access.
- [**Azure portal.**](../external-id/add-users-administrator) End users with the [Guest Inviter role](../external-id/external-collaboration-settings-configure) can sign in to the Azure portal and invite external users from the **Users** menu in Microsoft Entra ID.
- [**Programmatic (PowerShell, Graph API).**](../external-id/customize-invitation-api) End users with the [Guest Inviter role](../external-id/external-collaboration-settings-configure) can use PowerShell or Graph API to invite external users.

### Redeeming invitations

When you provision accounts to access a resource, email invitations go to the invited user's email address.

When an invited user receives an invitation, they can follow the link contained in the email to the redemption URL. In doing so, the invited user can approve or deny the invitation and, if necessary, create an external user account.

Invited users can also try to directly access the resource, referred to as just-in-time (JIT) redemption, if either of the following scenarios are true.

- The invited user already has a Microsoft Entra ID or Microsoft account, or
- Admins have enabled [email one-time passcodes](../external-id/one-time-passcode).

During JIT redemption, the following considerations might apply.

- If administrators haven't [suppressed consent prompts](../external-id/cross-tenant-access-settings-b2b-collaboration), the user must consent before accessing the resource.
- You can allow or block invitations to external users from specific organizations by using an [allowlist or a blocklist](../external-id/allow-deny-list).

For more information, see [Microsoft Entra B2B collaboration invitation redemption](../external-id/redemption-experience).

### Enabling one-time passcode authentication

In scenarios where you allow for ad hoc B2B, enable [email one-time passcode authentication](../external-id/one-time-passcode). This feature authenticates external users when you can't authenticate them through other means, such as:

- Microsoft Entra ID.
- Microsoft account.
- Gmail account through Google Federation.
- Account from a Security Assertion Markup Language (SAML)/WS-Fed IDP through Direct Federation.

With one-time passcode authentication, there's no need to create a Microsoft account. When the external user redeems an invitation or accesses a shared resource, they receive a temporary code at their email address. They then enter the code to continue signing in.

### Managing accounts

In the end user-initiated scenario, the resource tenant administrator manages external user accounts in the resource tenant (not updated based on the updated values in the home tenant). The only visible attributes received include the email address and display name.

You can configure more attributes on external user objects to facilitate different scenarios (such as entitlement scenarios). You can include populating the address book with contact details. For example, consider the following attributes.

- **HiddenFromAddressListsEnabled** [ShowInAddressList]
- **FirstName** [GivenName]
- **LastName** [SurName]
- **Title**
- **Department**
- **TelephoneNumber**

You might set these attributes to add external users to the global address list (GAL) and to people search (such as SharePoint People Picker). Other scenarios might require different attributes (such as setting entitlements and permissions for Access Packages, Dynamic Group Membership, and SAML Claims).

By default, the GAL hides invited external users. Set external user attributes to be unhidden to include them in the unified GAL. The Microsoft Exchange Online section of [Common considerations for multitenant user management](multi-tenant-common-considerations) describes how you can lessen limits by creating external member users instead of external guest users.

### Deprovisioning accounts

End user-initiated scenarios decentralize access decisions, which can create the challenge of deciding when to remove an external user and their associated access. [Entitlement management](../id-governance/entitlement-management-overview) and [access reviews](../id-governance/manage-guest-access-with-access-reviews) let you review and remove existing external users and their resource access.

When you invite users outside of entitlement management, you must create a separate process to review and manage their access. For example, if you directly invite an external user through SharePoint in Microsoft 365, it isn't in your entitlement management process.

## Scripted scenario

In the scripted scenario, resource tenant administrators deploy a scripted pull process to automate discovery and external user provisioning.

For example, a company acquires a competitor. Each company has a single Microsoft Entra tenant. They want the following Day One scenarios to work without users having to perform any invitation or redemption steps. All users must be able to:

- Use single sign-on to all provisioned resources.
- Find each other and resources in a unified GAL.
- Determine each other's presence and initiate chat.
- Access applications based on dynamic membership groups.

In this scenario, each organization's tenant is the home tenant for its existing employees while being the resource tenant for the other organization's employees.

### Provisioning accounts

With [Delta Query](/en-us/graph/delta-query-overview), tenant admins can deploy a scripted pull process to automate discovery and identity provisioning to support resource access. This process checks the home tenant for new users. It uses the B2B Graph APIs to provision new users as external users in the resource tenant as illustrated in the following multitenant topology diagram.

[!\[Diagram illustrates using B2B Graph APIs to provision new users as external users in the resource tenant.\](media/multi-tenant-user-management-scenarios/diagram-multi-tenant-scripted-scenario-inline.png)
 Diagram title: multitenant topology diagram. On the left, a box labeled Company A contains internal users and external users. On the right, a box labeled Company B contains internal users and external users. Between Company A and Company B, an interaction goes from Company A to Company B with the label, Script to pull A users to B. Another interaction goes from Company B to Company A with the label, Script to pull B users to A.](media/multi-tenant-user-management-scenarios/diagram-multi-tenant-scripted-scenario-expanded.png#lightbox)

- Tenant administrators prearrange credentials and consent to allow each tenant to read.
- Tenant administrators automate enumeration and pulling scoped users to the resource tenant.
- Use Microsoft Graph API with consented permissions to read and provision users with the invitation API.
- Initial provisioning can read source attributes and apply them to the target user object.

### Managing accounts

The resource organization may augment profile data to support sharing scenarios by updating the user's metadata attributes in the resource tenant. However, if ongoing synchronization is necessary, then a synchronized solution might be a better option.

### Deprovisioning accounts

[Delta Query](/en-us/graph/delta-query-overview) can signal when an external user needs to be deprovisioned. [Entitlement management](../id-governance/entitlement-management-overview) and [access reviews](../id-governance/manage-guest-access-with-access-reviews) can provide a way to review and remove existing external users and their access to resources.

If you invite users outside of entitlement management, create a separate process to review and manage external user access. For example, if you invite the external user directly through SharePoint in Microsoft 365, it isn't in your entitlement management process.

## Automated scenario

Synchronized sharing across tenants is the most complex of the patterns described in this article. This pattern enables more automated management and deprovisioning options than end user-initiated or scripted.

In automated scenarios, resource tenant admins use an identity provisioning system to automate provisioning and deprovisioning processes. In scenarios within Microsoft's Commercial Cloud instance, we have [cross-tenant synchronization](https://techcommunity.microsoft.com/t5/microsoft-entra-azure-ad-blog/seamless-application-access-and-lifecycle-management-for-multi/ba-p/3728752). In scenarios that span Microsoft Sovereign Cloud instances, you need other approaches because cross-tenant synchronization doesn't yet support cross-cloud.

For example, within a Microsoft Commercial Cloud instance, a multinational/regional conglomeration has multiple subsidiaries with the following requirements.

- Each has their own Microsoft Entra tenant and need to work together.
- In addition to synchronizing new users among tenants, automatically synchronize attribute updates and automate deprovisioning.
- If an employee is no longer at a subsidiary, remove their account from all other tenants during the next synchronization.

In an expanded, cross-cloud scenario, a Defense Industrial Base (DIB) contractor has a defense-based and commercial-based subsidiary. These have competing regulation requirements:

- The US defense business resides in a US Sovereign Cloud tenant such as Microsoft 365 US Government GCC High and Azure Government.
- The commercial business resides in a separate Microsoft Entra tenant in Commercial such as a Microsoft Entra environment running on the global Azure cloud.

To act like a single company deployed into a cross-cloud architecture, all users synchronize to both tenants. This approach enables unified GAL availability across both tenants and might ensure that users automatically synchronized to both tenants include entitlements and restrictions to applications and content. Example requirements include:

- US employees might have ubiquitous access to both tenants.
- Non-US employees show in the unified GAL of both tenants but don't have access to protected content in the GCC High tenant.

This scenario requires automatic synchronization and identity management to configure users in both tenants while associating them with the proper entitlement and data protection policies.

[Cross-cloud B2B](https://techcommunity.microsoft.com/t5/microsoft-entra-azure-ad-blog/collaborate-securely-across-organizational-boundaries-and/ba-p/3094109) requires you to configure [Cross-Tenant Access Settings](../external-id/cross-cloud-settings) for each organization with which you want to collaborate in the remote cloud instance.

### Provisioning accounts

This section describes three techniques for automating account provisioning in the automated scenario.

#### Technique 1: Use the [built-in cross-tenant synchronization capability in Microsoft Entra ID](../identity/multi-tenant-organizations/cross-tenant-synchronization-overview)

This approach only works when all tenants that you need to synchronize are in the same cloud instance (such as Commercial to Commercial).

#### Technique 2: Provision accounts with Microsoft Identity Manager

Use an external Identity and Access Management (IAM) solution such as [Microsoft Identity Manager (MIM)](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016) as a synchronization engine.

This advanced deployment uses MIM as a synchronization engine. MIM calls the [Microsoft Graph API](https://developer.microsoft.com/graph) and [Exchange Online PowerShell](/en-us/powershell/exchange/exchange-online-powershell?view=exchange-ps&amp;preserve-view=true). Alternative implementations can include the cloud-hosted [Active Directory Synchronization Service (ADSS)](/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview) managed service offering. There are non-Microsoft offerings that you can create from scratch with other IAM offerings (such as SailPoint, Omada, and OKTA).

You perform a cloud-to-cloud synchronization of identity (users, contacts, and groups) from one tenant to another as illustrated in the following diagram.

[!\[Diagram illustrates cloud-to-cloud synchronization of identity, such as users, contacts, and groups, from one tenant to another.\](media/multi-tenant-user-management-scenarios/diagram-cloud-to-cloud-sync-inline.png)
 Diagram title: Cloud-to-cloud identity synchronization. On the left, a box labeled Company A contains internal users and external users. On the right, a box labeled Company B contains internal users and external users. Between Company A and Company B, sync engine interactions go from Company A to Company B and from Company B to Company A.](media/multi-tenant-user-management-scenarios/diagram-cloud-to-cloud-sync-expanded.png#lightbox)

Considerations that are outside the scope of this article include integration of on-premises applications.

#### Technique 3: Provision accounts with Microsoft Entra Connect

This technique only applies for complex organizations that manage all identity in traditional Windows Server-based Active Directory Domain Services (AD DS). The approach uses Microsoft Entra Connect as the synchronization engine as illustrated in the following diagram.

[!\[Diagram illustrates an approach to provisioning accounts that uses Microsoft Entra Connect as the synchronization engine.\](media/multi-tenant-user-management-scenarios/diagram-sync-engine-inline.png)
 Diagram title: Provision accounts with Microsoft Entra Connect. The diagram shows four main components. A box on the left represents the Customer. A cloud shape on the right represents B2B Conversion. At the top center, a box containing a cloud shape represents Microsoft Commercial Cloud. At the bottom center, a box containing a cloud shape represents Microsoft US Government Sovereign Cloud. Inside the Customer box, a Windows Server Active Directory icon connects to two boxes, each with a Microsoft Entra Connect label. The connections are dashed red lines with arrows at both ends and a refresh icon. Inside the Microsoft Commercial Cloud shape is another cloud shape that represents Microsoft Azure Commercial. Inside is another cloud shape that represents Microsoft Entra ID. To the right of the Microsoft Azure Commercial cloud shape is a box that represents Office 365 with a label, Public Multitenant. A solid red line with arrows at both ends connects the Office 365 box with the Microsoft Azure Commercial cloud shape and a label, Hybrid Workloads. Two dashed lines connect from the Office 365 box to the Microsoft Entra cloud shape. One has an arrow on the end that connects to Microsoft Entra ID. The other has arrows on both ends. A dashed line with arrows on both ends connects the Microsoft Entra cloud shape to the top Customer Microsoft Entra Connect box. A dashed line with arrows on both ends connects the Microsoft Commercial Cloud shape to the B2B Conversion cloud shape. Inside the Microsoft US Government Sovereign Cloud box is another cloud shape that represents Microsoft Azure Government. Inside is another cloud shape that represents Microsoft Entra ID. To the right of the Microsoft Azure Commercial cloud shape is a box that represents Office 365 with a label, US Gov GCC-High L4. A solid red line with arrows at both ends connects the Office 365 box with the Microsoft Azure Government cloud shape and a label, Hybrid Workloads. Two dashed lines connect from the Office 365 box to the Microsoft Entra cloud shape. One has an arrow on the end that connects to Microsoft Entra ID. The other has arrows on both ends. A dashed line with arrows on both ends connects the Microsoft Entra cloud shape to the bottom Customer Microsoft Entra Connect box. A dashed line with arrows on both ends connects the Microsoft Commercial Cloud shape to the B2B Conversion cloud shape.](media/multi-tenant-user-management-scenarios/diagram-sync-engine-expanded.png#lightbox)

Unlike the MIM technique, all identity sources (users, contacts, and groups) come from traditional Windows Server-based Active Directory Domain Services (AD DS). The AD DS directory is typically an on-premises deployment for a complex organization that manages identity for multiple tenants. Cloud-only identity isn't in scope for this technique. All identity must be in AD DS to include them in scope for synchronization.

Conceptually, this technique synchronizes a user into a home tenant as an internal member user (default behavior). Alternatively, it might synchronize a user into a resource tenant as an external user (customized behavior).

Microsoft supports this dual sync user technique with careful considerations to what modifications occur in the Microsoft Entra Connect configuration. For example, if you make modifications to the wizard-driven setup configuration, you need to document the changes if you must rebuild the configuration during a support incident.

Out of the box, Microsoft Entra Connect can't synchronize an external user. You must augment it with an external process (such as a PowerShell script) to convert the users from internal to external accounts.

Benefits of this technique include Microsoft Entra Connect synchronizing identity with attributes stored in AD DS. Synchronization might include address book attributes, manager attributes, group memberships, and other hybrid identity attributes into all tenants within scope. It deprovisions identity in alignment with AD DS. It doesn't require a more complex IAM solution to manage the cloud identity for this specific task.

There's a one-to-one relationship of Microsoft Entra Connect per tenant. Each tenant has its own configuration of Microsoft Entra Connect that you can individually alter to support member or external user account synchronization.

### Choosing the right topology

Most customers use one of the following topologies in automated scenarios.

- A mesh topology enables sharing of all resources in all tenants. You create users from other tenants in each resource tenant as external users.
- A single resource tenant topology uses a single tenant (the resource tenant), in which users from other tenants are external users.

Reference the following table as a decision tree while you design your solution. Following the table, diagrams illustrate both topologies to help you determine which is right for your organization.

#### Comparison of mesh versus single resource tenant topologies

| Consideration | Mesh topology | Single resource tenant |
| --- | --- | --- |
| Each company has separate Microsoft Entra tenant with users and resources | Yes | Yes |
| **Resource location and collaboration** |  |  |
| Shared apps and other resources remain in their current home tenant | Yes | No. You can share only apps and other resources in the resource tenant. You can't share apps and other resources remaining in other tenants. |
| All viewable in individual company's GALs (Unified GAL) | Yes | No |
| **Resource access and administration** |  |  |
| You can share ALL applications connected to Microsoft Entra ID among all companies. | Yes | No. Only applications in the resource tenant are shared. You can't share applications remaining in other tenants. |
| Global resource administration | Continue at tenant level. | Consolidated in the resource tenant. |
| Licensing: Office 365 SharePoint in Microsoft 365, unified GAL, Teams access all support guests; however, other Exchange Online scenarios don't. | Continues at tenant level. | Continues at tenant level. |
| Licensing: [Microsoft Entra ID (premium)](../external-id/external-identities-pricing) | First 50 K Monthly Active Users are free (per tenant). | First 50 K Monthly Active Users are free. |
| Licensing: software as a service (SaaS) apps | Remain in individual tenants, might require licenses per user per tenant. | All shared resources reside in the single resource tenant. You can investigate consolidating licenses to the single tenant if appropriate. |

#### Mesh topology

The following diagram illustrates mesh topology.

[!\[Diagram illustrates mesh topology.\](media/multi-tenant-user-management-scenarios/diagram-mesh-topology-inline.png)
 Diagram title: Mesh topology. On the top left, a box labeled Company A contains internal users and external users. On the top right, a box labeled Company B contains internal users and external users. On the bottom left, a box labeled Company C contains internal users and external users. On the bottom right, a box labeled Company D contains internal users and external users. Between Company A and Company B and between Company C and Company D, sync engine interactions go between the companies on the left and the companies on the right.](media/multi-tenant-user-management-scenarios/diagram-mesh-topology-expanded.png#lightbox)

In a mesh topology, every user in each home tenant synchronizes to each of the other tenants, which become resource tenants.

- You can share any resource within a tenant with external users.
- Each organization can see all users in the conglomerate. In the above diagram, there are four unified GALs, each of which contains the home users and the external users from the other three tenants.

[Common considerations for multitenant user management](multi-tenant-common-considerations) provides information on provisioning, managing, and deprovisioning users in this scenario.

#### Mesh topology for cross-cloud

You can use the mesh topology in as few as two tenants, such as in the scenario for a DIB defense contractor straddling a cross-sovereign cloud solution. As with the mesh topology, each user in each home tenant synchronizes to the other tenant, which becomes a resource tenant. In the Technique 3 section diagram, the public Commercial tenant internal user synchronizes to the US sovereign GCC High tenant as an external user account. At the same time, the GCC High internal user synchronizes to Commercial as an external user account.

The diagram also illustrates data storage locations. Data categorization and compliance is outside the scope of this article, but you can include entitlements and restrictions to applications and content. Content might include locations where an internal user's user-owned data resides (such as data stored in an Exchange Online mailbox or OneDrive). The content might be in their home tenant and not in the resource tenant. Shared data might reside in either tenant. You can restrict access to the content through access control and Conditional Access policies.

#### Single resource tenant topology

The following diagram illustrates single resource tenant topology.

[!\[Diagram illustrates a single resource tenant topology.\](media/multi-tenant-user-management-scenarios/diagram-single-resource-tenant-scenario-inline.png)
 Diagram title: Single resource tenant topology. At the top, a box that represents Company A contains three boxes. On the left, a box represents all shared resources. In the middle, a box represents internal users. On the right, a box represents external users. Below the Company A box is a box that represents the sync engine. Three arrows connect the sync engine to Company A. Below the sync engine box, at the bottom of the diagram, are three boxes that represent Company B, Company C, and Company D. An arrow connects each of them to the sync engine box. Inside each of the bottom company boxes is a label, Microsoft Graph API Exchange Online PowerShell, and icons that represent internal users.](media/multi-tenant-user-management-scenarios/diagram-single-resource-tenant-scenario-expanded.png#lightbox)

In a single resource tenant topology, users and their attributes synchronize to the resource tenant (Company A in the above diagram).

- All resources shared among the member organizations must reside in the single resource tenant. If multiple subsidiaries have subscriptions to the same SaaS apps, there's an opportunity to consolidate those subscriptions.
- Only the GAL in the resource tenant displays users from all companies.

### Managing accounts

This solution detects and syncs attribute changes from source tenant users to resource tenant external users. You can use these attributes to make authorization decisions (such as when you're using dynamic membership groups).

### Deprovisioning accounts

Automation detects object deletion in the source environment and deletes the associated external user object in the target environment.

[Common considerations for multitenant user management](multi-tenant-common-considerations) provides additional information on provisioning, managing, and deprovisioning users in this scenario.