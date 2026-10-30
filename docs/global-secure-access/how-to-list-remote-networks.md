---
layout: Conceptual
title: How to list remote networks for Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-list-remote-networks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: View and review all remote networks in your Global Secure Access deployment using the Microsoft Entra admin center or Microsoft Graph API.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 28007f9b-02cf-e26c-7134-1eefcf752cf0
document_version_independent_id: aae60779-3243-5fce-ba67-46e37894de6f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-list-remote-networks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-list-remote-networks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-list-remote-networks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 1d11bf63-be58-40f1-6199-c1249c4f47fc
---

# How to list remote networks for Global Secure Access - Global Secure Access | Microsoft Learn

## Overview

Reviewing your remote networks is an important part of managing your Global Secure Access deployment. As your organization grows, you add more remote networks. You use the Microsoft Entra admin center or the Microsoft Graph API.

## Prerequisites

- A **Global Secure Access Administrator** role in Microsoft Entra ID.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

## List all remote networks using the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Remote networks**. All remote networks are listed.
3. To view the details, select a remote network.

## List all remote networks using the Microsoft Graph API

1. Sign in to [Graph Explorer](https://aka.ms/ge).
2. Select `GET` as the HTTP method from the dropdown.
3. Set the API version to beta.
4. Enter the following query. 

    ```
       GET https://graph.microsoft.com/beta/networkaccess/connectivity/branches
    ```
5. Select the **Run query** button to list the remote networks.