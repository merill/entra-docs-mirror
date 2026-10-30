---
layout: Conceptual
title: Microsoft Entra hybrid identity and isolation multitenant guide - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/tenant-estate-hybrid-identity
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: bathawes
ms.author: beathawe
ms.service: entra
manager: martinco
description: Learn about Microsoft Entra tenant architecture for hybrid identity and isolation so that you can identify your needs and compare architectural options.
ms.reviewer: ramical
ms.subservice: architecture
ms.topic: concept-article
ms.date: 2026-06-22T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: a14d6972-a28c-251d-cccb-84e9541d8a55
document_version_independent_id: a14d6972-a28c-251d-cccb-84e9541d8a55
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/tenant-estate-hybrid-identity.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/tenant-estate-hybrid-identity
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/tenant-estate-hybrid-identity.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: de84727b-9204-3014-0943-2db3045f710c
---

# Microsoft Entra hybrid identity and isolation multitenant guide - Microsoft Entra | Microsoft Learn

Designing your Microsoft Entra **tenant estate** — the set of tenants your organization operates — means balancing security, compliance, administrative complexity, and user experience. While a single production tenant is ideal for simplicity and user experience, your specific business and technical requirements might necessitate multiple production tenants.

This article series describes the following common tenant architecture patterns that Microsoft has observed across real-world deployments.

- [Microsoft Entra tenant estate guidance introduction](tenant-estate-guide)
- [Primary production tenant](tenant-estate-primary)
- [Collaborating production tenants](tenant-estate-collaborating)
- [Nonproduction environments](tenant-estate-nonproduction)
- [Isolated tenants for critical production systems](tenant-estate-critical-production)
- [Isolated tenants for business partner access](tenant-estate-business-partner)

This article describes hybrid identity and isolation. A multitenant architecture can provide strong isolation at the cloud layer. However, many organizations operate a hybrid identity model. Hybrid identity supports resource access and device management across on-premises and cloud environments. However, it increases attack surface and operational complexity. It requires a larger investment to deploy, monitor, and maintain.

Microsoft Entra ID tenants synchronize users, groups, and devices from on-premises Active Directory with tools like Microsoft Entra Connect, Cloud Sync or Microsoft Identity Manager.

When you design a multitenant architecture to meet isolation requirements, use segmentation controls in each Microsoft Entra tenant and in the underlying infrastructure. For example, if multiple tenants source identities from the same Active Directory forest (or from interconnected forests that use trusts), then shared identity sources can undermine tenant-level isolation. Plan for the following potential incidents.

- A compromised on-premises account might propagate to multiple tenants if that account synchronizes into each one.
- Group memberships managed on premises might inadvertently grant access across tenants if improperly scoped.
- Device compliance and Conditional Access policies can rely on signals from hybrid-joined devices that might share across tenants.

To achieve meaningful isolation in a hybrid scenario, consider the following recommendations.

- **Segment Active Directory forests or domains** to align with tenant boundaries. For example, use separate domains for each tenant and avoid cross-domain trusts unless explicitly required.
- **Scope synchronization connectors** to limit which identities synchronize into each tenant. Avoid overlapping sync scopes that could result in the same identity appearing in multiple tenants.
- **Review group management practices**, especially if groups synchronize from on premises. Ensure that group membership doesn't inadvertently span isolation boundaries.
- **Evaluate device management boundaries**, particularly if you use Intune or Configuration Manager in hybrid mode. Enroll and manage devices in alignment with the tenants that they support.
- **Apply least privilege principles** to on-premises administrators. Admins with rights in Active Directory might indirectly influence multiple tenants with improperly scoped synchronization.
- **Align cloud isolation with on-premises infrastructure isolation**. Without careful design, hybrid identity can become a bridge that bypasses tenant boundaries. If you implement multitenant architectures for security, compliance, or operational reasons, include Active Directory and device management architecture in your planning.

The preceding considerations highlight isolation risks specific to multitenant architectures that operate in hybrid identity models where shared on‑premises infrastructure can unintentionally weaken tenant boundaries. These recommendations are additive and not a substitute for established identity security best practices. Continue to apply well‑understood controls such as tiered Active Directory administration models, Privileged Access Workstations (PAW), and strict separation of Tier‑0 assets.