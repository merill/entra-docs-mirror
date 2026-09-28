---
layout: Conceptual
title: Plan a Privileged Identity Management deployment - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-deployment-plan
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to deploy Privileged Identity Management (PIM) in your Microsoft Entra organization.
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: pim, sfi-ga-nochange
locale: en-us
document_id: 66c20f5e-ca50-337e-8fc1-1d3d434178a7
document_version_independent_id: 4f7c30ee-a49c-a79e-e06d-2c788ae91e39
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-deployment-plan.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-deployment-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-deployment-plan.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: d8b56b22-6206-baa7-29fe-70bcbaefe5f3
---

# Plan a Privileged Identity Management deployment - Microsoft Entra ID Governance | Microsoft Learn

## Overview

**Privileged Identity Management (PIM)** provides a time-based and approval-based role activation to mitigate the risks of excessive, unnecessary, or misused access permissions to important resources. These resources include resources in Microsoft Entra ID, Azure, and other Microsoft Online Services such as Microsoft 365 or Microsoft Intune.

PIM enables you to allow a specific set of actions at a particular scope. Key features include:

- Provide **just-in-time** privileged access to resources
- Assign **eligibility for membership or ownership** of PIM for Groups
- Assign **time-bound** access to resources using start and end dates
- Require **approval** to activate privileged roles
- Enforce **Multifactor authentication** to activate any role
- Enforce **Conditional Access policies** to activate any role (Public preview)
- Use **justification** to understand why users activate
- Get **notifications** when privileged roles are activated
- Conduct **access reviews** to ensure users still need roles
- Download **audit history** for internal or external audit

To gain the most from this deployment plan, it’s important that you get a complete overview of [What is Privileged Identity Management](pim-configure).

## Understand PIM

The PIM concepts in this section help you understand your organization’s privileged identity requirements.

### What can you manage in PIM

Today, you can use PIM with:

- **Microsoft Entra roles** – Sometimes referred to as directory roles, Microsoft Entra roles include built-in, and custom roles to manage Microsoft Entra ID and other Microsoft 365 online services.
- **Azure roles** – The role-based access control (RBAC) roles in Azure that grant access to management groups, subscriptions, resource groups, and resources.
- **PIM for Groups** – To set up just-in-time access to member and owner role of a Microsoft Entra security group. PIM for Groups not only gives you an alternative way to set up PIM for Microsoft Entra roles and Azure roles, but also allows you to set up PIM for other permissions across Microsoft online services like Intune, Azure Key Vaults, and Azure Information Protection. If the group is configured for app provisioning, activation of group membership triggers provisioning of group membership (and the user account, if it wasn’t provisioned) to the application using the System for Cross-Domain Identity Management (SCIM) protocol.

You can assign the following to these roles or groups:

- **Users**- To get just-in-time access to Microsoft Entra roles, Azure roles, and PIM for Groups.
- **Groups**- Anyone in a group to get just-in-time access to Microsoft Entra roles and Azure roles. For Microsoft Entra roles, the group must be a newly created cloud group that’s marked as assignable to a role while for Azure roles, the group can be any Microsoft Entra security group. Assigning or nesting a group to a PIM for Groups isn't recommended.

Note

You can't assign service principals as eligible to Microsoft Entra roles, Azure roles, and PIM for Groups but you can grant a time-limited active assignment to all three.

### Principle of least privilege

You assign users the role with the [least privileges necessary to perform their tasks](../../identity/role-based-access-control/delegate-by-task). This practice minimizes the number of Global Administrators and instead uses specific administrator roles for certain scenarios.

Note

Microsoft has few Global Administrators. Learn more at [how Microsoft uses Privileged Identity Management](https://www.microsoft.com/insidetrack/blog/improving-security-by-protecting-elevated-privilege-accounts-at-microsoft/).

### Type of assignments

There are two types of assignment – **eligible** and **active**. If a user is eligible for a role, they can activate the role when they need to perform privileged tasks.

You can also set a start and end time for each type of assignment. This addition gives you four possible types of assignments:

- Permanent eligible
- Permanent active
- Time-bound eligible, with specified start and end dates for assignment
- Time-bound active, with specified start and end dates for assignment

In case the role expires, you can **extend** or **renew** these assignments.

Keep zero permanently active assignments for roles other than your [emergency access accounts](../../identity/role-based-access-control/security-emergency-access).

Microsoft recommends that organizations have two cloud-only emergency access accounts permanently assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role. These accounts are highly privileged and aren't assigned to specific individuals. The accounts are limited to emergency or "break glass" scenarios where normal accounts can't be used or all other administrators are accidentally locked out. These accounts should be created following the [emergency access account recommendations](/en-us/entra/identity/role-based-access-control/security-emergency-access).

## Plan the project

When technology projects fail, it’s typically because of mismatched expectations on impact, outcomes, and responsibilities. To avoid these pitfalls, [ensure that you’re engaging the right stakeholders](../../architecture/deployment-plans) and that stakeholder roles in the project are well understood.

### Plan a pilot

At each stage of your deployment ensure that you're evaluating that the results are as expected. See [best practices for a pilot](../../architecture/deployment-plans#best-practices-for-a-pilot).

- Start with a small set of users (pilot group) and verify that PIM behaves as expected.
- Verify whether all the configuration you set up for the roles or PIM for Groups are working correctly.
- Roll it to production only after it’s thoroughly tested.

### Plan communications

Communication is critical to the success of any new service. Proactively communicate with your users how their experience changes, when it changes, and how to gain support if they experience issues.

Set up time with your internal IT support to walk them through the PIM workflow. Provide them with the appropriate documentation and your contact information.

## Plan testing and rollback

Note

For Microsoft Entra roles, organizations often test and roll out Global Administrators first, while for Azure resources, they usually test PIM one Azure subscription at a time.

### Plan testing

Create test users to verify PIM settings work as expected before you impact real users and potentially disrupt their access to apps and resources. Build a test plan to have a comparison between the expected results and the actual results.

The following table shows an example test case:

| Role | Expected behavior during activation | Actual results |
| --- | --- | --- |
| Global Administrator | - Require MFA<br>- Require approval<br>- Require Conditional Access context (Public preview)<br>- Approver receives notification and can approve<br>- Role expires after preset time |  |

For both Microsoft Entra ID and Azure resource role, make sure that you have users represented who will take those roles. In addition, consider the following roles when you test PIM in your staged environment:

| Roles | Microsoft Entra roles | Azure Resource roles | PIM for Groups |
| --- | --- | --- | --- |
| Member of a group |  |  | x |
| Members of a role | x | x |  |
| IT service owner | x |  | x |
| Subscription or resource owner |  | x | x |
| PIM for Groups owner |  |  | x |

### Plan rollback

If PIM fails to work as desired in the production environment, you can change the role assignment from eligible to active once again. For each role that you’ve configured, select the ellipsis **(…)** for all users with assignment type as **eligible**. You can then select the **Make active** option to go back and make the role assignment **active**.

## Plan and implement PIM for Microsoft Entra roles

Follow these tasks to prepare PIM to manage Microsoft Entra roles.

### Discover and mitigate privileged roles

List who has privileged roles in your organization. Review the users assigned, identify administrators who no longer need the role, and remove them from their assignments.

You can use [Microsoft Entra roles access reviews](pim-create-roles-and-resource-roles-review) to automate the discovery, review, and approval or removal of assignments.

### Determine roles to be managed by PIM

Prioritize protecting Microsoft Entra roles that have the most permissions. It’s also important to consider what data and permission are most sensitive for your organization.

First, ensure that all Global Administrator and Security Administrator roles are managed using PIM because they’re the users who can do the most harm when compromised. Then consider more roles that should be managed that could be vulnerable to attack.

You can use the Privileged label to identify roles with high privileges that you can manage with PIM. Privileged label is present on [**Roles and Administrator**](../../identity/role-based-access-control/privileged-roles-permissions?tabs=admin-center) in Microsoft Entra admin center. See the article, [Microsoft Entra built-in roles](../../identity/role-based-access-control/permissions-reference) to learn more.

### Configure PIM settings for Microsoft Entra roles

[Draft and configure your PIM settings](pim-how-to-change-default-settings) for every privileged Microsoft Entra role that your organization uses.

The following table shows example settings:

| Role | Require MFA | Require Conditional Access | Notification | Incident ticket | Require approval | Approver | Activation duration | Perm admin |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Global Administrator | ✔️ | ✔️ | ✔️ | ✔️ | ✔️ | Other Global Administrator | One Hour | Emergency access accounts |
| Exchange Admin | ✔️ | ✔️ | ✔️ | ❌ | ❌ | None | Two Hours | None |
| Helpdesk Admin | ❌ | ❌ | ❌ | ✔️ | ❌ | None | Eight Hours | None |

### Assign and activate Microsoft Entra roles

For Microsoft Entra roles in PIM, only a user who is in the Privileged Role Administrator or Global Administrator role can manage assignments for other administrators. Global Administrators, Security Administrators, Global Readers, and Security Readers can also view assignments to Microsoft Entra roles in PIM.

Follow the instructions in each of the following steps:

1. [Give eligible assignments](pim-how-to-add-role-to-user).
2. [Allow eligible users to activate their Microsoft Entra role just-in-time](pim-how-to-activate-role).

When role nears its expiration, use [PIM to extend or renew the roles](pim-resource-roles-renew-extend). Both user-initiated actions require an approval from a Global Administrator or Privileged Role Administrator.

When these important events occur in Microsoft Entra roles, PIM [sends email notifications and weekly digest emails](pim-email-notifications) to privilege administrators depending on the role, event, and notification settings. These emails might also include links to relevant tasks, such as activating or renewing a role.

Note

You can also perform these PIM tasks [using the Microsoft Graph APIs for Microsoft Entra roles](pim-apis).

### Approve or deny PIM activation requests

A delegated approver receives an email notification when a request is pending for approval. Follow these steps to [approve or deny requests to activate an Azure resource role](pim-resource-roles-approval-workflow).

### View audit history for Microsoft Entra roles

[View audit history for all role assignments and activations](pim-how-to-use-audit-log) within past 30 days for Microsoft Entra roles. You can access the audit logs if you're a Global Administrator or a Privileged Role Administrator.

Have at least one administrator read through all audit events on a weekly basis and export your audit events on a monthly basis.

### Security alerts for Microsoft Entra roles

[Configure security alerts for Microsoft Entra roles](pim-how-to-configure-security-alerts) to trigger an alert in the event of suspicious and unsafe activity.

## Plan and implement PIM for Azure Resource roles

Follow these tasks to prepare PIM to manage Azure resource roles.

### Discover and mitigate privileged roles

Minimize Owner and User Access Administrator assignments attached to each subscription or resource and remove unnecessary assignments.

As a Global Administrator you can [elevate access to manage all Azure subscriptions](/en-us/azure/role-based-access-control/elevate-access-global-admin). You can then find each subscription owner and work with them to remove unnecessary assignments within their subscriptions.

Use [access reviews for Azure resources](pim-create-roles-and-resource-roles-review) to audit and remove unnecessary role assignments.

### Determine roles to be managed by PIM

When deciding which role assignments should be managed using PIM for Azure resource, you must first identify the [management groups](/en-us/azure/governance/management-groups/overview), subscriptions, resource groups, and resources that are most vital for your organization. Consider using management groups to organize all their resources within their organization.

Manage all Subscription Owner and User Access Administrator roles using PIM.

Work with Subscription owners to document resources managed by each subscription and classify the risk level of each resource if compromised. Prioritize managing resources with PIM based on risk level. This also includes custom resources attached to the subscription.

Work with Subscription or Resource owners of critical services to set up PIM workflow for all the roles inside sensitive subscriptions or resources.

For subscriptions or resources that aren’t as critical, you won’t need to set up PIM for all roles. However, you should still protect the Owner and User Access Administrator roles with PIM.

### Configure PIM settings for Azure Resource roles

[Draft and configure settings](pim-resource-roles-configure-role-settings) for the Azure Resource roles that you’ve planned to protect with PIM.

The following table shows example settings:

| Role | Require MFA | Notification | Require Conditional Access | Require approval | Approver | Activation duration | Active admin | Active expiration | Eligible expiration |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Owner of critical subscriptions | ✔️ | ✔️ | ✔️ | ✔️ | Other owners of the subscription | One Hour | None | n/a | Three months |
| User Access Administrator of less critical subscriptions | ✔️ | ✔️ | ✔️ | ❌ | None | One Hour | None | n/a | Three months |

### Assign and activate Azure Resource role

For Azure resource roles in PIM, only an owner or User Access Administrator can manage assignments for other administrators. Users who are Privileged Role Administrators, Security Administrators, or Security Readers don't by default have access to view assignments to Azure resource roles.

Follow the instructions in the links below:

1. [Give eligible assignments](pim-resource-roles-assign-roles).
2. [Allow eligible users to activate their Azure roles just-in-time](pim-resource-roles-activate-your-roles).

When privileged role assignment nears its expiration, [use PIM to extend or renew the roles](pim-resource-roles-renew-extend). Both user-initiated actions require an approval from the resource owner or User Access Administrator.

When these important events occur in Azure resource roles, PIM sends [email notifications](pim-email-notifications) to Owners and Users Access Administrators. These emails might also include links to relevant tasks, such as activating or renewing a role.

Note

You can also perform these PIM tasks [using the Microsoft Azure Resource Manager APIs for Azure resource roles](pim-apis).

### Approve or deny PIM activation requests

[Approve or deny activation requests for Microsoft Entra role](pim-approval-workflow)- A delegated approver receives an email notification when a request is pending for approval.

### View audit history for Azure Resource roles

[View audit history for all assignments and activations](azure-pim-resource-rbac) within past 30 days for Azure resource roles.

### Security alerts for Azure Resource roles

[Configure security alerts for the Azure resource roles](pim-resource-roles-configure-alerts) that triggers an alert when there's suspicious and unsafe activity.

## Plan and implement PIM for PIM for Groups

Follow these tasks to prepare PIM to manage PIM for Groups.

### Discover PIM for Groups

Someone could have five or six eligible assignments to Microsoft Entra roles through PIM. They have to activate each role individually, which can reduce productivity. Worse still, they can also have tens or hundreds of Azure resources assigned to them, which aggravates the problem.

In this case, you should use PIM for Groups. Create a PIM for Groups and grant it permanent active access to multiple roles. See [Privileged Identity Management (PIM) for Groups (preview)](concept-pim-for-groups).

To manage a Microsoft Entra role-assignable group as a PIM for Groups, you must [bring it under management in PIM](groups-discover-groups).

### Configure PIM settings for PIM for Groups

[Draft and configure settings](groups-role-settings) for the PIM for Groups that you plan to protect with PIM.

The following table shows example settings:

| Role | Require MFA | Notification | Require Conditional Access | Require approval | Approver | Activation duration | Active admin | Active expiration | Eligible expiration |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Owner | ✔️ | ✔️ | ✔️ | ✔️ | Other owners of the resource | One Hour | None | n/a | Three months |
| Member | ✔️ | ✔️ | ✔️ | ❌ | None | Five Hours | None | n/a | Three months |

### Assign eligibility for PIM for Groups

You can [assign eligibility to members or owners of PIM for Groups.](groups-assign-member-owner) With just one activation, they have access to all linked resources.

Note

You can assign the group to one or more Microsoft Entra ID and Azure resource roles in the same way as you assign roles to users. A maximum of 500 role-assignable groups can be created in a single Microsoft Entra organization (tenant).

![Diagram of assign eligibility for PIM for Groups.](media/pim-deployment-plan/pim-for-groups.png)

When group assignment nears its expiration, use [PIM to extend or renew the group assignment](groups-renew-extend). This operation requires group owner approval.

### Approve or deny PIM activation request

Configure PIM for Groups members and owners to require approval for activation and choose users or groups from your Microsoft Entra organization as delegated approvers. We recommend selecting two or more approvers for each group to reduce workload for the Privileged Role Administrator.

[Approve or deny role activation requests for PIM for Groups](groups-approval-workflow). Delegated approvers receive email notifications when a request is awaiting approval.

### View audit history for PIM for Groups

[View audit history for all assignments and activations](groups-audit) within past 30 days for PIM for Groups.