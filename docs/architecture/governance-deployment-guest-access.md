---
layout: Conceptual
title: Microsoft Entra ID Governance deployment guide to govern guest and partner access - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/governance-deployment-guest-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra-id-governance
manager: martinco
description: Learn how to govern guest and partner access to resources in Microsoft Entra ID Governance.
ms.topic: concept-article
ms.date: 2025-03-25T00:00:00.0000000Z
ms.reviewer: gasinh
locale: en-us
document_id: 4c177df6-f3dc-c29b-a51a-33e682772abb
document_version_independent_id: 4c177df6-f3dc-c29b-a51a-33e682772abb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/governance-deployment-guest-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/governance-deployment-guest-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/governance-deployment-guest-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9bc92bef-9a87-711b-c6c0-ccaee9c58290
---

# Microsoft Entra ID Governance deployment guide to govern guest and partner access - Microsoft Entra | Microsoft Learn

Deployment scenarios are guidance on how to combine and test Microsoft Security products and services. You can discover how capabilities work together to improve productivity, strengthen security, also help you meet compliance and regulatory requirements.

The following products and services appear in this guide:

- [Microsoft Entra ID Governance](../id-governance/identity-governance-overview)
- [Microsoft Entra](../fundamentals/what-is-entra)
- [Entitlement management](../id-governance/entitlement-management-overview)
- [Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-overview)
- Privileged Identity Management [(PIM) for Groups](../id-governance/privileged-identity-management/concept-pim-for-groups)
- [Identity Governance dashboard](../id-governance/governance-dashboard)

Use this scenario to help determine the need for [Microsoft Entra ID Governance](../id-governance/identity-governance-overview) to create and grant access for your organization. Learn how to manage guest users in your environment.

## Timelines

Timelines show approximate delivery stage duration and are based on scenario complexity. Times are estimations and vary depending on the environment.

- Onboarding and discovery - 2 hours
- Auto assign resources - 1 hour
- Custom workflows - 2 hours
- Convert external users - 1 hour
- Access review - 1 hour

## Scenario requirements

To enable the scenario, ensure the following requirements are met:

- [Microsoft Entra ID](../fundamentals/licensing) P1 or P2 license
- Microsoft Entra ID Governance SKU
    - Microsoft Logic Apps and auto assignment policies
- Two tenants, target and source
- A cloud user account on the target tenant to approve and access
- A cloud user on the source tenant to request access
- An account on the target tenant:
    - User Administrator,
    - Identity Governance Administrator,
    - Privileged Role Administrator, or
    - Global Administrator

### B2B collaboration and guest users

To collaborate with guest users, you can let them use their preferred identity to sign in to your app or other enterprise apps: SaaS, custom-developed, and more. Typically, B2B collaboration users are in your directory as guest users.

Learn more in the overview, [B2B collaboration with external guests for your workforce](../external-id/what-is-b2b).

## Provision guest users in Microsoft Entra ID

Users can use Microsoft Entra [entitlement management](../id-governance/entitlement-management-overview) self-service features to sign up for access. Learn about [self-service sign-up](../external-id/self-service-sign-up-overview), and how to [manage external access with entitlement management](6-secure-access-entitlement-managment).

### Entitlement management or self-service signup

Use the following table to ease decision making.

| Entitlement management | Both | Self-service signup |
| --- | --- | --- |
| - Requested with My Access portal or link  - Access packages  - Built-in approval workflows  - Scope requests by organization  - Lifecycle automation  - Supports Security Assertion Markup Language (SAML) and Web Service Federation (WS-Fed) identities | - Request triggered by end user  - Collect other attributes  - Trigger custom logic apps and APIs  - Available to anyone  - Supports: Microsoft Entra ID, email one-time pass (OTP) | - Branded onboarding sign-in page  - Users create accounts at the app  - Language options  - Supports: Google, Microsoft Account (MSA), Facebook |

## Onboarding and discovery

With the [Microsoft Identity Governance dashboard](../id-governance/governance-dashboard), discover usage information about identity features configured in your tenant. See the current state of your environment, determine response actions, and find links to documentation.

### External user insights

Over time, external user accounts are created in the Microsoft Entra tenant. When external users, or guests, stop accessing the tenant, the external user account becomes stale.

You can [monitor and clean up stale guest access accounts using access reviews](../identity/users/clean-up-stale-guest-accounts).

### External user attribute management

Approvers allow or deny requests for access packages. To help Approvers make access decisions about onboarding external users, you can include custom questions in an access request flow. Store Requestor information for apps or other processes.

## Entitlement management

Decentralized identity solutions enable individuals to control their digital identities and manage identity data without reliance on a centralized authority or intermediary. Reduce the need for new employees or business partners to perform self-attestation. Simplify approval processes and simplify your compliance posture. Learn more about [Microsoft Verified ID](../verified-id/decentralized-identifier-overview) in entitlement management.

### External user assignments and access packages

When external users request initial access, they're invited to your directory and assigned access. In entitlement management, use access packages to assign access to multiple resources. Ensure access packages are in a container called a catalog, which has resources you can add to access package.

- [Govern access for external users in entitlement management](../id-governance/entitlement-management-external-users)
- [Create an access package in entitlement management](../id-governance/entitlement-management-access-package-create)
- [View, add, and remove assignments for an access package](../id-governance/entitlement-management-access-package-assignments)

## Deploy external user access

1. [Add connected organization](/en-us/azure/active-directory/governance/entitlement-management-organization).
2. [Learn settings for external users](/en-us/azure/active-directory/governance/entitlement-management-external-users).
3. [Create an access package in entitlement management](/en-us/azure/active-directory/governance/entitlement-management-access-package-create).
4. [Change the Hidden setting](/en-us/azure/active-directory/governance/entitlement-management-access-package-edit).
5. [Create an access package with Verified ID requirements](/en-us/azure/active-directory/governance/entitlement-management-verified-id-settings).
6. [Assign users](/en-us/azure/active-directory/governance/entitlement-management-access-package-assignments).
7. [Share a link to request an access package in entitlement management](/en-us/azure/active-directory/governance/entitlement-management-access-package-settings).

For more detail, see [Govern access for external users in entitlement management](../id-governance/entitlement-management-external-users).

### Assign and remove resources

To learn how to assign access, remove it, and more guidance, go to [Scenario 2: Assign employee access to resources](governance-deployment-employee-access).

### Custom workflows with Azure Logic Apps

To create and run automated workflows with [Azure Logic Apps](/en-us/azure/logic-apps/), learn about custom use cases and more, or go to [Scenario 2: Assign employee access to resources](governance-deployment-employee-access).

## Manage the external user lifecycle

In entitlement management, external users have three states: governed, ungoverned, and blank. External users invited to your tenant are ungoverned. The ungoverned can lose their last access package assignment yet remain in the tenant indefinitely. To manage the lifecycle, convert the ungoverned to governed while they have access.

Learn to [govern access for external users in entitlement management](../id-governance/entitlement-management-external-users).

## Deploy guest user lifecycle

- [Create an access package in entitlement management](/en-us/azure/active-directory/governance/entitlement-management-access-package-create)
- [Create an automatic assignment policy](/en-us/azure/active-directory/governance/entitlement-management-access-package-auto-assignment-policy)
- [Manage guest user lifecycle in the Microsoft Entra admin center](/en-us/azure/active-directory/governance/entitlement-management-access-package-manage-lifecycle)

### Access reviews

To learn to enable recurring access reviews, go to [Scenario 2: Assign employee access to resources](governance-deployment-employee-access).

### Multistage reviews

Learn about multistage reviews that ease reviewer burdens, go to [Scenario 2: Assign employee access to resources](governance-deployment-employee-access).

### Inactive users

You can conduct inactive user reviews to discern stale accounts. To learn more, go to [Scenario 2: Assign employee access to resources](governance-deployment-employee-access).

### User-to-Group Affiliation

The User-to-Group Affiliation feature helps you make access decisions based on machine-learning derived recommendations. To learn more, go to [Scenario 2: Assign employee access to resources](governance-deployment-employee-access).

### Guest user risk in Microsoft Teams and Microsoft 365 Groups

Access reviews include new groups with guest users and groups with recently added guests. Review recommendations are based on last sign-in details. As an option, denied guests are blocked from sign-in, then the account is deleted.

Learn more:

- [Guest access in Microsoft Teams](/en-us/microsoftteams/guest-access)
- [Manage guest access in Microsoft 365 Groups](/en-us/microsoft-365/admin/create-groups/manage-guest-access-in-groups?view=o365-worldwide&amp;preserve-view=true)
- [Overview of Microsoft 365 Groups for Administrators](/en-us/microsoft-365/admin/create-groups/office-365-groups?view=o365-worldwide&amp;preserve-view=true)
- [Microsoft 365 guest sharing settings reference](/en-us/microsoft-365/solutions/microsoft-365-guest-settings?view=o365-worldwide&amp;preserve-view=true)

### Guest user access reviews

When conducting access reviews, you can review groups that have guest user members. Or you can review apps with assigned guest users. Guests are inactive after 30 days with no sign-in.

The **New access review** dialog, with the **Review type** tab, and guest user options highlighted.

[![Screenshot of the New access review dialog with guest user options highlighted.](media/governance-deployment/guest-user-options.png)](media/governance-deployment/guest-user-options-expanded.png#lightbox)

### Access review history report

To learn more about downloadable review-history reports, see [Scenario 2: Assign employee access to resources](governance-deployment-employee-access).

## Deploy access review guide

For deployment instructions, go to [Scenario 2: Assign employee access to resources](governance-deployment-employee-access).