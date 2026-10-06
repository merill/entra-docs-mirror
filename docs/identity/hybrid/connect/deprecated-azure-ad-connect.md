---
layout: Conceptual
title: Using a deprecated version of Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/deprecated-azure-ad-connect
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn what to do when Microsoft Entra Connect is deprecated, how to check your version, and whether Microsoft Entra Cloud Sync meets your synchronization needs.
ms.topic: how-to
ms.date: 2026-10-06T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1023
ai-usage: ai-assisted
ms.subservice: hybrid-connect
locale: en-us
document_id: fae3b43e-973c-ce45-bc6e-e50aa19b1dcd
document_version_independent_id: cbbb61df-5bc1-b807-3e2c-07a6b93527b8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/deprecated-azure-ad-connect.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/deprecated-azure-ad-connect
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/deprecated-azure-ad-connect.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5ac5849a-d540-4e40-1501-befed7b0df4a
---

# Using a deprecated version of Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn

You may have received a notification email that says that your [Microsoft Entra Connect version is deprecated](whatis-azure-ad-connect-v2) and no longer supported. Or, you may have read a portal recommendation about upgrading your Microsoft Entra Connect version. What is next?

Important

Instead of upgrading to the latest version of Microsoft Entra Connect, see if cloud sync is right for you. For more information, evaluate your options using the [supported sync scenarios comparison](../common-scenarios)

Using a deprecated and unsupported version of Microsoft Entra Connect isn't recommended and not supported. Deprecated and unsupported versions of Microsoft Entra Connect may **unexpectedly stop working**. In these instances, you may need to install the latest version of Microsoft Entra Connect as your only remedy to restore your sync process.

We regularly update Microsoft Entra Connect with [newer versions](reference-connect-version-history). The new versions have bug fixes, performance improvements, new functionality, and security fixes, so it's important to stay up to date.

## How to replace your deprecated version

If you're still using a deprecated and unsupported version of Microsoft Entra Connect, here's what you should do:

1. Check which version to install. Many organizations can use [Microsoft Entra Cloud Sync](/en-us/azure/active-directory/cloud-sync/what-is-cloud-sync) instead of Microsoft Entra Connect. Cloud Sync synchronizes users, groups, and contacts from Active Directory to Microsoft Entra ID. When device sync is enabled, it can also synchronize computer objects for Microsoft Entra hybrid join. For device setup, see [Configure device sync with Microsoft Entra Cloud Sync](../cloud-sync/device-sync). Cloud Sync uses a lightweight agent, is managed from the cloud, and updates automatically.
2. If you're not yet eligible for Microsoft Entra Cloud Sync, [download Microsoft Entra Connect](https://www.microsoft.com/download/details.aspx?id=47594) and install the latest version. For more information, see [Upgrade Microsoft Entra Connect from a previous version](how-to-upgrade-previous-version).