---
layout: Conceptual
title: Prerequisites to use PowerShell or Graph Explorer for Microsoft Entra roles - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/prerequisites
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Prerequisites to use PowerShell or Graph Explorer for Microsoft Entra roles.
ms.topic: how-to
ms.date: 2025-03-30T00:00:00.0000000Z
ms.reviewer: anandy
ms.custom: oldportal, it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done
locale: en-us
document_id: defb134f-458b-32f5-f91a-e16fdea9c9bd
document_version_independent_id: 894dbde3-3458-f92f-1645-a7298f73efaf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/prerequisites.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/prerequisites
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/prerequisites.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 1c1048c2-30f5-0dd4-cbec-340cb27e0813
---

# Prerequisites to use PowerShell or Graph Explorer for Microsoft Entra roles - Microsoft Entra ID | Microsoft Learn

If you want to manage Microsoft Entra roles using PowerShell or Graph Explorer, you must have the required prerequisites. This article lists the PowerShell and Graph Explorer prerequisites for different Microsoft Entra role features.

## Microsoft Graph PowerShell

To use PowerShell commands to do the following:

- Add users, groups, or devices to an administrative unit
- Create a new group in an administrative unit

You must have the Microsoft Graph PowerShell SDK installed:

- [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation)

## Graph Explorer

To manage Microsoft Entra roles using the [Microsoft Graph API](/en-us/graph/overview) and [Graph Explorer](/en-us/graph/graph-explorer/graph-explorer-overview), you must do the following:

1. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
3. Browse to **Entra ID** &gt; **Enterprise apps**.
4. In the applications list, find and select **Graph explorer**.
5. Select **Permissions**.
6. Select **Grant admin consent for Graph explorer**.

    ![Screenshot showing the &quot;Grant admin consent for Graph explorer&quot; link.](media/prerequisites/select-graph-explorer.png)
7. Use [Graph Explorer tool](https://aka.ms/ge).