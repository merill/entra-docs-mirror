---
layout: Conceptual
title: Governance relationships in Tenant Governance - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/governance-relationships
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn about governance relationships and how they enable centralized management of tenants in Microsoft Entra Tenant Governance
ms.topic: concept-article
ms.date: 2026-03-10T00:00:00.0000000Z
locale: en-us
document_id: 7ad715f8-8020-72ca-d4df-89b1b14f5987
document_version_independent_id: 7ad715f8-8020-72ca-d4df-89b1b14f5987
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/governance-relationships.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/governance-relationships
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/governance-relationships.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3d7062b4-5324-6e59-10eb-b1089da3b27d
---

# Governance relationships in Tenant Governance - Microsoft Entra ID Governance | Microsoft Learn

A governance relationship establishes a directional connection between two Microsoft Entra tenants. One tenant (the *governing* tenant) governs another tenant (the *governed* tenant). These relationships enable organizations to securely manage multiple tenants at scale from a central location.

Governance relationships enable four key scenarios:

| Scenario | Description |
| --- | --- |
| Cross-tenant delegated administration | Use governance relationships to centralize **least-privileged administrative access** across multiple Microsoft Entra tenants. Administrators sign in using accounts from the governing tenant. This approach eliminates the need to create and manage local or B2B administrator accounts in every governed tenant. |
| Multitenant application management | Manage custom, multitenant applications from the governing tenant. Administrators can monitor and maintain least-privileged application access across governed tenants without signing into each tenant individually. This approach reduces operational overhead and configuration drift. |
| Tenant configuration management | If you configured cross-tenant delegated administration in your governance relationship, use this administrative access to ensure that the tenant meets your organization's security and compliance objectives on an ongoing basis. |
| Secure tenant creation | When you create a new add-on tenant from an existing tenant, Tenant Governance automatically establishes a governance relationship between the parent tenant and the new tenant by using a default governance policy template. This step immediately brings newly created tenants under centralized administration and governance controls, reducing the risk of unmanaged or misconfigured tenants. |

## Relationship handshake

Any two Microsoft Entra tenants can create a new governance relationship through the three-step handshake. To create a new governance relationship, or update an existing one, administrators from both tenants must configure and agree on the roles and permissions that the governing tenant has over the governed tenant.

1. The future governed tenant sends the future governing tenant a governance invitation.
2. Upon receiving a governance invitation, the future governing tenant sends the future governed tenant a governance request (with a selected governance policy template).
3. After the future governed tenant reviews and accepts the request, the tenants establish a governance relationship.

Tenants that meet these criteria can skip the invitation step:

- The future governing tenant identifies the future governed tenant as a related tenant through tenant discovery with a shared billing account.
- Tenants in an active governance relationship can skip the invitation step to update their relationship or create a new one.

## Relationship lifecycle

A governance relationship moves through several states from creation to termination. The following sections describe the states for both requests and established relationships.

### Request states

Governance requests progress through these states:

| State | Description |
| --- | --- |
| Pending | The governing tenant sent the request and awaits a response from the governed tenant. |
| Accepted | The governed tenant accepted the request, creating a governance relationship. |
| Rejected | The governed tenant rejected the request. |

### Relationship states

Governance relationships progress through these states:

| State | Description |
| --- | --- |
| Active | The relationship is established and operational. |
| Termination requested | The governing tenant has requested to terminate the relationship. |
| Terminated | Both tenants terminated the relationship, and Tenant Governance deleted all related resources. |

## Governance models

When you set up governance relationships between a pair of tenants, note these supported models.

| Supported? | Model type | Description |
| --- | --- | --- |
| ✅ | One to many | A tenant can govern multiple tenants. |
| ✅ | Many to one | Multiple tenants can govern a tenant. |
| ❌ | Multi-tier | A tenant can't be both a governing and governed tenant. For example, if Contoso governs Fabrikam, Fabrikam can't request to govern another tenant. |