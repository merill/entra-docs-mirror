---
layout: Conceptual
title: Recommendation to remove unused credentials from apps - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/recommendation-remove-unused-credential-from-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how the Microsoft Entra recommendation to remove unused credentials from apps works and why it's important.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.reviewer: saumadan
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3d76bf74-817f-6267-c194-fe9728e04950
document_version_independent_id: b64adbe3-44da-7eb2-2f02-b3cf758bb377
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/recommendation-remove-unused-credential-from-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/recommendation-remove-unused-credential-from-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/recommendation-remove-unused-credential-from-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2f0df9fb-9765-0106-584d-55719ac2ae2a
---

# Recommendation to remove unused credentials from apps - Microsoft Entra ID | Microsoft Learn

[Microsoft Entra recommendations](overview-recommendations) is a feature that provides you with personalized insights and actionable guidance to align your tenant with recommended best practices.

This article covers the recommendation to remove unused credentials from apps. This recommendation is called `staleAppCreds` in the recommendations API in Microsoft Graph.

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

Application credentials can include certificates and other types of secrets that need to be registered with that application. These credentials are used to prove the identity of the application. Only credentials actively in use by an application should remain registered with the application.

A credential is considered unused if:

- It has not been used in the past 30 days.
- It's a credential that was added to an application to be used for OAuth/OIDC flows or to the service principal for SAML flow.

The following credentials are exempted from the recommendation:

- Expired credentials do not show in the **Impacted resources** list.
- Credentials that were identified as unused but have expired since being flagged show as **Completed** in the **Impacted resources** list.

## Value

Removing unused application credentials helps reduce the attack surface area and helps declutter the app portfolio of a tenant.

## Action plan

This recommendation is available in the Microsoft Entra admin center and using the Microsoft Graph API.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
Applications that the recommendation identified appear in the list of **Impacted resources** at the bottom of the recommendation.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#search-administrator).
2. Browse to **Entra ID** &gt; **Overview**.
3. Select the **Recommendations** tab and select the **Remove unused credentials from applications** recommendation.
4. Take note of the following details from the **Impacted resources** table.

    - The **Resource** column displays the application name
    - The **ID** column displays the application ID
5. Select **More Details** from the **Actions** column to view more details.

    [![Screenshot of the recommendation with the More details options highlighted.](media/recommendation-remove-unused-credential-from-apps/recommendation-remove-unused-credentials-from-apps.png)](media/recommendation-remove-unused-credential-from-apps/recommendation-remove-unused-credentials-from-apps-expanded.png#lightbox)

    Note

    If the origin of the credential is Service Principal, follow the guidance in the **Service principals** section.
6. From the panel that opens, select **Update Credential** to navigate directly to the **Certificates & secrets** area of the app registration to remove the unused credential.

    1. Alternatively, browse to **Entra ID** &gt; **App registrations** and select the application that was surfaced as part of this recommendation.

        [![Screenshot of the Microsoft Entra app registration page.](media/recommendation-remove-unused-credential-from-apps/app-registrations-list.png)](media/recommendation-remove-unused-credential-from-apps/app-registrations-list-expanded.png#lightbox)
    2. Then navigate to the **Certificates & Secrets** section of the app registration.

        [![Screenshot of the Certificates and secrets section of Microsoft Entra ID.](media/recommendation-remove-unused-credential-from-apps/app-certificates-secrets.png)](media/recommendation-remove-unused-credential-from-apps/app-certificates-secrets-expanded.png#lightbox)
7. **Locate the unused credential and remove it.**

# [Microsoft Graph API](#tab/microsoft-graph-api)
The following requests can be used to retrieve the recommendation and the impacted resources using the Microsoft Graph API. To use the Microsoft Graph API, you need the `DirectoryRecommendations.Read.All` and `DirectoryRecommendations.ReadWrite.All` permissions. For more information, see [How to use Identity Recommendations](howto-use-recommendations).

1. Sign in to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Select **GET** as the HTTP method from the dropdown.

To retrieve all recommendations for your tenant:

```http
GET https://graph.microsoft.com/beta/directory/recommendations
```

From the response, find the ID of the recommendation that matches the following pattern: `{tenantId}_staleAppCreds`.

To identify impacted resources:

```http
GET https://graph.microsoft.com/beta/directory/recommendations/{tenantId}_staleAppCreds
```

To filter the resources based on their status (for example, *active* resources):

```http
GET https://graph.microsoft.com/eta/directory/recommendations/{tenantId}_staleAppCreds/impactedResources?$filter=status eq Microsoft.Graph.recommendationStatus'active'
```

- Take note of the `AppId`, `CredentialId`, and origin of the credential you want to remove.
- Use these Microsoft Graph APIs to add a new password or key credential:
    - [removePassword](/en-us/graph/api/application-removepassword?view=graph-rest-1.0&amp;preserve-view=true)
    - [removeKey](/en-us/graph/api/application-removekey?view=graph-rest-1.0&amp;preserve-view=true)

#### Sample response

```json
{
  "id": "aaaabbbb-0000-cccc-1111-dddd2222eeee_staleAppCreds",
  "recommendationType": "staleAppCreds",
  "createdDateTime": "2022-09-07T21:25:36Z",
  "impactStartDateTime": "2022-09-07T21:25:36Z",
  "postponeUntilDateTime": null,
  "lastModifiedDateTime": "2024-07-22T15:23:29Z",
  "lastModifiedBy": "System",
  "displayName": "Remove unused credentials from applications",
  "featureAreas": [
    "applications"
  ],
  "insights": "Your tenant has applications with credentials which have not been used in more than 30 days.",
  "benefits": "An application credential is used to get a token that grants access to a resource or another service.",
  "category": "identityBestPractice",
  "status": "active",
  "priority": "medium",
  "releaseType": "preview",
  "requiredLicenses": "microsoftEntraWorkloadId",
  "impactType": "apps",
  "actionSteps": [
    {
      "stepNumber": 1,
      "text": "1. For application resources, navigate to the app registration section in your tenant."
    },
    {
      "stepNumber": 2,
      "text": "2. In the ‘Certificate and Secrets’ blade, find the credential and remove it."
    },
    {
      "stepNumber": 3,
      "text": "3. To remove a credential from a service principal resource, use the MS Graph Service Principal API service action ",
      "actionUrl": {
        "displayName": "`removePassword`",
        "url": "https://docs.microsoft.com/graph/api/serviceprincipal-removepassword?view=graph-rest-1.0&tabs=http"
      }
    }
  ]
}
```

---

## Service principals

If the origin of the credential is **service principal**, there are a few considerations and extra steps to follow.

Because there's often multiple service principals for a single application, it might be easier to navigate to Enterprise apps to view everything in one place.

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), browse to **Entra ID** &gt; **Enterprise apps**.
2. Search for and open the application that was surfaced as part of this recommendation.
3. Select **Single sign-on** from the side menu.

    If the credential is a service principal but there are SAML certificates in use, you can identify the details of the credential using the Microsoft Graph API. To use the Microsoft Graph API, you need the `DirectoryRecommendations.Read.All` and `DirectoryRecommendations.ReadWrite.All` permissions. For more information, see [How to use Identity Recommendations](howto-use-recommendations).
4. Sign in to [Graph Explorer](https://aka.ms/ge).
5. Select **GET** as the HTTP method from the dropdown.
6. Set the API version to **beta**.
7. Query the `keyCredential` and `passwordCredential` endpoints.
8. Use the `removePassword` or `removeKey` endpoints to remove the credential from the service principal.