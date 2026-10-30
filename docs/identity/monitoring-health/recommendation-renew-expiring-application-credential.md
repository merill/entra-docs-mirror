---
layout: Conceptual
title: Recommendation to renew expiring application credentials - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/recommendation-renew-expiring-application-credential
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how the Microsoft Entra recommendation to renew expiring application credentials works and why it's important.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.reviewer: saumadan
ms.custom: sfi-image-nochange
locale: en-us
document_id: 08f516f2-8b4d-7043-387a-96c746f47598
document_version_independent_id: 6a932262-af92-8ac4-6b84-5adc0bf7e894
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/recommendation-renew-expiring-application-credential.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/recommendation-renew-expiring-application-credential
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/recommendation-renew-expiring-application-credential.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4074ac66-59c3-43d7-dd30-fb2c6e964e19
---

# Recommendation to renew expiring application credentials - Microsoft Entra ID | Microsoft Learn

[Microsoft Entra recommendations](overview-recommendations) is a feature that provides you with personalized insights and actionable guidance to align your tenant with recommended best practices.

This article covers the recommendation to renew expiring application credentials. This recommendation is called `applicationCredentialExpiry` in the recommendations API in Microsoft Graph.

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

Application credentials can include certificates and other types of secrets that need to be registered with that application. These credentials are used to prove the identity of the application.

This recommendation shows up if your tenant has application credentials that will expire soon.

An application credential is expiring if:

- It's on an application registration AND is expiring within the next 30 days.

The following credentials are exempted from this recommendation:

- Credentials that were identified as expiring but have since been removed from the app registration
- Credentials whose expiration date has lapsed show as **completed** in the list of **Impacted resources**.

## Value

Renewing an application’s credentials prior to their expiry date is crucial for maintaining uninterrupted operations and minimizing the risk of any downtime resulting from outdated credentials.

## Action plan

This recommendation is available in the Microsoft Entra admin center and using the Microsoft Graph API.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#search-administrator).
2. Browse to **Entra ID** &gt; **Overview**.
3. Select the **Recommendations** tab and select the **Renew expiring application credentials** recommendation.
4. Take note of the following details from the **Impacted resources** table.

    - The **Resource** column displays the application name
    - The **ID** column displays the application ID

        [![Screenshot of the recommendation with the More details options highlighted.](media/recommendation-renew-expiring-application-credential/recommendation-renew-expiring-app-credentials.png)](media/recommendation-renew-expiring-application-credential/recommendation-renew-expiring-app-credentials-expanded.png#lightbox)
5. Select **More Details** from the **Actions** column.
6. From the panel that opens, select **Update Credential** to navigate directly to the **Certificates & secrets** area of the app registration to renew the expiring credential.

    1. Alternatively, browse to **Entra ID** &gt; **App registrations** and locate the application for which the credential needs to be rotated.

    [![Screenshot of the Microsoft Entra app registration page.](media/recommendation-renew-expiring-application-credential/app-registrations-list.png)](media/recommendation-renew-expiring-application-credential/app-registrations-list-expanded.png#lightbox)

    1. Navigate to the **Certificates & Secrets** section of the app registration.
7. Pick the credential type that you want to rotate and navigate to either **Certificates** or **Client Secret** tab and follow the prompts.

    [![Screenshot of the Certificates and secrets section of Microsoft Entra ID.](media/recommendation-renew-expiring-application-credential/app-certificates-secrets.png)](media/recommendation-renew-expiring-application-credential/app-certificates-secrets-expanded.png#lightbox)
8. Once the certificate or secret is successfully added, update the service code to ensure it works with the new credential and doesn't negatively affect customers.
9. Use the Microsoft Entra sign-in logs to validate that the Key ID of the credential matches the one that was recently added.
10. After validating the new credential, navigate back to **App registrations** &gt; **Certificates and Secrets** for the app and remove the old credential.

# [Microsoft Graph API](#tab/microsoft-graph-api)
The following requests can be used to retrieve the recommendation and the impacted resources using the Microsoft Graph API. To use the Microsoft Graph API, you need the `DirectoryRecommendations.Read.All` and `DirectoryRecommendations.ReadWrite.All` permissions. For more information, see [How to use Identity Recommendations](howto-use-recommendations).

1. Sign in to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Select **GET** as the HTTP method from the dropdown.

To retrieve all recommendations for your tenant:

```http
GET https://graph.microsoft.com/beta/directory/recommendations
```

From the response, find the ID of the recommendation that matches the following pattern: `{tenantId}_ApplicationCredentialExpiry`.

To identify impacted resources:

```http
GET https://graph.microsoft.com/beta/directory/recommendations/{tenantId}_ApplicationCredentialExpiry
```

To filter the resources based on their status (for example, *active* resources):

```http
GET https://graph.microsoft.com/beta/directory/recommendations/536279f6-15cc-45f2-be2d-61e352b51eef_ ApplicationCredentialExpiry’/impactedResources?$filter=status eq Microsoft.Graph.recommendationStatus'active'
```

Take note of the `AppId`, `CredentialId`, and `Origin` of the credential you want to remove. To remove the credential, use the following Microsoft Graph guidance:

- [addPassword](/en-us/graph/api/application-addpassword?view=graph-rest-1.0&amp;preserve-view=true)
- [addKey](/en-us/graph/api/application-addkey?view=graph-rest-1.0&amp;preserve-view=true)
- [removePassword](/en-us/graph/api/application-removepassword?view=graph-rest-1.0&amp;preserve-view=true)
- [removeKey](/en-us/graph/api/application-removekey?view=graph-rest-1.0&amp;preserve-view=true)

#### Sample response

```json
 {
  "id": "aaaabbbb-6666-cccc-7777-dddd8888eeee_ApplicationCredentialExpiry",
  "recommendationType": "applicationCredentialExpiry",
  "createdDateTime": "2022-06-08T00:08:01Z",
  "impactStartDateTime": "2022-06-08T00:08:01Z",
  "postponeUntilDateTime": null,
  "lastModifiedDateTime": "2024-07-29T12:03:16Z",
  "lastModifiedBy": "System",
  "displayName": "Renew expiring application credentials",
  "featureAreas": [
    "applications"
  ],
  "insights": "Your tenant has applications with credentials that will expire soon.",
  "benefits": "Renewing the app credential(s) before its expiration ensures the application continues to function and reduces the possibility of downtime due to an expired credential.",
  "category": "identityBestPractice",
  "status": "active",
  "priority": "high",
  "requiredLicenses": "microsoftEntraWorkloadId",
  "impactType": "apps",
  "actionSteps": [
    {
      "stepNumber": 1,
      "text": "1. Navigate to the App registration section and locate the application for which the credential needs to be rotated."
    },
    {
      "stepNumber": 2,
      "text": "2. Navigate to the “Certificates & Secrets” blade of the app registration."
    },
    {
      "stepNumber": 3,
      "text": "3. Pick the credential type that you want to rotate and navigate to either “Certificates” or “Client Secret” tab and follow the prompts.",
      "actionUrl": null
    },
    {
      "stepNumber": 4,
      "text": "4. Once the certificate or secret is successfully added, update the service code to ensure it works with the new credential and has no negative customer impact. You should use Microsoft Entra ID’s sign-in logs to validate that the thumbprint of the certificate matches the one that was just uploaded.",
      "actionUrl": null
    },
    {
      "stepNumber": 5,
      "text": "5. After validating the new credential, navigate back to the Certificates and Secrets blade for the app and remove the old credential.",
      "actionUrl": null
    }
  ]
}
```

---