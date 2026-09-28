---
layout: Conceptual
title: Recommendation to migrate to Microsoft Graph API - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/recommendation-migrate-to-microsoft-graph-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the Microsoft Entra recommendation to migrate from Azure Active Directory Graph APIs to Microsoft Graph APIs.
ms.topic: how-to
ms.date: 2026-04-28T00:00:00.0000000Z
ms.reviewer: krbash
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9e92692e-ab17-1588-5027-5620f068423a
document_version_independent_id: 9e92692e-ab17-1588-5027-5620f068423a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/recommendation-migrate-to-microsoft-graph-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/recommendation-migrate-to-microsoft-graph-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/recommendation-migrate-to-microsoft-graph-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: edb5b1ae-3152-4c58-d0d4-579aafaa456c
---

# Recommendation to migrate to Microsoft Graph API - Microsoft Entra ID | Microsoft Learn

[Microsoft Entra recommendations](overview-recommendations) provide you with personalized insights and actionable guidance to align your tenant with recommended best practices.

This article covers two recommendations to migrate applications and service principals from Azure AD Graph APIs to Microsoft Graph. These recommendations are called `aadGraphDeprecationApplication` and `aadGraphDeprecationServicePrincipal` in the recommendations API in Microsoft Graph.

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

The deprecation of Azure Active Directory (Azure AD) Graph APIs was announced in 2020 and are now in the retirement cycle. All applications and service principals need to migrate to the new Microsoft Graph APIs.

In general, applications and service principals that are still using Azure AD Graph APIs were developed by your organization or a vendor. These applications likely need to be updated by your developers or upgraded to a new version.

There are two recommendations associated with the deprecation of Azure AD Graph. One provides a list of applications and one provides a list of service principals. Both recommendations need to be addressed separately.

### Applications and Service Principals

The Applications version of this recommendation details applications that are registered in your tenant and calling Azure AD Graph APIs. Think, app registrations in the Microsoft Entra admin center.

The Service Principals version of this recommendation details applications that are registered in another tenant, but consented for use in your tenant. Think, enterprise applications in the Microsoft Entra admin center. These applications could be supplied by a developer in your multitenant company or a software vendor. For Service Principals, you likely need to contact the vendor to identify how to get an update to a newer version of the application.

## Value

Microsoft Graph offers a single unified endpoint to access Microsoft Entra and Microsoft 365 services. Microsoft Graph APIs have all the capabilities of Azure AD Graph APIs, plus many newer API features. The Microsoft Graph client libraries offer built-in support for features, such as retry handling, secure redirects, transparent authentication, and payload compression. These capabilities weren't available with Azure AD Graph.

Any applications or service principals still calling Azure AD Graph will be affected by future retirement activity. To prevent loss of functionality, we recommend migrating to Microsoft Graph.

## Action plan

Both of the recommendations include a list of impacted resources. The process to review and update applications and service principals are similar.

1. Review the list of **applications** and **service principals** calling Azure AD Graph under **Impacted Resources** in the recommendations details.
2. Select the **More Details** link to view the following details about the Azure AD Graph API activity.

    ![Screenshot of the impacted applications.](media/recommendation-migrate-to-microsoft-graph-api/applications-to-migrate.png)

    - **Operation Name**: Description of the API operation, such as List Application, Create User, or Delete Group
    - **Requests - 30 Days**: The number of requests made by this application in the last 30 days
    - **Last Request Date**: The date and time the operation was last performed by the operation.

    ![Screenshot of the additional details for the selected app.](media/recommendation-migrate-to-microsoft-graph-api/applications-to-migrate-additional-details.png)
3. Work with the owner or publisher of the corresponding application to identify the steps required to update the application.

These recommendations show as **Active** until there is no Azure AD Graph API activity for 30 days. After 30 days of no Azure AD Graph API activity, that application or service principal is marked as **Completed**. Once all resources are addressed, the recommendation is marked as **Completed**.