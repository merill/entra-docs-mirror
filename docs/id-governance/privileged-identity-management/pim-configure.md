---
layout: Conceptual
title: What is Privileged Identity Management? - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-configure
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Provides an overview of Microsoft Entra Privileged Identity Management (PIM).
ms.topic: overview
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: ilyal
ms.custom: pim, azuread-video-2020, content-engagement, sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: d7338196-8434-f76e-ec0d-15bc85d51434
document_version_independent_id: c7003b7a-91f8-3727-0f3e-93f52f5809fa
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-configure.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7df81cdf-9920-f097-f254-8ad149a1df54
---

# What is Privileged Identity Management? - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Privileged Identity Management (PIM) is a service in Microsoft Entra ID that enables you to manage, control, and monitor access to important resources in your organization. These resources include resources in Microsoft Entra ID, Azure, and other Microsoft Online Services such as Microsoft 365 or Microsoft Intune. The following video explains important PIM concepts and features. 

## Reasons to use

Organizations want to minimize the number of people who have access to secure information or resources, because that reduces the chance of

- a malicious actor getting access
- an authorized user inadvertently impacting a sensitive resource

However, users still need to carry out privileged operations in Microsoft Entra ID, Azure, Microsoft 365, or SaaS apps. Organizations can give users just-in-time privileged access to Azure and Microsoft Entra resources and can oversee what those users are doing with their privileged access.

## License requirements

Using Privileged Identity Management requires licenses. For more information on licensing, see [Microsoft Entra ID Governance licensing fundamentals](../licensing-fundamentals) .

## What does it do?

Privileged Identity Management provides time-based and approval-based role activation to mitigate the risks of excessive, unnecessary, or misused access permissions on resources that you care about. Here are some of the key features of Privileged Identity Management:

- Provide **just-in-time** privileged access to Microsoft Entra ID and Azure resources
- Assign **time-bound** access to resources using start and end dates
- Require **approval** to activate privileged roles
- Enforce **multifactor authentication** to activate any role
- Use **justification** to understand why users activate
- Get **notifications** when privileged roles are activated
- Conduct **access reviews** to ensure users still need roles
- Download **audit history** for internal or external audit
- Prevent removal of the **last active Global Administrator** and **Privileged Role Administrator** role assignments

## What can I do with it?

Once you set up Privileged Identity Management, you'll see **Tasks**, **Manage**, and **Activity** options in the left navigation menu. As an administrator, you can choose between options such as managing **Microsoft Entra roles**, managing **Azure resource** roles, or PIM for Groups. When you choose what you want to manage, you see the appropriate set of options for that option.

![Screenshot of Privileged Identity Management in the Azure portal.](media/pim-configure/pim-quickstart.png)

## Who can do what?

For Microsoft Entra roles in Privileged Identity Management, only a user who is in the Privileged Role Administrator or Global Administrator role can manage assignments for other administrators. Global Administrators, Security Administrators, Global Readers, and Security Readers can also view assignments to Microsoft Entra roles in Privileged Identity Management.

For Azure resource roles in Privileged Identity Management, only a subscription administrator, a resource Owner, or a resource User Access Administrator can manage assignments for other administrators. Users who are Privileged Role Administrators, Security Administrators, or Security Readers don't by default have access to view assignments to Azure resource roles in Privileged Identity Management.

## Terminology

To better understand Privileged Identity Management and its documentation, you should review the following terms.

| Term or concept | Role assignment category | Description |
| --- | --- | --- |
| eligible | Type | A role assignment that requires a user to perform one or more actions to use the role. If a user is eligible for a role, they can activate the role when they need to perform privileged tasks. There's no difference in the access given to someone with a permanent versus an eligible role assignment. The only difference is that some people don't need that access all the time. |
| active | Type | A role assignment that doesn't require a user to perform any action to use the role. Users assigned as active have the privileges assigned to the role. |
| activate |  | The process of performing one or more actions to use a role that a user is eligible for. Actions might include performing a multifactor authentication (MFA) check, providing a business justification, or requesting approval from designated approvers. |
| assigned | State | A user that has an active role assignment. |
| activated | State | A user that has an eligible role assignment, performed the actions to activate the role, and is now active. Once activated, the user can use the role for a preconfigured period of time before they need to activate again. |
| permanent eligible | Duration | A role assignment where a user is always eligible to activate the role. |
| permanent active | Duration | A role assignment where a user can always use the role without performing any actions. |
| time-bound eligible | Duration | A role assignment where a user is eligible to activate the role only within start and end dates. |
| time-bound active | Duration | A role assignment where a user can use the role only within start and end dates. |
| just-in-time (JIT) access |  | A model in which users receive temporary permissions to perform privileged tasks, which prevents malicious or unauthorized users from gaining access after the permissions expire. Access is granted only when users need it. |
| principle of least privilege access |  | A recommended security practice in which every user is provided with only the minimum privileges needed to accomplish the tasks they're authorized to perform. This practice minimizes the number of Global Administrators and instead uses specific administrator roles for certain scenarios. |

## Role assignment overview

The PIM role assignments give you a secure way to grant access to resources in your organization. This section describes the assignment process. It includes assigning roles to members, activating assignments, approving or denying requests, and extending and renewing assignments.

PIM keeps you informed by sending you and other participants [email notifications](pim-email-notifications). These emails might also include links to relevant tasks, such as activating, approving, or denying a request.

The following screenshot shows an email message sent by PIM. The email informs Patti that Alex updated a role assignment for Emily.

![Screenshot shows an email message sent by Privileged Identity Management.](media/pim-configure/pim-email.png)

### Assign

The assignment process starts by assigning roles to members. To grant access to a resource, the administrator assigns roles to users, groups, service principals, or managed identities. The assignment includes the following data:

- The members or owners to assign the role.
- The scope of the assignment. The scope limits the assigned role to a particular set of resources.
- The type of the assignment.
    - **Eligible** assignments require the member of the role to perform an action to use the role. Actions might include activation, or requesting approval from designated approvers.
    - **Active** assignments don't require the member to perform any action to use the role. Members assigned as active have the privileges assigned to the role.
- The duration of the assignment, using start and end dates or permanent. For eligible assignments, the members can activate or request approval during the start and end dates. For active assignments, the members can use the assigned role during this period of time.

The following screenshot shows how administrator assigns a role to members.

![Screenshot of Privileged Identity Management role assignment.](media/pim-configure/role-assignment.png)

For more information, check out the following articles: [Assign Microsoft Entra roles](pim-how-to-add-role-to-user), [Assign Azure resource roles](pim-resource-roles-assign-roles), and [Assign eligibility for a PIM for Groups](groups-assign-member-owner).

### Activate

If users are eligible for a role, then they must activate the role assignment before using the role. To activate the role, users select specific activation duration within the maximum (configured by administrators), and the reason for the activation request.

The following screenshot shows how members activate their role to a limited time.

![Screenshot of Privileged Identity Management role activation.](media/pim-configure/role-activation.png)

If the role requires [approval](pim-resource-roles-approval-workflow) to activate, a notification appears in the upper right corner of the user's browser informing them the request is pending approval. If an approval isn't required, the member can start using the role.

For more information, check out the following articles: [Activate Microsoft Entra roles](pim-how-to-activate-role), [Activate my Azure resource roles](pim-resource-roles-activate-your-roles), and [Activate my PIM for Groups roles](groups-activate-roles)

### Approve or deny

Delegated approvers receive email notifications when a role request is pending their approval. Approvers can view, approve, or deny these pending requests in PIM. After the request is approved, the member can start using the role. For example, if a user or a group was assigned with Contribution role to a resource group, they can manage that particular resource group.

For more information, check out the following articles: [Approve or deny requests for Microsoft Entra roles](pim-approval-workflow), [Approve or deny requests for Azure resource roles](pim-resource-roles-approval-workflow), and [Approve activation requests for PIM for Groups](groups-approval-workflow)

### Extend and renew assignments

After administrators set up time-bound owner or member assignments, the first question you might ask is what happens if an assignment expires? In this new version, we provide two options for this scenario:

- **Extend** – When a role assignment nears expiration, the user can use Privileged Identity Management to request an extension for the role assignment
- **Renew** – When a role assignment expires, the user can use Privileged Identity Management to request a renewal for the role assignment

Both user-initiated actions require an approval from a Global Administrator or Privileged Role Administrator. Admins don't need to be in the business of managing assignment expirations. You can just wait for the extension or renewal requests to arrive for simple approval or denial.

For more information, check out the following articles: [Extend or renew Microsoft Entra role assignments](pim-how-to-renew-extend), [Extend or renew Azure resource role assignments](pim-resource-roles-renew-extend), and [Extend or renew PIM for Groups assignments](groups-renew-extend)

## Scenarios

Privileged Identity Management supports the following scenarios:

### Privileged Role Administrator permissions

- Enable approval for specific roles
- Specify approver users or groups to approve requests
- View request and approval history for all privileged roles

### Approver permissions

- View pending approvals (requests)
- Approve or reject requests for role elevation (single and bulk)
- Provide justification for my approval or rejection

### Eligible role user permissions

- Request activation of a role that requires approval
- View the status of your request to activate
- Complete your task in Microsoft Entra ID if activation was approved

## Microsoft Graph APIs

You can use Privileged Identity Management programmatically through the following Microsoft Graph APIs:

- [PIM for Microsoft Entra roles APIs](/en-us/graph/api/resources/privilegedidentitymanagementv3-overview)
- [PIM for groups APIs](/en-us/graph/api/resources/privilegedidentitymanagement-for-groups-api-overview)