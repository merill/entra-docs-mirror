---
layout: Conceptual
title: Turn off per user MFA in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/recommendation-turn-off-per-user-mfa
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn why you should turn off per user MFA in Microsoft Entra ID with Microsoft Entra recommendations
ms.topic: how-to
ms.date: 2026-04-28T00:00:00.0000000Z
ms.reviewer: deawari
locale: en-us
document_id: fd87ffd0-745a-6e8e-417b-72f45f6f0710
document_version_independent_id: 97dad2aa-1c1e-d7f1-90bc-bf127da82dd3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/recommendation-turn-off-per-user-mfa.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/recommendation-turn-off-per-user-mfa
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/recommendation-turn-off-per-user-mfa.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: c57fc360-61aa-3154-968e-3a9bcbfdd53e
---

# Turn off per user MFA in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

[Microsoft Entra recommendations](overview-recommendations) is a feature that provides you with personalized insights and actionable guidance to align your tenant with recommended best practices.

This article covers the recommendation to switch per-user multifactor authentication (MFA) accounts to Conditional Access MFA accounts. This recommendation is called `switchFromPerUserMFA` in the recommendations API in Microsoft Graph.

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

As an admin, you want to maintain security for your company’s resources, but you also want your employees to easily access resources as needed. MFA enables you to enhance the security posture of your tenant.

In your tenant, you can enable MFA on a per-user basis. In this scenario, your users perform MFA each time they sign in. There are some exceptions, such as when they sign in from trusted IP addresses or when the "remember MFA on trusted devices" feature is turned on. While enabling MFA is a good practice, switching per-user MFA to MFA based on [Conditional Access](../conditional-access/overview) can reduce the number of times your users are prompted for MFA.

This recommendation shows up if:

- You have per-user MFA configured for at least 5% of your users.
- Conditional Access policies are active for more than 1% of your users (indicating familiarity with Conditional Access policies).

## Value

This recommendation improves your user's productivity and minimizes the sign-in time with fewer MFA prompts. Conditional Access and MFA used together help ensure that your most sensitive resources can have the tightest controls, while your least sensitive resources can be more freely accessible. For an overview of available functionality in Conditional Access, see [Building a Conditional Access policy](../conditional-access/concept-conditional-access-policies).

## Action plan

1. Require MFA using a Conditional Access policy.

    - [Enable Microsoft Entra multifactor authentication with Conditional Access](../authentication/tutorial-enable-azure-mfa).
    - Ensure that you're covering all resources and users you would like to secure with MFA.
2. Ensure that the per-user MFA configuration is turned off.

    1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
    2. Browse to **Users** &gt; **All users** and select the **Per-user MFA** button.

    [![Screenshot of the per-user MFA button in Microsoft Entra admin center.](media/recommendation-turn-off-per-user-mfa/disable-per-user-mfa.png)](media/recommendation-turn-off-per-user-mfa/disable-per-user-mfa-expanded.png#lightbox)

    1. Select **Disable MFA** for all users who had this option enabled.

    ![Screenshot of the per-user MFA settings in the admin center.](media/recommendation-turn-off-per-user-mfa/per-user-mfa-details.png)

After all users are migrated to Conditional Access MFA accounts, the recommendation status automatically updates the next time the service runs. Continue to review your Conditional Access policies.