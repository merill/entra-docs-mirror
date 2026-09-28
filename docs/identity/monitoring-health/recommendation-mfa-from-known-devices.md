---
layout: Conceptual
title: Recommendation to minimize MFA prompts from known devices - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/recommendation-mfa-from-known-devices
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the recommendation to minimize multifactor authentication prompts from known devices in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2026-04-28T00:00:00.0000000Z
ms.reviewer: jadedsouza
ms.custom: sfi-image-nochange
locale: en-us
document_id: e130a08a-c072-13b7-247b-449398bb406b
document_version_independent_id: 3524fdcc-522f-4370-362f-0bc9a890aabd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/recommendation-mfa-from-known-devices.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/recommendation-mfa-from-known-devices
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/recommendation-mfa-from-known-devices.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 7dea34af-43a8-dd42-76a1-988d1844c192
---

# Recommendation to minimize MFA prompts from known devices - Microsoft Entra ID | Microsoft Learn

[Microsoft Entra recommendations](overview-recommendations) is a feature that provides you with personalized insights and actionable guidance to align your tenant with recommended best practices.

This article covers the recommendation to minimize multifactor authentication prompts from known devices. This recommendation is called `tenantMFA` in the recommendations API in Microsoft Graph.

Note

If you have a Microsoft Entra ID P1 or P2 license, Microsoft recommends using [Conditional Access sign-in frequency](../conditional-access/howto-conditional-access-session-lifetime) to control how often users are prompted for MFA, rather than the **remember multifactor authentication** setting described in this article. For more information, see [Reauthentication prompts and session lifetime for Microsoft Entra multifactor authentication](../authentication/concepts-azure-multi-factor-authentication-prompts-session-lifetime).

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

As an admin, you want to maintain security for your company’s resources, but you also want your employees to easily access resources as needed. While enabling MFA is a good practice, you should try to keep the number of MFA prompts your users have to go through at a minimum. One option you have to accomplish this goal is to **allow users to remember multifactor authentication on trusted devices**.

The *remember multifactor authentication on trusted device* feature sets a persistent cookie on the browser when a user selects the *Don't ask again for X days* option at sign-in. The user isn't prompted again for MFA from that browser until the cookie expires. If the user opens a different browser on the same device or clears the cookies, they're prompted again to verify.

For more information, see [Configure Microsoft Entra multifactor authentication settings](../authentication/howto-mfa-mfasettings).

This recommendation shows up if the **remember multifactor authentication** feature is set to less than 30 days.

## Value

This recommendation improves your user's productivity and minimizes the sign-in time with fewer MFA prompts. Ensure that your most sensitive resources can have the tightest controls, while your least sensitive resources can be more freely accessible.

## Action plan

If you have a Microsoft Entra ID P1 or P2 license, consider migrating to [Conditional Access sign-in frequency](../conditional-access/howto-conditional-access-session-lifetime) for session management instead of using the **remember multifactor authentication** setting. For tenants that continue to use this setting, complete the following steps to ensure the duration is set to at least 90 days.

1. Review the [How to configure Microsoft Entra multifactor authentication settings](../authentication/howto-mfa-mfasettings) article.
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
3. Browse to **Entra ID** &gt; **Multifactor authentication**.
4. Under the **Configure** heading, select the **Additional cloud-based multifactor authentication settings** link.

    ![Screenshot of the configuration settings link in Microsoft Entra multifactor authentication section.](media/recommendation-mfa-from-known-devices/multifactor-authentication-configure-link.png)
5. Select the **Service settings** tab.

    ![Screenshot of the MFA page with the Service settings tab selected.](media/recommendation-mfa-from-known-devices/multifactor-authentication-service-settings.png)
6. Under the **Remember multifactor authentication on trusted device** heading, select the checkbox, and set the number of days to 90.

    ![Screenshot of remember MFA on trusted devices.](media/recommendation-mfa-from-known-devices/multifactor-authentication-remember-known-devices.png)