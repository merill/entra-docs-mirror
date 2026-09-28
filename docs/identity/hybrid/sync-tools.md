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
description: This article introduces the various tools that can be used to synchronize the cloud with on-premises environments.
ms.topic: concept-article
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
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
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/fecfc034-c4c2-43e6-be47-948bd4addcea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/16cf36da-59bd-4744-91e9-295292c63e5e
platformId: a1daade6-acf1-933c-4bc7-7af0dda957b9
---

# Tools used for synchronization - Microsoft Entra ID | Microsoft Learn

The following article briefly describes the Microsoft tools that current exist today for synchronization.

## List of tools

- **Cloud sync and the provisioning agent** - Microsoft Entra Cloud Sync is the newest offering from Microsoft designed to meet and accomplish your hybrid identity goals for synchronization of users, groups, and contacts to Microsoft Entra ID. It uses the light-weight provisioning agent and is fully configurable via the portal. For more information, see [What is cloud sync?](cloud-sync/what-is-cloud-sync) and [What is the provisioning agent?](cloud-sync/what-is-provisioning-agent)
- **Connect sync** - Microsoft Entra Connect is an on-premises Microsoft application designed to meet and accomplish your hybrid identity goals. For more information, see [What is Microsoft Entra Connect?](connect/whatis-azure-ad-connect-v2).
- **Microsoft Identity Manager with the Graph connector** - Microsoft's on-premises identity and access management solution that provides advanced inter-directory provisioning to achieve hybrid identity environments for Active Directory, Microsoft Entra ID, and other directories. For more information, see [Microsoft Identity Manager](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016). MIM is slowly being deprecated and should only be used in advanced scenarios. For more information, see [Deprecated Features and planning for the future](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016-deprecated-features)
- **ECMA Host connector** - The ECMA host works with the provisioning agent to provision and synchronize users from the cloud into on-premises applications such as SQL and LDAP. For more information, see [Microsoft Entra on-premises application identity provisioning architecture](../app-provisioning/on-premises-application-provisioning-architecture) and [What is the provisioning agent?](cloud-sync/what-is-provisioning-agent)

## Selecting the right tool

Each of these tools can accomplish similar results. So selecting the right tool is essential. For most scenarios, cloud sync is going to be the recommended tool. Then connect sync and for advanced/complex scenarios, MIM. For on-premises applications, the ECMA Host would be the preferred tool. For more information, [see the supported sync scenarios table](common-scenarios#supported-sync-scenarios). To determine which tool is right for you, you should use the wizard at the [Choosing the right sync tool](common-scenarios) site.