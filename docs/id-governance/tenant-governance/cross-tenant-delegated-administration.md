---
layout: Conceptual
title: Cross-tenant delegated administration - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/cross-tenant-delegated-administration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn about cross-tenant delegated administration and the GDAP-based permission model for managing tenants in Microsoft Entra.
ms.topic: concept-article
ms.date: 2026-07-27T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: c9240db5-1708-f4d6-4f0c-67c2a2799767
document_version_independent_id: c9240db5-1708-f4d6-4f0c-67c2a2799767
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/cross-tenant-delegated-administration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/cross-tenant-delegated-administration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/cross-tenant-delegated-administration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: f8a251aa-228f-a7e3-000f-d6e1aa1a5868
---

# Cross-tenant delegated administration - Microsoft Entra ID Governance | Microsoft Learn

Cross-tenant delegated administration is a capability in Tenant Governance that enables administrators in one tenant to manage another tenant by using their home tenant credentials. Administrators don't need local accounts or business-to-business (B2B) guest accounts in every tenant. This capability uses granular delegated admin privileges (GDAP) technology to provide delegated, least-privileged administration and access across tenant boundaries.

This article explains the GDAP-based permission model that Tenant Governance and other Microsoft services use. It serves as the central reference for customers, partners, and Microsoft workloads that expose delegated administration capabilities through their own products and services.

## How the permission model works

Cross-tenant delegated administration has two permission layers:

- **Relationship-level permissions** establish the delegated administration relationship between tenants.
- **Workload-specific permissions** are the additional permissions that individual Microsoft services might require when they use their own role-based access control (RBAC) systems.

### Relationship-level permissions

Before delegated administrators can access a governed tenant, a [governance relationship](governance-relationships) (or GDAP relationship) is established between the governing tenant and the governed tenant. This relationship establishes the trust boundary and defines the delegated administration policies: the roles and permissions available to administrators from the governing tenant.

In Tenant Governance, delegated administration roles are defined in a [governance policy template](governance-policy-templates). The template identifies the Microsoft Entra built-in roles that are enabled for administration and maps those roles to security groups in the governing tenant. When the relationship is established, remote tenant groups (or group proxies) are created in the governed tenant. Each group proxy maps back to a security group in the governing tenant, so you manage membership in the governing tenant while access is represented in the governed tenant. The roles assigned to these group proxies, as defined in the relationship, are GDAP role assignments.

For more information about relationship-level permissions in Partner Center, see [Granular delegated admin privileges (GDAP)](/en-us/partner-center/customers/gdap-introduction).

### Workload-specific permissions

Microsoft workloads might have RBAC systems in addition to Microsoft Entra roles. The delegated administration relationship establishes the trust and identity foundation, but a workload might require additional role assignments in the governed tenant before administrators can manage that workload's resources.

A workload-specific role assignment that you make after the relationship is established might target a remote tenant group (or group proxy) that maps back to a security group in the governing tenant. This mapping allows the governing tenant to manage membership in its own security group, while the governed tenant assigns workload permissions to the corresponding proxy. Assign additional workload permissions to remote tenant groups only when those permissions are required for the partner or governing tenant to perform agreed-upon administrative work. Partners should be aware that workload-specific permissions might be assigned in the customer tenant after the relationship is established.

## Expected behavior by permission type

The following table summarizes how each permission type is configured and controlled.

| Permission type | Where configured | Who approves or assigns | What it controls |
| --- | --- | --- | --- |
| Microsoft Entra built-in roles (from the delegated administration relationship) | During governance or GDAP relationship setup | The governed (customer) tenant reviews and accepts the request | Baseline delegated administration access for Microsoft Entra roles |
| Azure RBAC roles | In the governed (customer) tenant, after the relationship exists | An admin in the governed (customer) tenant | Access to Azure resources governed by Azure RBAC |
| Defender RBAC or Unified RBAC roles | In the governed (customer) tenant, after the relationship exists | An admin in the governed (customer) tenant | Access to Defender or related workload permissions |
| Security group membership | In the governing (partner) tenant | The governing (partner) tenant | Which partner users receive the delegated access that the group represents |

For more information about delegated administration in Microsoft Defender, see [Configure delegated access with governance relationships for multitenant organizations](/en-us/unified-secops/governance-relationships).

## Recommended practices for customers

### Review the requested relationship before accepting

Before you accept a delegated administration relationship through Tenant Governance or Partner Center, carefully review the request. Check which roles are included, and confirm that you recognize the organization or tenant that sent the request.

If a request comes from an organization or tenant that you don't recognize, don't accept it. When you accept a governance (GDAP) request, you grant administrators from the governing tenant access to your tenant through the approved roles. The relationship defines the delegated administration baseline and determines which administrators from the governing tenant can access your tenant. Accept a request only when you expect the relationship and trust the requesting organization.

### Assign workload-specific permissions only when needed

If a governing tenant admin asks you to assign permissions to a remote tenant group, confirm that the assignment is required for an agreed-upon service or administration scenario. Don't assign additional Azure or Defender permissions unless you understand why the partner or governing tenant needs that access.

### Monitor delegated administrator activity

Use the governed tenant's sign-in logs and audit logs to monitor administrator activity. A governed tenant can track governing tenant administrator activity in its sign-in and audit logs. For more information, see [Monitor governing tenant admin activity in a governed tenant](how-to-monitor-governing-activity).

### Use preventive controls where available

For Azure role assignments, consider using [Azure Policy](/en-us/azure/governance/policy/overview) to restrict assignments to remote tenant groups if your organization doesn't want tenant administrators to grant those permissions.

## Recommended practices for partners and governing tenants

### Communicate required permissions

Tell customers which workload-specific roles you need them to configure. Clear communication helps avoid cases where a customer grants broader access than intended.

### Manage access through security groups

Assign named security groups to delegated administration roles, and manage technician membership from the governing (partner) tenant. Assign a security group in your tenant to an approved role in the customer tenant. Then manage membership in that security group so that it includes only the technicians who help that customer.

### Monitor for unexpected workload assignments

Establish a process to detect and review workload-specific role assignments to remote tenant groups, such as Azure and Defender role assignments. Consider aggregating Azure logs and Microsoft 365 logs through [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview). To find Azure and Defender role assignments in your audit logs, see [Microsoft Defender XDR auditing](/en-us/defender-xdr/microsoft-xdr-auditing).