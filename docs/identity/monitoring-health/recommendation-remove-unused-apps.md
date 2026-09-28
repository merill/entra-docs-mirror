---
layout: Conceptual
title: Recommendation to remove unused apps - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/recommendation-remove-unused-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how the Microsoft Entra recommendation to remove unused apps works and why you should follow the guidance.
ms.topic: how-to
ms.date: 2026-01-07T00:00:00.0000000Z
ms.reviewer: saumadan
locale: en-us
document_id: cfcc3850-9717-41b7-94fd-7c6780f6a9ce
document_version_independent_id: 3d47cffa-f296-cf5b-755f-7a4563564e95
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/recommendation-remove-unused-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/recommendation-remove-unused-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/recommendation-remove-unused-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: 9e917f8c-5687-faf8-ea53-f5594f68b115
---

# Recommendation to remove unused apps - Microsoft Entra ID | Microsoft Learn

[Microsoft Entra recommendations](overview-recommendations) is a feature that provides you with personalized insights and actionable guidance to align your tenant with recommended best practices.

This article covers the recommendation to investigate unused applications. This recommendation is called `staleApps` in the recommendations API in Microsoft Graph.

Note

With [Microsoft Security Copilot](/en-us/copilot/security/microsoft-security-copilot), you can use natural language prompts to get insights on unused applications. Learn more about how to [Assess application risks using Microsoft Security Copilot](/en-us/entra/fundamentals/copilot-security-entra-investigate-risky-apps#explore-unused-microsoft-entra-applications).

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

This recommendation shows up if your tenant has applications that haven't been used for over 90 days. The following scenarios are included in this recommendation:

- The app was created but never used.
- The app isn't [soft deleted](../../identity-platform/howto-restore-app) from the application portfolio.
- The app isn't used by the tenant where it resides nor any of its instances (Service Principal) in other tenants.
- It's a client app that calls other resource apps, but hasn't been issued any tokens in the past 90 days.
- It's a resource app that doesn't have a record of any client apps requesting a token in the past 90 days.

The following apps are exempted from this recommendation:

- Apps that are managed by Microsoft, including anything created or modified by Microsoft-owned applications.
- Apps that work with other apps to obtain tokens or are used to enable scenarios that don't require tokens.
    - For example, [Peer-to-peer server](/en-us/windows/win32/p2psdk/what-is-peer-networking-), [Application proxy](../app-proxy/overview-what-is-app-proxy), [Microsoft Entra Cloud Sync](../hybrid/cloud-sync/what-is-cloud-sync), [linked single-sign-on](../enterprise-apps/configure-linked-sign-on), [password SSO](../enterprise-apps/configure-password-single-sign-on-non-gallery-applications), [Office add-ins](/en-us/office/dev/add-ins/publish/host-an-office-add-in-on-microsoft-azure), and [managed identities](../managed-identities-azure-resources/overview) are excluded from this recommendation.
- Apps that were created within the past 90 days.

## Value

Removing unused applications helps reduce the attack surface area and helps clean up the app portfolio of a tenant.

## Action plan

This recommendation is available in the Microsoft Entra admin center and using the Microsoft Graph API. Once you identify the applications that aren't being used, you can decide whether to remove them or keep them based on your organization's needs. The action plan is therefore broken down into two parts:

1. Review the applications that are flagged as unused.
2. Determine if the application is needed and how to address it.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
Applications identified by the recommendation appear in the list of **Impacted resources** at the bottom of the recommendation.

### Review the applications

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#search-administrator).
2. Browse to **Entra ID** &gt; **Overview**.
3. Select the **Recommendations** tab and select the **Remove unused applications** recommendation.
4. From the **Impacted resources** table, select **More details** to view more details.
5. Select the **Resource**link to go directly to the app registration for the app.
    - Alternatively, you can browse to **Entra ID** &gt; **App registrations** and locate the application that was surfaced as part of this recommendation.

### Determine if the application is needed

There are many reasons why an app might be unused. Consider the app's usage scenario and business function. For example:

- Was the app deprecated?
- Is the app used for a business function that only happens at certain times of the year?

To remove the application:

1. [Soft delete](../../identity-platform/howto-restore-app) the app from your tenant.
2. Wait 15 days and then [permanently delete the app](../../identity-platform/howto-restore-app#permanently-delete-an-application).

To indicate the application is still needed and skip the recommendation:

- [Update the recommendation status](howto-use-recommendations#how-to-update-a-recommendation-and-impacted-resources) to **dismissed** or **postponed**.
    - Use **dismissed** if determined that the app will remain inactive for the rest of its lifecycle.
    - Use **dismissed** if you think the app as included in the recommendation in error.
    - Use **postponed** if you need more time to review the app.

# [Microsoft Graph API](#tab/microsoft-graph-api)
The following requests can be used to retrieve the recommendation and the impacted resources using the Microsoft Graph API. To use the Microsoft Graph API, you need the `DirectoryRecommendations.Read.All` and `DirectoryRecommendations.ReadWrite.All` permissions. For more information, see [How to use Identity Recommendations](howto-use-recommendations).

1. Sign in to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Select **GET** as the HTTP method from the dropdown.

### Review the applications

To retrieve all recommendations for your tenant:

```http
GET https://graph.microsoft.com/beta/directory/recommendations
```

From the response, find the ID of the recommendation that matches the following pattern: `{tenantId}_staleApps`.

To identify impacted resources:

```http
GET https://graph.microsoft.com/beta/directory/recommendations/{tenantId}_staleApps
```

To filter the resources based on their status (for example, *active* resources):

```http
GET https://graph.microsoft.com/beta/directory/recommendations/{tenantId}_staleApps/impactedResources?$filter=status eq Microsoft.Graph.recommendationStatus'active' 
```

Identify the `applicationObjectId` or `appId` of the unused app you want to delete.

#### Sample response

```json
{
    "id": "ccccdddd-2222-eeee-3333-ffff4444aaaa_staleApps",
    "recommendationType": "staleApps",
    "createdDateTime": "2022-06-16T01:18:55Z",
    "impactStartDateTime": "2022-06-16T01:18:55Z",
    "postponeUntilDateTime": null,
    "lastModifiedDateTime": "2024-07-26T14:17:24Z",
    "lastModifiedBy": "System",
    "displayName": "Remove unused applications",
    "featureAreas": [
        "applications"
    ],
    "insights": "Your tenant has some applications that have not been used in the past 90 days.",
    "benefits": "Removing unused applications improves the security posture and promotes good application hygiene.",
    "category": "identityBestPractice",
    "status": "active",
    "priority": "medium",
    "requiredLicenses": "microsoftEntraWorkloadId",
    "impactType": "apps",
    "actionSteps": [
        {
            "stepNumber": 1,
            "text": "1. Navigate to the app registration blade and delete the unused application."
        },
        {
            "stepNumber": 2,
            "text": "2. We suggest you take appropriate steps to ensure the application is not used in longer intervals of more than 90 days. If so, you should change the frequency of access such that the application’s last used time is within 90 days from its last access date."
        }
    ]
}
```

### Determine if the application is needed

Consider the app's usage scenario and business function:

- Was the app deprecated?
- Is the app used for a business function that only happens at certain times of the year?

If you can delete the app, run one of the following queries to delete the application:

```http
DELETE /applications/{applicationObjectId}
DELETE /applications(appId='{appId}')
```

Wait 15 days and then follow the [Permanently delete an item](/en-us/graph/api/directory-deleteditems-delete?view=graph-rest-1.0&amp;preserve-view=true) Microsoft Graph API guidance.

---