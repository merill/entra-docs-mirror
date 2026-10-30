---
layout: Conceptual
title: Govern cloud users that are provisioned from on-premises to Microsoft Entra ID with Microsoft Identity Manager | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/scenarios/provision-microsoft-identity-manager-to-entra
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: femila
description: This article a tutorial on how to provision users and groups from on-premises to cloud using MIM.
ms.topic: concept-article
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: 
locale: en-us
document_id: a3802c3b-454d-1435-7f29-7428610ffa0b
document_version_independent_id: a3802c3b-454d-1435-7f29-7428610ffa0b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/scenarios/provision-microsoft-identity-manager-to-entra.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/scenarios/provision-microsoft-identity-manager-to-entra
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/scenarios/provision-microsoft-identity-manager-to-entra.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fecfc034-c4c2-43e6-be47-948bd4addcea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/16cf36da-59bd-4744-91e9-295292c63e5e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 18cfb981-8e66-885b-0856-2050d4af5193
---

# Govern cloud users that are provisioned from on-premises to Microsoft Entra ID with Microsoft Identity Manager | Microsoft Learn

**Scenario:** Manage cloud users that are provisioned from on-premises to Microsoft Entra ID with Microsoft Identity Manager.

[![Conceptual drawing showing MIM provisioning.](media/provision-microsoft-identity-manager-to-entra/provision-microsoft-identity-manager-to-entra.png)](media/provision-microsoft-identity-manager-to-entra/provision-microsoft-identity-manager-to-entra.png#lightbox)

If you have integration scenarios, for users and groups, that aren't in scope for Microsoft Entra Connect cloud sync or Microsoft Entra Connect Sync, then you should consider using the [Microsoft Identity Manager](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016) and the [Microsoft Identity Manager connector for Microsoft Graph](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016-connector-graph). This connector communicates with Microsoft Entra ID via the [Microsoft Graph API v1.0](/en-us/graph/overview) and beta. The end of [support](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016#support-update-for-microsoft-entra-id-p1-or-p2-customers) for Microsoft Identity Manager 2016 is January 9, 2029.