---
layout: Conceptual
title: Identity Governance and optimization with Microsoft Security Copilot | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-governance-optimization
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Use Microsoft Security Copilot in the Microsoft Entra admin center to improve security posture, manage access reviews, entitlement management, and privileged identity management.
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: how-to
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: bb6e490a-faad-381d-fc14-4efc402c6a7e
document_version_independent_id: bb6e490a-faad-381d-fc14-4efc402c6a7e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-governance-optimization.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-governance-optimization
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-governance-optimization.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: fbb7c761-7cfc-360d-e800-5c83127a6523
---

# Identity Governance and optimization with Microsoft Security Copilot | Microsoft Learn

Microsoft Security Copilot empowers administrators to implement comprehensive governance and continuously optimize their Microsoft Entra environment using natural language queries. This capability helps you improve security posture through recommendations, manage access lifecycle through reviews and entitlement management, and secure privileged access through just-in-time controls.

This article describes how an IT administrator could prepare for their annual governance and compliance audit by using Microsoft Security Copilot governance and optimization skills for the following use cases in the Microsoft Entra admin center;

- Validate access through access reviews
- Manage structured access through entitlement management
- Secure privileged access through privileged identity management

Use the prompts and examples in this article to compile your findings into actionable insights and reports for reviews and audits by your team or management.

## Prerequisites

- A tenant with Security Copilot enabled. Refer to [Get started with Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot#option-2-provision-capacity-in-azure) for more information.
- The following roles and licenses are required for different governance and optimization use cases.

    | Use case | Role(s) | License | Tenant |
    | --- | --- | --- | --- |
    | Access reviews | [Identity Governance Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#identity-governance-administrator) | [Microsoft Entra ID P2](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Tenant with access reviews configured |
    | Entitlement management | [Identity Governance Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#identity-governance-administrator) | [Microsoft Entra ID P2](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Any tenant |
    | Privileged Identity Management | [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator), [Global Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader), [Security Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#security-reader) | [Microsoft Entra ID P2](/en-us/entra/id-protection/overview-identity-protection#license-requirements) | Tenant with PIM configured |

## Launch Security Copilot in Microsoft Entra

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with the appropriate administrative role(s) for your scenario based off the specific use cases.
2. Launch Security Copilot from the **Copilot** button in the Microsoft Entra admin center.

    ![Screenshot that shows Security Copilot in the Microsoft Entra admin center.](media/copilot-security-entra/security-copilot-entra-admin-center.png)
3. Refer to the following use cases and prompts to retrieve information or perform actions using natural language queries.

Note

If an action is blocked by insufficient permissions, a recommended role is displayed. You can use the following prompt in the Security Copilot chat to activate the required role. This is dependent on having an eligible role assignment that provides the necessary access.

- *Activate the {required role} so that I can perform {the desired task}.*

## Validate access through access reviews

To begin your assessment, you can analyze the current state of access reviews in your organization. Access reviews ensure that users have appropriate access to resources, and that access permissions are regularly validated for compliance to ensure that access is removed when no longer needed. You can extract and analyze access review data to explore, track, and analyze access reviews at scale, understand approval patterns, and identify reviewers who need attention.

### Access review exploration and management

Start by exploring your current access reviews and retrieving information about specific review instances to understand the scope and status of reviews in your organization. Use the following prompts to get the information you need:

- *Show me the top 10 pending access reviews.*
- *Get access review details for Finance Microsoft 365 Groups Q2.*
- *Who are the reviewers for the Sales App Access Q2 review?*

### Access review decision analysis

Analyze access review decisions to understand approval patterns, identify reviewers who need attention, and investigate where AI recommendations were overridden. This can help you identify the effectiveness of your access review processes and identify areas for improvement. Use the following prompts to get the information you need:

- *Who approved or denied access in the Q2 finance review?*
- *List reviews where Alex Chen is the assigned reviewer*
- *Which access review decisions overrode AI-suggested actions?*

## Manage structured access through entitlement management

Now, you can assess your entitlement management configuration to ensure that access packages and policies are properly structured and managed. Get quick access to information about access packages, policies, connected organizations, and catalog resources to manage identity and access lifecycle at scale through automated workflows.

### Catalog and access package management

You can explore your entitlement management structure, including catalogs and access packages, to understand how resources are organized and configured. Use the following prompts to get the information you need:

- *What resources are in catalog "XYZ"?*
- *How many catalogs are in the tenant?*
- *Which access packages are in catalog "XYZ"?*
- *How many access packages are in the tenant?*
- *What resource role scopes are in access package "XYZ"?*
- *Find all access packages where the name contains "Sales"?*

### User assignments and connected organizations

You can review the access package assignments and external organization relationships to ensure proper governance of both internal users and external partners who have access to your organization's resources. Use the following prompts to get the information you need:

- *What access package assignments does "User" have?*
- *Who are the external users of connected organization "XYZ"?*
- *Who are the sponsors for connected organization "XYZ"?*
- *What custom extensions does catalog "XYZ" have?*

## Secure privileged access through privileged identity management

Finally, you can review privileged identity management (PIM) configurations to ensure that just-in-time (JIT) access mechanisms and high-risk roles are properly managed and monitored.

### PIM role assignment queries

Examine current and eligible privileged role assignments to understand PIM configurations, that JIT access is being used effectively, and identify any potential risks associated with privileged access. Use the following prompts to get the information you need:

- *Which PIM roles are currently assigned to "User"?*
- *Which PIM eligible roles are assigned to "User"?*
- *Which PIM active roles are assigned to "User"?*
- *Who has PIM eligible assignment of {Specific Role}?*
- *Who has PIM active assignment of a {Specific role}?*

## Deactivate your role

After completing your tasks with Microsoft Security Copilot, ensure that you deactivate any elevated roles you activated during your session to maintain security best practices. Use the following prompt to deactivate your role:

- *I am done with my investigation or {desired task}, deactivate my access.*