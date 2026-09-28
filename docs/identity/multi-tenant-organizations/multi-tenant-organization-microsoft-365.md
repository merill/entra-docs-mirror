---
layout: Conceptual
title: Multitenant organization identity provisioning for Microsoft 365 - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/multi-tenant-organizations/multi-tenant-organization-microsoft-365
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
description: Learn how multitenant organizations identity provisioning and Microsoft 365 work together.
ms.topic: concept-article
ms.date: 2026-03-18T00:00:00.0000000Z
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: 87777d79-2d1d-9045-67b9-2a9ee1bd5a50
document_version_independent_id: c50ef6c6-2704-fbd8-9ac2-c3ac0b6f26bd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/multi-tenant-organizations/multi-tenant-organization-microsoft-365.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/multi-tenant-organizations/multi-tenant-organization-microsoft-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/multi-tenant-organizations/multi-tenant-organization-microsoft-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 0cfbc0a4-d93b-1402-ae5b-c38816d41ca2
---

# Multitenant organization identity provisioning for Microsoft 365 - Microsoft Entra ID | Microsoft Learn

## Overview

The multitenant organization capability is designed for organizations that own multiple Microsoft Entra tenants and want to streamline intra-organization cross-tenant collaboration in Microsoft 365. It's built on the premise of reciprocal provisioning of B2B member users across multitenant organization tenants.

## Microsoft 365 people search

[Teams external access](/en-us/microsoftteams/communicate-with-users-from-other-organizations) and [Teams shared channels](/en-us/microsoftteams/shared-channels#getting-started-with-shared-channels) excluded, [Microsoft 365 people search](/en-us/microsoft-365/enterprise/multi-tenant-people-search) is typically scoped to within local tenant boundaries. In multitenant organizations with increased need for cross-tenant coworker collaboration, it's recommended to reciprocally provision users from their home tenants into the resource tenants of collaborating coworkers.

## New Microsoft Teams

The [new Microsoft Teams](/en-us/microsoftteams/new-teams-desktop-admin) experience improves upon Microsoft 365 people search and Teams external access for a unified seamless collaboration experience. For this improved experience to light up, the multitenant organization representation in Microsoft Entra ID is required and collaborating users shall be provisioned as B2B members. For more information, see [Announcing more seamless collaboration in Microsoft Teams for multitenant organizations](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/announcing-more-seamless-collaboration-in-microsoft-teams-for/ba-p/3901092).

## Collaborating user set

Collaboration in Microsoft 365 is built on the premise of reciprocal provisioning of B2B identities across multitenant organization tenants.

For example, say Annie in tenant A, Bob and Barbara in tenant B, and Charlie in tenant C want to collaborate. Conceptually, these four users represent a collaborating user set of four internal identities across three tenants.

[![Diagram that shows users in multiple tenants.](media/multi-tenant-organization-microsoft-365/multi-tenant-users.png)](media/multi-tenant-organization-microsoft-365/multi-tenant-users.png#lightbox)

For people search to succeed, while scoped to local tenant boundaries, the entire collaborating user set must be represented within the scope of each multitenant organization tenant A, B, and C, in the form of either internal or B2B identities.

[![Diagram that shows users represented across multiple tenants.](media/multi-tenant-organization-microsoft-365/multi-tenant-user-set.png)](media/multi-tenant-organization-microsoft-365/multi-tenant-user-set.png#lightbox)

Depending on your organization's needs, the collaborating user set might contain a subset of collaborating employees, or eventually all employees.

## Sharing your users

One of the simpler ways to achieve a collaborating user set in each multitenant organization tenant is for each tenant administrator to define their user contribution and synchronization them outbound. Tenant administrators on the receiving end should accept the shared users inbound.

- Administrator A contributes or shares Annie
- Administrator B contributes or shares Bob and Barbara
- Administrator C contributes or shares Charles

[![Diagram that shows users synchronized across multiple tenants.](media/multi-tenant-organization-microsoft-365/multi-tenant-user-sync.png)](media/multi-tenant-organization-microsoft-365/multi-tenant-user-sync.png#lightbox)

Microsoft 365 admin center facilitates orchestration of such a collaborating user set across multitenant organization tenants. For more information, see [Synchronize users in multitenant organizations in Microsoft 365](/en-us/microsoft-365/enterprise/sync-users-multi-tenant-orgs).

Alternatively, pair-wise configuration of inbound and outbound cross-tenant synchronization can be used to orchestrate such collating user set across multitenant organization tenants. For more information, see [What is a cross-tenant synchronization](cross-tenant-synchronization-overview).

## B2B member users

To ensure a seamless collaboration experience across the multitenant organization in new Microsoft Teams, B2B identities are provisioned as B2B users of [Member userType](../../external-id/user-properties#user-type).

| User synchronization method | Default userType property |
| --- | --- |
| [Synchronize users in multitenant organizations in Microsoft 365](/en-us/microsoft-365/enterprise/sync-users-multi-tenant-orgs) | **Member** Remains Guest, if the B2B identity already existed as Guest |
| [Cross-tenant synchronization in Microsoft Entra ID](cross-tenant-synchronization-overview) | **Member** Remains Guest, if the B2B identity already existed as Guest |

From a security perspective, you should review the default permissions granted to B2B member users. For more information, see [Compare member and guest default permissions](../../fundamentals/users-default-permissions#compare-member-and-guest-default-permissions).

To change the userType from **Guest** to **Member** (or vice versa), a source tenant administrator can amend the [attribute mappings](cross-tenant-synchronization-configure#step-9-review-attribute-mappings), or a target tenant administrator can [change the userType](../../fundamentals/how-to-manage-user-profile-info#add-or-change-profile-information) if the property isn't recurringly synchronized.

## Unsharing your users

To unshare users, you deprovision users by using the user deprovisioning capabilities available in Microsoft Entra cross-tenant synchronization. By default, when provisioning scope is reduced while a synchronization job is running, users fall out of scope and are soft deleted, unless Target Object Actions for Delete is disabled. For more information, see [Deprovisioning](cross-tenant-synchronization-overview#deprovisioning) and [Define who is in scope for provisioning](cross-tenant-synchronization-configure#step-8-optional-define-who-is-in-scope-for-provisioning-with-scoping-filters).