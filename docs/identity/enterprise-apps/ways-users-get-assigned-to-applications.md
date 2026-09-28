---
layout: Conceptual
title: Understand how users are assigned to apps - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/ways-users-get-assigned-to-applications
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Understand how users get assigned to an app that is using Microsoft Entra ID for identity management.
ms.topic: reference
ms.date: 2021-01-07T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.custom: enterprise-apps
locale: en-us
document_id: 93597292-2326-629a-3d21-267980e4e6d3
document_version_independent_id: 02e7e532-c6e6-332e-85eb-d7480cf1275a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/ways-users-get-assigned-to-applications.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/ways-users-get-assigned-to-applications
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/ways-users-get-assigned-to-applications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a16fcd77-5f31-ebc7-39cc-d38df15c3fff
---

# Understand how users are assigned to apps - Microsoft Entra ID | Microsoft Learn

This article helps you to understand how users get assigned to an application in your tenant.

## How do users get assigned an application in Microsoft Entra ID?

There are several ways a user can be assigned an application. Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves. Below describes the ways users can get assigned to applications:

- An administrator [assigns a user](assign-user-or-group-access-portal) to the application directly
- An administrator [assigns a group](assign-user-or-group-access-portal) that the user is a member of to the application, including:

    - A group that was synchronized from on-premises
    - A static security group created in the cloud
    - A [dynamic security group](../users/groups-dynamic-membership) created in the cloud
    - A Microsoft 365 group created in the cloud
    - The [All Users](/en-us/entra/fundamentals/how-to-manage-groups) group
- An administrator enables [Self-service Application Access](manage-self-service-access) to allow a user to add an application using [My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510)**Add App** feature **without business approval**
- An administrator enables [Self-service Application Access](manage-self-service-access) to allow a user to add an application using [My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510)**Add App** feature, but only **with prior approval from a selected set of business approvers**
- An administrator enables [Self-service Group Management](../users/groups-self-service-management) to allow a user to join a group that an application is assigned to **without business approval**
- An administrator enables [Self-service Group Management](../users/groups-self-service-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**
- One of the application's roles is included in an [entitlement management access package](../../id-governance/entitlement-management-access-package-resources), and a user requests or is assigned to that access package
- An administrator assigns a license to a user directly, for a Microsoft service such as [Microsoft 365](https://www.microsoft.com/microsoft-365)
- An administrator assigns a license to a group that the user is a member of, for a Microsoft service.
- A user [consents to an application](user-admin-consent-overview#user-consent) on behalf of themselves.