---
layout: Conceptual
title: Common hybrid scenarios with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/common-scenarios
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes the common scenarios for using Microsoft Entra Cloud Sync and Microsoft Entra Connect.
ms.topic: concept-article
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
locale: en-us
document_id: 046da8df-6e74-696f-4b4a-ce920e1e30e1
document_version_independent_id: 0a20365b-4e77-d9f2-98f0-ba1a914c49c4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/common-scenarios.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/common-scenarios
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/common-scenarios.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 01da382d-781f-56ac-4257-9bf1eb2b5518
---

# Common hybrid scenarios with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The following document describes the common and supported hybrid sync scenarios.

## Supported sync scenarios

The following table outlines the most common and supported sync scenarios.

| Scenario | Supported with cloud sync | Supported with connect sync | Supported with MIM and the Graph Connector | Supported with ECMA Host connector |
| --- | --- | --- | --- | --- |
| New Hybrid customers managing identities | ● | ● | ● | N/A |
| Mergers and acquisitions (disconnected forest) | ● | N/A | ● | N/A |
| High availability - latency (I need high availability) | ● | N/A | ● | N/A |
| Migration from connect sync to cloud sync | ● | ● | N/A | N/A |
| Microsoft Entra hybrid join | N/A | ● | N/A | N/A |
| Exchange hybrid | ● | ● | N/A | N/A |
| User accounts in one forest / mailboxes in resource forest | N/A | ● | N/A | N/A |
| Sync large domains with more than 250K objects | N/A | ● | ● | N/A |
| Filter directory objects based on attribute values | N/A | ● | ● | N/A |
| Windows Hello for Business | N/A | ● | N/A | N/A |
| Synchronize from cloud to on-premises AD | N/A | N/A | ● | N/A |
| Synchronize from cloud to on-premises LDAP | N/A | N/A | ● | ● |
| Synchronize from cloud to on-premises SQL | N/A | N/A | ● | ● |

## Supported provisioning scenarios

The following table outlines the common and supported provisioning scenarios.

| Scenario | Supported with cloud sync | Supported with connect sync | Supported with MIM and the Graph Connector | Supported with ECMA Host connector |
| --- | --- | --- | --- | --- |
| Group provisioning to Active Directory | ● | N/A | ● | N/A |

For more information, see [Supported topologies for cloud sync](cloud-sync/plan-cloud-sync-topologies) and [Supported topologies for connect sync](connect/plan-connect-topologies).

## Additional information

- You can sync users & groups from the same domain using Connect Sync and cloud sync if:
    - Scoping filters in each sync is mutually exclusive
    - If inclusive, don’t have the same attributes values clashing (Precedence isn’t supported)
- You can sync users & groups using Connect Sync while using cloud sync’s net new capabilities (\*called out in Roadmap)
- You can sync objects from a single AD to multiple Azure ADs if writeback capabilities are enabled only in a single Microsoft Entra tenant.

## Cloud sync and connect sync in parallel

You can run cloud sync and Microsoft Entra Connect in the same forest. You may decide to do allow cloud sync to handle 80% and use Microsoft Entra Connect for some of your more obscure, 20% scenarios. The tutorial, [Migrate to Microsoft Entra Cloud Sync for an existing synced AD forest](cloud-sync/tutorial-pilot-aadc-aadccp) shows an example of how you would run each.

## Common authentication methods and scenarios

Hybrid identity scenarios use one of three authentication methods. The three methods are:

- **[Password hash synchronization (PHS)](connect/whatis-phs)**
- **[Pass-through authentication (PTA)](connect/how-to-connect-pta)**
- **[Federation (AD FS)](connect/whatis-fed)**

These authentication methods also provide [single-sign on](connect/how-to-connect-sso) capabilities. Single-sign on automatically signs your users in when they are on their corporate devices, connected to your corporate network.

For additional information, see [Choose the right authentication method for your Microsoft Entra hybrid identity solution](connect/choose-ad-authn).

| I need to: | PHS and SSO | PTA and SSO | Federation |
| --- | --- | --- | --- |
| Sync new user, contact, and group accounts created in my on-premises Active Directory to the cloud automatically. | ● | ● | ● |
| Set up my tenant for Microsoft 365 hybrid scenarios. | ● | ● | ● |
| Enable my users to sign in and access cloud services using their on-premises password. | ● | ● | ● |
| Implement single sign-on using corporate credentials. | ● | ● | ● |
| Ensure no password hashes are stored in the cloud. |  | ● | ● |
| Enable cloud-based multifactor authentication solutions. | ● | ● | ● |
| Enable on-premises multifactor authentication solutions. |  |  | ● |
| Support smartcard authentication for my users. |  |  | ● |