---
layout: Conceptual
title: Microsoft Entra licensing - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/licensing
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: This article documents licensing requirements for Microsoft Entra features.
ms.topic: concept-article
ms.date: 2026-06-18T00:00:00.0000000Z
locale: en-us
document_id: 4adc9210-6b5b-0bc6-858f-ac8890d95baa
document_version_independent_id: 6f7a6b66-304b-7196-89e1-875b86c4a264
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/licensing.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/licensing
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/licensing.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 582d1cc7-69d1-3bd6-a334-bf7570fd510a
---

# Microsoft Entra licensing - Microsoft Entra | Microsoft Learn

## Overview

This article discusses licensing options for the Microsoft Entra product family. It's intended for security decision makers, identity and network access administrators, and IT professionals who are considering Microsoft Entra solutions for their organizations.

Note

If you're troubleshooting licensing assignment issues, review [Manage group-based licensing errors](/en-us/microsoft-365/admin/manage/manage-group-licenses?view=o365-worldwide&amp;preserve-view=true#manage-group-based-licensing-errors).

## Microsoft Entra licensing options

Microsoft Entra is available in several licensing options that allow you to choose the package best suited to your needs.

Note

The licensing options on this page aren't comprehensive. You can get detailed information about the various options at the [Microsoft Entra pricing page](https://www.microsoft.com/security/business/microsoft-entra-pricing) and at the [Compare Microsoft 365 Enterprise plans and pricing page](https://www.microsoft.com/microsoft-365/enterprise/microsoft365-plans-and-pricing).

**Microsoft Entra ID Free**: Included with Microsoft cloud subscriptions such as Microsoft Azure, Microsoft 365, and others.

**Microsoft Entra ID P1**: Microsoft Entra ID P1 is available as a standalone product. It is also included with the following offers for enterprise customers:

- Microsoft 365 E3, E5, E7
- Microsoft 365 F1, F3
- Enterprise Mobility + Security E3

Entra ID P1 is also included in Microsoft 365 Business Premium for small to medium businesses.

**Microsoft Entra ID P2**: Microsoft Entra ID P2 is available as a standalone product. It is also included with the following offers for enterprise customers:

- Microsoft 365 E5, E7
- Microsoft Defender Suite (formerly Microsoft 365 E5 Security)
- Microsoft Defender Suite FLW
- Microsoft Defender + Purview Suite FLW
- Enterprise Mobility + Security E5

Entra ID P2 is also included in Microsoft Defender Suite for Microsoft 365 Business Premium and Microsoft Defender and Purview Suites for Microsoft 365 Business Premium for small to medium businesses. For more information, see the [Microsoft 365 for small and medium businesses pricing page](https://www.microsoft.com/security/pricing/small-medium-business/security-add-on-plans).

**Microsoft Entra Suite**: The suite combines Microsoft Entra products to secure access for your employees. It allows administrators to provide secure access from anywhere to any app or resource whether cloud or on-premises, while ensuring least privilege access. A Microsoft Entra ID P1 subscription or a package that includes Microsoft Entra ID P1is required. The Microsoft Entra Suite is available as a standalone plan or included in Microsoft 365 E7. The suite includes five products:

- Microsoft Entra Private Access
- Microsoft Entra Internet Access
- Microsoft Entra ID Governance
- Microsoft Entra ID Protection
- Microsoft Entra Verified ID (premium capabilities)

Important

User and group license assignments are managed through the Microsoft 365 Admin Center. For more information on how to assign or unassign licenses to users and groups, see this article: - [Assign or unassign licenses for users in the Microsoft 365 admin center](/en-us/microsoft-365/admin/manage/assign-licenses-to-users)

## App provisioning

Microsoft Entra application proxy requires Microsoft Entra ID P1 or P2 licenses. For more information about licensing, see [Microsoft Entra pricing.](https://www.microsoft.com/security/business/microsoft-entra-pricing)

## Authentication

The following table lists features that are available for authentication in the various versions of Microsoft Entra ID. Plan out your needs for securing user sign-in, then determine which approach meets those requirements. For example, although Microsoft Entra ID Free provides security defaults with multifactor authentication, only Microsoft Authenticator can be used for the authentication prompt, including text and voice calls. This approach might be a limitation if you can't make sure that Authenticator is installed on a user's personal device.

Note

Microsoft 365 E7 includes the Microsoft Entra Suite, which provides all Microsoft Entra ID P2 authentication features listed in this table.

| Feature | Microsoft Entra ID Free - Security defaults (enabled for all users) | Microsoft Entra ID Free - Global Administrators only | Office 365 | Microsoft Entra ID P1 | Microsoft Entra ID P2 |
| --- | --- | --- | --- | --- | --- |
| Protect Microsoft Entra tenant admin accounts with MFA | ✅ | ✅ (*Microsoft Entra Global Administrator* accounts only) | ✅ | ✅ | ✅ |
| Mobile app as a second factor | ✅ | ✅ | ✅ | ✅ | ✅ |
| Phone call as a second factor |  |  | ✅ | ✅ | ✅ |
| SMS as a second factor |  | ✅ | ✅ | ✅ | ✅ |
| Admin control over verification methods |  | ✅ | ✅ | ✅ | ✅ |
| Fraud alert |  |  |  | ✅ | ✅ |
| MFA Reports |  |  |  | ✅ | ✅ |
| Custom greetings for phone calls |  |  |  | ✅ | ✅ |
| Custom caller ID for phone calls |  |  |  | ✅ | ✅ |
| Trusted IPs |  |  |  | ✅ | ✅ |
| Remember MFA for trusted devices |  | ✅ | ✅ | ✅ | ✅ |
| MFA for on-premises applications |  |  |  | ✅ | ✅ |
| Conditional Access |  |  |  | ✅ | ✅ |
| Risk-based Conditional Access |  |  |  |  | ✅ |
| Self-service password reset (SSPR) | ✅ | ✅ | ✅ | ✅ | ✅ |
| SSPR with writeback |  |  |  | ✅ | ✅ |

## Managed identities

There are no licensing requirements for using Managed identities for Azure resources. Managed identities for Azure resources provide an automatically managed identity for applications to use when connecting to resources that support Microsoft Entra authentication. One of the benefits of using managed identities is that you don't need to manage credentials, and they can be used at no extra cost. For more information, see [What is managed identities for Azure resources?](../identity/managed-identities-azure-resources/overview).

## Microsoft Entra Agent ID

Microsoft Entra Agent ID is a product within Microsoft Entra that provides the platform for creating and managing agent identities and agent identity blueprints. Agent ID is available for all Microsoft Entra customers.

[Microsoft Agent 365](/en-us/microsoft-agent-365/overview) enables agents to operate across Microsoft 365 services and enterprise workflows, which requires a **Microsoft Agent 365** license for each user. For pricing details, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing).

Extending Microsoft Entra security features to agents requires Microsoft Agent 365. Agent 365 is included with Microsoft 365 E7 and is available as an add-on to Microsoft E5/A5/Business Premium (or Microsoft Defender Suite + Microsoft Purview Suite). See our latest [Agent 365 product terms for more details](https://www.microsoft.com/licensing/terms/productoffering/Agent365/EAEAS#clause-2755-h3-1).

## Microsoft Entra ID Governance

The following table shows the licensing requirements for Microsoft Entra ID Governance features for member users. Microsoft Entra Suite includes all features of Microsoft Entra ID Governance. Microsoft 365 E7 also includes all ID Governance features through the Entra Suite and Agent 365. Licensing information and example license scenarios for Entitlement management, Access reviews, and Lifecycle Workflows are provided following the table.

### Features by license

The following table shows what features associated with identity governance are available with each license. For more information on other features, see [Microsoft Entra plans and pricing](https://www.microsoft.com/security/business/microsoft-entra-pricing). Not all features are available in all clouds; see [Microsoft Entra feature availability](../identity/authentication/feature-availability) for Azure Government.

| Feature | Free | Microsoft Entra ID P1 | Microsoft Entra ID P2 | Microsoft Entra ID Governance | Microsoft Entra Suite | Microsoft Agent 365 |
| --- | --- | --- | --- | --- | --- | --- |
| **Provisioning** |  |  |  |  |  |  |
| [API-driven provisioning](../identity/app-provisioning/inbound-provisioning-api-concepts) |  | ✅ | ✅ | ✅ | ✅ |  |
| [HR-driven provisioning](../identity/app-provisioning/what-is-hr-driven-provisioning) |  | ✅ | ✅ | ✅ | ✅ |  |
| [Account Discovery](../identity/app-provisioning/how-to-account-discovery) |  |  |  | ✅ | ✅ |  |
| [Automated user provisioning to SaaS apps](../identity/saas-apps/tutorial-list) | ✅ | ✅ | ✅ | ✅ | ✅ |  |
| [Automated group provisioning to SaaS apps](../identity/saas-apps/tutorial-list) |  | ✅ | ✅ | ✅ | ✅ |  |
| [Automated provisioning to on-premises apps](../identity/app-provisioning/on-premises-application-provisioning-architecture) |  | ✅ | ✅ | ✅ | ✅ |  |
| [Cross-tenant synchronization for users (same cloud)](../identity/multi-tenant-organizations/cross-tenant-synchronization-configure?pivots=cross-cloud-synchronization) |  | ✅ | ✅ | ✅ | ✅ |  |
| [Cross-tenant synchronization for groups (same cloud)](../identity/multi-tenant-organizations/cross-tenant-synchronization-configure?pivots=cross-cloud-synchronization) |  |  |  | ✅ | ✅ |  |
| [Cross-cloud synchronization](../identity/multi-tenant-organizations/cross-tenant-synchronization-configure?pivots=cross-cloud-synchronization) |  |  |  | ✅ | ✅ |  |
| **Lifecycle Workflows (LCW)** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [Lifecycle Workflows](../id-governance/what-are-lifecycle-workflows) |  |  |  | ✅ | ✅ |  |
| [LCW + Custom Extensions (Logic Apps)](../id-governance/lifecycle-workflow-extensibility) |  |  |  | ✅ | ✅ |  |
| [LCW + Agent Sponsorship tasks](../id-governance/agent-sponsor-tasks) |  |  |  |  |  | ✅ |
| **Access reviews (AR)** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [AR - Capabilities previously generally available in Microsoft Entra ID P2](../id-governance/access-reviews-overview) |  |  | ✅ | ✅ | ✅ |  |
| [AR - PIM For Groups (Preview)](../id-governance/create-access-review-pim-for-groups) |  |  |  | ✅ | ✅ |  |
| [AR - Reviews scoped to inactive users without active users in the review](../id-governance/create-access-review#scope) |  |  |  | ✅ | ✅ |  |
| [AR - Reviews scoped to active and inactive users with review decision helpers for inactive users for the reviewer](../id-governance/review-recommendations-access-reviews#inactive-user-recommendations) |  |  | ✅ | ✅ | ✅ |  |
| [AR - Machine learning assisted access certifications and reviews](../id-governance/review-recommendations-access-reviews#user-to-group-affiliation) |  |  |  | ✅ | ✅ |  |
| [AR - Catalog Access Reviews (Preview)](../id-governance/catalog-access-reviews) |  |  |  | ✅ | ✅ |  |
| [AR - Custom data provided resource (Preview)](../id-governance/custom-data-resource-access-reviews) |  |  |  | ✅ | ✅ |  |
| **Entitlement management (EM)** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [EM - Capabilities previously generally available in Microsoft Entra ID P2](../id-governance/entitlement-management-overview) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Users assigned to access packages](../id-governance/entitlement-management-access-package-create#allow-users-service-principals-and-agent-identities-in-your-directory-to-request-the-access-package) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Agents and service principals assigned to access packages](../id-governance/entitlement-management-access-package-create#allow-users-service-principals-and-agent-identities-in-your-directory-to-request-the-access-package) |  |  |  |  |  | ✅ |
| [EM - Users request access for themselves](../id-governance/entitlement-management-overview) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Admins directly assign a user assignments(including guests)](../id-governance/entitlement-management-access-package-assignments#directly-assign-an-identity) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Admins directly assign agents and service principals](../id-governance/entitlement-management-access-package-assignments#directly-assign-any-identity) |  |  |  |  |  | ✅ |
| [EM - Admins directly assign any user - via email address for users not yet in your directory](../id-governance/entitlement-management-access-package-assignments#directly-assign-any-identity) |  |  |  | ✅ | ✅ |  |
| [EM - Managers requesting on behalf of employees](../id-governance/entitlement-management-request-behalf) |  |  |  | ✅ | ✅ |  |
| [EM - Owners and sponsors request access on behalf of their agents or service principals](../id-governance/entitlement-management-request-behalf#scenarios-for-requesting-on-behalf-of-agent-identities) |  |  |  |  |  | ✅ |
| **EM - Supported resources** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [EM - Groups and teams in access packages](../id-governance/entitlement-management-access-package-resources#add-a-group-or-team-resource-role) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Eligible group ownerships and memberships in access packages (PIM for Groups)](../id-governance/entitlement-management-access-package-eligible) |  |  |  | ✅ | ✅ |  |
| [EM - Applications in access packages](../id-governance/entitlement-management-access-package-resources#add-an-application-resource-role) |  |  | ✅ | ✅ | ✅ |  |
| [EM - SharePoint sites in access packages](../id-governance/entitlement-management-access-package-resources#add-a-sharepoint-site-resource-role) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Microsoft Entra Roles (Preview)](../id-governance/entitlement-management-roles) |  |  |  | ✅ | ✅ |  |
| [EM - SAP Identity Access Governance (IAG) business roles (Preview)](../id-governance/entitlement-management-sap-integration) |  |  |  | ✅ | ✅ |  |
| [EM - API permissions in access packages](../id-governance/entitlement-management-access-package-resources#add-an-api-permission) |  |  |  |  |  | ✅ |
| **EM - Approval options** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [EM - Multi-stage approvals with alternate approvers if no action is taken](../id-governance/entitlement-management-access-package-approval-policy) |  |  | ✅ | ✅ | ✅ | ✅ |
| [EM - Specific approvers](../id-governance/entitlement-management-access-package-approval-policy) |  |  | ✅ | ✅ | ✅ | ✅ |
| [EM - Managers as approvers](../id-governance/entitlement-management-access-package-approval-policy) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Internal sponsors as approvers (from assignees' connected organizations)](../id-governance/entitlement-management-access-package-approval-policy) |  |  | ✅ | ✅ | ✅ |  |
| [EM - External sponsors as approvers (from assignees' connected organizations)](../id-governance/entitlement-management-access-package-approval-policy) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Sponsors as approvers (from assignees' user profile)](../id-governance/entitlement-management-access-package-approval-policy) |  |  |  | ✅ | ✅ |  |
| [EM - Agent Sponsors as approvers](../id-governance/entitlement-management-access-package-approval-policy) |  |  |  |  |  | ✅ |
| [EM - Externally determine approval requirements using custom extensions](../id-governance/entitlement-management-dynamic-approval) |  |  |  | ✅ | ✅ |  |
| [EM - Collect additional requestor information for approval](../id-governance/entitlement-management-access-package-approval-policy#collect-additional-requestor-information-for-approval) |  |  | ✅ | ✅ | ✅ |  |
| **EM - Lifecycle** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [EM - Expiration of access package assignments](../id-governance/entitlement-management-access-package-lifecycle-policy) |  |  | ✅ | ✅ | ✅ | ✅ |
| [EM - Manage the lifecycle of external users](../id-governance/entitlement-management-external-users#manage-the-lifecycle-of-external-users) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Mark guest as governed](../id-governance/entitlement-management-access-package-manage-lifecycle) |  |  |  | ✅ | ✅ |  |
| **EM - Additional capabilities** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [EM - Separation of duties](../id-governance/entitlement-management-access-package-incompatible) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Custom Extensions (Logic Apps)](../id-governance/entitlement-management-logic-apps-integration) |  |  |  | ✅ | ✅ |  |
| [EM - Auto Assignment Policies](../id-governance/entitlement-management-access-package-auto-assignment-policy) |  |  |  | ✅ | ✅ |  |
| [EM - Verified ID integration](../id-governance/entitlement-management-verified-id-settings) |  |  |  | ✅ | ✅ |  |
| [EM - Microsoft Entra ID Protection integration](../id-governance/entitlement-management-configure-id-protection-approvals) |  |  |  | ✅ | ✅ |  |
| [EM - Microsoft Purview Insider Risk Management integration](../id-governance/entitlement-management-configure-insider-risk-management-approvals) |  |  |  | ✅ | ✅ |  |
| [EM - Conditional Access Scoping](../id-governance/entitlement-management-external-users#review-your-conditional-access-policies) |  |  | ✅ | ✅ | ✅ |  |
| **My Access** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [My Access portal](../id-governance/my-access-portal-overview) |  |  | ✅ | ✅ | ✅ | ✅ |
| [EM - My Access Search](../id-governance/my-access-portal-overview) |  |  | ✅ | ✅ | ✅ | ✅ |
| [EM - Suggested access packages in My Access](../id-governance/entitlement-management-suggested-access-packages) |  |  |  | ✅ | ✅ |  |
| [EM - Configure whether requestors can see approver details in My Access (Preview)](../id-governance/my-access-approver-details) |  |  |  | ✅ | ✅ |  |
| [EM - Delegate approvals in My Access (Preview)](../id-governance/my-access-portal-overview) |  |  |  | ✅ | ✅ |  |
| **Privileged Identity Management (PIM)** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [Privileged Identity Management (PIM)](../id-governance/privileged-identity-management/pim-configure) |  |  | ✅ | ✅ | ✅ |  |
| [PIM For Groups](../id-governance/privileged-identity-management/concept-pim-for-groups) |  |  | ✅ | ✅ | ✅ |  |
| [PIM Conditional Access Controls](../id-governance/privileged-identity-management/pim-how-to-change-default-settings#on-activation-require-microsoft-entra-conditional-access-authentication-context) |  |  | ✅ | ✅ | ✅ |  |
| [PIM - Custom extensions for role activation (Preview)](/en-us/entra/id-governance/privileged-identity-management/privileged-identity-management-custom-extensions) |  |  |  | ✅ | ✅ |  |
| **Other** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [Identity governance dashboard](../id-governance/governance-dashboard) |  | ✅ | ✅ | ✅ | ✅ |  |
| [Insights and reporting - Inactive guest accounts](../identity/users/clean-up-stale-guest-accounts) |  |  |  | ✅ | ✅ |  |
| [Conditional Access - Terms of use attestation](../identity/conditional-access/terms-of-use) |  | ✅ | ✅ | ✅ | ✅ |  |

### Entitlement Management

Using this feature requires a Microsoft Entra ID Governance subscription for your organization's member users. Some capabilities within this feature can operate with a Microsoft Entra ID P2 subscription. Some capabilities within this feature require guest billing.

#### Example license scenarios

Here are some example license scenarios to help you determine the number of licenses you must have.

| Scenario | Calculation | Number of licenses |
| --- | --- | --- |
| An Identity Governance Administrator at Woodgrove Bank creates initial catalogs. One of the policies specifies that **All employees** (2,000 employees) can request a specific set of access packages. 150 employees request the access packages. | 2,000 employees who **can** request the access packages | 2,000 |
| An Identity Governance Administrator at Woodgrove Bank creates initial catalogs. They create an auto-assignment policy that grants **All members of the Sales department** (350 employees) access to a specific set of access packages. 350 employees are auto-assigned to the access packages. | 350 employees need licenses. | 351 |

### Access reviews

Using this feature requires a Microsoft Entra ID Governance subscription for your organization's member users, including for all employees who are reviewing access or having their access reviewed. Some capabilities within this feature might operate with a Microsoft Entra ID P2 subscription. Some capabilities within this feature require guest billing.

#### Example license scenarios

Here are some example license scenarios to help you determine the number of licenses you must have.

| Scenario | Calculation | Number of licenses |
| --- | --- | --- |
| An administrator creates an access review of Group A with 75 member users and 1 group owner, and assigns the group owner as the reviewer. | 1 license for the group owner as reviewer, and 75 licenses for the 75 users. | 76 |
| An administrator creates an access review of Group B with 500 member users and 3 group owners, and assigns the 3 group owners as reviewers. | 500 licenses for users, and 3 licenses for each group owner as reviewers. | 503 |
| An administrator creates an access review of Group B with 500 member users. Makes it a self-review. | 500 licenses for each user as self-reviewers | 500 |
| An administrator creates an access review of Group C with 50 member users. Makes it a self-review. | 50 licenses for each user as self-reviewers. | 50 |
| An administrator creates an access review of Group D with 6 member users. Makes it a self-review. | 6 licenses for each user as self-reviewers. No additional licenses are required. | 6 |

### Lifecycle Workflows

With Microsoft Entra ID Governance licenses for Lifecycle Workflows, you can:

- Create, manage, and delete workflows up to the total limit of 50 workflows.
- Trigger on-demand and scheduled workflow execution.
- Manage and configure existing tasks to create workflows that are specific to your needs.
- Create up to 100 custom task extensions to be used in your workflows.

Using this feature requires a Microsoft Entra ID Governance subscription for your organization's member users. Some capabilities within this feature require guest billing.

#### Example license scenarios

| Scenario | Calculation | Number of licenses |
| --- | --- | --- |
| A Lifecycle Workflows Administrator creates a workflow to add new hires in the Marketing department to the Marketing teams group. 250 new hire member users are assigned to the Marketing teams group via this workflow once. Other 150 new hire member users are assigned to the Marketing teams group via this workflow later the same year. | 1 license for the Lifecycle Workflows Administrator, and 400 licenses for the users. | 401 |
| A Lifecycle Workflows Administrator creates a workflow to pre-offboard a group of employees before their last day of employment. The scope of users who will be pre-offboarded are 40 users once. We offboard 40 licensed users. Now, we can re-assign these 40 licenses and assign 10 more licenses later in the year to pre-offboard 50 more users. | 50 licenses for users, and 1 license for the Lifecycle Workflows Administrator. | 51 |

## Microsoft Entra Tenant Governance

The following tables show which Tenant Governance features are available with each license.

Note

Microsoft Entra P1 is also included in Microsoft 365 E3 and Microsoft 365 Business Premium. Microsoft Entra P2 is also included in Microsoft 365 E5. Microsoft Entra ID Governance is also included in Microsoft Entra Suite and Microsoft 365 E7.

### Configuration management

| Feature | Free | Microsoft Entra P1 | Microsoft Entra P2 | Microsoft Entra ID Governance |
| --- | --- | --- | --- | --- |
| Single tenant configuration monitoring and drift reporting |  | ✅ Up to 30 monitors and 800 configuration resources per tenant per day | ✅ Up to 30 monitors and 800 configuration resources per tenant per day | ✅ Base capacity plus 10 additional configuration resources per day for each license |
| Single tenant configuration snapshots |  | ✅ Up to 20,000 resources per tenant per month and 12 active snapshot jobs | ✅ Up to 20,000 resources per tenant per month and 12 active snapshot jobs | ✅ Base capacity plus 35 additional configuration resources per month for each license |

### Related tenants

| Feature | Free | Microsoft Entra P1 | Microsoft Entra P2 | Microsoft Entra ID Governance |
| --- | --- | --- | --- | --- |
| Discover related tenants through B2B collaboration, multitenant apps, and shared billing accounts |  |  |  | ✅ |

### Governance relationships

| Feature | Free | Microsoft Entra P1 | Microsoft Entra P2 | Microsoft Entra ID Governance |
| --- | --- | --- | --- | --- |
| Governance relationship with cross-tenant granular delegated admin privileges (GDAP) |  | ✅ | ✅ | ✅ |
| Governance relationship with custom multitenant app injection |  |  |  | ✅ |

### Secure tenant creation

| Feature | Free | Microsoft Entra P1 | Microsoft Entra P2 | Microsoft Entra ID Governance |
| --- | --- | --- | --- | --- |
| New tenant creation with governance relationship | ✅ | ✅ | ✅ | ✅ |

## Microsoft Entra Connect

Using this feature is free and included in your Azure subscription.

## Microsoft Entra Connect Health

Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/microsoft-entra-pricing).

## Microsoft Entra Conditional Access

Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

Microsoft Entra Suite includes all Microsoft Entra Conditional Access features. Microsoft 365 E7 also includes Conditional Access features through the Entra Suite.

Customers with [Microsoft 365 Business Premium licenses](/en-us/office365/servicedescriptions/office-365-service-descriptions-technet-library) also have access to Conditional Access features.

Risk-based policies require access to [Microsoft Entra ID Protection](../id-protection/overview-identity-protection), which is a Microsoft Entra ID P2 feature.

Conditional Access for agents requires a [Microsoft Agent 365 license](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing) to apply policies to agents through [Microsoft Entra Agent ID](../agent-id/what-is-microsoft-entra-agent-id#how-to-get-started). This can be with one of the following license plans: - **Microsoft 365 E7**, which includes Agent 365 and Microsoft Entra Suite, to provide governance of user and agent identities. - **Microsoft Agent 365** license paired with at least Microsoft Entra P1 or Microsoft 365 E3.

Other products and features that could interact with Conditional Access policies require appropriate licensing for those products and features.

When licenses required for Conditional Access expire, policies aren't automatically disabled or deleted. This grants customers the ability to migrate away from Conditional Access policies without a sudden change in their security posture. Remaining policies can be viewed and deleted, but no longer updated.

[Security defaults](security-defaults) help protect against identity-related attacks and are available for all customers.

## Microsoft Entra Domain Services

Microsoft Entra [Domain Services](../identity/domain-services/overview) charges accrue per hour based on the [SKU](https://azure.microsoft.com/pricing/details/microsoft-entra-ds/) the tenant owner selects.

## Microsoft External ID

Microsoft Entra [External ID](../external-id/external-identities-overview) core features are free for your first 50,000 monthly active users. More licensing information is available at the [External ID FAQ](https://aka.ms/ExternalIDPricing).

## Microsoft Entra ID Protection

Using this feature requires Microsoft Entra ID P2 licenses. To find the right license for your requirements, see [Microsoft Entra plans and pricing](https://www.microsoft.com/en-us/security/business/microsoft-entra-pricing).

Starting soon, ID Protection for agents will require a [Microsoft Agent 365 license](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing) to extend protection to agents through [Microsoft Entra Agent ID](../agent-id/what-is-microsoft-entra-agent-id#how-to-get-started).

| Capability | Details | Microsoft Entra ID Free / Microsoft 365 Apps | Microsoft Entra ID P1 | Microsoft Entra ID P2 / Microsoft Entra Suite / Microsoft 365 E7 |
| --- | --- | --- | --- | --- |
| Risk policies | Sign-in and user risk policies (via Conditional Access) | No | No | Yes |
| Security reports | Overview | No | No | Yes |
| Security reports | Risky users | Limited Information. Only users with medium and high risk are shown. No details drawer or risk history. | Limited Information. Only users with medium and high risk are shown. No details drawer or risk history. | Full access |
| Security reports | Risky sign-ins | Limited Information. No risk detail or risk level is shown. | Limited Information. No risk detail or risk level is shown. | Full access |
| Security reports | Risk detections | No | Limited Information. No details drawer. | Full access |
| Notifications | Users at risk detected alerts | No | No | Yes |
| Notifications | Weekly digest | No | No | Yes |
| MFA registration policy | Require MFA (via Conditional Access) | No | No | Yes |

## Microsoft Entra Internet Access

[Microsoft Entra Internet Access](../global-secure-access/overview-what-is-global-secure-access) is available on its own or as part of the Microsoft Entra Suite. It's also included in Microsoft 365 E7.

## Microsoft Entra monitoring and health

The required licenses vary based on the monitoring and health capability.

| Capability | Microsoft Entra ID Free | Microsoft Entra ID P1 or P2 / Microsoft Entra Suite |
| --- | --- | --- |
| Audit logs | Yes | Yes |
| Sign-in logs | Yes | Yes |
| Provisioning logs | No | Yes |
| Custom security attributes | Yes | Yes |
| Health | No | Yes |
| Microsoft Graph activity logs | No | Yes |
| Usage and insights | No | Yes |

## Microsoft Entra Private Access

[Microsoft Entra Private Access](../global-secure-access/overview-what-is-global-secure-access) is available on its own or as part of the Microsoft Entra Suite. It's also included in Microsoft 365 E7.

## Microsoft Entra Privileged Identity Management

To use Microsoft Entra Privileged Identity Management, a tenant must have a valid license. This article describes the license requirements to use Privileged Identity Management. To use Privileged Identity Management, you must have one of the following licenses:

### Valid licenses for PIM

You need either Microsoft Entra ID Governance licenses or Microsoft Entra ID P2 licenses to use PIM and all of its settings. Currently, you can scope an access review to service principals with access to Microsoft Entra ID, resource roles with a Microsoft Entra ID P2 or users with Microsoft Entra ID Governance edition active in your tenant.

### Licenses you must have for PIM

Ensure that your directory has Microsoft Entra ID P2 or Microsoft Entra ID Governance licenses for the following categories of users:

- Users with eligible and/or time-bound assignments to Microsoft Entra ID or Azure roles managed using PIM
- Users with eligible and/or time-bound assignments as members or owners of PIM for Groups
- Users able to approve or reject activation requests in PIM
- Users assigned to an access review
- Users who perform access reviews

### Example license scenarios for PIM

Here are some example license scenarios to help you determine the number of licenses you must have.

| Scenario | Calculation | Number of licenses |
| --- | --- | --- |
| Woodgrove Bank has 10 administrators for different departments and 2 [Privileged Role Administrators](/en-us/entra/identity/role-based-access-control/permissions-reference#privileged-role-administrator) that configure and manage PIM. They make five administrators eligible. | Five licenses for the administrators who are eligible | 5 |
| Graphic Design Institute has 25 administrators of which 14 are managed through PIM. Role activation requires approval and there are three different users in the organization who can approve activations. | 14 licenses for the eligible roles + three approvers | 17 |
| Contoso has 50 administrators of which 42 are managed through PIM. Role activation requires approval and there are five different users in the organization who can approve activations. Contoso also does monthly reviews of users assigned to administrator roles and reviewers are the users' managers of which six aren't in administrator roles managed by PIM. | 42 licenses for the eligible roles + five approvers + six reviewers | 53 |

### When a license expires for PIM

If a Microsoft Entra ID P2, Microsoft Entra ID Governance, or trial license expires, Privileged Identity Management features are no longer available in your directory:

- Permanent role assignments to Microsoft Entra roles are unaffected.
- The Privileged Identity Management service in the Microsoft Entra admin center, and the Graph API cmdlets and PowerShell interfaces of Privileged Identity Management, will no longer be available for users to activate privileged roles, manage privileged access, or perform access reviews of privileged roles.
- Eligible role assignments of Microsoft Entra roles are removed, as users will no longer be able to activate privileged roles.
- Any ongoing access reviews of Microsoft Entra roles ends, and Privileged Identity Management configuration settings are removed.
- Privileged Identity Management no longer sends emails on role assignment changes.

## Microsoft Entra Verified ID

Microsoft Entra Verified ID is included with any Microsoft Entra ID subscription, including Microsoft Entra ID free, at no extra cost. Core Verified ID functionality help organizations:

- Verify and issue organizational credentials for any unique identity attributes.
- Empower end-users with ownership of their digital credential and greater visibility
- Reduce organizational risk and simplify the audit process
- Create user-centric, serverless apps that use Verified ID credentials.

Microsoft Entra Verified ID also provides Face Check as a premium feature available as an add-on. Face Check is included as a full capability in the Microsoft Entra Suite.

## Microsoft Entra Workload ID

Microsoft Entra [Workload ID](../workload-id/workload-identities-overview) supports application identities and service principals in Azure, requiring licenses per workload identity per month.

## Multitenant organizations

In the source tenant: Using this feature requires Microsoft Entra ID P1 licenses. Each user who is synchronized with cross-tenant synchronization must have a P1 license in their home/source tenant. To find the right license for your requirements, see [Microsoft Entra ID Plans & Pricing](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

In the target tenant: Cross-tenant sync relies on the Microsoft Entra External ID billing model. To understand the external identities licensing model, see [MAU billing model for Microsoft Entra External ID](../external-id/external-identities-pricing). You also need at least one Microsoft Entra ID P1 license in the target tenant to enable autoredemption.

All multitenant organizations features are included as part of Microsoft Entra suite.

## Role-based access control

Using built-in roles in Microsoft Entra ID is free. Using custom roles require a Microsoft Entra ID P1 license for every user with a custom role assignment. To find the right license for your requirements, see [Comparing generally available features of the Free and Premium editions](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

### Roles

### Administrative units

Using administrative units requires a Microsoft Entra ID P1 license for each administrative unit administrator who is assigned directory roles over the scope of the administrative unit, and a Microsoft Entra ID Free license for each administrative unit member. Creating administrative units is available with a Microsoft Entra ID Free license. If you are using [rules for dynamic membership groups](../identity/users/groups-dynamic-membership) for administrative units, each administrative unit member requires a Microsoft Entra ID P1 license. To find the right license for your requirements, see [Comparing generally available features of the Free and Premium editions](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

### Restricted management administrative units

Restricted management administrative units require a Microsoft Entra ID P1 license for each administrative unit administrator, and Microsoft Entra ID Free licenses for administrative unit members. To find the right license for your requirements, see [Comparing generally available features of the Free and Premium editions](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## Features in preview

Licensing information for any features currently in preview is included here when applicable. For more information about preview features, see [Microsoft Entra ID preview features](whats-new).