---
layout: Conceptual
title: Get started integrating with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/get-started
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Start integrating on-premises Active Directory with Microsoft Entra ID by choosing and configuring Cloud Sync or Connect Sync for users, groups, and devices.
ms.topic: get-started
ms.tgt_pltfrm: na
ms.date: 2026-10-06T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1023
ai-usage: ai-assisted
locale: en-us
document_id: e8a1ddc1-46f6-3f47-d323-2df8ac841c96
document_version_independent_id: 2a11a4b0-ff64-350e-50a4-143723ceb17a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/get-started.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/get-started.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: ec94ef4b-c328-d196-8585-a4dd459695bd
---

# Get started integrating with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Use this guide to integrate on-premises Active Directory with Microsoft Entra ID. It explains how to choose between Microsoft Entra Cloud Sync and Microsoft Entra Connect Sync and configure synchronization for users, groups, and devices.

First, use [Choose the right sync tool](common-scenarios) to select a synchronization tool. Then follow the section for that tool.

## Cloud Sync

Use these tasks to deploy Cloud Sync and integrate Active Directory with Microsoft Entra ID.

| Task | Description |
| --- | --- |
| [Choose the right sync tool](common-scenarios) | Use the wizard to determine whether Cloud Sync or Connect Sync is right for you. |
| [Review Cloud Sync prerequisites](cloud-sync/how-to-prerequisites) | Review the prerequisites before you begin. |
| [Download and install the provisioning agent](cloud-sync/how-to-install) | Download and install the Microsoft Entra provisioning agent. |
| [Configure Cloud Sync](cloud-sync/how-to-configure) | Configure synchronization for your organization. |
| [Configure device sync](cloud-sync/device-sync) | Synchronize Active Directory computer objects to Microsoft Entra ID for Microsoft Entra hybrid join. |
| [Verify that users synchronize](cloud-sync/tutorial-single-forest#verify-users-are-created-and-synchronization-is-occurring) | Confirm that synchronization is working. |

## Microsoft Entra Connect

Use these tasks if you're deploying Microsoft Entra Connect to integrate with Active Directory.

| Task | Description |
| --- | --- |
| [Choose the right sync tool](common-scenarios) | Use the wizard to determine whether Cloud Sync or Connect Sync is right for you. |
| [Review the Microsoft Entra Connect prerequisites](connect/how-to-connect-install-prerequisites) | Review the necessary prerequisites before getting started. |
| [Review and choose an installation type](connect/how-to-connect-install-select-installation) | Determine whether you'll use express or custom installation. |
| [Download Microsoft Entra Connect](https://www.microsoft.com/download/details.aspx?id=47594) | Download Microsoft Entra Connect. |
| [Install and configure Microsoft Entra Connect express settings](connect/how-to-connect-install-express) | If you're using express settings, install and configure Microsoft Entra Connect with express settings. |
| [Install and configure Microsoft Entra Connect custom settings](connect/how-to-connect-install-custom) | If you're using custom settings, install and configure Microsoft Entra Connect with express settings. |
| [Perform post installation tasks](connect/how-to-connect-post-installation) | Perform the post installation tasks. |
| [Verify users are synchronizing](cloud-sync/tutorial-single-forest#verify-users-are-created-and-synchronization-is-occurring) | Make sure it's working. |