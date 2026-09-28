---
layout: Conceptual
title: Microsoft Entra ID Governance licensing fundamentals - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/licensing-fundamentals
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn about Microsoft Entra ID Governance license types, prerequisites, feature requirements, trials, and licensing for employees, guests, and agents.
ms.topic: concept-article
ms.date: 2026-07-29T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1018
ai-usage: ai-assisted
locale: en-us
document_id: c48d98ed-5170-140d-59cc-344c755311cc
document_version_independent_id: 0ace47ad-ae37-5b99-0bc0-63f0d05f8ed6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/licensing-fundamentals.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/licensing-fundamentals
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/licensing-fundamentals.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b7f46b64-ee63-7e22-2d1e-cd57754f7336
---

# Microsoft Entra ID Governance licensing fundamentals - Microsoft Entra ID Governance | Microsoft Learn

This article discusses Microsoft Entra ID Governance licensing for employees. It's intended for IT decision makers, IT administrators, and IT professionals who are considering Microsoft Entra ID Governance services for their organizations.

For governance licensing for guest users, see [Microsoft Entra ID Governance licensing for guest users](microsoft-entra-id-governance-licensing-for-guest-users). For agent identity licensing requirements in preview, see [Governing agent identities (preview)](agent-id-governance-overview#license-requirements). For licensing that applies to Tenant Governance administrators and features, see [Licensing for Microsoft Entra Tenant Governance](tenant-governance/licensing).

## Types of licenses

The following licenses are available for use with Microsoft Entra ID Governance in the commercial and government clouds. The choice of licenses you need in a tenant depends on the features you're using in that tenant.

- **Free** - Included with Microsoft cloud subscriptions such as Microsoft Azure, Microsoft 365, and others.
- **Microsoft Entra ID P1** - Microsoft Entra ID P1 is available as a standalone product or included with Microsoft 365 E3 for enterprise customers and Microsoft 365 Business Premium for small to medium businesses.
- **Microsoft Entra ID P2** - Microsoft Entra ID P2 is available as a standalone product or included with Microsoft 365 E5 for enterprise customers.
- **Microsoft Entra ID Governance** - Microsoft Entra ID Governance is an advanced set of identity governance capabilities available for Microsoft Entra ID P1 and P2 customers. Microsoft Entra ID Governance is available as six products **Microsoft Entra ID Governance**, **Microsoft Entra ID Governance Step Up for Microsoft Entra ID P2**, **Entra ID Governance Frontline Worker**, **Microsoft Entra ID Governance Step up for Microsoft Entra ID F2**, **Microsoft Entra ID Governance for Government** and **Microsoft Entra ID Governance Add-on for Microsoft Entra ID P2 for Government**. These six products differ only in their prerequisites; they contain both the entitlement management, privileged identity management and access reviews capabilities that were in Microsoft Entra ID P2, and additional advanced identity governance capabilities. The following section goes into more detail on the different prerequisites of these products.
- **Microsoft Entra Suite** - Microsoft Entra Suite is a complete cloud-based solution for workforce access, available for Microsoft Entra ID P1 and P2 customers. Microsoft Entra Suite brings together **Microsoft Entra Private Access**, **Microsoft Entra Internet Access**, **Microsoft Entra ID Governance**, **Microsoft Entra ID Protection**, and **Microsoft Entra Verified ID**. The Microsoft Entra ID Governance portion provides the same identity governance capabilities as the **Microsoft Entra ID Governance** product. The difference is that they have different prerequisites.
- **Microsoft Agent 365** - Microsoft Agent 365 provides identity governance capabilities for agent identities, providing access governance for agents and service principals via Entra's Entitlement Management, additional automations via Lifecycle workflows as well as end user experiences for sponsors to manage agent identity and access lifecycle. The following section goes into more detail on the prerequisites and capabilities. For more information about Microsoft Agent 365, see: [Microsoft Agent 365](https://www.microsoft.com/licensing/faqs/122).

Note

Some Microsoft Entra ID Governance scenarios can be configured to depend upon other features that aren't covered by Microsoft Entra ID Governance. These features might have additional licensing requirements. For more information on governance scenarios using other features, see the [Identity Governance overview](identity-governance-overview) page.

The Microsoft Entra ID Governance for Government and Microsoft Entra ID Governance Add-on for Microsoft Entra ID P2 for Government products are available in the US Government community cloud (GCC), GCC-High, and Department of Defense cloud environments.

### Governance products and prerequisites

The Microsoft Entra ID Governance capabilities are currently available in six standalone products. These six products provide the same identity governance capabilities. The difference between the six products is that they have different prerequisites.

- A subscription to **Microsoft Entra ID Governance** or **Microsoft Entra ID Governance for Government**, listed in the product terms as the **Microsoft Entra ID Governance (User SL)** product, requires that the tenant also have an active subscription to another product, one that contains the `AAD_PREMIUM` or `AAD_PREMIUM_P2` service plan. Examples of products meeting this prerequisite include **Microsoft Entra ID P1**, **Microsoft 365 E3/E5/A3/A5/G3/G5** or **Enterprise Mobility + Security E3/E5**.
- A subscription to **Microsoft Entra ID Governance Step Up for Microsoft Entra ID P2** or **Microsoft Entra ID Governance Add-on for Microsoft Entra ID P2 for Government**, listed in the product terms as the **Microsoft Entra ID Governance P2** product, requires that the tenant also have an active subscription to another product, one that contains the `AAD_PREMIUM_P2` service plan. Examples of products meeting this prerequisite include **Microsoft Entra ID P2**, **Microsoft 365 E5/A5/G5**, **Enterprise Mobility + Security E5**, **Microsoft 365 E5/F5 Security** or **Microsoft 365 F5 Security + Compliance**.
- A subscription to the **Entra ID Governance Frontline Worker (User SL)** product requires that the tenant also have an active subscription to another product, one that contains the `AAD_PREMIUM` or `AAD_PREMIUM_P2` service plan. Examples of products meeting this prerequisite include **Microsoft Entra ID P1**, **Microsoft 365 E3/E5/A3/A5/G3/G5**, **Enterprise Mobility + Security E3/E5** or **Microsoft 365 F1/F3**.
- A subscription to **Microsoft Entra ID Governance Step up for Microsoft Entra ID F2**, listed in the product terms as the **Microsoft Entra ID Governance F2** or **Microsoft Entra ID Governance Step-Up for Microsoft Entra ID F2 for Frontline Worker (User SL)** product, requires that the tenant also have an active subscription to another product, one that contains the `AAD_PREMIUM_P2` service plan. Examples of products meeting this prerequisite include **Microsoft Entra ID F2**.
- A subscription to **Microsoft Agent 365** requires that the tenant also have an active subscription to another product, one that contains the `AAD_PREMIUM` service plan. Examples of products meeting this prerequisite include **Microsoft Entra ID P1** or **Microsoft 365 E3**.

Microsoft Entra ID Governance capabilities are also included in the Microsoft Entra Suite. The available Microsoft Entra Suite products include **Microsoft Entra Suite (User SL)**, **Microsoft Entra Suite Add-on for Microsoft Entra ID F2 for FLW (User SL)**, **Microsoft Entra Suite Add-on for Microsoft Entra ID P2 (User SL)**, **Microsoft Entra Suite Add-on for Microsoft Entra ID P2 EDU (User SL)**, **Microsoft Entra Suite FLW (User SL)**, and **Microsoft Entra Suite for EDU (User SL)**.

The [product names and service plan identifiers for licensing](../identity/users/licensing-service-plan-reference) lists additional products that include the prerequisite service plans.

Note

A subscription to a prerequisite for a Microsoft Entra ID Governance product must be active in the tenant. If a prerequisite isn't present, or the subscription expires, then Microsoft Entra ID Governance scenarios might not function as expected.

To check if the prerequisite products for a Microsoft Entra ID Governance product are present in a tenant, you can use the Microsoft Entra admin center or the Microsoft 365 admin center to view the list of products.

1. Sign into the [Microsoft Entra admin center](https://entra.microsoft.com) as a [License Administrator](../identity/role-based-access-control/permissions-reference#license-administrator).
2. Browse to **Billing** &gt; **Licenses**.
3. In the **Manage** menu, select **Licensed features**. The information bar indicates the current Microsoft Entra ID license plan.
4. To view the existing products in the tenant, in the **Manage** menu, select **All products**.

Governance of guest users requires an Azure subscription be selected for guest billing. For more information, see: [Microsoft Entra ID Governance licensing for guest users](microsoft-entra-id-governance-licensing-for-guest-users).

## Starting a trial

A Global Administrator in a commercial tenant that has an appropriate prerequisite product, such as Microsoft Entra ID P1, already purchased, and isn't already using or has previously trialed Microsoft Entra ID Governance, can request a trial of Microsoft Entra ID Governance in their tenant.

1. Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/AdminPortal/Home) as a [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator)
2. In the **Billing** menu, select **Purchase services**.
3. In the **Search all product categories** box, type `"Microsoft Entra ID Governance"`.
4. Select **Details** below **Microsoft Entra ID Governance** to view the trial and purchase information for the product. If your tenant has Microsoft Entra ID P2, then select **Details** below **Microsoft Entra ID Governance Step-Up for Microsoft Entra ID P2**.
5. In the product details page, select **Start free trial**.

## Microsoft Entra ID Governance features

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
| [Lifecycle Workflows](what-are-lifecycle-workflows) |  |  |  | ✅ | ✅ |  |
| [LCW + Custom Extensions (Logic Apps)](lifecycle-workflow-extensibility) |  |  |  | ✅ | ✅ |  |
| [LCW + Agent Sponsorship tasks](agent-sponsor-tasks) |  |  |  |  |  | ✅ |
| **Access reviews (AR)** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [AR - Capabilities previously generally available in Microsoft Entra ID P2](access-reviews-overview) |  |  | ✅ | ✅ | ✅ |  |
| [AR - PIM For Groups (Preview)](create-access-review-pim-for-groups) |  |  |  | ✅ | ✅ |  |
| [AR - Reviews scoped to inactive users without active users in the review](create-access-review#scope) |  |  |  | ✅ | ✅ |  |
| [AR - Reviews scoped to active and inactive users with review decision helpers for inactive users for the reviewer](review-recommendations-access-reviews#inactive-user-recommendations) |  |  | ✅ | ✅ | ✅ |  |
| [AR - Machine learning assisted access certifications and reviews](review-recommendations-access-reviews#user-to-group-affiliation) |  |  |  | ✅ | ✅ |  |
| [AR - Catalog Access Reviews (Preview)](catalog-access-reviews) |  |  |  | ✅ | ✅ |  |
| [AR - Custom data provided resource (Preview)](custom-data-resource-access-reviews) |  |  |  | ✅ | ✅ |  |
| **Entitlement management (EM)** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [EM - Capabilities previously generally available in Microsoft Entra ID P2](entitlement-management-overview) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Users assigned to access packages](entitlement-management-access-package-create#allow-users-service-principals-and-agent-identities-in-your-directory-to-request-the-access-package) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Agents and service principals assigned to access packages](entitlement-management-access-package-create#allow-users-service-principals-and-agent-identities-in-your-directory-to-request-the-access-package) |  |  |  |  |  | ✅ |
| [EM - Users request access for themselves](entitlement-management-overview) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Admins directly assign a user assignments(including guests)](entitlement-management-access-package-assignments#directly-assign-an-identity) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Admins directly assign agents and service principals](entitlement-management-access-package-assignments#directly-assign-any-identity) |  |  |  |  |  | ✅ |
| [EM - Admins directly assign any user - via email address for users not yet in your directory](entitlement-management-access-package-assignments#directly-assign-any-identity) |  |  |  | ✅ | ✅ |  |
| [EM - Managers requesting on behalf of employees](entitlement-management-request-behalf) |  |  |  | ✅ | ✅ |  |
| [EM - Owners and sponsors request access on behalf of their agents or service principals](entitlement-management-request-behalf#scenarios-for-requesting-on-behalf-of-agent-identities) |  |  |  |  |  | ✅ |
| **EM - Supported resources** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [EM - Groups and teams in access packages](entitlement-management-access-package-resources#add-a-group-or-team-resource-role) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Eligible group ownerships and memberships in access packages (PIM for Groups)](entitlement-management-access-package-eligible) |  |  |  | ✅ | ✅ |  |
| [EM - Applications in access packages](entitlement-management-access-package-resources#add-an-application-resource-role) |  |  | ✅ | ✅ | ✅ |  |
| [EM - SharePoint sites in access packages](entitlement-management-access-package-resources#add-a-sharepoint-site-resource-role) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Microsoft Entra Roles (Preview)](entitlement-management-roles) |  |  |  | ✅ | ✅ |  |
| [EM - SAP Identity Access Governance (IAG) business roles (Preview)](entitlement-management-sap-integration) |  |  |  | ✅ | ✅ |  |
| [EM - API permissions in access packages](entitlement-management-access-package-resources#add-an-api-permission) |  |  |  |  |  | ✅ |
| **EM - Approval options** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [EM - Multi-stage approvals with alternate approvers if no action is taken](entitlement-management-access-package-approval-policy) |  |  | ✅ | ✅ | ✅ | ✅ |
| [EM - Specific approvers](entitlement-management-access-package-approval-policy) |  |  | ✅ | ✅ | ✅ | ✅ |
| [EM - Managers as approvers](entitlement-management-access-package-approval-policy) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Internal sponsors as approvers (from assignees' connected organizations)](entitlement-management-access-package-approval-policy) |  |  | ✅ | ✅ | ✅ |  |
| [EM - External sponsors as approvers (from assignees' connected organizations)](entitlement-management-access-package-approval-policy) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Sponsors as approvers (from assignees' user profile)](entitlement-management-access-package-approval-policy) |  |  |  | ✅ | ✅ |  |
| [EM - Agent Sponsors as approvers](entitlement-management-access-package-approval-policy) |  |  |  |  |  | ✅ |
| [EM - Externally determine approval requirements using custom extensions](entitlement-management-dynamic-approval) |  |  |  | ✅ | ✅ |  |
| [EM - Collect additional requestor information for approval](entitlement-management-access-package-approval-policy#collect-additional-requestor-information-for-approval) |  |  | ✅ | ✅ | ✅ |  |
| **EM - Lifecycle** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [EM - Expiration of access package assignments](entitlement-management-access-package-lifecycle-policy) |  |  | ✅ | ✅ | ✅ | ✅ |
| [EM - Manage the lifecycle of external users](entitlement-management-external-users#manage-the-lifecycle-of-external-users) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Mark guest as governed](entitlement-management-access-package-manage-lifecycle) |  |  |  | ✅ | ✅ |  |
| **EM - Additional capabilities** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [EM - Separation of duties](entitlement-management-access-package-incompatible) |  |  | ✅ | ✅ | ✅ |  |
| [EM - Custom Extensions (Logic Apps)](entitlement-management-logic-apps-integration) |  |  |  | ✅ | ✅ |  |
| [EM - Auto Assignment Policies](entitlement-management-access-package-auto-assignment-policy) |  |  |  | ✅ | ✅ |  |
| [EM - Verified ID integration](entitlement-management-verified-id-settings) |  |  |  | ✅ | ✅ |  |
| [EM - Microsoft Entra ID Protection integration](entitlement-management-configure-id-protection-approvals) |  |  |  | ✅ | ✅ |  |
| [EM - Microsoft Purview Insider Risk Management integration](entitlement-management-configure-insider-risk-management-approvals) |  |  |  | ✅ | ✅ |  |
| [EM - Conditional Access Scoping](entitlement-management-external-users#review-your-conditional-access-policies) |  |  | ✅ | ✅ | ✅ |  |
| **My Access** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [My Access portal](my-access-portal-overview) |  |  | ✅ | ✅ | ✅ | ✅ |
| [EM - My Access Search](my-access-portal-overview) |  |  | ✅ | ✅ | ✅ | ✅ |
| [EM - Suggested access packages in My Access](entitlement-management-suggested-access-packages) |  |  |  | ✅ | ✅ |  |
| [EM - Configure whether requestors can see approver details in My Access (Preview)](my-access-approver-details) |  |  |  | ✅ | ✅ |  |
| [EM - Delegate approvals in My Access (Preview)](my-access-portal-overview) |  |  |  | ✅ | ✅ |  |
| **Privileged Identity Management (PIM)** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [Privileged Identity Management (PIM)](privileged-identity-management/pim-configure) |  |  | ✅ | ✅ | ✅ |  |
| [PIM For Groups](privileged-identity-management/concept-pim-for-groups) |  |  | ✅ | ✅ | ✅ |  |
| [PIM Conditional Access Controls](privileged-identity-management/pim-how-to-change-default-settings#on-activation-require-microsoft-entra-conditional-access-authentication-context) |  |  | ✅ | ✅ | ✅ |  |
| [PIM - Custom extensions for role activation (Preview)](/en-us/entra/id-governance/privileged-identity-management/privileged-identity-management-custom-extensions) |  |  |  | ✅ | ✅ |  |
| **Other** | **Free** | **Microsoft Entra ID P1** | **Microsoft Entra ID P2** | **Microsoft Entra ID Governance** | **Microsoft Entra Suite** | **Microsoft Agent 365** |
| [Identity governance dashboard](governance-dashboard) |  | ✅ | ✅ | ✅ | ✅ |  |
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

## Privileged Identity Management

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

## API-driven provisioning

This feature is available with Microsoft Entra ID P1, P2, and Microsoft Entra ID Governance subscriptions. A subscription license is required with enough seats for every identity that is sourced using the [/bulkUpload](/en-us/graph/api/synchronization-synchronizationjob-post-bulkupload) API and provisioned to either on-premises Active Directory or Microsoft Entra ID.

### License scenarios

| Customer License | Usage limits enforced at tenant level for API-driven provisioning |
| --- | --- |
| Microsoft Entra ID P1 or P2 | Daily usage quota (number of user records that can be uploaded over 24-hour period): **100K user records (2000 /bulkUpload API calls with each request containing max of 50 records)**.Max number of API-driven provisioning jobs for each flow: 2o Max 2 apps for API-driven provisioning to on-premises Active Directory.o Max 2 apps for API-driven provisioning to Microsoft Entra ID. |
| Microsoft Entra ID Governance alongside Microsoft Entra ID P1 or P2 | Daily usage quota (number of user records that can be uploaded over 24-hour period): **300K user records (6000 /bulkUpload API calls with each request containing max of 50 records)**.Max number of API-driven provisioning jobs for each flow: 20o Max 20 apps for API-driven provisioning to on-premises Active Directory.o Max 20 apps for API-driven provisioning to Microsoft Entra ID. |

## Account Discovery

Account Discovery requires the Microsoft Entra ID Governance add-on or Microsoft Entra Suite. This feature allows administrators to discover existing user accounts in target applications and identify which users have matching Entra accounts or are orphan accounts. For more information, see [Discover identities in target applications with Account Discovery](../identity/app-provisioning/how-to-account-discovery).

## Licensing FAQs

### Do licenses need to be assigned to users to use Identity Governance features?

Users don't need to be assigned a Microsoft Entra ID Governance license, but there needs to be as many licenses to include all member users in scope of, or who configures, the Identity Governance features. In addition, the guest billing model must be enabled if there are guest users to be governed, as described in the next answer.

### How can I license usage of Microsoft Entra ID Governance features for business guests?

Microsoft Entra ID Governance utilizes Monthly Active User (MAU) licensing for guest users which is different than licensing for employees and requires an Azure subscription.

Under the guest billing model, guests are identified by a *userType* of Guest regardless of where the user authenticates. A *userType* of Guest is the default userType for all B2B invitation methods and can also be set by an Identity administrator. The bill for each month includes a record for each guest user with one or more governance actions in that month. See the Azure pricing page for pricing details.

For more information, see: [Microsoft Entra ID Governance licensing for guest users](microsoft-entra-id-governance-licensing-for-guest-users).

### What happens to PIM when a license expires?

If a Microsoft Entra ID P2 or Microsoft Entra ID Governance license expires or trial ends, Privileged Identity Management features will no longer be available in your directory. The following changes listed are applicable to PIM for Microsoft Entra roles, PIM for Azure resources, and PIM for Groups.

- Active permanent assignments aren't affected.
- Active time-bound assignments become active permanent, which means they'll no longer expire at a designated time.
- Eligible role assignments are removed, as users will no longer be able to activate privileged roles.
- Privileged Identity Management blades on Microsoft Entra admin center or Azure portal, API, and PowerShell interfaces of Privileged Identity Management, will no longer be available for users to activate roles, manage assignments, or perform access reviews of privileged roles.
- Any ongoing access reviews of Microsoft Entra roles end, and Privileged Identity Management configuration settings are removed.
- Privileged Identity Management will no longer send emails on role assignment changes and PIM Alerts.

### Will any IGA features and capabilities be added under the Microsoft Entra ID P2 License?

All currently Generally Available features in Microsoft Entra ID P2 will remain, but no new Identity Governance & Administration (IGA) features or capabilities will be added to the Microsoft Entra ID P2 SKU.