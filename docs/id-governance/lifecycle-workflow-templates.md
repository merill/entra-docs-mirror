---
layout: Conceptual
title: Lifecycle Workflows templates and categories - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/lifecycle-workflow-templates
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Conceptual article discussing workflow templates and categories with Lifecycle Workflows.
ms.subservice: lifecycle-workflows
ms.topic: concept-article
ms.date: 2026-04-25T00:00:00.0000000Z
ms.custom: template-concept
locale: en-us
document_id: 0f027bcf-ac81-8dfe-13b6-d97aa2e8afdc
document_version_independent_id: e18836de-5235-f9ee-9b10-2398b53f5fdd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/lifecycle-workflow-templates.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/lifecycle-workflow-templates
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/lifecycle-workflow-templates.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d8f6e1bb-fb27-569a-0c39-5c486e376dea
---

# Lifecycle Workflows templates and categories - Microsoft Entra ID Governance | Microsoft Learn

Lifecycle Workflows allows you to automate the lifecycle management process for your organization by creating workflows that contain both built-in tasks, and custom task extensions. These workflows, and the tasks within them, all fall into categories based on the Joiner-Mover-Leaver(JML) model of lifecycle management. To make this process even more efficient, Lifecycle Workflows also provide you with templates, which you can use to accelerate the setup, creation, and configuration of common lifecycle management processes. You can create workflows based on these templates as is, or you can customize them even further to match the requirements for users within your organization. In this article, you get the complete list of workflow templates, common template parameters, default template parameters for specific templates, and the list of compatible tasks for each template. For full task definitions, see [Lifecycle Workflow tasks and definitions](lifecycle-workflow-tasks).

## Lifecycle Workflows built-in templates

Lifecycle Workflows currently have 14 built-in templates you can use or customize:

[![Screenshot of a list of lifecycle workflow templates.](media/lifecycle-workflow-templates/templates-list.png)](media/lifecycle-workflow-templates/templates-list.png#lightbox)

The list of templates is as follows:

- [Onboard pre-hire employee](lifecycle-workflow-templates#onboard-pre-hire-employee)
- [Onboard new hire employee](lifecycle-workflow-templates#onboard-new-hire-employee)
- [Post-Onboarding of an employee](lifecycle-workflow-templates#post-onboarding-of-an-employee)
- [Real-time employee change](lifecycle-workflow-templates#real-time-employee-change)
- [Real-time employee termination](lifecycle-workflow-templates#real-time-employee-termination)
- [Pre-Offboarding of an employee](lifecycle-workflow-templates#pre-offboarding-of-an-employee)
- [Offboard an employee](lifecycle-workflow-templates#offboard-an-employee)
- [Post-Offboarding of an employee](lifecycle-workflow-templates#post-offboarding-of-an-employee)
- [Employee group membership changes](lifecycle-workflow-templates#employee-group-membership-changes)
- [Employee job profile change](lifecycle-workflow-templates#employee-job-profile-change)
- [Pre-Offboard inactive users](lifecycle-workflow-templates#pre-offboard-inactive-users)
- [Offboard inactive users](lifecycle-workflow-templates#offboard-inactive-users)
- [Transition agent sponsorships when a sponsor leaves](lifecycle-workflow-templates#transition-agent-sponsorships-when-a-sponsor-leaves)
- [Transition agent sponsorships when a sponsor changes roles](lifecycle-workflow-templates#transition-agent-sponsorships-when-a-sponsor-changes-roles)

For a complete guide on creating a new workflow from a template, see: [Tutorial: On-boarding users to your organization using Lifecycle workflows with the Microsoft Entra admin center](tutorial-onboard-custom-workflow-portal).

Note

Lifecycle workflows enhances Microsoft Entra ID Governance's [HR-driven provisioning](../identity/app-provisioning/what-is-hr-driven-provisioning) by automating routine processes. While HR provisioning manages the creation and attribute updates of user accounts, lifecycle workflows provide additional automation of tasks.

### Onboard pre-hire employee

The **Onboard pre-hire employee** template is designed to configure tasks that must be completed before an employee's start date.

![Screenshot of a Lifecycle Workflow onboard pre-hire template.](media/lifecycle-workflow-templates/onboard-pre-hire-template.png)

The default specific parameters and properties for the **Onboard pre-hire employee** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Joiner | ❌ |
| Trigger Type | Time based attribute, Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Time based**: Days from event, Event timing, Event user attribute • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Days from event | -7 | ✔️ |
| Event timing | Before | ❌ |
| Event User attribute | EmployeeHireDate | ❌ |
| Scope | Depends on trigger. **Rule based**: Time based attribute, Attribute changes.**Group membership change**: Group based. | ✔️ |
| Tasks | **Generate TAP And Send Email** | ✔️ |

For a tutorial on setting up a workflow that uses the **Onboard pre-hire employee** template, see: [Automate employee onboarding tasks before their first day of work with the Microsoft Entra admin center](tutorial-onboard-custom-workflow-portal).

### Onboard new hire employee

The **Onboard new-hire employee** template is designed to configure tasks that are completed on an employee's start date.

![Screenshot of a Lifecycle Workflow onboard new hire template.](media/lifecycle-workflow-templates/onboard-new-hire-template.png)

The default specific parameters for the **Onboard new hire employee** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Joiner | ❌ |
| Trigger Type | Time based attribute, Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Time based**: Days from event, Event timing, Event user attribute • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Days from event | 0 | ❌ |
| Event timing | On | ❌ |
| Event User attribute | EmployeeHireDate, createdDateTime | ✔️ |
| Scope | Depends on trigger. **Rule based**: Time based attribute, Attribute changes.**Group membership change**: Group based. | ✔️ |
| Tasks | **Add User To Group**, **Enable User Account**, **Send Welcome Email** | ✔️ |

### Post-Onboarding of an employee

The **Post-Onboarding of an employee** template is designed to configure tasks that are completed after an employee's start, or creation, date.

![Screenshot of a Lifecycle Workflow post-onboard new hire template.](media/lifecycle-workflow-templates/onboard-post-employee-template.png)

The default specific parameters for the **Post-Onboarding of an employee** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Joiner | ❌ |
| Trigger Type | Time based attribute, Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Time based**: Days from event, Event timing, Event user attribute • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Days from event | 7 | ✔️ |
| Event timing | After | ❌ |
| Event User attribute | EmployeeHireDate, createdDateTime | ✔️ |
| Scope | Depends on trigger. **Rule based**: Time based attribute, Attribute changes.**Group membership change**: Group based. | ✔️ |
| Tasks | **Add User To Group**, **Add user to selected teams** | ✔️ |

### Real-time employee change

The **Real-time employee change** template is designed to configure tasks that are completed immediately when an employee changes roles.

![Screenshot of a Lifecycle Workflow real time employee change template.](media/lifecycle-workflow-templates/on-demand-change-template.png)

The default specific parameters for the **Real-time employee change** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Mover | ❌ |
| Trigger Type | On-demand | ❌ |
| Tasks | **Run a Custom Task Extension**, **Remove all access package assignments for user** (scheduled removal defaulting to 15 days) | ✔️ |

Note

As this template is designed to run on-demand, no execution condition is present.

### Real-time employee termination

The **Real-time employee termination** template is designed to configure tasks that are completed immediately when an employee is terminated.

![Screenshot of a Lifecycle Workflow real time employee termination template.](media/lifecycle-workflow-templates/on-demand-termination-template.png)

The default specific parameters for the **Real-time employee termination** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Leaver | ❌ |
| Trigger Type | On-demand | ❌ |
| Tasks | **Remove user from all groups**, **Delete User Account**, **Remove user from all Teams** | ✔️ |

Note

As this template is designed to run on-demand, no execution condition is present.

### Pre-Offboarding of an employee

The **Pre-Offboarding of an employee** template is designed to configure tasks that are completed before an employee's last day of work.

![Screenshot of a pre offboarding employee template.](media/lifecycle-workflow-templates/offboard-pre-employee-template.png)

The default specific parameters for the **Pre-Offboarding of an employee** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Leaver | ❌ |
| Trigger Type | Time based attribute, Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Time based**: Days from event, Event timing, Event user attribute • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Days from event | 7 | ✔️ |
| Event timing | Before | ❌ |
| Event User attribute | employeeLeaveDateTime | ❌ |
| Scope | Depends on trigger. **Rule based**: Time based attribute, Attribute changes.**Group membership change**: Group based. | ✔️ |
| Tasks | **Remove user from selected groups**, **Remove user from selected Teams** | ✔️ |

### Offboard an employee

The **Offboard an employee** template is designed to configure tasks that are completed on an employee's last day of work.

![Screenshot of an offboard employee template lifecycle workflow.](media/lifecycle-workflow-templates/offboard-employee-template.png)

The default specific parameters for the **Offboard an employee** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Leaver | ❌ |
| Trigger Type | Time based attribute, Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Time based**: Days from event, Event timing, Event user attribute • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Days from event | 0 | ✔️ |
| Event timing | On | ❌ |
| Event User attribute | employeeLeaveDateTime | ❌ |
| Scope | Depends on trigger. **Rule based**: Time based attribute, Attribute changes.**Group membership change**: Group based. | ✔️ |
| Tasks | **Disable User Account**, **Remove user from all groups**, **Remove user from all Teams** | ✔️ |

### Post-Offboarding of an employee

The **Post-Offboarding of an employee** template is designed to configure tasks that are completed after an employee's last day of work.

![Screenshot of an offboarding an employee after last day template.](media/lifecycle-workflow-templates/offboard-post-employee-template.png)

The default specific parameters for the **Post-Offboarding of an employee** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Leaver | ❌ |
| Trigger Type | Time based attribute, Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Time based**: Days from event, Event timing, Event user attribute • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Event User attribute | employeeLeaveDateTime | ❌ |
| Scope | Depends on trigger. **Rule based**: Time based attribute, Attribute changes.**Group membership change**: Group based. | ✔️ |
| Tasks | **Remove all licenses for user**, **Remove user from all Teams**, **Delete User Account** | ✔️ |

For a tutorial on setting up a workflow that uses the **Post-Offboarding of an employee** template, see: [Automate employee offboarding tasks after their last day of work with the Microsoft Entra admin center](tutorial-scheduled-leaver-portal).

### Employee group membership changes

The **Employee group membership changes** template is designed to configure tasks that are completed when an employee has a change in a group membership.

![Screenshot of an Employee group membership changes template.](media/lifecycle-workflow-templates/employee-group-membership-changes-template.png)

The default specific parameters for the **Employee group membership changes** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | mover | ❌ |
| Trigger Type | Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Scope | Depends on trigger. **Rule based**: Attribute changes.**Group membership change**: Group based. | ✔️ |
| Tasks | **Remove all access package assignments for user** (scheduled removal defaulting to 15 days), **Remove user from selected Teams**, **Send email to notify manager of user move** | ✔️ |

### Employee job profile change

The **Employee job profile change** template is designed to configure tasks that are completed when an employee has a change in job title.

![Screenshot of the Employee job profile change template.](media/lifecycle-workflow-templates/employee-job-profile-change-template.png)

The default specific parameters for the **Employee job profile change** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | mover | ❌ |
| Trigger Type | Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Scope | Depends on trigger. **Rule based**: Attribute changes.**Group membership change**: Group based. | ✔️ |
| Tasks | **Send email to notify manager of user move**, **Remove all access package assignments for user** (scheduled removal defaulting to 15 days), **Remove user from selected groups**, **Remove user from selected Teams**, **Request user access package assignment** | ✔️ |

For a tutorial on setting up a workflow that uses the **Employee job profile change** template, see: [Automate employee mover tasks when they change jobs using the Microsoft Entra admin center](tutorial-mover-custom-workflow-portal).

### Pre-Offboard inactive users

The **Pre-Offboard inactive users** template is designed to configure tasks that must be completed before offboarding inactive users.

![Screenshot of the pre-offboard inactive users template.](media/lifecycle-workflow-templates/begin-off-board-inactive-users-template.png)

The default specific parameters for the **Pre-Offboard inactive users** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Leaver | ❌ |
| Trigger Type | Sign-in inactivity, Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Sign-in inactivity**: Days of inactivity • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Days of inactivity | 90 | ✔️ |
| Event timing | Before | ❌ |
| Event User attribute | lastSuccessfulSignInDateTime | ❌ |
| Scope | Depends on trigger. **Rule based**: Time based attribute, Attribute changes.**Group membership change**: Group based. | ✔️ |
| Tasks | **Disable user account**, **Send inactivity notification email** | ✔️ |

### Offboard inactive users

The **Offboard inactive users** template is designed to configure tasks that must be completed to offboard inactive users.

![Screenshot of the offboard inactive users template.](media/lifecycle-workflow-templates/off-board-inactive-users-template.png)

The default specific parameters for the **Offboard inactive users** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Leaver | ❌ |
| Trigger Type | Sign-in inactivity, Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Sign-in inactivity**: Days of inactivity  • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Days from event | 120 | ✔️ |
| Event timing | After | ❌ |
| Event User attribute | lastSuccessfulSignInDateTime | ❌ |
| Scope | Depends on trigger. **Rule based**: Time based attribute, Attribute changes**Group membership change**: Group based. | ✔️ |
| Tasks | **Disable user account**, **Send inactivity notification email** | ✔️ |

### Transition agent sponsorships when a sponsor leaves

The **Transition agent sponsorships when a sponsor leaves** template is designed to configure tasks that transition agent sponsorships when a sponsor leaves the organization. This template is available for tenants with the Microsoft Agent 365 license. For more information, see: [Microsoft Agent 365 Documentation](https://aka.ms/entraagent365).

The default specific parameters for the **Transition agent sponsorships when a sponsor leaves** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Leaver | ❌ |
| Trigger Type | Time based attribute, Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Time based**: Days from event, Event timing, Event user attribute • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Days from event | 0 | ✔️ |
| Event timing | On | ❌ |
| Event User attribute | employeeLeaveDateTime | ❌ |
| Scope | Depends on trigger. **Rule based**: Time based attribute, Attribute changes.**Group membership change**: Group based. | ✔️ |
| Tasks | **Send email to manager about sponsorship changes**, **Send email to co-sponsors about sponsor changes**, **Transfer agent sponsorships to manager** | ✔️ |

### Transition agent sponsorships when a sponsor changes roles

The **Transition agent sponsorships when a sponsor changes roles** template is designed to configure tasks that transition agent sponsorships when a sponsor changes roles within the organization. This template is available for tenants with the Microsoft Agent 365 license. For more information, see: [Microsoft Agent 365 Documentation](https://aka.ms/entraagent365).

The default specific parameters for the **Transition agent sponsorships when a sponsor changes roles** template are as follows:

| Parameter | Description | Customizable |
| --- | --- | --- |
| Category | Mover | ❌ |
| Trigger Type | Attribute changes, Group Membership change | ✔️ |
| Trigger details | Depends on trigger type selection.  • **Attribute changes**: Trigger attribute • **Group membership changes**: Added to group/Remove from group | ✔️ |
| Scope | Depends on trigger. **Rule based**: Attribute changes.**Group membership change**: Group based. | ✔️ |
| Tasks | **Send email to manager about sponsorship changes**, **Send email to co-sponsors about sponsor changes**, **Transfer agent sponsorships to manager** | ✔️ |