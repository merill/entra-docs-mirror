---
layout: Conceptual
title: Topologies for cross-tenant synchronization - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-topology
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
description: Learn about topologies for cross-tenant synchronization in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2026-03-18T00:00:00.0000000Z
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: a2ec0a2d-5912-3cb1-4d4b-3d119c86cfd7
document_version_independent_id: 02295fe0-1e7f-6137-06d7-338a12c3174e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/multi-tenant-organizations/cross-tenant-synchronization-topology.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/multi-tenant-organizations/cross-tenant-synchronization-topology
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/multi-tenant-organizations/cross-tenant-synchronization-topology.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 077841f5-b868-2aeb-ab6a-2c8423045cb3
---

# Topologies for cross-tenant synchronization - Microsoft Entra ID | Microsoft Learn

## Overview

Organizations often find themselves managing multiple tenants due to mergers and acquisitions, regulatory requirements, or administrative boundaries. Regardless of your scenario, Microsoft Entra offers a flexible and ready-to-use solution for provisioning accounts across tenants and facilitating seamless collaboration. Microsoft Entra accommodates the following three models and can adapt to your evolving organizational needs.

- Hub and spoke
- Mesh
- Just-in-time

## Hub and spoke

The hub and spoke topology presents two common patterns:

- **Option 1 (application hub):** In this option, you can integrate commonly used applications into a central hub tenant that users from across the organization can access.
- **Option 2 (user hub):** Alternatively, option 2 centralizes all your users in a single tenant and provisions them into spoke tenants where resources are managed.

Let's examine a few real-world scenarios and see how they align with each of these models.

### Mergers and acquisitions (application hub)

During mergers and acquisitions, the ability to quickly enable collaboration is crucial, allowing businesses to function cohesively while complex IT decisions are being made. For instance, when a newly acquired company's employees need immediate access to applications such as the internal help desk ticketing system or benefits application, cross-tenant synchronization proves invaluable. This synchronization process allows users from the acquired company to be provisioned into the application hub from day one, granting them access to SaaS apps, on-premises applications, and other cloud resources. Within the target tenant, admins can set up access packages to grant time limited access to additional applications such as Salesforce and Amazon Web Services that contain business critical data. The following diagram shows recently acquired tenants on the left and their users being provisioned into the parent company's tenant, which grants users access to the necessary resources.

![Diagram that shows multiple source tenants synchronizing with a single target tenant.](media/cross-tenant-synchronization-topology/hub-1.png)

## Separate collaboration and resource tenants (user hub)

As organizations scale their usage of Azure, they often create dedicated tenants for managing critical Azure resources. Meanwhile, they rely on a central hub tenant for user provisioning. This model empowers administrators in the hub tenant to establish central security and governance policies while granting development teams greater autonomy and agility to deploy required Azure resources. Cross-tenant synchronization supports this topology by enabling administrators to provision a subset of users into the spoke tenants and manage the lifecycle of those users.

![Diagram that shows a source tenant synchronizing with multiple target tenants.](media/cross-tenant-synchronization-topology/hub-2.png)

## Mesh

While some companies centralize their users within a single tenant, others have a more decentralized structure with applications, HR systems, and Active Directory domains integrated into each tenant. Cross-tenant synchronization offers the flexibility to choose which users are provisioned into each tenant.

### Collaborate within a portfolio company (partial-mesh)

In this scenario, each tenant represents a different company within the same parent organization. Administrators in each tenant choose a subset of users to provision into the target tenant. This solution provides flexibility for each tenant to operate independently, while facilitating collaboration when users need access to critical resources.

![Diagram that shows a partial-mesh topology synchronizing with multiple tenants.](media/cross-tenant-synchronization-topology/mesh.png)

Cross-tenant synchronization is one way. An internal member user can be synchronized into multiple tenants as an external user. When the topology shows a synchronization going in both directions, it's a distinct set of users in each direction and each arrow is a separate configuration.

### Collaborate across business units (full-mesh)

In this scenario, the organization has designated different tenants for each business unit. The business units work closely together, in particular using Microsoft Teams. As a result, each tenant has chosen to provision all users across the four tenants in the organization. As new users join the company or leave, the provisioning service takes care of creating and deleting users. The organization has also configured a multitenant organization that includes all four tenants. Now when users need to collaborate in Teams, they're able to easily find users across the company and start chats and meetings with those users.

![Diagram that shows a ful-mesh topology synchronizing with multiple tenants.](media/cross-tenant-synchronization-topology/mesh-2.png)

## Just-in-time

While the scenarios discussed so far cover collaboration within an organization, there are cases where cross-organization collaboration is vital. This could be in the context of joint ventures or organizations of independent legal entities. By employing connected organizations and entitlement management, you can define policies for accessing resources across connected organizations and enable users to request access to the resources they need.

### Joint ventures

Consider Contoso and Litware, separate organizations engaged in a multi-year joint venture. They need to collaborate closely. Administrators at Contoso have defined access packages containing the resources required by Litware users. When a new Litware employee needs access to Contoso's resources, they can request access to the access package. Upon approval, they are provisioned with the necessary resources. Access can be time-limited and subject to periodic review to ensure compliance with Contoso's governance requirements.

The following diagram shows how two organizations can just-in-time collaborate by using connected organizations and entitlement management.

![Diagram that shows just-in-time collaboration by using connected organizations and entitlement management.](media/cross-tenant-synchronization-topology/connected-organization.png)

## Supported scenarios

Cross-tenant synchronization supports importing [internal users](/en-us/entra/external-id/user-properties) in the source tenant and provisioning [external users](/en-us/entra/external-id/user-properties) in the target tenant.

| Source tenant credentials | Source tenant userType | Target tenant credentials | Target tenant userType | Scenario supported? |
| --- | --- | --- | --- | --- |
| Internal | Member | External | Member | Yes |
| Internal | Member | External | Guest | Yes |
| Internal | Guest | External | Member | Yes |
| Internal | Guest | External | Guest | Yes |
| Internal | Member | Internal | Member | No |
| Internal | Member | Internal | Guest | No |
| Internal | Guest | Internal | Member | No |
| Internal | Guest | Internal | Guest | No |
| External | Member | External | Member | No |
| External | Member | External | Guest | No |
| External | Guest | External | Member | No |
| External | Guest | External | Guest | No |