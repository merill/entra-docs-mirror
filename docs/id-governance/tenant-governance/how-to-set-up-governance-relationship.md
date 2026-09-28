---
layout: Conceptual
title: Set up a governance relationship - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-set-up-governance-relationship
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to set up a governance relationship between a governing and governed tenant using the handshake process in Microsoft Entra
ms.topic: how-to
ms.date: 2026-03-10T00:00:00.0000000Z
locale: en-us
document_id: b59095ee-d313-1bf7-9d2d-321dfefd8cd2
document_version_independent_id: b59095ee-d313-1bf7-9d2d-321dfefd8cd2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-set-up-governance-relationship.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-set-up-governance-relationship
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-set-up-governance-relationship.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 46cdb254-8ff1-24dc-4677-8fef3422b593
---

# Set up a governance relationship - Microsoft Entra ID Governance | Microsoft Learn

Governance relationships enable centralized, cross-tenant administration and multitenant application management. A governance relationship is a directional relationship between two tenants: one tenant acts as the *governing tenant*, and the other acts as the *governed tenant*.

Establish a governance relationship between any two Microsoft Entra tenants by using the three-step handshake process, or the two-step handshake if tenants meet certain criteria. This article describes both options.

## Prerequisites

- You need the **Tenant Governance Administrator** role.
- Review license requirements for sending governance requests in [Microsoft Entra licensing](../../fundamentals/licensing#microsoft-entra-tenant-governance).
- You must create a governance policy template in the governing tenant before you initiate the handshake process.
- If you're using the three-step handshake, you must enable governance invitations in the governing tenant.

## Create a governance policy template

Before you can set up a governance relationship, you must create a governance policy template in the governing tenant. The policy template defines the type of relationship and the level of access the governing tenant has over the governed tenant. Reuse templates across distinct relationships.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the governing tenant.
2. Browse to **Tenant governance** &gt; **Templates**.
3. Create a new policy template and configure these options as needed:

    - **Delegated administration**: Select one or more Microsoft Entra built-in roles and assign them to a role assignable security group in the governing tenant. Members of this group can use their governing tenant credentials to sign in to the governed tenant without needing an account in the governed tenant. Each group can have multiple role assignments, and each policy template can have multiple groups defined.
    - **Multitenant application management**: Select a custom, multitenant application. The governed tenant creates a service principal with the same permissions when you establish the relationship.

## Set up a governance relationship using a three-step handshake

Use the three-step handshake when there's no preexisting billing signal or active relationship between the two tenants.

### Enable governance invitations in the governing tenant

Before you start the handshake, enable governance invitations in the governing tenant to receive invitations from other tenants. By default, this setting is turned off.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the governing tenant.
2. Browse to **Tenant governance** &gt; **Settings**.
3. Enable the invitations setting to allow governance invitations. Disable this setting after you receive the invitation.

### Step 1: Send a governance invitation from the governed tenant

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the future governed tenant.
2. Browse to **Tenant governance** &gt; **Governing tenants** &gt; **Sent invitations**.
3. Send a governance invitation to the future governing tenant. The future governing tenant receives an email notification about the invitation.

Note

Governance invitations are valid for 30 days.

### Step 2: Send a governance request from the governing tenant

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the governing tenant.
2. Browse to **Tenant governance** &gt; **Governed tenants** &gt; **Received invitations**.
3. Review the received governance invitation.
4. Send a governance request to the governed tenant, selecting the appropriate governance policy template. The future governed tenant receives an email notification that a request is pending.

Note

Governance requests are valid for 14 days.

### Step 3: Accept the governance request in the governed tenant

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the governed tenant.
2. Browse to **Tenant governance** &gt; **Governing tenants** &gt; **Received requests**.
3. Select a request ID to review the governance request.
4. Accept the governance request to create the governance relationship. The governing tenant receives an email notification that you accepted the request and created the relationship.

## Set up a governance relationship using a two-step handshake

Use the two-step handshake when either of these conditions is met:

- A billing signal identifies the target tenant as a related tenant.
- There's an existing, active governance relationship between the two tenants, and you're seeking to establish another relationship between them.

### Step 1: Send a governance request from the governing tenant

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the governing tenant.
2. Browse to **Tenant governance** &gt; **Governed tenants** &gt; **Send governance request**.
3. Send a governance request to the governed tenant, selecting the appropriate governance policy template.

Note

Governance requests are valid for 14 days.

### Step 2: Accept the governance request in the governed tenant

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the governed tenant.
2. Browse to **Tenant governance** &gt; **Governing tenants** &gt; **Received requests**.
3. Review the governance request.
4. Accept the governance request to create the governance relationship.

## Verify the governance relationship

When you successfully create a governance relationship, Tenant Governance provisions these resources:

- A governance relationship object in both the governing and governed tenants.
- In the governed tenant:

    - If you configured delegated administration, Tenant Governance updates the partner-specific configuration for cross-tenant access and creates cross-tenant role assignments.
    - If you configured multitenant application management, Tenant Governance creates the corresponding service principal and its permissions.