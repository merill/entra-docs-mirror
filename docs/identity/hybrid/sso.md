---
layout: Conceptual
title: Get started with single sign-on - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/sso
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes how you can configure the synchronization tools to use single sign-on.
ms.topic: get-started
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
locale: en-us
document_id: 5c9313af-5596-69e7-a701-0a12c89c88fd
document_version_independent_id: 0cd45781-6c6f-0628-5c72-bcf884be3b23
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/sso.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/sso
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/sso.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3c72d12f-1791-90d2-1cb8-4c5526468f58
---

# Get started with single sign-on - Microsoft Entra ID | Microsoft Learn

Setting up single sign-on, depends on which synchronization tool you're using and what your business goals are. Use the following tables to determine which features meet your target objectives.

## Cloud sync

After installing the Microsoft Entra Connect provisioning agent, you need to configure single sign-on for cloud sync. The following table provides a list of steps required for using single sign-on.

| Task | Description |
| --- | --- |
| Download and extract Microsoft Entra Connect files | Download and extract the Microsoft Entra Connect files to use the PowerShell modules. |
| Import the Seamless single sign-on PowerShell module | Import the PowerShell modules into a PowerShell session. |
| Get the list of Active Directory forests with Seamless single sign-on enabled. | Determine where single sign-on is enabled. |
| Enable Seamless single sign-on for each Active Directory forest | Enable single sign-on on your forests. |
| Enable the feature on your tenant | Enable single sign-on on your tenant. |

For more information, see [configuring single sign-on with cloud sync](cloud-sync/how-to-sso).

## Microsoft Entra Connect

Microsoft Entra seamless single sign-on (Seamless single sign-on) automatically signs in users when they're using their corporate desktops that are connected to your corporate network. The following table provides a list of steps required for using single sign-on.

| Task | Description |
| --- | --- |
| Check the prerequisites | Review the prerequisites and ensure you can enable single sign-on. |
| Enable the feature | Use the Microsoft Entra Connect wizard to enable single sign-on. |
| Roll out the feature | Gradually implement single sign-on. |
| Test single sign-on | Ensure single sign-on is working. |

For more information, see [configuring single sign-on with Microsoft Entra Connect](connect/how-to-connect-sso-quick-start) and [configuring single sign-on with cloud sync](cloud-sync/how-to-sso).