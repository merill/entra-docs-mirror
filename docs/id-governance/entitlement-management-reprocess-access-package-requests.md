---
layout: Conceptual
title: Reprocess requests for an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-reprocess-access-package-requests
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to reprocess a request for an access package in entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2024-07-15T00:00:00.0000000Z
locale: en-us
document_id: cc1d6971-7c41-204a-6371-fb72e9678b1d
document_version_independent_id: 330cc68b-7b02-0159-cfc5-3a2016a18270
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-reprocess-access-package-requests.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-reprocess-access-package-requests
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-reprocess-access-package-requests.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b8932893-874f-48e4-b2d5-5521fe75a61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/e757ef92-a039-44aa-8ed6-705843b26fea
platformId: a2bfd7f4-702b-c419-7392-9ef419cb729c
---

# Reprocess requests for an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

As an access package manager, you can automatically retry a user’s request for access to an access package at any time by using the reprocess functionality. Reprocessing eliminates the need for users to repeat the access package request process if their access to resources isn't successfully provisioned.

Note

You can reprocess a request for up to 14 days from the time that the original request is completed. For requests that were completed more than 14 days ago, users will need to cancel and make new requests in MyAccess.

This article describes how to reprocess requests for an existing access package.

## Prerequisites

To use entitlement management and assign users to access packages, you must have one of the following licenses:

- Microsoft Entra ID P2 or Microsoft Entra ID Governance
- Enterprise Mobility + Security (EMS) E5 license

## Open an existing access package and reprocess user requests

If you have a set of users whose requests are in the "Partially Delivered" or "Failed" state, you might need to reprocess some of those requests. Follow these steps to reprocess requests for an existing access package:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner, Access package manager, and Access package assignment manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the Access packages,\*\* open the access package.
4. Underneath **Manage** on the left side, select **Requests**.
5. Select all users whose requests you wish to reprocess.
6. Select **Reprocess**.