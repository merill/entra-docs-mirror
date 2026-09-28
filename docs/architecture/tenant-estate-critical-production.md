---
layout: Conceptual
title: Microsoft Entra tenants for critical business systems guidance - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/tenant-estate-critical-production
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: bathawes
ms.author: beathawe
ms.service: entra
manager: martinco
description: Learn about Microsoft Entra tenant architecture for critical business systems so that you can identify your needs and compare architectural options.
ms.reviewer: ramical
ms.subservice: architecture
ms.topic: concept-article
ms.date: 2026-06-22T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 38172749-cd62-b9a5-11ef-61d98b012886
document_version_independent_id: 38172749-cd62-b9a5-11ef-61d98b012886
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/tenant-estate-critical-production.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/tenant-estate-critical-production
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/tenant-estate-critical-production.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 448c49f6-e025-e1f9-111a-78efb370b258
---

# Microsoft Entra tenants for critical business systems guidance - Microsoft Entra | Microsoft Learn

Designing your Microsoft Entra **tenant estate** — the set of tenants your organization operates — means balancing security, compliance, administrative complexity, and user experience. While a single production tenant is ideal for simplicity and user experience, your specific business and technical requirements might necessitate multiple production tenants.

This article series describes the following common tenant architecture patterns that Microsoft has observed across real-world deployments.

- [Microsoft Entra tenant estate guidance introduction](tenant-estate-guide)
- [Primary production tenant](tenant-estate-primary)
- [Collaborating production tenants](tenant-estate-collaborating)
- [Nonproduction environments](tenant-estate-nonproduction)
- [Isolated tenants for business partner access](tenant-estate-business-partner)
- [Hybrid identity and isolation](tenant-estate-hybrid-identity)

Separate tenants for critical production systems isolate an organization's most sensitive, high-value, or mission-critical applications and resources in a dedicated tenant, apart from the main workforce tenant. This pattern commonly arises when the residual risk of a security incident or operational error in the main tenant is unacceptable for those workloads — even with strong security controls in place — and it contains blast radius, enforces stricter compliance boundaries, and reduces lateral movement.

This pattern builds on the [Primary production tenant](tenant-estate-primary) baseline, which covers the seven architecture evaluation areas in detail. This article describes only the incremental considerations for isolating critical production systems, in the context of those same evaluation areas. For the full series, see [Microsoft Entra tenant estate guidance introduction](tenant-estate-guide).

## Example scenario

Contoso maintains dedicated tenants to host high-value and mission-critical applications and resources. Contoso isolates dedicated tenants from the broader enterprise environment.

A risk assessment drives Contoso's architectural choice. They apply all available security controls and best practices within a single tenant. However, the potential impact of a security incident or operational error in the main workforce tenant is unacceptable for certain critical workloads. As a result, Contoso deliberately separates these critical workloads into dedicated tenants to protect the most sensitive systems should an incident occur in the broader environment.

Dedicated tenants enforce stricter security controls and governance. This solution reflects Contoso's decision to not assume residual risk of exposing critical assets to the primary tenant blast radius even with optimal security posture in place.

The following diagram shows an isolated `FabrikamSaas.onmicrosoft.com` tenant for the critical SaaS products that Contoso offers to their customers.

![Example scenario diagram shows an isolated tenant for critical software-as-a-service products to customers.](media/multi-tenant-architecture-guide/separate-tenant-critical-production-architecture.png)

## Administration

Separate tenant architecture for critical production systems creates a new boundary (a separate set of Microsoft Entra directory roles) so that you can configure different sets of administrators. It provides a separate set of tenant-wide settings to accommodate resources and trust applications that have requirements for configurations that differ from main workforce tenants. Separate tenant architecture for critical production systems allows you to isolate instances of Microsoft services (for example, Exchange, SharePoint Online, Teams, Intune) from the main workforce tenant.

Tenants that host mission-critical applications and resources implement more restrictive security controls than the main workforce tenant. These restrictions result in higher friction user experiences and more administrative involvement in approval workflows. For example, lock down self-service capabilities, collaboration-optimized defaults replaced with their most restrictive values, and restrictions on IP address ranges and locations from which users can sign in.

Evaluate [multitenant administration patterns](tenant-estate-guide#multitenant-administration-patterns) to determine how administrators access the dedicated tenant. When maximum isolation is the priority, local accounts with separate credentials align with the security posture described in this pattern.

## Change control

Separate tenant architecture for critical production systems decouples critical workloads from changes in the main workforce tenant. Admins in dedicated tenants can independently plan changes. Apply the same considerations on change control within a tenant as described in previous **Change control** sections.

## Account lifecycle

Administrators typically preselect and tightly control workforce user access to critical workload tenants. They might provision these accounts following exhaustive workflow-implemented controls. They limit access to only users with a business need and rigorously enforce lifecycle governance. For example, access might automatically expire when employees move to different roles. In the example scenario, when an employee leaves their engineering role at Fabrikam, automation removes their account and access to the SaaS tenant. Administrators can require periodic re-certification with access reviews. They can disable external collaboration even with other tenants within the same organization.

## Credential management

To maximize isolation from the corporate environment, you can provision separate accounts and devices for users who need access to mission critical production tenants. Conditional Access policies force phishing-resistant authentication strength and compliant devices for every session.

## Collaboration

Separate tenant architecture for critical production systems explicitly restricts external collaboration. This isolation reduces exposure to and compromise of users in other tenants.

## Role-based resource assignment

Separate tenant architecture for critical production systems tightly scopes role assignments. You can assign application access through [entitlement management](../id-governance/entitlement-management-overview). Resource owners justify access requests. All assignments can undergo periodic review. The tenant can use [administrative units](../identity/role-based-access-control/administrative-units) and [restricted management administrative units](../identity/role-based-access-control/admin-units-restricted-management) to segment access within the critical workload environment.

## Risk management

### Blast radius

Separate tenant architecture for critical production systems provides isolation for extra mitigation when residual risk of a security incident or operational error in the main workforce tenant is unacceptable. When you host critical applications in a separate tenant, you can contain breaches, enforce stricter compliance boundaries, and reduce lateral movement risks. You can configure audit logs, Conditional Access, and device management policies independently from the main workforce tenant.

To realize the benefits of separate tenant architecture for critical production systems, avoid environment dependencies that break isolation. For example, if the main workforce tenant and the dedicated tenant synchronize from the same set of Active Directory forests, incidents in those forests affect both tenants. Read about potential incidents in [Hybrid identity and isolation](tenant-estate-hybrid-identity).

### Regulatory requirements

A separate tenant provides a separate boundary that allows you to create dedicated tenants in different clouds and geolocation to comply with data sovereignty regulation requirements. A dedicated tenant can help reduce audit scope.

## Other considerations

When you operate critical workload tenants, you have more overhead such as separate security baselines and monitoring. Over time, implement and audit organization-wide policy changes on security or operations across multiple tenants and monitor them for drift with capabilities such as [configuration management](../id-governance/tenant-governance/configuration-management), which is especially valuable for the stricter baselines and audit evidence these tenants require.

Duplicate licenses across tenants results in higher operational overhead. Workloads that support core business functions, regulated data, or national security interests justify the tradeoff. Document the rationale for isolation and ensure that lifecycle, access, and audit processes align with enterprise risk management.