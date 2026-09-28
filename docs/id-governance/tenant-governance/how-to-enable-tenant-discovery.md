---
layout: Conceptual
title: Enable tenant discovery - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-enable-tenant-discovery
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to enable tenant discovery in Microsoft Entra Tenant Governance to identify related tenants across your organization
ms.topic: how-to
ms.date: 2026-03-10T00:00:00.0000000Z
locale: en-us
document_id: cc1376cd-08eb-a19a-d69a-bdf4f251624c
document_version_independent_id: cc1376cd-08eb-a19a-d69a-bdf4f251624c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-enable-tenant-discovery.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-enable-tenant-discovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-enable-tenant-discovery.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: bd31632e-c9ac-9b30-c4a6-98ad9936570e
---

# Enable tenant discovery - Microsoft Entra ID Governance | Microsoft Learn

Related tenants help administrators discover other Microsoft Entra tenants that have observable relationships with their tenant. Microsoft Entra infers these relationships from activity signals such as B2B collaboration, multitenant application consent, and shared billing accounts. A related tenant doesn't imply ownership or administrative control. It indicates an observed association across Microsoft services.

After you enable related tenant discovery, it remains enabled for your tenant if your tenant meets the licensing requirements.

## Prerequisites

Before you enable related tenants, make sure:

- You have the necessary permissions to enable related tenants. You must hold either the Tenant Governance Administrator or Global Administrator Microsoft Entra role.
- Your tenant is eligible for related tenants with the correct license.
- You understand that this setting isn't a toggle and remains enabled after you turn it on.

## Enable related tenants through the Microsoft Entra admin center

Use this option to enable discovery through the admin center rather than APIs.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator**.
2. Browse to **Tenant Governance** &gt; **Related tenants**.
3. Review the description of enabling related tenants.
4. Select **Discover related tenants**.

After you enable the setting, Microsoft Entra begins aggregating discovery signals and surfaces related tenants in the admin center. The discovery data is synthesized from existing activity and might take time to populate.

## Enable related tenants through Microsoft Graph API

Use this option to enable discovery through scripts or automation.

**Endpoint**

```http
POST /directory/tenantGovernance/settings/enableRelatedTenants
```

This action enables related tenant discovery for the calling tenant.

**Important notes**

- The setting defaults to `false` for new tenants.
- After you enable the setting, `isRelatedTenantsEnabled` changes to `true` and can't be reverted.