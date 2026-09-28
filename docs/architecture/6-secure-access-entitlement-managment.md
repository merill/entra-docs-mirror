---
layout: Conceptual
title: Manage external access with Microsoft Entra entitlement management - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/6-secure-access-entitlement-managment
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: How to use Microsoft Entra Entitlement Management as a part of your overall external access security plan.
ms.topic: how-to
ms.date: 2025-04-29T00:00:00.0000000Z
ms.reviewer: jercon
ms.subservice: architecture
locale: en-us
document_id: 1340d3e9-a0e0-a429-65e7-9fc8a307ae63
document_version_independent_id: 3c5b57a4-9906-2c7a-6fa8-289446866c01
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/6-secure-access-entitlement-managment.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/6-secure-access-entitlement-managment
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/6-secure-access-entitlement-managment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 67d1f9a5-0aed-338e-5756-67592aaedf93
---

# Manage external access with Microsoft Entra entitlement management - Microsoft Entra | Microsoft Learn

Use the entitlement management feature to manage the identity and access lifecycle. You can automate access request workflows, access assignments, reviews, and expiration. Delegated non-admins use entitlement management to create access packages that external users, from other organizations, can request access to. One and multistage approval workflows are configurable to evaluate requests, and provision users for time-limited access with recurring reviews. Use entitlement management for policy-based provisioning and deprovisioning of external accounts.

Learn more:

- [What is entitlement management?](../id-governance/entitlement-management-overview)
- [What are access packages and what resources can I manage with them?](../id-governance/entitlement-management-overview#what-are-access-packages-and-what-resources-can-i-manage-with-them)
- [What is provisioning?](../id-governance/what-is-provisioning)

## Before you begin

This article is number 6 in a series of 10 articles. We recommend you review the articles in order. Go to the **Next steps** section to see the entire series.

## Enable entitlement management

The following key concepts are important to understand for entitlement management.

### Access packages

An access package is the foundation of entitlement management: groupings of policy-governed resources for users to collaborate on a project or do other tasks. For example, an access package might include:

- Access to SharePoint sites
- Enterprise applications, including your custom in-house and software as a service (SaaS) apps, like Salesforce
- Microsoft Teams
- Microsoft 365 Groups

### Catalogs

Access packages reside in catalogs. When you want to group related resources and access packages and delegate their management, you create a catalog. First, you add resources to a catalog, and then you can add resources to access packages. For example, you can create a finance catalog, and delegate its management to a member of the finance team. That person can add resources, create access packages, and manage access approval.

Learn more:

- [Create and manage a catalog of resources in entitlement management](../id-governance/entitlement-management-catalog-create)
- [Delegation and roles in entitlement management](../id-governance/entitlement-management-delegate)
- [Add resources to a catalog](../id-governance/entitlement-management-catalog-create#add-resources-to-a-catalog)

The following diagram shows a typical governance lifecycle of an external user gaining access to an access package, with an expiration.

![A diagram of the external user governance cycle.](media/secure-external-access/6-governance-lifecycle.png)

### Self-service external access

You can make access packages available, through the Microsoft Entra My Access portal, to enable external users to request access. Policies determine who can request an access package. See, [Request access to an access package in entitlement management](../id-governance/entitlement-management-request-access).

You specify who is allowed to request the access package:

- Connected organizations
    - See, [Add a connected organization in entitlement management](../id-governance/entitlement-management-organization)
- Configured connected organizations
- Users from organizations
- Member or guest users in your tenant

### Approvals

Access packages can include mandatory approval for access. Approvals can be single or multistage and are determined by policies. If internal and external users need to access the same package, you can set up access policies for categories of connected organizations, and for internal users.

Important

Implement approval processes for external users.

### Expiration

Access packages can include an expiration date or a number of days you set for access. When the access package expires, and access ends, the B2B Guest User object representing the user can be deleted or blocked from signing in. We recommend you enforce expiration on access packages for external users. Not all access packages have expirations.

Important

For packages without expiration, perform regular access reviews.

### Access reviews

Access packages can require periodic access reviews, which require the package owner or a designee to attest to the continued need for users' access. See, [Manage guest access with access reviews](../id-governance/manage-guest-access-with-access-reviews).

Before you set up your review, determine the following criteria:

- Who
    - Criteria for continued access
    - Reviewers
- How often
    - Built-in options are monthly, quarterly, BI-annually, or annually
    - We recommend quarterly, or more frequent, reviews for packages that support external access

Important

Access package reviews examine access granted through entitlement management. Set up other processes to review access to external users, outside entitlement management.

Learn more: [Plan a Microsoft Entra access reviews deployment](../id-governance/deploy-access-reviews).

## Using entitlement management automation

- [Working with the Microsoft Entra entitlement management API](/en-us/graph/api/resources/entitlementmanagement-overview?view=graph-rest-1.0&amp;preserve-view=true)
- [`accessPackage` resource type](/en-us/graph/api/resources/accesspackage?view=graph-rest-1.0&amp;preserve-view=true)
- [Microsoft Entra access reviews](/en-us/graph/api/resources/accessreviewsv2-overview?view=graph-rest-1.0&amp;preserve-view=true)
- [`connectedOrganization` resource type](/en-us/graph/api/resources/connectedorganization?view=graph-rest-1.0&amp;preserve-view=true)
- [`entitlementManagementSettings` resource type](/en-us/graph/api/resources/entitlementmanagementsettings?view=graph-rest-1.0&amp;preserve-view=true)

## External access governance recommendations

### Best practices

We recommend the following practices to govern external access with entitlement management.

- For projects with one or more business partners, create and use access packages to onboard and provide access to resources.
    - [Create a new access package in entitlement management](../id-governance/entitlement-management-access-package-create)
- If you have B2B users in your directory, you can assign them to access packages.
- You can assign access in the Azure portal or with Microsoft Graph
    - [View, add, and remove assignments for an access package in entitlement management](../id-governance/entitlement-management-access-package-assignments)
    - [Create a new access package in entitlement management](../id-governance/entitlement-management-access-package-create)

### Identity Governance - Control Configurations

Select the **Lifecycle of external users** setting in Control Configurations to remove users from your directory when their access packages expire. The following settings apply to users onboarded with entitlement management.

![Screenshot of settings and entries for Manage the lifecycle of external users.](media/secure-external-access/6-manage-external-lifecycle.png)

### Delegate catalog and package management

You can delegate catalog and package management to business owners, who have more information on who should access. See, [Delegation and roles in entitlement managements](../id-governance/entitlement-management-delegate)

![Screenshot of options and entries under Roles and administrators.](media/secure-external-access/6-catalog-management.png)

### Enforce access package expiration

You can enforce access expiration for external users. See, [Change lifecycle settings for an access package in entitlement management](../id-governance/entitlement-management-access-package-lifecycle-policy).

![Screenshot of options and entries for Expiration.](media/secure-external-access/6-access-package-expiration.png)

- For the end date of a project-based access package, use **On date**to set the date.
    - Otherwise we recommend expiration to be no longer 365 days, unless it's a multiyear project
- Allow users to extend access
    - Require approval to grant the extension

### Enforce guest-access package reviews

You can enforce reviews of guest-access packages to avoid inappropriate access for guests. See, [Manage guest access with access reviews](../id-governance/manage-guest-access-with-access-reviews).

![Screenshot of options and entries under New access package.](media/secure-external-access/6-new-access-package.png)

- Enforce quarterly reviews
- For compliance-related projects, set the reviewers to be reviewers, rather than self-review for external users.
    - You can use access package managers as reviewers
- For less sensitive projects, users self-reviewing reduces the burden to remove access from users no longer with the organization.

Learn more: [Govern access for external users in entitlement management](../id-governance/entitlement-management-external-users)