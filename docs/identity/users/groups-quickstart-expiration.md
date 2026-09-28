---
layout: Conceptual
title: Group expiration policy quickstart - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-quickstart-expiration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Expiration for Microsoft 365 groups
ms.topic: quickstart
ms.date: 2025-01-15T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro, mode-other
ms.collection: M365-identity-device-management
locale: en-us
document_id: 1024d06a-31d8-9bed-5ece-216ac704aa91
document_version_independent_id: 66c657d9-93aa-936b-5fa0-2276ee1a91b6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-quickstart-expiration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-quickstart-expiration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-quickstart-expiration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7133447b-88fe-e602-0866-a578561427e7
---

# Group expiration policy quickstart - Microsoft Entra ID | Microsoft Learn

## Overview

In this quickstart, you set the expiration policy for your Microsoft 365 groups. When users can set up their own groups, unused groups can multiply. One way to manage unused groups is to set those groups to expire, to reduce the maintenance of manually deleting groups.

Expiration policy is simple:

- Groups with user activities are automatically renewed as the expiration nears.
- Group owners are notified to renew an expiring group.
- A group that isn't renewed is deleted.
- A deleted Microsoft 365 group can be restored within 30 days by a group owner or by a Microsoft Entra administrator.

Note

Microsoft Entra ID, part of Microsoft Entra, uses intelligence to automatically renew groups based on whether they have been in recent use. This renewal decision is based on user activity in groups across Microsoft 365 services like Outlook, SharePoint, Teams, Yammer, and others.

If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisite

The least-privileged role required to set up group expiration is User Administrator in the organization.

## Turn on user creation for groups

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups** and then select **General**.

    ![Screenshot of the Self-service group settings page.](media/groups-quickstart-expiration/self-service-settings.png)
3. Set **Users can create Microsoft 365 groups in Azure portals, API or PowerShell** to **Yes**.
4. Select **Save** to save the groups settings when you're done.

## Set group expiration

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups** &gt; **Expiration** to open the expiration settings.

    ![Screenshot of the Expiration settings page for group.](media/groups-quickstart-expiration/expiration-settings.png)
3. Set the expiration interval. Select a preset value or enter a custom value over 31 days.
4. Provide an email address where expiration notifications should be sent when a group has no owner.
5. For this quickstart, set **Enable expiration for these Microsoft 365 groups** to **All**.
6. Select **Save** to save the expiration settings when you're done.

That's it! In this quickstart, you successfully set the expiration policy for the selected Microsoft 365 groups.

## Clean up resources

To remove the expiration policy and turn off user creation for groups, use the following steps.

### Remove the expiration policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups** &gt; **Expiration**.
3. Set **Enable expiration for these Microsoft 365 groups** to **None**.

### Turn off user creation for groups

1. Browse to **Entra ID** &gt; **Groups** &gt; **Group settings** &gt; **General**.
2. Set **Users can create Microsoft 365 groups in Azure portals** to **No**.