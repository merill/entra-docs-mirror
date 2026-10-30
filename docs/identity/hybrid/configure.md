---
layout: Conceptual
title: Configure your integration with Active Directory - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/configure
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Learn how to configure Microsoft Entra Cloud Sync and Connect Sync to synchronize users, groups, and contacts from Active Directory, and how to enable device sync for hybrid join.
ms.topic: concept-article
ms.tgt_pltfrm: na
ms.date: 2026-10-06T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1023
ai-usage: ai-assisted
locale: en-us
document_id: d8f402d4-dfb7-f4c7-e431-a578964f6a0a
document_version_independent_id: 0f8f19f0-3ba3-4b00-b709-ee0e25034e17
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/configure.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 80460bb7-1a6b-1c5d-05d2-a3956efc1d4e
---

# Configure your integration with Active Directory - Microsoft Entra ID | Microsoft Learn

Choose Microsoft Entra Cloud Sync or Microsoft Entra Connect Sync based on your synchronization goals. The tables below link to configuration tasks for each tool.

## Cloud Sync

After you install the Microsoft Entra provisioning agent, configure Cloud Sync in the Microsoft Entra admin center. The following table lists configuration tasks.

| Task | Description |
| --- | --- |
| [Configure a new Cloud Sync installation](cloud-sync/how-to-configure) | Configure synchronization for your organization. |
| [Configure device sync](cloud-sync/device-sync) | Synchronize Active Directory computer objects to Microsoft Entra ID for Microsoft Entra hybrid join. |
| [Scope provisioning to specific users and groups](cloud-sync/how-to-configure#scope-provisioning-to-specific-users-and-groups) | Scope Cloud Sync to selected users and groups. |
| [Mapping user and group attributes](cloud-sync/how-to-configure#attribute-mapping) | Map attributes for users and groups. |
| [Working with directory extensions and custom attributes](cloud-sync/how-to-configure#directory-extensions-and-custom-attribute-mapping) | Use directory extensions and custom attributes |
| [Configure single sign-on](cloud-sync/how-to-sso) | Set up Cloud Sync single sign-on. |

## Microsoft Entra Connect

Several of the configuration tasks used with Microsoft Entra Connect are set up when you install the tool. You should review the custom installation section to make sure you have the information you'll need when setting up. Also, the post installation tasks should be reviewed to further validate and customize your specific configuration.

| Task | Description |
| --- | --- |
| [Configure sync features](connect/how-to-connect-install-roadmap#configure-sync-features) | Review the configurable sync features for Microsoft Entra Connect. |
| [Customize Microsoft Entra Connect Sync](connect/how-to-connect-install-roadmap#customize-azure-ad-connect-sync) | How to customize the default configuration. |
| [Configure federation](connect/how-to-connect-install-roadmap#configure-federation-features) | How to federate with Microsoft Entra Connect. |
| [Post installation tasks](connect/how-to-connect-post-installation) | More tasks for managing Microsoft Entra Connect |
| [Mapping user and group attributes](cloud-sync/how-to-configure#attribute-mapping) | Map attributes for users and groups. |
| [Device writeback](connect/how-to-connect-device-writeback) | Configure device writeback. |
| [Configure single sign-on](connect/how-to-connect-sso-quick-start) | Set up Microsoft Entra Connect to use single sign-on. |