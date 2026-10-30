---
layout: Conceptual
title: Multitenant organization capabilities in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/multi-tenant-organizations/overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.reviewer: hafowler
ms.service: entra-id
ms.subservice: multitenant-organizations
manager: dougeby
description: Learn about the multitenant organization scenario and capabilities in Microsoft Entra ID.
ms.topic: overview
ms.date: 2026-03-18T00:00:00.0000000Z
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: df552597-54a7-50e4-55b3-4cd0f0a91977
document_version_independent_id: a7b0a42e-c1a8-58f4-28c0-8a9e2b7e2a99
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/multi-tenant-organizations/overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/multi-tenant-organizations/overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/multi-tenant-organizations/overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 618ad9a7-0039-d3f0-d235-a82bc4d9c2b0
---

# Multitenant organization capabilities in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

## Overview

This article provides an overview of the multitenant organization scenario and the related capabilities in Microsoft Entra ID.

## What is the multitenant organization scenario?

The multitenant organization scenario occurs when an organization has more than one tenant instance of Microsoft Entra ID. Here are the primary reasons why an organization might have multiple tenants:

- **Conglomerates:** Organizations with multiple subsidiaries or business units that operate independently.
- **Mergers and acquisitions:** Organizations that merge or acquire companies.
- **Divestiture activity:** In a divestiture, one organization splits off part of its business to form a new organization or sell it to an existing organization.
- **Multiple clouds:** Organizations that have compliance or regulatory needs to exist in multiple cloud environments.
- **Multiple geographical boundaries:** Organizations that operate in multiple geographic locations with various residency regulations.
- **Test or staging tenants:** Organizations that need multiple tenants for testing or staging purposes before deploying more broadly to primary tenants.
- **Department or employee-created tenants:** Organizations where departments or employees have created tenants for development, testing, or separate control.

## What is a Microsoft Entra tenant?

A *tenant* is an instance of Microsoft Entra ID in which information about a single organization resides including organizational objects such as users, groups, and devices and also application registrations, such as Microsoft 365 and third-party applications. A tenant also contains access and compliance policies for resources, such as applications registered in the directory. The primary functions served by a tenant include identity authentication as well as resource access management.

From a Microsoft Entra perspective, a tenant forms an identity and access management scope. For example, a tenant administrator makes an application available to some or all the users in the tenant and enforces access policies on that application for users in that tenant. In addition, a tenant contains organizational branding data that drives end-user experiences, such as the organizations email domains and SharePoint URLs used by employees in that organization. From a Microsoft 365 perspective, a tenant forms the default collaboration and licensing boundary. For example, users in Microsoft Teams or Microsoft Outlook can easily find and collaborate with other users in their tenant, but don't have the ability to find or see users in other tenants.

Tenants contain privileged organizational data and are securely isolated from other tenants. In addition, tenants can be configured to have data persisted and processed in a specific region or cloud, which enables organizations to use tenants as a mechanism to meet data residency and handling compliance requirements.

## Multitenant challenges

Your organization might have recently acquired a new company, merged with another company, or restructured based on newly formed business units. If you have disparate identity management systems, it might be challenging for users in different tenants to access resources and collaborate.

The following diagram shows how users in other tenants might not be able to access applications across tenants in your organization.

[![Diagram that shows users unable to access applications across tenants.](media/overview/multi-tenant-no-access.png)](media/overview/multi-tenant-no-access.png#lightbox)

As your organization evolves, your IT team must adapt to meet the changing needs. This often includes integrating with an existing tenant or forming a new one. Regardless of how the identity infrastructure is managed, it's critical that users have a seamless experience accessing resources and collaborating. Today, you might be using custom scripts or on-premises solutions to bring the tenants together to provide a seamless experience across tenants.

## Multitenant capabilities for multitenant organizations

[Multitenant organizations in Microsoft Entra ID](multi-tenant-organization-overview) offers a portfolio of multitenant capabilities you can use to securely interact with users across your organization of multiple tenants and to automatically provision and manage those users across your tenants.

Several of these multitenant capabilities share a common technology stack with [Microsoft Entra External ID for business guests](../../external-id/external-identities-overview) and [app provisioning in Microsoft Entra ID](../app-provisioning/user-provisioning), so you might frequently find cross-references to these other areas. [Microsoft 365 for Enterprise](/en-us/microsoft-365/enterprise/plan-multi-tenant-org-overview) uses multitenant capabilities to enable or facilitate seamless multitenant collaboration experiences in Microsoft Teams and across Microsoft 365 applications.

The following set of multitenant capabilities support the needs of multitenant organizations:

- **Cross-tenant access settings** - Manages how your tenant allows or disallows access to your tenant from other tenants in your organization or vice versa. They govern B2B collaboration, B2B direct connect, cross-tenant synchronization, and they indicate whether another tenant of your organization is known to be part of your multitenant organization.
- **B2B direct connect** - Establishes a mutual, two-way trust with another Microsoft Entra tenant for seamless collaboration. B2B direct connect users aren't represented in your directory, but they're visible in Teams for collaboration in Teams shared channels.
- **B2B collaboration** – Enables application access for and collaboration with external users. B2B collaboration users are represented in your directory. They're available in Microsoft Teams for collaboration, if enabled. They're also available across Microsoft 365 applications.
- **Cross-tenant synchronization** - Provides a synchronization service that automates creating, updating, and deleting B2B collaboration users across your organization of multiple tenants. The service can be used to scope Microsoft 365 people search in target tenants. The service is governed by cross-tenant synchronization settings under cross-tenant access settings.
- **Microsoft 365 multitenant people search** - Collaboration with B2B collaboration users. If shown in address list, B2B collaboration users are available as contacts in Outlook. If elevated to user type Member, B2B collaboration member users are available in most Microsoft 365 applications.
- **Multitenant organization** - Defines a boundary around the Microsoft Entra tenants that your organization owns, facilitated by an invite-and-accept flow. In conjunction with B2B member provisioning, enables seamless collaboration experiences in Microsoft Teams and Microsoft 365 applications like Microsoft Viva Engage. Cross-tenant access settings provide a flag for your multitenant organization tenants.
- **Microsoft 365 admin center for multitenant collaboration** - Provides an intuitive admin portal experience to create a multitenant organization. For smaller multitenant organizations, also provides a simplified experience to synchronize users to multitenant organization tenants as an alternative to using Microsoft Entra admin center.

The following sections describe each of these capabilities in more detail.

### Cross-tenant access settings

Microsoft Entra tenant administrators staying in control of their tenant-scoped resources is a guiding principle, even within your organization of multiple tenants. As such, cross-tenant access settings are required for each tenant-to-tenant relationship, and tenant administrators explicitly configure each cross-tenant access relationship as needed.

The following diagram shows the basic cross-tenant access inbound and outbound settings capabilities.

![Overview diagram of cross-tenant access settings.](../../external-id/media/cross-tenant-access-overview/cross-tenant-access-settings-overview.png)

For more information, see [Cross-tenant access overview](../../external-id/cross-tenant-access-overview).

### B2B direct connect

To enable users across tenants to collaborate in [Teams Connect shared channels](/en-us/microsoftteams/platform/concepts/build-and-test/shared-channels), you can use [Microsoft Entra B2B direct connect](../../external-id/b2b-direct-connect-overview). B2B direct connect is a feature of External ID that lets you set up a mutual trust relationship with another Microsoft Entra tenant for seamless collaboration in Teams. When the trust is established, the B2B direct connect user has single sign-on access using credentials from their home tenant.

Here's the primary constraint with using B2B direct connect across multiple tenants:

- Currently, B2B direct connect works only with Teams Connect shared channels.

[![Diagram that shows using B2B direct connect across tenants.](media/overview/multi-tenant-b2b-direct-connect.png)](media/overview/multi-tenant-b2b-direct-connect.png#lightbox)

For more information, see [B2B direct connect overview](../../external-id/b2b-direct-connect-overview).

### B2B collaboration

To enable users across tenants to collaborate, you can use [Microsoft Entra B2B collaboration](../../external-id/what-is-b2b). B2B collaboration is a feature within External ID that lets you invite guest users to collaborate with your organization. Once the external user has redeemed their invitation or completed sign-up, they're represented in your tenant as a user object. With B2B collaboration, you can securely share your tenant's applications and services with external users, while maintaining control over your tenant's data.

Here are the primary constraints with using B2B collaboration across multiple tenants:

- Administrators must invite users using the B2B invitation process or build an onboarding experience using the [B2B collaboration invitation manager](../../external-id/external-identities-overview#azure-ad-microsoft-graph-api-for-b2b-collaboration).
- Administrators might have to synchronize users using custom scripts.
- Depending on automatic redemption settings, users might need to accept a consent prompt and follow a redemption process in each tenant.

[![Diagram that shows using B2B collaboration across tenants.](media/overview/multi-tenant-b2b-collaboration.png)](media/overview/multi-tenant-b2b-collaboration.png#lightbox)

For more information, see [B2B collaboration overview](../../external-id/what-is-b2b).

### Cross-tenant synchronization

If you want users to have a more seamless collaboration experience across tenants, you can use [cross-tenant synchronization in Microsoft Entra ID](cross-tenant-synchronization-overview). Cross-tenant synchronization is a one-way synchronization service in Microsoft Entra ID that automates creating, updating, and deleting B2B collaboration users across tenants in an organization. Cross-tenant synchronization builds on the B2B collaboration functionality and utilizes existing B2B cross-tenant access settings. Users are represented in the target tenant as a B2B collaboration user object.

Here are the primary benefits with using cross-tenant synchronization:

- Automatically create B2B collaboration users within your organization and provide them access to the applications they need, without creating and maintaining custom scripts.
- Improve the user experience and ensure that users can access resources, without receiving an invitation email and having to accept a consent prompt in each tenant.
- Automatically update users and remove them when they leave the organization.

Here are the primary constraints with using cross-tenant synchronization across multiple tenants:

- Synchronized users will have the same cross-tenant Teams and Microsoft 365 experiences available to any other B2B collaboration user.
- Doesn't synchronize devices or contacts.

[![Diagram that shows using cross-tenant synchronization across tenants.](media/overview/multi-tenant-cross-tenant-sync.png)](media/overview/multi-tenant-cross-tenant-sync.png#lightbox)

For more information, see [What is cross-tenant synchronization?](cross-tenant-synchronization-overview).

### Microsoft 365 multitenant people search

B2B collaboration users can now be enabled for collaboration in Microsoft 365, beyond the well-known [B2B collaboration guest user](../../external-id/what-is-b2b) experience.

Multitenant organization people search is a collaboration feature that enables search and discovery of people across multiple tenants. If shown in address list, B2B collaboration users are available as contacts in Outlook. In addition to being shown in address list, if further elevated to user type Member, B2B collaboration member users are available in most Microsoft 365 applications.

Here are the primary benefits of using Microsoft 365 people search across multiple tenants:

- B2B collaboration users can be made available for collaboration in Outlook. This can be enabled using the [showInAddressList](/en-us/graph/api/resources/user#properties) property set to true for Exchange Online mail users in the host tenant, or using cross-tenant synchronization from the source tenant.
- B2B collaboration users already shown in address lists can be made available for collaboration in most Microsoft 365 applications using the [userType](/en-us/graph/api/resources/user#properties) property set to Member, managed in [Microsoft Entra admin center](../../fundamentals/how-to-manage-user-profile-info) of the host tenant, or using cross-tenant synchronization from the source tenant.

Here are the primary constraints of using Microsoft 365 people search across multiple tenants:

- For collaboration in most Microsoft 365 applications, a B2B collaboration user should be shown in address lists as well as be set to user type Member.
- For additional address list constraints, see [Global address list limitations in multitenant organizations](multi-tenant-organization-known-issues#global-address-list-managed-in-the-host-tenant).

For more information, see [Microsoft 365 multitenant people search](/en-us/microsoft-365/enterprise/multi-tenant-people-search).

### Multitenant organization

[Multitenant organization](multi-tenant-organization-overview) is a feature in Microsoft Entra ID and Microsoft 365 that enables you to define a boundary around the Microsoft Entra tenants that your organization owns. In the directory, it takes the form of a tenant group that represents your organization. Each pair of tenants in the group is governed by cross-tenant access settings that you can use to configure B2B collaboration.

Here are the primary benefits of a multitenant organization:

- Differentiate in-organization and out-of-organization external users
- Improved collaborative experience in new Microsoft Teams
- Improved collaborative experience in Viva Engage

Here are the primary constraints with using a multitenant organization:

- If you already have B2B collaboration member users in tenants that are part of the multitenant organization, those users will immediately become multitenant organization members upon multitenant organization creation. Therefore, applications with multitenant organization experiences will recognize existing B2B collaboration member users as multitenant organization users.
- Improved Microsoft Teams collaboration relies on reciprocal provisioning of B2B collaboration member users.
- Improved Viva Engage collaboration relies on centralized provisioning of B2B collaboration members.
- For additional constraints, see [Limitations in multitenant organizations](multi-tenant-organization-known-issues).

[![Diagram that shows a multitenant organization topology and cross-tenant access settings.](media/common/multi-tenant-organization-topology.png)](media/common/multi-tenant-organization-topology.png#lightbox)

For more information, see [What is a multitenant organization in Microsoft Entra ID?](multi-tenant-organization-overview).

### Microsoft 365 admin center for multitenant collaboration

[Microsoft 365 admin center for multitenant collaboration](/en-us/microsoft-365/enterprise/plan-multi-tenant-org-overview) provides an intuitive admin portal experience to create your multitenant organization.

- [Create a multitenant organization](/en-us/microsoft-365/enterprise/set-up-multi-tenant-org) in Microsoft 365 admin center.

Following the creation of a multitenant organization, Microsoft offers two methods to provision employees into neighboring multitenant organization tenants at scale.

- For enterprise organizations with complex identity topologies, consider using [cross-tenant synchronization in Microsoft Entra ID](cross-tenant-synchronization-overview). Cross-tenant synchronization is highly configurable and allows the provisioning of any multi-hub multi-spoke identity topology.
- For smaller multitenant organizations where employees are to be provisioned into all tenants, consider staying in Microsoft 365 admin center to [simultaneously synchronize users into multiple tenants](/en-us/microsoft-365/enterprise/sync-users-multi-tenant-orgs) of your multitenant organization.

If you already have your own at-scale user provisioning engine, you can enjoy the new multitenant organization benefits while continuing to use your own engine to manage the lifecycle of your employees.

Here are the primary benefits of using Microsoft 365 admin center to create your multitenant organization and provision employees.

- Microsoft 365 admin center provides a graphical user experience to create the multitenant organization.
- Microsoft 365 admin center will pre-configure your tenants for auto-redemption of B2B collaboration invitations.
- Microsoft 365 admin center will pre-configure your tenants for inbound user synchronization, though usage of cross-tenant synchronization remains optional.
- Microsoft 365 admin center allows easy provisioning of employees into multiple tenants of your multitenant organization.
- Microsoft 365 admin center can create Exchange Online Organization Relationships to view calendar availability information.

Here are the primary constraints with using Microsoft 365 admin center to create your multitenant organization or provision employees:

- Microsoft 365 admin center will pre-configure but not start cross-tenant synchronization jobs, even if you intend to use cross-tenant synchronization in Microsoft Entra admin center.
- Complex identity topologies, such as multi-hub, multi-spoke systems, are better provisioned using cross-tenant synchronization in Microsoft Entra admin portal.

For more information, see [Microsoft 365 multitenant collaboration](/en-us/microsoft-365/enterprise/plan-multi-tenant-org-overview).

## Compare multitenant capabilities

Depending on the needs of your organization, you can use any combination of B2B direct connect, B2B collaboration, cross-tenant synchronization, and multitenant organization capabilities. B2B direct connect and B2B collaboration are independent capabilities, while cross-tenant synchronization and multitenant organization capabilities are independent of each other, though both rely on underlying B2B collaboration.

The following table compares the capabilities of each feature. For more information about different external identity scenarios, see [Comparing External ID feature sets](../../external-id/external-identities-overview#comparing-external-identities-feature-sets).

| - | B2B direct connect(Org-to-org external or internal) | B2B collaboration(Org-to-org external or internal) | Cross-tenant synchronization(Org internal) | Multitenant organization(Org internal) |
| --- | --- | --- | --- | --- |
| **Purpose** | Users can access Teams Connect shared channels hosted in external tenants. | Users can access apps/resources hosted in external tenants, usually with limited guest privileges. Depending on automatic redemption settings, users might need to accept a consent prompt in each tenant. | Users can seamlessly access apps/resources across the same organization, even if they're hosted in different tenants. | Users can more seamlessly collaborate across a multitenant organization in new Teams and Viva Engage. |
| **Value** | Enables external collaboration within Teams Connect shared channels only. More convenient for administrators because they don't have to manage B2B users. | Enables external collaboration. More control and monitoring for administrators by managing the B2B collaboration users. Administrators can limit the access that these external users have to their apps/resources. | Enables collaboration across organizational tenants. Administrators don't have to manually invite and synchronize users between tenants to ensure continuous access to apps/resources within the organization. | Enables collaboration across organizational tenants. Administrators continue to have full configuration ability using cross-tenant access settings. Optional cross-tenant access templates allow preconfiguration of cross-tenant access settings. |
| **Primary administrator workflow** | Configure cross-tenant access to provide external users inbound access to tenant the credentials for their home tenant. | Add external users to resource tenant by using the B2B invitation process or build your own onboarding experience using the [B2B collaboration invitation manager](../../external-id/external-identities-overview#azure-ad-microsoft-graph-api-for-b2b-collaboration). | Configure the cross-tenant synchronization engine to synchronize users between multiple tenants as B2B collaboration users. | Create a multitenant organization, add (invite) tenants, join a multitenant organization. Use existing B2B collaboration users or use cross-tenant synchronization to provision B2B collaboration users. |
| **Trust level** | Mid trust. B2B direct connect users are less easy to track, mandating a certain level of trust with the external organization. | Low to mid trust. User objects can be tracked easily and managed with granular controls. | High trust. All tenants are part of the same organization, and users are typically granted member access to all apps/resources. | High trust. All tenants are part of the same organization, and users are typically granted member access to all apps/resources. |
| **Effect on users** | Users access the resource tenant using the credentials for their home tenant. User objects aren't created in the resource tenant. | External users are added to a tenant as B2B collaboration users. | Within the same organization, users are synchronized from their home tenant to the resource tenant as B2B collaboration users. | Within the same multitenant organization, B2B collaboration users, particularly member users, benefit from enhanced, seamless collaboration across Microsoft 365. |
| **User type** | B2B direct connect user- N/A | B2B collaboration user- External member- External guest (default) | B2B collaboration user- External member (default)- External guest | B2B collaboration user- External member (default)- External guest |

The following diagram shows how B2B direct connect, B2B collaboration, and cross-tenant synchronization capabilities could be used together.

[![Diagram that shows different multitenant capabilities.](media/overview/multi-tenant-capabilities.png)](media/overview/multi-tenant-capabilities.png#lightbox)

## Terminology

To better understand multitenant organization scenario related Microsoft Entra capabilities, you can refer back to the following list of terms.

| Term | Definition |
| --- | --- |
| tenant | An instance of Microsoft Entra ID. |
| organization | The top level of a business hierarchy. |
| multitenant organization | An organization that has more than one instance of Microsoft Entra ID, as well as a capability to group those instances in Microsoft Entra ID. |
| creator tenant | The tenant that created the multitenant organization. |
| owner tenant | A tenant with the Owner role. Initially, the creator tenant. |
| added tenant | A tenant that was added by an owner tenant. |
| joiner tenant | A tenant that is joining the multitenant organization. |
| join request | A joiner or added tenant submits a join request to join the multitenant organization. |
| pending tenant | A tenant that was added by an owner but that hasn't yet joined. |
| active tenant | A tenant that created or joined the multitenant organization. |
| member tenant | A tenant with the member role. Most joiner tenants start as members. |
| multitenant organization tenant | An active tenant of the multitenant organization, not pending. |
| cross-tenant synchronization | A one-way synchronization service in Microsoft Entra ID that automates creating, updating, and deleting B2B collaboration users across tenants in an organization. |
| cross-tenant access settings | Settings to manage collaboration for specific Microsoft Entra organizations. |
| cross-tenant access settings template | An optional template to preconfigure cross-tenant access settings that are applied to any partner tenant newly joining the multitenant organization. |
| organizational settings | Cross-tenant access settings for specific Microsoft Entra organizations. |
| configuration | An application and underlying service principal in Microsoft Entra ID that includes the settings (such as target tenant, user scope, and attribute mappings) needed for cross-tenant synchronization. |
| provisioning | The process of automatically creating or synchronizing objects across a boundary. |
| automatic redemption | A B2B setting to automatically redeem invitations so newly created users don't receive an invitation email or have to accept a consent prompt when added to a target tenant. |