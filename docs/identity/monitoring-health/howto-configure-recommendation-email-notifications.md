---
layout: Conceptual
title: How to configure Microsoft Entra recommendation emails - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-configure-recommendation-email-notifications
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to configure the automatically generated Microsoft Entra recommendation email notification settings for your tenant.
ms.topic: how-to
ms.date: 2026-01-20T00:00:00.0000000Z
ms.reviewer: jadedsouza
locale: en-us
document_id: 1b9bb2dc-4db1-87a7-fc54-70c7b1cca230
document_version_independent_id: 1b9bb2dc-4db1-87a7-fc54-70c7b1cca230
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-configure-recommendation-email-notifications.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-configure-recommendation-email-notifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-configure-recommendation-email-notifications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: a306aaa2-6050-70b6-efd9-400a754c9125
---

# How to configure Microsoft Entra recommendation emails - Microsoft Entra ID | Microsoft Learn

Microsoft Entra recommendations are a powerful resource to monitor and maintain the health and security of your tenant. Email notifications are sent to specific tenant administrative roles when a new recommendation is available for your tenant. These emails help administrators stay on top of the latest recommendations so they can take quick action, but you can turn off these emails for the tenant.

Important

Microsoft Entra recommendation emails are currently in PREVIEW. This information relates to a prerelease product that might be substantially modified before release. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

To update the Microsoft Entra recommendation email notification settings for your tenant, you need to have the [Security Administrator](../role-based-access-control/permissions-reference#security-administrator) role.

## What do the recommendation emails contain?

The email notifications provide a basic summary of the specific recommendation with a link to the related area of the Microsoft Entra admin center. The email also includes a link to related documentation so you can learn more about the recommendation and how to resolve it. These emails are enabled by default, aren't promotional or marketing emails, and don't contain any upselling content. These emails are purely informational and designed to help you act quickly when a new recommendation is available.

## Who receives email notifications?

Not all Microsoft Entra recommendations send email notifications. For those recommendations that do send email notifications, the administrative roles that receive the notifications vary. For details, see the [Recommendations overview table](overview-recommendations#recommendations-overview-table).

## How to update your email notification settings

Tenants are opted in to receive Microsoft Entra recommendation emails by default. To turn off these emails, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Overview** &gt; **Recommendations**.
3. Select **Email settings**.

    [![Screenshot of the recommendations page with the email settings button highlighted.](media/howto-configure-recommendation-email-notifications/recommendation-email-settings.png)](media/howto-configure-recommendation-email-notifications/recommendation-email-settings.png#lightbox)
4. In the **Recommendation email settings** panel that opens, uncheck the **Send email notifications for new recommendations** box and select the **Submit** button.

    [![Screenshot of the email notifications checkbox.](media/howto-configure-recommendation-email-notifications/recommendation-email-settings-checkbox.png)](media/howto-configure-recommendation-email-notifications/recommendation-email-settings-checkbox.png#lightbox)

All email notifications for all Microsoft Entra recommendations are now blocked for the entire tenant and are no longer sent to the tenant's administrative roles.