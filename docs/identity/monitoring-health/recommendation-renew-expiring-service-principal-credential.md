---
layout: Conceptual
title: Renew expiring service principal credentials recommendation - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/recommendation-renew-expiring-service-principal-credential
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how the Microsoft Entra recommendation to renew expiring service principal credentials work and why it's important.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.reviewer: saumadan
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2d06424a-c23c-821a-a319-88ffe9a731c4
document_version_independent_id: 3ff156a2-d077-d58c-68e9-e8be8934c54c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/recommendation-renew-expiring-service-principal-credential.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/recommendation-renew-expiring-service-principal-credential
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/recommendation-renew-expiring-service-principal-credential.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: aa16050e-ef59-c079-1239-f60bc2c5183a
---

# Renew expiring service principal credentials recommendation - Microsoft Entra ID | Microsoft Learn

[Microsoft Entra recommendations](overview-recommendations) is a feature that provides you with personalized insights and actionable guidance to align your tenant with recommended best practices.

This article covers the recommendation to renew expiring service principal credentials. This recommendation is called `servicePrincipalKeyExpiry` in the recommendations API in Microsoft Graph.

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

Service principal credentials include certificates and client secrets added to a service principal. The credentials are used to prove the identity of that service principal. If the credentials expire, the service principal can't authenticate, which can cause downtime for your business scenario. This recommendation shows up if your tenant has service principals with credentials that are expiring soon.

A service principal credential is expiring if:

- It's on a service principal AND is expiring within the next 30 days.

The following credentials are exempted from this recommendation:

- Credentials that were identified as expiring but have since been removed from the application registration.
- Credentials whose expiration date has lapsed show as **completed** in the list of **Impacted resources**.

## Value

Renewing a service principal's credentials prior to their expiry date is crucial for maintaining uninterrupted operations and minimizing the risk of any downtime resulting from outdated credentials.

## Action plan

This recommendation is available in the Microsoft Entra admin center and using the Microsoft Graph API.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#search-administrator).
2. Browse to **Entra ID** &gt; **Overview**.
3. Select the **Recommendations** tab and select the **Renew expiring service principal credentials** recommendation.
4. Select **More Details** from the **Actions** column.
5. From the panel that opens, select **Update Credential** to navigate directly to the **Single sign-on** area of the app registration.

    1. Alternatively, browse to **Entra ID** &gt; **App registrations** and locate the application for which the credential needs to be rotated.

    [![Screenshot of the Microsoft Entra app registration page.](media/recommendation-renew-expiring-service-principal-credential/app-registrations-list.png)](media/recommendation-renew-expiring-service-principal-credential/app-registrations-list-expanded.png#lightbox)

    1. Navigate to the **Single sign-on** section of the app registration.
6. Edit the **SAML signing certificate** section and follow the prompts to add a new certificate.

    [![Screenshot of the edit single-sign-on process.](media/recommendation-renew-expiring-service-principal-credential/recommendation-edit-single-sign-on.png)](media/recommendation-renew-expiring-service-principal-credential/recommendation-edit-single-sign-on-expanded.png#lightbox)
7. Once the certificate or secret is successfully added, update the SAML signing certificate configuration to make the new cert active.
8. Verify that the application works as expected then remove the inactive SAML certificate from the SAML certificates collection.

Note

If you don't have any SAML credentials configured but you received this recommendation, use the Microsoft Graph [**ServicePrincipalAPI**](/en-us/graph/api/resources/serviceprincipal?view=graph-rest-1.0&amp;preserve-view=true) endpoint to check the `keyCredentials` and `passwordCredentials` properties of the service principal object. Locate and rotate the credential.

We highly recommend changing your service so that it works with the credential defined on the backing application object instead of the service principal.

# [Microsoft Graph API](#tab/microsoft-graph-api)
The following requests can be used to retrieve the recommendation and the impacted resources using the Microsoft Graph API. To use the Microsoft Graph API, you need the `DirectoryRecommendations.Read.All` and `DirectoryRecommendations.ReadWrite.All` permissions. For more information, see [How to use Identity Recommendations](howto-use-recommendations).

When renewing service principal credentials using Microsoft Graph, you need to run a query to get the password credentials on a service principal, add a new password credential, then remove the old credentials.

1. Sign in to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Select **GET** as the HTTP method from the dropdown.

To retrieve all recommendations for your tenant:

```http
GET https://graph.microsoft.com/beta/directory/recommendations
```

From the response, find the ID of the recommendation that matches the following pattern: `{tenantId}_servicePrincipalKeyExpiry`.

To identify impacted resources:

```http
GET https://graph.microsoft.com/beta/directory/recommendations/{tenantId}_servicePrincipalKeyExpiry
```

To filter the list of resources based on their status, for example only resources that are marked as `active`:

```http
https://graph.microsoft.com/beta/directory/recommendations/{tenantId}_ servicePrincipalKeyExpiry/impactedResources?$filter=status eq Microsoft.Graph.recommendationStatus'active'
```

- Take note of the `AppId`, `CredentialId`, and the origin of the credential you want to remove.
- Use these Microsoft Graph APIs to add a new password or key credential:
    - [addPassword](/en-us/graph/api/serviceprincipal-addpassword?view=graph-rest-1.0&amp;preserve-view=true)
    - [addKey](/en-us/graph/api/serviceprincipal-addkey?view=graph-rest-1.0&amp;preserve-view=true)
- Use these Microsoft Graph APIs to remove the old credential:
    - [removePassword](/en-us/graph/api/serviceprincipal-removepassword?view=graph-rest-1.0&amp;preserve-view=true)
    - [removeKey](/en-us/graph/api/serviceprincipal-removekey?view=graph-rest-1.0&amp;preserve-view=true)

#### Sample response

```json
{
  "id": "ddddeeee-3333-ffff-4444-aaaa5555bbbb_ServicePrincipalKeyExpiry",
  "recommendationType": "servicePrincipalKeyExpiry",
  "createdDateTime": "2022-05-29T00:11:17Z",
  "impactStartDateTime": "2022-05-29T00:11:17Z",
  "postponeUntilDateTime": null,
  "lastModifiedDateTime": "2024-07-26T12:31:58Z",
  "lastModifiedBy": "System",
  "displayName": "Renew expiring service principal credentials",
  "featureAreas": [
    "applications"
  ],
  "insights": "Your tenant has service principals with credentials that will expire soon.",
  "benefits": "Renewing the service principal credential(s) before expiration ensures the application continues to function and reduces the possibility of downtime due to an expired credential.",
  "category": "identityBestPractice",
  "status": "completedBySystem",
  "priority": "high",
  "requiredLicenses": "microsoftEntraWorkloadId",
  "impactType": "apps",
  "actionSteps": [
    {
      "stepNumber": 1,
      "text": "1. Navigate to the Enterprise applications section and locate the Enterprise application for which the credential needs to be rotated."
    },
    {
      "stepNumber": 2,
      "text": "2. Navigate to the “Single sign-on” blade."
    },
    {
      "stepNumber": 3,
      "text": "3. Edit the 'SAML signing certificate' section and follow prompts to add a new certificate."
    },
    {
      "stepNumber": 4,
      "text": "4. After adding the certificate, change its properties to make certificate active. This will make the previous certificate inactive."
    },
    {
      "stepNumber": 5,
      "text": "5. Once the certificate is successfully added and activated, validate that your service is working with the new credential, and remove the old credential."
    },
    {
      "stepNumber": 6,
      "text": "6. If the service principal does not show any credentials after navigating to the enterprise apps blade, we recommend checking the 'passwordCredentials' and 'keyCredentials' property of the service principal object using PowerShell or Microsoft Graph service principal API and use the Microsoft Graph API to rotate credentials."
    }
  ]
}
```

---