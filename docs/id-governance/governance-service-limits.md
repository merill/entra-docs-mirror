---
layout: Conceptual
title: Microsoft Entra ID Governance service limits - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/governance-service-limits
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article details service limits for offerings within Microsoft Entra ID Governance
ms.topic: concept-article
ms.date: 2024-12-10T00:00:00.0000000Z
locale: en-us
document_id: 21beff85-d30b-af2c-2ea5-ddd00abf11a9
document_version_independent_id: 21beff85-d30b-af2c-2ea5-ddd00abf11a9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/governance-service-limits.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/governance-service-limits
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/governance-service-limits.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9934fd38-2411-7fa0-9885-872168349b5e
---

# Microsoft Entra ID Governance service limits - Microsoft Entra ID Governance | Microsoft Learn

This article contains the default usage constraints for the Microsoft Entra ID Governance, part of Microsoft Entra, service. If you’re looking for the full set of non-governance specific Microsoft Entra service limits, see: [Microsoft Entra service limits and restrictions](../identity/users/directory-service-limits-restrictions).

Note

Limits can be increased if your usage exceeds these listed default constraints. To go beyond the default quota, you must contact Microsoft Support.

## Entitlement Management

Tip

We recommend that access packages contain more than one resource role and are modeled on the basis of departments, job functions, locations, projects or a combination of these.

| Feature | Limit |
| --- | --- |
| Access Packages | 20,000 per tenant |
| Access Package Assignments - An access package assignment is an assignment of an access package to a particular user | 300,000 per tenant |
| Access Package Assignments from a given automatic assignment policy | 15,000 per automatic assignment policy |
| Catalogs | 7,500 per tenant |
| Connected Organizations | 2,500 per tenant |
| Custom extensions | 500 per tenant |
| Policies - An access package assignment policy specifies the policy by which users can request or be assigned an access package | 25,000 per tenant |
| Connected Organizations referenced in a single policy as part of the 'Users who can request access' definition | 1,000 per policy |
| Combined number of users and groups explicitly referenced in a single policy as part of the 'Users who can request access' definition. | 500 per policy |
| Requests (within three months) - An access package assignment request is created by or on behalf of a user who wants to obtain, update, or remove an access package assignment. This includes requests that are created by the system for automatic assignment policies | 200,000 per tenant |

## Lifecycle Workflows

| Category | Limit |
| --- | --- |
| Number of Workflows | 100 per tenant |
| Number of Tasks | 25 per workflow |
| Number of Custom Task Extensions | 100 per tenant |
| offsetInDays range of triggerAndScopeBasedConditions executionConditions | 180 days |
| Workflow schedule interval in hours | 1-24 hours |
| Number of users per on-demand selection | 10 |
| durationBeforeTimeout range of custom task extensions | 30 minutes-3 hours |
| Administrative scopes per workflow | 5 |

Note

If creating, or updating, a workflow via API the offsetInDays range will be between -180 - 180 days. The negative value signals happening before the timeBasedAttribute, while the positive value signals happening afterwards.