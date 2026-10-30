---
layout: Conceptual
title: Microsoft Entra ID Governance licensing for guest users - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/microsoft-entra-id-governance-licensing-for-guest-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how Microsoft Entra ID is licensed for guest users.
ms.subservice: entitlement-management
ms.topic: reference
ms.date: 2026-09-23T00:00:00.0000000Z
ms.reviewer: jercon
ai-usage: ai-assisted
locale: en-us
document_id: d7a61daa-1a4e-a0f8-175a-2e7bc2ef402e
document_version_independent_id: d7a61daa-1a4e-a0f8-175a-2e7bc2ef402e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/microsoft-entra-id-governance-licensing-for-guest-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/microsoft-entra-id-governance-licensing-for-guest-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/microsoft-entra-id-governance-licensing-for-guest-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a886c88c-189a-a94a-1e5e-1ec583df511e
---

# Microsoft Entra ID Governance licensing for guest users - Microsoft Entra ID Governance | Microsoft Learn

This article outlines the pricing structure for Microsoft Entra ID Governance for guests add-on and describes how to link your tenant to an Azure subscription to ensure correct billing and feature access.

## Monthly active users (MAU) billing model

Microsoft Entra ID Governance utilizes Monthly Active User (MAU) licensing for guest users that's different than licensing for employees. See [Microsoft Entra ID Governance licensing fundamentals](/en-us/entra/id-governance/licensing-fundamentals) for complete details on licensing for employees.

Under the guest billing model, guests are identified by a userType of **Guest** regardless of where the user authenticates. A userType of **Guest** is the default userType for all B2B invitation methods and can also be set by an Identity administrator. The bill for each month includes a record for each guest user with one or more governance actions in that month. See the Azure pricing page for pricing details.

## Billable governance features

Guest users are only billed when they actively use features that are exclusive to Microsoft Entra ID Governance. Microsoft Entra P2 features are not billed, and linking an Azure subscription is not required or enforced for P2 actions. Additionally, if a guest doesn't take any active governance-related action during a month, such as in cases where access was auto-assigned in a prior month, they won't be billed for that month.

You can identify actions that will be billed to the Microsoft Entra ID Governance for guests add-on by looking at your audit logs. Specifically, each billable action has these properties included:

- TargetId: object ID of the target user
- TargetUserType: Guest
- GovernanceLicenseFeatureUsed: True

The following table contains a list of currently billable actions for **guest users**. This list might change as more features are added to Microsoft Entra ID Governance.

| Service | Action | Billable event & API | Audit Log Where TargetUserType is Guest and GovernanceLicenseFeatureUsed is True |
| --- | --- | --- | --- |
| Entitlement Management | [Request access package on-behalf-of other users](entitlement-management-request-behalf) | Bill on successful request creation. User requests or updates an access package assignment on-behalf-of another user.**API**`https://graph.microsoft.com/v1.0/identityGovernance/entitlementManagement/assignmentRequests` when the requestor (manager) is extracted from the token, and the target object is determined by the ID of the direct employee who is receiving access. | User requests access package assignment, Create access package assignment user update request, Administrator directly assigns user to access package |
| Entitlement Management | [Guest is assigned to an Microsoft Entra role assignment](entitlement-management-roles) | Bill on successful request creation when a Microsoft Entra role is included in the access package.**API**`https://graph.microsoft.com/v1.0/identityGovernance/entitlementManagement/assignmentRequests` when the access package contains a Microsoft Entra role. | User requests access package assignment, Create access package assignment user update request, Administrator directly assigns user to access package |
| Entitlement Management | [Sponsor policy is applied to assignment](entitlement-management-access-package-create) | Bill on successful request creation when a sponsor is included as an approver in the access package policy.**API**`https://graph.microsoft.com/v1.0/identityGovernance/entitlementManagement/assignmentRequests` where a sponsor is included as an approver in the access package policy. | User requests access package assignment, Create access package assignment user update request, Administrator directly assigns user to access package |
| Entitlement Management | [EM – PIM for groups](create-access-review-pim-for-groups) | Bill on successful request creation when a PIM group is included in the access package.**API**`https://graph.microsoft.com/v1.0/identityGovernance/entitlementManagement/assignmentRequests` when the access package contains a PIM group. | User requests access package assignment, Create access package assignment user update request, Administrator directly assigns user to access package |
| Entitlement Management | [Guest uses verified ID for request](entitlement-management-verified-id-settings) | Bill on successful request creation when verified ID is required in the policy.**API**`https://graph.microsoft.com/v1.0/identityGovernance/entitlementManagement/assignmentRequests` when the access package policy requires a Verified ID. | User requests access package assignment, Create access package assignment user update request, Administrator directly assigns user to access package |
| Entitlement Management | [Guest policy assigned with custom extension](entitlement-management-logic-apps-integration) | Bill on successful request creation when a custom extension is included in the assignment policy.**API**`https://graph.microsoft.com/v1.0/identityGovernance/entitlementManagement/assignmentRequests` when a custom extension is included in the assignment policy. | User requests access package assignment, Create access package assignment user update request, Administrator directly assigns user to access package |
| Entitlement Management | [Guest is granted an auto-assignment policy](entitlement-management-access-package-auto-assignment-policy) | Bill on successful request creation with an auto-assignment policy. | Entitlement Management creates access package assignment request for user. |
| Entitlement Management | [Directly assign any identity](entitlement-management-access-package-assignments#directly-assign-an-identity) | Bill on successful request creation when using directly assigning an access package to a user not yet in the directory.**API**`https://graph.microsoft.com/v1.0/identityGovernance/entitlementManagement/assignmentRequests` when using requestType "*AdminAdd*" for a user who doesn’t exist in the directory. | Entitlement Management invites external user. |
| Entitlement Management | [Mark guest as governed](entitlement-management-access-package-manage-lifecycle) | Bill on conversion to governed user.**API**`https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/subjects` where *"subjectLifecycle"* is set to "governed". | Update access package user lifecycle. |
| Lifecycle Workflows | [Workflow is run for guest](what-are-lifecycle-workflows) | Bill on workflow execution.**API**`https://graph.microsoft.com/v1.0/identityGovernance/lifecycleWorkflows/workflows/{workflowId}/activate` | Workflow execution started for user. |
| Lifecycle Workflows | Guest is disabled by a Guest Lifecycle Policy | N/A | Guest user disabled by lifecycle policy |
| Lifecycle Workflows | Guest is deleted by a Guest Lifecycle Policy | N/A | Guest user deleted by lifecycle policy |
| Lifecycle Workflows | Sponsor attests to a guest user (extends sponsorship) | POST /beta/users/{guestUserId}/microsoft.graph.identityGovernance.attest | Attest guest user |
| Lifecycle Workflows | User sponsors a new guest user | POST /beta/users/{guestUserId}/microsoft.graph.identityGovernance.addSelfAsSponsor | Sponsor guest user |
| Access Reviews | [Access Review – machine learning assisted access reviews](review-recommendations-access-reviews#user-to-group-affiliation) | Bill when guest user is included in review. **API**`https://graph.microsoft.com/v1.0/identityGovernance/accessReviews/definitions` where recommendation settings are enabled in a group review. | Decision item summary. |
| Access Reviews | [Access Review – inactive users](../identity/users/clean-up-stale-guest-accounts#monitor-guest-accounts-at-scale-with-inactive-guest-insights) | Bill when guest user is included in review.**API**`https://graph.microsoft.com/v1.0/identityGovernance/accessReviews/definitions` where inactive guest reviews are included in the policy for a group resource. | Decision item summary. |
| Access Reviews | [Access Review – Catalog Access Reviews](catalog-access-reviews) | Bill when guest user is included in review.**API**`https://graph.microsoft.com/v1.0/identityGovernance/accessReviews/unified/definitions/` | Decision item summary. |

## Guest billing in multitenant organizations

Governance guest billing only applies for users with a userType of **guest**, so if Microsoft Entra ID Governance licensed member users are brought into other organization tenants with a userType of **member**, they won't accrue to the billing meter.

If these users are brought in with a userType of **guest** they accrue to the meter, however you can avoid being charged by setting up or joining a multitenant organization. If the guest user is from a participating organizational tenant, the guest won't accrue to the billing meter. See [Set up a multitenant org in Microsoft 365](/en-us/microsoft-365/enterprise/set-up-multi-tenant-org?view=o365-worldwide&amp;preserve-view=true).

## Billing examples

### Scenario 1: Automating access package assignments

**March**: 

- Contoso creates an autoassignment policy that assigns an access package to 500 guest users.
- Contoso IT runs the guest conversion API for another set of 500 guest users.
- Billing: For March, Contoso is billed for 1,000 total guest users: 500 users for the autoassignment policy and 500 users for the guest conversion API.

**April**: 

- The 500 guest users who were auto-assigned an access package in March retain their assignments but aren't billed since there wasn't an explicit action taken on these users in April.
- Additionally, Contoso IT runs an inactive access review on 100 guests.
- Billing: For April, Contoso is billed for 100 users for the inactive access review.

### Scenario 2: Lifecycle workflow and access review for inactive users

**March**:

- Fabrikam executes a lifecycle workflow for 300 guest users.
- They also perform an access review for inactive users, targeting 100 of the same guests as before, plus a different set of 200 guests.
- Billing: For March, Fabrikam is billed for 300 users for the lifecycle workflow and 200 users for the inactive access review. Since 100 of the guest users already incurred a charge for the lifecycle workflow, they didn't incur any additional charge for the inactive user review, since each guest user will only be charged once for one or more governance actions in the month.

**April**:

- From the second group of 200 guest users in March, all 200 guests receive an auto-assigned access package that grants access to an app and have the same inactive user access review that was run in March, repeated in April.
- Billing: For April, Fabrikam is billed for 200 users. Although these users had both an inactive access review and an access‑package auto‑assignment in April, each guest is charged only once for the month.

### Scenario 3: Access Reviews for inactive users and user-to-group affiliation

**May**:

- Tailspin Toys creates an inactive guest access review for 200 users.
- Tailspin creates a second access review for a security group with a different set of 300 guest users with the user-to-group affiliation feature enabled.
- Billing: For May, Tailspin is billed for 500 users – 200 for the inactive guest access review and 300 for the review with user-to-group affiliation.

**June**:

- Contoso has 10,000 guest accounts in their tenant and they want to perform an access review on those guests who are inactive.
- Contoso creates an Access Review scoped to Guests only and to Inactive Users only. The Access Review scans all 10,000 guest users and identifies 240 that are considered inactive. The campaign includes those 240 guest users only.
- There are no other governance-related events that take place on any of the 10,000 guest users.
- Billing: For June, Contoso is billed for 240 users – only those inactive guests who had an Access Review performed on them.

### Link your tenant to a subscription

Your tenants must be linked to an Azure subscription for proper billing and access to features. To link your tenant to a subscription, follow these steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) with an account that has at least the Owner role within the subscription or a resource group within the subscription.
2. Select the directory you want to link: In the Microsoft Entra admin center toolbar, select the **Settings** icon in the portal toolbar. Then on the **Portal settings | Directories + subscriptions** page, find your workforce tenant in the **Directory name** list, and then select **Switch**.
3. Browse to **Entra ID** &gt; **ID Governance** &gt; **Dashboard**.
4. On the governance dashboard, locate the guest governance panel and select **Get Started**.
5. In the **Link a subscription** pane, select a **Subscription** and a **Resource group**. Then select **Turn on**.

After you complete these steps, your Azure subscription is billed based on your Azure Direct or Enterprise Agreement details, if applicable.

## What if I can't find a subscription?

If no subscriptions are available in the **Link a subscription** pane, here are some possible reasons:

- You don't have the appropriate permissions. Be sure to sign in with an Azure account that has at least the Owner role within the subscription or a resource group within the subscription.
- A subscription exists, but it isn't associated with your directory yet. You can [associate an existing subscription to your tenant](../fundamentals/how-subscriptions-associated-directory) and then repeat the steps for [linking it to your tenant](../external-id/external-identities-pricing#link-your-azure-ad-tenant-to-a-subscription).
- No subscription exists. In the **Link a subscription** pane, you can create a subscription by selecting **if you don't already have a subscription you may create one here**. After you create a new subscription, you'll need to [create a resource group](/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal) in the new subscription, and then repeat the steps for [linking it to your tenant](../external-id/external-identities-pricing#link-your-azure-ad-tenant-to-a-subscription).

## Turn off guest billing

You can turn off governance guest billing by returning to the governance dashboard and selecting **Edit** on the guest governance panel. In the Edit Guest Access panel, select "Turn Off" to disable billing and Microsoft Entra ID Governance features for your guest users.

## Guest user licensing FAQs

**Do I need to have a subscription to Microsoft Entra ID Governance or Microsoft Entra Suite if I only want to govern guests?**

Yes. While you don’t need a subscription for your guest users, you need to have at least one Microsoft Entra ID Governance or Microsoft Entra Suite license for an administrator in the tenant.

**I have been using access reviews and entitlement management features included in Microsoft Entra P2 for my guest users. Will I start getting billed for this usage?**

Governance features included with Microsoft Entra P2 including basic access reviews and entitlement management capabilities won't be billed to the governance guest add-on. Only governance features that are exclusive to Microsoft Entra Suite or standalone Microsoft Entra ID Governance will be billed to the meter. See the billable tables action on this page for details.

**Does Governance guest billing apply to all guest users, including those within the first 50,000 Monthly Active Users (MAU)?**

Yes, there's no free tier for governance billing. Governance guest billing applies to all guest users, even those within the first 50,000 MAU.

**How can I estimate or understand my guest usage for Microsoft Entra ID Governance billing?**

You can use the EIG Guest Usage Monitoring Workbook to understand the guest usage trend within your tenant. This report shows past usage that would have been billed, but future usage may differ. To provide feedback about the EIG Guest Usage Monitoring Workbook, visit this [form](https://forms.office.com/r/N4dYnQcXTN).

## Guest Governance Features Unavailable Without the Microsoft Entra ID Governance for Guests Add-on

To use Microsoft Entra ID Governance features for guest users, your tenant must be linked to an Azure subscription with the Microsoft Entra ID Governance for guests add-on. If the guest billing meter isn't enabled, the following behavior applies:

Note

Connecting the Microsoft Entra ID Governance for Guests Add-on will be enforced beginning in January 2026. This list might change as more features are added to Microsoft Entra ID Governance.

### Access Reviews

- You won't be able to create new access reviews scoped to guest users if any of the following features are selected:
    - Inactive user access review
    - User-to-group affiliation recommendation helper

### Entitlement Management

- You won't be able to create policies with guests in scope (“*For all users in your directory including guests*” or “*For users not in your directory*”) and the Microsoft Entra ID Governance features listed in this documentation (For example, sponsor approvers, custom extensions, and Verified ID).
- You won't be able to create new auto-assignment policies where a configured rule includes `userType=Guest`
- You won't be able to update existing entitlement management policies that add these features.
- You won't be able to perform these operations:
    - Mark guest as governed
    - Directly assign any guest user

### Lifecycle Workflows

- You won't be able to create new workflows if the workflow scope includes guest users:
    - The configured rule includes `userType=Guest`
- You won't be able to update existing workflows where the execution conditions include a scope with `userType=Guest`.