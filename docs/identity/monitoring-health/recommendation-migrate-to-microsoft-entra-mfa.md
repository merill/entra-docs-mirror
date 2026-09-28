---
layout: Conceptual
title: Recommendation to migrate to Microsoft Entra MFA - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/recommendation-migrate-to-microsoft-entra-mfa
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the Microsoft Entra recommendation to migrate to Microsoft Entra multifactor authentication from MFA server
ms.topic: how-to
ms.date: 2026-04-28T00:00:00.0000000Z
ms.reviewer: jupetter
locale: en-us
document_id: 38b607bb-7095-55d2-597a-f99e6f621e0b
document_version_independent_id: 38b607bb-7095-55d2-597a-f99e6f621e0b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/recommendation-migrate-to-microsoft-entra-mfa.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/recommendation-migrate-to-microsoft-entra-mfa
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/recommendation-migrate-to-microsoft-entra-mfa.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ce9e14cf-31a4-da5b-da5e-5b26e690e875
---

# Recommendation to migrate to Microsoft Entra MFA - Microsoft Entra ID | Microsoft Learn

[Microsoft Entra recommendations](overview-recommendations) provide you with personalized insights and actionable guidance to align your tenant with recommended best practices.

This article covers the recommendation to migrate from MFA server to Microsoft Entra MFA. This recommendation is called `mfaServerDeprecation` in the recommendations API in Microsoft Graph.

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

Azure Multi-Factor Authentication Server (MFA Server) was scheduled for retirement on September 30th, 2024. To help organizations migrate to Microsoft Entra MFA, this Microsoft Entra recommendation identifies tenants with MFA server activity. This recommendation identifies tenants with active users and MFA attempts for MFA Server in the last seven days. MFA Server client integrations, including a list of affected clients are also surfaced as a part of this recommendation.

## Value

MFA Server is a component for deploying and managing MFA on-premises. In 2019, Microsoft stopped allowing new deployments of MFA Server and investing in feature enhancements. In September 2022, [Microsoft formally announced the deprecation of MFA Server](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/microsoft-entra-change-announcements-september-2022-train/ba-p/2967454).

Cloud-based, Microsoft Entra multifactor authentication offers better resiliency, availability, and data compliancy. Migrating to Microsoft Entra MFA helps you improve your security posture by giving you access to the latest phishing-resistant authentication methods and more fine-grained access controls. It also helps reduce cost and deployment complexity by no longer having to maintain an on-premises component.

## Action plan

1. [Learn how to migrate MFA Server to Microsoft Entra MFA](../authentication/how-to-migrate-mfa-server-to-mfa-user-authentication).
2. Migrate MFA user information from on-premises to Microsoft Entra.

    - You can either migrate this information manually or use the MFA Server Migration Utility (recommended).
    - [How to use the MFA Server Migration Utility](../authentication/how-to-mfa-server-migration-utility).
3. Use [Staged Rollout](../authentication/how-to-mfa-server-migration-utility#enable-staged-rollout) to reroute users to authenticate against Microsoft Entra instead of MFA Server.
4. Identify and migrate any MFA Server dependencies, such as applications using [RADIUS or LDAP authentication](../authentication/how-to-mfa-server-migration-utility#authentication-services).
5. Update domain federation settings and decommission MFA Server.