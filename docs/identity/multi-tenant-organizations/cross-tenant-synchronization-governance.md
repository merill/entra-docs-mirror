---
layout: Conceptual
title: Governance and cross-tenant synchronization - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-governance
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.reviewer: gasinh
ms.service: entra-id
ms.subservice: multitenant-organizations
manager: martinco
description: Learn to govern and manage identity and access lifecycles across multitenant organizations.
ms.topic: concept-article
ms.date: 2026-03-18T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 1560778f-2ecc-4cbd-1eea-faffa9a840d4
document_version_independent_id: 1560778f-2ecc-4cbd-1eea-faffa9a840d4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/multi-tenant-organizations/cross-tenant-synchronization-governance.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/multi-tenant-organizations/cross-tenant-synchronization-governance
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/multi-tenant-organizations/cross-tenant-synchronization-governance.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 0721cdee-1a9a-101b-6bbb-1c92d328c187
---

# Governance and cross-tenant synchronization - Microsoft Entra ID | Microsoft Learn

Cross-tenant synchronization is a flexible and ready-to-use solution to provision accounts and facilitate seamless collaboration across tenants in an organization. Cross-tenant synchronization automatically manages user identity lifecycle across tenants. It provisions, synchronizes, and deprovisions users in the scope of synchronization from source tenants.

This article describes how [Microsoft Entra ID Governance](../../id-governance/identity-governance-overview) customers can use cross-tenant synchronization to manage identity and access lifecycles across multitenant organizations.

## Deployment example

In this example, Contoso is a multitenant organization with three production Microsoft Entra tenants. Contoso is deploying cross-tenant synchronization and Microsoft Entra ID Governance features to address the following scenarios:

- Manage employee identity lifecycles across multiple tenants
- Use workflows to automate lifecycle processes for employees that originate in other tenants
- Assign resource access automatically to employees that originate in other tenants
- Allow employees to request access to resources in multiple tenants
- Review the access of synchronized users

From a cross-tenant synchronization perspective, Contoso Europe, Middle East, and Africa (Contoso EMEA) and Contoso United States (Contoso US) are source tenants and Contoso is a target tenant. The following diagram illustrates the topology.

![Diagram of a cross-tenant synchronization topology.](media/cross-tenant-synchronization-governance/cross-tenant-topology.png)

This supported [topology for cross-tenant synchronization](cross-tenant-synchronization-topology) is one of many in Microsoft Entra ID. Tenants can be a source tenant, a target tenant, or both. In the following sections, learn how cross-tenant synchronization and Microsoft Entra ID Governance features address several scenarios.

## Manage employee lifecycles across tenants

[Cross-tenant synchronization in Microsoft Entra ID](cross-tenant-synchronization-overview) automates creating, updating, and deleting B2B collaboration users.

When organizations create, or provision, a B2B collaboration user in a tenant, user access depends partly on how the organization provisioned them: Guest or Member user type. When you select user type, consider the various [properties of a Microsoft Entra B2B collaboration user](../../external-id/user-properties). The Member user type is suitable if users are part of the larger multitenant organization and need member-level access to resources in the organizational tenants. Microsoft Teams requires the Member user type in [Multitenant organizations](/en-us/microsoft-365/enterprise/plan-multi-tenant-org-overview?view=o365-worldwide&amp;preserve-view=true).

By default, cross-tenant synchronization includes commonly used attributes on the user object in Microsoft Entra ID. The following diagram illustrates this scenario.

![Diagram of synchronization with commonly used attributes.](media/cross-tenant-synchronization-governance/common-attributes.png)

Organizations use the attributes to help create dynamic membership groups and access packages in the source and target tenant. Some Microsoft Entra ID features have user attributes to target, such as lifecycle workflow user scoping.

To remove, or deprovision, a B2B collaboration user from a tenant automatically stops access to resources in that tenant. This configuration is relevant when employees leave an organization.

## Automate lifecycle processes with workflows

Microsoft Entra ID lifecycle workflows are an identity governance feature to manage Microsoft Entra users. Organizations can automate joiner, mover, and leaver processes.

With cross-tenant synchronization, multitenant organizations can configure lifecycle workflows to run automatically for B2B collaboration users it manages. For example, configure a user onboarding workflow, triggered by the `createdDateTime` event user attribute, to request access package assignment for new B2B collaboration users. Use attributes such as `userType` and `userPrincipalName` to scope lifecycle workflows for users homed in other tenants the organization owns.

## Govern synchronized user access with access packages

Multitenant organizations can ensure B2B collaboration users have access to shared resources in a target tenant. Users can request access, where needed. In the following scenarios, see how the identity governance feature, [entitlement management](../../id-governance/entitlement-management-overview) access packages govern resource access.

### Automatically assign access in target tenants to employees from source tenants

The term birthright assignment refers to automatically granting resource access based on one or more user properties. To configure birthright assignment, create [automatic assignment policies for access packages](../../id-governance/entitlement-management-access-package-auto-assignment-policy) in entitlement management and configure resource roles to grant shared resource access.

Organizations manage cross-tenant synchronization configuration in the source tenant. Therefore, organizations can delegate resource access management to other source tenant administrators for synchronized B2B collaboration users:

- In the source tenant, administrators configure cross-tenant synchronization attribute mappings for the users that require cross-tenant resource access
- In the target tenant, administrators use attributes in automatic assignment policies to determine access package membership for synchronized B2B collaboration users

To drive automatic assignment policies in the target tenant, synchronize default attribute mappings, such as department or map directory extensions, in the source tenant.

### Enable source-tenant employees to request access to target-tenant shared resources

With identity governance [access package](../../id-governance/entitlement-management-access-package-create) policies, multitenant organizations can allow B2B collaboration users, created by cross-tenant synchronization, to request access to shared resources in a target tenant. This process is useful if employees need just-in-time (JIT) access to a resource that another tenant owns.

## Review synchronized-user access

[Access reviews in Microsoft Entra ID](../../id-governance/access-reviews-overview) enable organizations to manage group memberships, access to enterprise applications, and role assignments. Regularly review user access to ensure the right people have access.

When resource access configuration doesn't automatically assign access, such as with dynamic membership groups or access packages, configure access reviews to apply the results to resources upon completion. The following sections describe how multitenant organizations can configure access reviews for users across tenants in source and target tenants.

### Review source-tenant user access

Multitenant organizations can include internal users in access reviews. This action enables access recertification in source tenants that synchronizes users. Use this approach for regular review of security groups assigned to cross-tenant synchronization. Therefore, ongoing B2B collaboration access to other tenants has approval in the user home tenant.

Use access reviews of users in source tenants to avoid potential conflicts between cross-tenant synchronization and access reviews that remove denied users upon completion.

### Review target-tenant user access

Organizations can include B2B collaboration users in access reviews, including users provisioned by cross-tenant synchronization in target tenants. This option enables access recertification of resources in target tenants. Although organizations can target all users in access reviews, guest users can be explicitly targeted if necessary.

For organizations that synchronize B2B collaboration users, typically Microsoft doesn't recommend removing denied guest users automatically from access reviews. Cross-tenant synchronization reprovisions the users if they're in the synchronization scope.