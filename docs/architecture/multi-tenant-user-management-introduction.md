---
layout: Conceptual
title: Configuring multitenant user management in Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/multi-tenant-user-management-introduction
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn about the different patterns used to configure user access across Microsoft Entra tenants with guest accounts
ms.topic: concept-article
ms.date: 2023-04-19T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: b93d6eda-7ae1-c4c2-708a-d64a36dbf516
document_version_independent_id: 5792d6bf-fc03-ee93-b243-c0c092ac6e09
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/multi-tenant-user-management-introduction.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/multi-tenant-user-management-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/multi-tenant-user-management-introduction.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 36d11fec-17ad-18bd-3900-568b96483c4d
---

# Configuring multitenant user management in Microsoft Entra ID - Microsoft Entra | Microsoft Learn

This article is the first in a series of articles that provide guidance for configuring and providing user lifecycle management in Microsoft Entra multitenant environments. The following articles in the series provide more information as described.

- [Multitenant user management scenarios](multi-tenant-user-management-scenarios) describes three scenarios for which you can use multitenant user management features: end user-initiated, scripted, and automated.
- [Common considerations for multitenant user management](multi-tenant-common-considerations) provides guidance for these considerations: cross-tenant synchronization, directory object, Microsoft Entra Conditional Access, additional access control, and Office 365.
- [Common solutions for multitenant user management](multi-tenant-common-solutions) when single tenancy doesn't work for your scenario, this article provides guidance for these challenges: automatic user lifecycle management and resource allocation across tenants, sharing on-premises apps across tenants.

The guidance helps to you achieve a consistent state of user lifecycle management. Lifecycle management includes provisioning, managing, and deprovisioning users across tenants using the available Azure tools that include [Microsoft Entra B2B collaboration](../external-id/what-is-b2b) (B2B) and [cross-tenant synchronization](../identity/multi-tenant-organizations/cross-tenant-synchronization-overview).

Provisioning users into a single Microsoft Entra tenant provides a unified view of resources and a single set of policies and controls. This approach enables consistent user lifecycle management.

Microsoft recommends a single tenant when possible. Having multiple tenants can result in unique cross-tenant collaboration and management requirements. When consolidation to a single Microsoft Entra tenant isn't possible, multitenant organizations might span two or more Microsoft Entra tenants for reasons that include the following.

- Mergers
- Acquisitions
- Divestitures
- Collaboration across public, sovereign, and regional clouds
- Political or organizational structures that prohibit consolidation to a single Microsoft Entra tenant

## Microsoft Entra B2B collaboration

Microsoft Entra B2B collaboration (B2B) enables you to securely share your company's applications and services with external users. When users can come from any organization, B2B helps you maintain control over access to your IT environment and data.

You can use B2B collaboration to provide external access for your organization's users to access multiple tenants that you manage. Traditionally, B2B external user access can authorize access to users that your own organization doesn't manage. However, external user access can manage access across multiple tenants that your organization manages.

An area of confusion with Microsoft Entra B2B collaboration surrounds the [properties of a B2B Guest User](../external-id/user-properties). The difference between internal versus external user accounts and member versus Guest User types contributes to confusion. Initially, all internal users are member users with **UserType** attribute set to *Member* (member users). An internal user has an account in your Microsoft Entra ID that is authoritative and authenticates to the tenant where the user resides. A member user is a licensed user with default [member-level permissions](../fundamentals/users-default-permissions) in the tenant. Treat member users as employees of your organization.

You can invite an internal user of one tenant into another tenant as an external user. An external user signs in with an external Microsoft Entra account, social identity, or other external identity provider. External users authenticate outside the tenant to which you invite the external user. At the B2B first release, all external users were of **UserType***Guest* (guest users). Guest users have [restricted permissions](../fundamentals/users-default-permissions) in the tenant. For example, guest users can't enumerate the list of all users nor groups in the tenant directory.

For the **UserType** property on users, B2B supports flipping the bit from internal to external, and vice versa, which contributes to the confusion.

You can change an internal user from member user to Guest User. For example, you can have an unlicensed internal Guest User with guest-level permissions in the tenant, which is useful when you provide a user account and credentials to a person that isn't an employee of your organization.

You can change an external user from Guest User to member user, giving member-level permissions to the external user. Making this change is useful when you manage multiple tenants for your organization and need to give member-level permissions to a user across all tenants. This need might occur regardless of whether the user is internal or external in any given tenant. Member users might require more [licenses](../external-id/external-identities-pricing).

Most documentation for B2B refers to an external user as a Guest User. It conflates the **UserType** property in a way that assumes all guest users are external. When documentation calls out a Guest User, it assumes that it's an external Guest User. This article specifically and intentionally refers to external versus internal and member user versus Guest User.

## Cross-tenant synchronization

[Cross-tenant synchronization](../identity/multi-tenant-organizations/cross-tenant-synchronization-overview) enables multitenant organizations to provide seamless access and collaboration experiences to end users, using existing B2B external collaboration capabilities. The feature doesn't allow cross-tenant synchronization across Microsoft sovereign clouds (such as Microsoft 365 US Government GCC High, DOD or Office 365 in China). See [Common considerations for multitenant user management](multi-tenant-common-considerations#cross-tenant-synchronization) for help with automated and custom cross-tenant synchronization scenarios.

Watch Arvind Harinder talk about the cross-tenant sync capability in Microsoft Entra ID (embedded below).

The following conceptual and how-to articles provide information about Microsoft Entra B2B collaboration and cross-tenant synchronization.

### Conceptual articles

- [B2B best practices](../external-id/b2b-fundamentals) features recommendations for providing the smoothest experience for users and administrators.
- [B2B and Office 365 external sharing](../external-id/what-is-b2b) explains the similarities and differences among sharing resources through B2B, Office 365, and SharePoint/OneDrive.
- [Properties on a Microsoft Entra B2B collaboration user](../external-id/user-properties) describes the properties and states of the external user object in Microsoft Entra ID. The description provides details before and after invitation redemption.
- [Conditional Access for B2B](../external-id/authentication-conditional-access) describes how Conditional Access and multifactor authentication work for external users.
- [Cross-tenant access settings](../external-id/cross-tenant-access-overview) provides granular control over how external Microsoft Entra organizations collaborate with you (inbound access) and how your users collaborate with external Microsoft Entra organizations (outbound access).
- [Cross-tenant synchronization overview](../identity/multi-tenant-organizations/cross-tenant-synchronization-overview) explains how to automate creating, updating, and deleting Microsoft Entra B2B collaboration users across tenants in an organization.

### How-to articles

- [Use PowerShell to bulk invite Microsoft Entra B2B collaboration users](../external-id/bulk-invite-powershell) describes how to use PowerShell to send bulk invitations to external users.
- [Enforce multifactor authentication for B2B guest users](../external-id/b2b-tutorial-require-mfa) explains how you can use Conditional Access and multifactor authentication policies to enforce tenant, app, or individual external user authentication levels.
- [Email one-time passcode authentication](../external-id/one-time-passcode) describes how the Email one-time passcode feature authenticates external users when they can't authenticate through other means like Microsoft Entra ID, a Microsoft account, or Google Federation.

## Terminology

The following terms in Microsoft content refer to multitenant collaboration in Microsoft Entra ID.

- **Resource tenant:** The Microsoft Entra tenant containing the resources that users want to share with others.
- **Home tenant:** The Microsoft Entra tenant containing users that require access to the resources in the resource tenant.
- **Internal user:** An internal user has an account that is authoritative and authenticates to the tenant where the user resides.
- **External user:** An external user has an external Microsoft Entra account, social identity, or other external identity provider to sign in. The external user authenticates somewhere outside the tenant to which you have invited the external user.
- **Member user:** An internal or external member user is a licensed user with default member-level permissions in the tenant. Treat member users as employees of your organization.
- **Guest user:** An internal or external Guest User has restricted permissions in the tenant. Guest users aren't employees of your organization (such as users for partners). Most B2B documentation refers to B2B Guests, which primarily refers to external Guest User accounts.
- **User lifecycle management:** The process of provisioning, managing, and deprovisioning user access to resources.
- **Unified GAL:** Each user in each tenant can see users from each organization in their Global Address List (GAL).

## Deciding how to meet your requirements

Your organization's unique requirements influence your strategy for managing users across tenants. To create an effective strategy, consider the following requirements.

- Number of tenants
- Type of organization
- Current topologies
- Specific user synchronization needs

### Common requirements

Organizations initially focus on requirements that they want in place for immediate collaboration. Sometimes called *Day One* requirements, they focus on enabling end users to smoothly merge without interrupting their ability to generate value. As you define Day One and administrative requirements, consider including the following requirements and needs.

### Communications requirements

- **Unified global address list:** Each user can see all other users in the GAL in their home tenant.
- **Free/busy information:** Enable users to discover each other's availability. You can do so with [Organization relationships in Exchange Online](/en-us/exchange/sharing/organization-relationships/create-an-organization-relationship).
- **Chat and presence:** Enable users to determine others' presence and initiate instant messaging. Configure through [external access in Microsoft Teams](/en-us/microsoftteams/trusted-organizations-external-meetings-chat).
- **Book resources such as meeting rooms:** Enable users to book conference rooms or other resources across the organization. Cross-tenant conference room booking isn't currently available in Exchange Online.
- **Single email domain:** Enable all users to send and receive mail from a single email domain (for example, `users@contoso.com`). Sending requires an email address rewrite solution.

### Access requirements

- **Document access:** Enable users to share documents from SharePoint, OneDrive, and Teams.
- **Administration:** Allow administrators to manage configuration of subscriptions and services deployed across multiple tenants.
- **Application access:** Allow end users to access applications across the organization.
- **Single Sign On:** Enable users to access resources across the organization without the need to enter more credentials.

### Patterns for account creation

Microsoft mechanisms for creating and managing the lifecycle of your external user accounts follow three common patterns. You can use these patterns to help define and implement your requirements. Choose the pattern that best aligns with your scenario and then focus on the pattern details.

| Mechanism | Description | Best when |
| --- | --- | --- |
| [End user-initiated](multi-tenant-user-management-scenarios#end-user-initiated-scenario) | Resource tenant admins delegate the ability to invite external users to the tenant, an app, or a resource to users within the resource tenant. You can invite users from the home tenant or they can individually sign up. | Unified Global Address List on Day One not required. |
| [Scripted](multi-tenant-user-management-scenarios#scripted-scenario) | Resource tenant administrators deploy a scripted *pull* process to automate discovery and provisioning of external users to support sharing scenarios. | Small number of tenants (such as two). |
| [Automated](multi-tenant-user-management-scenarios#automated-scenario) | Resource tenant admins use an identity provisioning system to automate the provisioning and deprovisioning processes. | You need Unified Global Address List across tenants. |