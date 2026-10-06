---
layout: Conceptual
title: Tools used for synchronization - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/sync-tools
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Compare Microsoft identity synchronization tools for users, groups, contacts, and devices to choose an approach for hybrid identity with Active Directory.
ms.topic: concept-article
ms.tgt_pltfrm: na
ms.date: 2026-10-06T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1023
ai-usage: ai-assisted
locale: en-us
document_id: 52771d2d-eda3-6a3b-ef5d-286d544d4992
document_version_independent_id: 4dc7d457-c42b-0792-8ca9-1e5308e82d37
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/sync-tools.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/sync-tools
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/sync-tools.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/fecfc034-c4c2-43e6-be47-948bd4addcea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/16cf36da-59bd-4744-91e9-295292c63e5e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a1daade6-acf1-933c-4bc7-7af0dda957b9
---

# Tools used for synchronization - Microsoft Entra ID | Microsoft Learn

This article compares Microsoft Entra Cloud Sync, Connect Sync, Microsoft Identity Manager (MIM), and the ECMA host connector. Use the comparison to choose a tool for synchronizing identities or provisioning users to on-premises applications.

## List of tools

- **Cloud Sync and the provisioning agent** - Microsoft Entra Cloud Sync synchronizes users, groups, and contacts from Active Directory to Microsoft Entra ID. When device sync is enabled, it can also synchronize computer objects for Microsoft Entra hybrid join. Cloud Sync uses the lightweight provisioning agent and is configurable through the Microsoft Entra admin center. For more information, see [What is Microsoft Entra Cloud Sync?](cloud-sync/what-is-cloud-sync), [What is the provisioning agent?](cloud-sync/what-is-provisioning-agent), and [Configure device sync with Microsoft Entra Cloud Sync](cloud-sync/device-sync).
- **Connect Sync** - Microsoft Entra Connect is an on-premises application for synchronizing identities with Microsoft Entra ID. For more information, see [What is Microsoft Entra Connect?](connect/whatis-azure-ad-connect-v2).
- **Microsoft Identity Manager with the Graph connector** - Microsoft's on-premises identity and access management solution that provides advanced inter-directory provisioning to achieve hybrid identity environments for Active Directory, Microsoft Entra ID, and other directories. For more information, see [Microsoft Identity Manager](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016). MIM is slowly being deprecated and should only be used in advanced scenarios. For more information, see [Deprecated Features and planning for the future](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016-deprecated-features)
- **ECMA Host connector** - The ECMA host works with the provisioning agent to provision and synchronize users from the cloud into on-premises applications such as SQL and LDAP. For more information, see [Microsoft Entra on-premises application identity provisioning architecture](../app-provisioning/on-premises-application-provisioning-architecture) and [What is the provisioning agent?](cloud-sync/what-is-provisioning-agent)

## Selecting the right tool

These tools support different hybrid identity scenarios. Compare their capabilities in the [supported sync scenarios table](common-scenarios#supported-sync-scenarios), then use the [sync tool selection wizard](common-scenarios) to choose a tool.