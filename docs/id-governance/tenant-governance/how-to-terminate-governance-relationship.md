---
layout: Conceptual
title: Terminate a governance relationship - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-terminate-governance-relationship
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to terminate a governance relationship between tenants in Microsoft Entra Tenant Governance and understand what resources are removed
ms.topic: how-to
ms.date: 2026-03-10T00:00:00.0000000Z
locale: en-us
document_id: 8c4c4123-c1ee-d227-50ad-4b73ae2f3f6e
document_version_independent_id: 8c4c4123-c1ee-d227-50ad-4b73ae2f3f6e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-terminate-governance-relationship.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-terminate-governance-relationship
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-terminate-governance-relationship.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 9f48d605-8cdc-9635-d8e8-288ba7c94715
---

# Terminate a governance relationship - Microsoft Entra ID Governance | Microsoft Learn

This article describes how to terminate a governance relationship between a governing tenant and a governed tenant. When you terminate a governance relationship, Tenant Governance deletes all relationship-related resources from the governed tenant, including granular delegated admin privileges (GDAP) role assignments, service principals, and their permissions.

Terminate a governance relationship in two ways, depending on whether the governing tenant or the governed tenant initiates the termination.

| Initiated by | Process |
| --- | --- |
| Governing tenant | Sends a termination request to the governed tenant. The governed tenant must confirm to complete termination. |
| Governed tenant | Directly terminates the relationship. The governing tenant doesn't need to take any action. |

## Prerequisites

- You must have an active governance relationship between two tenants.
- You need the **Tenant Governance Administrator** role.

## Terminate a relationship: Governing tenant initiation

The governing tenant can request to terminate a governance relationship. This process requires confirmation from the governed tenant before Tenant Governance removes the relationship and its resources.

### Initiate termination as the governing tenant

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the governing tenant.
2. Browse to **Tenant governance** &gt; **Governed tenants**.
3. Select the active governance relationship you want to terminate.
4. Select **Terminate governance**.

    The relationship status changes to **Termination requested**. Tenant Governance sends an email notification to the governed tenant about the termination request.
5. Wait for the governed tenant to confirm the termination.

    When the governed tenant confirms, Tenant Governance deletes all relationship-related resources from the governed tenant, and the relationship status changes to **Terminated**.

### Confirm termination as the governed tenant

When the governing tenant initiates termination, the governed tenant must confirm the request to complete the process.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the governed tenant.
2. Browse to **Tenant governance** &gt; **Governing tenants**.
3. Change the **Relationship status** filter to **Termination requested**.
4. Select the tenant that requested termination.
5. Select **Confirm termination**.

    Tenant Governance deletes all relationship-related resources from the governed tenant, and the relationship status changes to **Terminated**. Tenant Governance sends an email notification to the governing tenant that termination is complete.

## Directly terminate a relationship: Governed tenant

As the governed tenant, directly terminate a governance relationship without requiring approval from the governing tenant.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the governed tenant.
2. Browse to **Tenant governance** &gt; **Governing tenants**.
3. Select the tenant whose governance relationship you want to terminate.
4. Select **Terminate governance**.
5. Review the details of the relationship, then confirm termination.

    Tenant Governance deletes all relationship-related resources from the governed tenant, and the relationship status changes to **Terminated**. Tenant Governance sends an email notification to the governing tenant that the relationship is terminated.

## What happens when you terminate a governance relationship

When you terminate a governance relationship, Tenant Governance updates or deletes these resources from the governed tenant:

- **Cross-tenant access policy**: Tenant Governance removes the governing tenant as a partner from the partner-specific cross-tenant access configuration in the governed tenant.
- **GDAP role assignments**: Tenant Governance removes cross-tenant role assignments that allowed users from the governing tenant to sign in to and manage the governed tenant.
- **Service principals**: If an admin configured multitenant application management, Tenant Governance removes the corresponding service principal and its permissions from the governed tenant.

After termination, users from the governing tenant can no longer sign in to the governed tenant with their governing tenant credentials through the governance relationship.