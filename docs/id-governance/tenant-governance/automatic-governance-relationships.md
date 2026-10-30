---
layout: Conceptual
title: Automatic formation of governance relationships - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/automatic-governance-relationships
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how Microsoft Entra Tenant Governance automatically establishes governance relationships when you create add-on tenants using secure tenant creation.
ms.topic: concept-article
ms.date: 2026-03-26T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 226145df-d76e-93da-1614-8f57c0036549
document_version_independent_id: 226145df-d76e-93da-1614-8f57c0036549
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/automatic-governance-relationships.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/automatic-governance-relationships
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/automatic-governance-relationships.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: d8375569-cbbb-c5cd-36cc-995740081f40
---

# Automatic formation of governance relationships - Microsoft Entra ID Governance | Microsoft Learn

When a permissioned user in your organization creates a new tenant using the secure add-on tenant creation feature, Microsoft Entra can automatically establish a governance relationship to the newly created tenant on your behalf.

If you defined a default [governance policy template](governance-policy-templates), a new governance relationship forms between the home (governing) tenant and the newly created add-on (governed) tenant, using the default policy template.

If roles and permissions haven't been defined in the default governance policy template, a governance relationship won't be established when a new add-on tenant is created. Changes to the template don't affect governance relationships that have already been established.

## Microsoft Entra ID Free billing asset

When you create a new Microsoft Entra tenant using the secure add-on tenant creation feature, you're prompted to select an existing subscription and resource group from your billing account. When you create your new tenant, Microsoft generates a new billing asset called **Entra ID Free** under that subscription and resource group, which links to the newly created tenant.

The subscription tracks new tenants created with the same billing account, allowing you to maintain an inventory of all new tenants. The subscription also helps prove tenant ownership and helps regain administrative access if you ever lose it. To learn more, see [Microsoft Entra ID Free](/en-us/azure/cost-management-billing/manage/microsoft-entra-id-free).