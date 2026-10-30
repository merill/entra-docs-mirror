---
layout: Conceptual
title: Recommendation to migrate applications away from AD FS - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/recommendation-migrate-apps-from-adfs-to-azure-ad
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the recommendation to migrate application authentication from AD FS to Microsoft Entra ID
ms.topic: how-to
ms.date: 2026-04-28T00:00:00.0000000Z
ms.reviewer: jadedsouza
locale: en-us
document_id: 08c73b17-8961-b8d3-9e7f-5009ccb25638
document_version_independent_id: f9da2994-8cfb-b0ec-0efe-fb86a7848aef
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/recommendation-migrate-apps-from-adfs-to-azure-ad.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/recommendation-migrate-apps-from-adfs-to-azure-ad
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/recommendation-migrate-apps-from-adfs-to-azure-ad.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ed51ca62-004d-8f37-826c-1422d55a8c07
---

# Recommendation to migrate applications away from AD FS - Microsoft Entra ID | Microsoft Learn

[Microsoft Entra recommendations](overview-recommendations) provides you with personalized insights and actionable guidance to align your tenant with recommended best practices.

This article covers the recommendation to migrate apps from Active Directory Federated Services (AD FS) to Microsoft Entra ID. This recommendation is called `adfsAppsMigration` in the recommendations API in Microsoft Graph.

## Prerequisites

There are different role requirements for viewing or updating a recommendation. Use the least-privileged role for the type of access needed. For a full list of roles, see [Least privileged roles by task](../role-based-access-control/delegate-by-task#monitoring-and-health---recommendations-least-privileged-roles).

| Microsoft Entra role | Access type |
| --- | --- |
| Reports Reader | Read-only |
| Security Reader | Read-only |
| Global Reader | Read-only |
| Authentication Policy Administrator | Update and read |
| Exchange Administrator | Update and read |
| Security Administrator | Update and read |
| `DirectoryRecommendations.Read.All` | Read-only in Microsoft Graph |
| `DirectoryRecommendations.ReadWrite.All` | Update and read in Microsoft Graph |

Some recommendations might require a P2 or other license. For more information, see the [Recommendations overview table](overview-recommendations#recommendations-overview-table).

## Description

As an admin responsible for managing applications, you want your applications to use the security features of Microsoft Entra ID and maximize their value. This recommendation shows up if your tenant has apps on ADFS that can 100% be migrated to Microsoft Entra ID. For more information, see [Understand the stages of migrating application authentication from AD FS to Microsoft Entra ID](../enterprise-apps/migrate-adfs-apps-stages).

## Value

Using Microsoft Entra ID gives you granular per-application access controls to secure access to applications. With Microsoft Entra B2B collaboration, you can increase user productivity. Automated app provisioning automates the user identity lifecycle in cloud SaaS apps such as Dropbox, Salesforce, and more.

## Action plan

1. [Install Microsoft Entra Connect](../hybrid/connect/how-to-connect-install-roadmap) on your AD FS server.
2. [Review the AD FS application activity report](../enterprise-apps/migrate-adfs-application-activity) to get insights about your AD FS applications.
3. Read the solution guide for [migrating applications to Microsoft Entra ID](../enterprise-apps/migrate-adfs-apps-stages).
4. Migrate applications to Microsoft Entra ID. For more information, see the article [Migrate from federation to cloud authentication](../hybrid/connect/migrate-from-federation-to-cloud-authentication).

### Guided walkthrough

For a guided walkthrough of many of the recommendations in this article, see the migration guide [Migrate from AD FS to Microsoft Entra ID for identity management](https://go.microsoft.com/fwlink/?linkid=2225005) when signed in to the Microsoft 365 admin center. To review best practices without signing in and activating automated setup features, go to the Microsoft 365 Setup portal.