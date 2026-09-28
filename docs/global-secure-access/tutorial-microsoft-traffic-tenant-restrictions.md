---
layout: Conceptual
title: 'Tutorial: Configure universal tenant restrictions - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-microsoft-traffic-tenant-restrictions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure universal tenant restrictions with Global Secure Access for Microsoft traffic.
ms.topic: tutorial
ms.date: 2026-06-22T00:00:00.0000000Z
ms.subservice: entra-internet-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3dffa3bf-e8b5-249f-e274-a0ddaff1ceee
document_version_independent_id: 3dffa3bf-e8b5-249f-e274-a0ddaff1ceee
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-microsoft-traffic-tenant-restrictions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-microsoft-traffic-tenant-restrictions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-microsoft-traffic-tenant-restrictions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 6c42b17d-33ac-540c-d29d-71ba78523016
---

# Tutorial: Configure universal tenant restrictions - Global Secure Access | Microsoft Learn

Universal tenant restrictions enhance [tenant restrictions v2](../external-id/tenant-restrictions-v2) by using Global Secure Access to tag authentication traffic. When you enable universal tenant restrictions, Global Secure Access adds tenant restrictions v2 policy information to authentication-plane traffic for Microsoft Entra ID and Microsoft Graph.

In this tutorial, you learn how to:

- Recognize what universal tenant restrictions do and why they matter.
- Configure the underlying tenant restrictions v2 policy.
- Enable Global Secure Access signaling for tenant restrictions.
- Validate that sign-ins to unauthorized tenants are blocked.

## Key concepts

Universal tenant restrictions help prevent data exfiltration across browsers, devices, and networks by enabling Microsoft Entra ID, Microsoft accounts, and Microsoft applications to look up and enforce the associated tenant restrictions v2 policy.

Universal tenant restrictions support devices with the Global Secure Access client and remote network connectivity. This tutorial validates the experience with the Global Secure Access client.

## Step 1: Configure the tenant restrictions v2 policy

Universal tenant restrictions enforce the tenant restrictions v2 policy. Before you turn on signaling, define the default policy and any partner-specific exceptions.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an administrator with the Security Administrator role.
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**.
3. On the **Default settings** tab, configure the default tenant restrictions v2 policy. For example, block all external users and external apps.
4. On the **Organizational settings** tab, add any partner tenants that you want to allow and configure tenant restrictions v2 for those partners.

For step-by-step guidance, see [Set up tenant restrictions v2](../external-id/tenant-restrictions-v2).

## Step 2: Enable Universal tenant restrictions

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an administrator with the Global Secure Access Administrator role.
2. Go to **Global Secure Access** &gt; **Settings** &gt; **Session Management**.
3. On the **Universal Tenant Restrictions** tab, turn on the **Enable Tenant Restrictions for Microsoft Entra ID and Microsoft Graph** toggle.

    [![Screenshot that shows the Enable Tenant Restrictions for Microsoft Entra ID and Microsoft Graph toggle enabled.](media/tutorial-microsoft-traffic/universal-tenant-restrictions.png)](media/tutorial-microsoft-traffic/universal-tenant-restrictions.png#lightbox)

Global Secure Access now adds tenant restrictions v2 headers to authentication-plane traffic for users who connect through the Microsoft traffic profile.

## Step 3: Validate authentication-plane protection

1. With the Global Secure Access client running, attempt to sign in using an identity from a different tenant that isn't on the allow list.
2. Confirm that Microsoft Entra ID blocks authentication to the external tenant.

    [![Screenshot that shows a Microsoft access blocked message stating that the user can't get there from here.](media/tutorial-microsoft-traffic/tenant-restrictions-blocked.png)](media/tutorial-microsoft-traffic/tenant-restrictions-blocked.png#lightbox)

## What you learned

In this exercise, you accomplished the following tasks:

- **Configured a tenant restrictions v2 policy:** You defined which external tenants your users can access.
- **Enabled Global Secure Access signaling for tenant restrictions:** Global Secure Access can tag authentication-plane traffic with tenant restrictions v2 policy information.
- **Validated authentication-plane protection:** You confirmed that an identity from a tenant not on the allow list was blocked.