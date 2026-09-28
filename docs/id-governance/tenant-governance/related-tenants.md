---
layout: Conceptual
title: Related tenants in Tenant Governance - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/related-tenants
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how Microsoft Entra Tenant Governance discovers related tenants through identity, application, and billing signals across your organization
ms.topic: concept-article
ms.date: 2026-07-14T00:00:00.0000000Z
locale: en-us
document_id: 99cbdcd2-ba88-8643-066a-b7e5a6e1e7c3
document_version_independent_id: 99cbdcd2-ba88-8643-066a-b7e5a6e1e7c3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/related-tenants.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/related-tenants
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/related-tenants.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 778a6dec-0615-f330-dd56-389ba7335d4a
---

# Related tenants in Tenant Governance - Microsoft Entra ID Governance | Microsoft Learn

The **related tenants** feature is a Tenant Governance capability that helps organizations gain visibility into Microsoft Entra tenants that interact with their tenant through observable activity. These interactions might involve tenants that are external (partners, vendors, and customers) as well as tenants that were created internally without central oversight, such as employee-created test or development tenants.

Modern organizations rarely operate within a single Microsoft Entra tenant. Mergers, acquisitions, divestitures, geographic expansion, developer experimentation, and decentralized IT models have led to tenant sprawl. The result is an expanding ecosystem of Microsoft Entra tenants that interact in ways that are often invisible or poorly understood.

The related tenants feature isn't an authoritative inventory of tenants an organization owns. Instead, it provides situational awareness by surfacing tenant connections based on evidence already present across identity, application, and billing systems. This awareness enables organizations to understand their tenant ecosystem and decide where governance actions might be appropriate.

At its core, the related tenants feature answers the question:

*"Which other Microsoft Entra tenants interact with mine, and what activity establishes those connections?"*

This visibility forms the foundation for effective Tenant Governance, without presupposing ownership or enforcement decisions.

## What are related tenants?

A related tenant is a Microsoft Entra tenant that demonstrates a verifiable connection to another tenant based on observable discovery signals. These signals are derived from real configuration and activity data and are refreshed over time.

Tenant Governance discovers related tenants. You don't manually declare them. Discovery establishes context, not intent. A related tenant might be:

- An external partner, vendor, or customer tenant
- A software as a service (SaaS) provider tenant accessed through multitenant applications
- An unsanctioned or shadow-IT tenant, such as one created by an employee for testing, development, or experimentation

**Tenant discovery** surfaces:

- Which tenants are related
- The discovery signal or signals that establish the relationship
- The activity and discovery metrics associated with those signals, such as identity interactions, application usage, or billing associations

These metrics describe how tenants are connected. They don't assign qualitative scores or imply that every related tenant must be governed. Instead, they provide the evidence needed to determine whether governance action is warranted.

## Microsoft-managed tenants

Some discovered related tenants are Microsoft-owned infrastructure tenants rather than tenants that belong to your organization or your partners. Tenant Governance identifies these tenants and flags them as **Microsoft managed**.

Microsoft-managed tenants appear because routine Microsoft cloud operations create observable cross-tenant activity. They're expected and generally require no governance action. The **Microsoft managed** indicator helps you quickly recognize and set aside this class of related tenant so you can focus on tenants that need attention.

The Microsoft managed indicator is available to administrators who have a Tenant Governance license and permission to read related tenants.

## Why related tenants matter

Related tenants provide value in several key areas, from surfacing unsanctioned tenants to enabling informed governance decisions.

### Visibility into both external and shadow-IT tenants

Organizations often have limited visibility into tenants that exist outside formal provisioning processes. Employees might create tenants for proof-of-concept work, testing, or experimentation, while business units might engage directly with external tenants for collaboration or SaaS usage.

Without discovery, these tenants remain invisible, even though they might:

- Exchange identities with the organization
- Host applications used by employees
- Be associated with shared billing or commerce relationships

The related tenants feature makes these interactions visible, including unsanctioned shadow-IT tenants, enabling organizations to distinguish between expected external relationships and internally created tenants that might require governance attention.

### Cross-tenant identity, application, and billing activity

Modern identity and application models are inherently cross-tenant. External collaboration, multitenant applications, and shared billing constructs introduce interactions that span tenants with different ownership models.

The related tenants feature provides visibility into:

- Cross-tenant identity activity
- Application usage across tenant boundaries
- Financial or billing associations between tenants

This visibility allows organizations to understand where and how interactions occur, forming the basis for informed security and governance decisions.

### Governance starts with awareness

Tenant Governance depends on knowing what exists before deciding what to govern. The related tenants feature provides the discovery layer that enables this awareness.

By surfacing both external tenants and internally created shadow-IT tenants, the related tenants feature lets administrators:

- Identify tenants that are expected and externally managed
- Detect tenants that might fall outside organizational policy
- Decide whether to initiate governance actions

This approach ensures governance is intentional and evidence-based rather than reactive.

## How related tenants fit into Tenant Governance

Tenant Governance is designed to help organizations manage multiple tenants as a system, recognizing that different tenants require different levels of oversight.

The related tenants feature represents the discovery layer of Tenant Governance:

1. **Discovery**: Identify tenants that interact with your tenant
2. **Understanding**: Review discovery signals and activity metrics
3. **Governance**: Decide whether governance actions are appropriate

For unsanctioned or shadow-IT tenants discovered through this process, organizations can initiate governance actions using Tenant Governance capabilities, such as establishing governance relationships or applying centralized oversight. For external tenants, discovery might simply provide awareness without further action.

## Discovery signals used to identify related tenants

Discovery signals identify related tenants. Each signal is an observable indicator that two tenants interact in meaningful ways. Each signal is accompanied by aggregated activity metrics that describe the nature of the interaction.

Metrics appear as orders of magnitude rather than exact values and refresh as activity changes, providing ongoing visibility while protecting individual user privacy.

### B2B collaboration

Business-to-business (B2B) collaboration signals identify tenant relationships based on cross-tenant identity interactions, such as guest user registrations and sign-in activity.

These signals commonly surface:

- Partner, vendor, or customer tenants
- Employee-created tenants used for collaboration or testing

Associated metrics describe inbound and outbound identity activity, enabling administrators to understand where cross-tenant identity usage exists and whether further governance consideration is needed.

### Multitenant applications

Multitenant application signals surface relationships where applications registered in one tenant are consented to or accessed by users in another tenant.

These signals might reveal:

- SaaS provider tenants
- Internally created tenants hosting shared applications

Metrics describe inbound and outbound multitenant application usage, highlighting application-level dependencies across tenants.

### Shared billing accounts

Shared billing account signals identify tenants that are connected through one or more shared billing accounts.

These signals are particularly useful for identifying:

- Organizationally affiliated tenants
- Internally created tenants associated with centralized billing

Associated metrics describe billing relationships and active capabilities, helping administrators understand financial linkages that might warrant governance action.

## From discovery to governance

**Tenant discovery** is intentionally a starting point, not an automatic enforcement mechanism.

Once related tenants are discovered, organizations can:

1. Review which tenants interact with their environment
2. Identify unsanctioned or shadow-IT tenants
3. Use discovery metrics to prioritize investigation
4. Initiate governance actions for tenants that require oversight

Some related tenants might require governance; others might require monitoring; and many might require no action at all. The related tenants feature enables this differentiation by providing visibility first, then enabling deliberate governance decisions.