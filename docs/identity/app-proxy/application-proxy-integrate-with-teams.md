---
layout: Conceptual
title: Access Microsoft Entra application proxy apps in Teams - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-integrate-with-teams
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Use Microsoft Entra application proxy to access your on-premises application through Microsoft Teams.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: dca7f631-c489-e08b-efba-79c8f12ee7db
document_version_independent_id: 243127da-fac7-1483-3cea-75bfa5a8837c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-integrate-with-teams.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-integrate-with-teams
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-integrate-with-teams.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 803e4dca-6f53-9504-1e9f-d5bbf2193e1c
---

# Access Microsoft Entra application proxy apps in Teams - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra application proxy gives you single sign-on to on-premises applications no matter where you are. Microsoft Teams streamlines your collaborative efforts in one place. Integrating the two together means that your users can be productive with their teammates in any situation.

Your users can add cloud apps to their Teams channels [using tabs](https://support.microsoft.com/office/use-a-tab-in-a-channel-or-chat-in-microsoft-teams-83d0514f-2134-4db5-80f2-e9b43e111d57), but what about the SharePoint sites or planning tool that are hosted on-premises? Application proxy is the solution. They can add apps published through application proxy to their channels using the same external URLs they always use to access their apps remotely. And because application proxy authenticates through Microsoft Entra ID, your users get a single sign-on experience.

## Install the private network connector and publish your app

If you haven't already, [configure application proxy for your tenant and install the connector](application-proxy-add-on-premises-application). Then, publish your on-premises application for remote access. Make note of the external URL because you use it to add the app to Teams.

If you already have your apps published but don't remember their external URLs, look them up in the [Microsoft Entra admin center](https://entra.microsoft.com). Sign in, then browse to **Entra ID** &gt; **Enterprise apps** &gt; select your app &gt; **Application proxy**.

## Add your app to Teams

Let users know they add it as a tab directly in their Teams channels. The app is available for everyone in the team to use.

1. Navigate to the Teams channel where you want to add this app and select **+** to add a tab.
2. Select **Website** from the tab options.
3. Give the tab a name and set the URL to the application proxy external URL.

Once one member of a team adds the tab, it shows up for everyone in the channel. Any users who have access to the app get single sign-on access with the credentials they use for Microsoft Teams. Any users who don't have access to the app can see the tab in Teams, but are blocked until you give them permissions to the on-premises app and the Microsoft Entra admin center published version of the app.