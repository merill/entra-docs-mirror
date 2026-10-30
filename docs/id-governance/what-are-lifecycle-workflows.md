---
layout: Conceptual
title: What are lifecycle workflows? - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/what-are-lifecycle-workflows
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Get an overview of the lifecycle workflow feature of Microsoft Entra ID.
ms.subservice: lifecycle-workflows
ms.topic: overview
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: c76a7cb7-547a-f77c-e410-e20290b26cf4
document_version_independent_id: d7d4818d-734d-d585-62a6-d8f3a042d2f0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/what-are-lifecycle-workflows.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/what-are-lifecycle-workflows
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/what-are-lifecycle-workflows.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 31da10c2-c257-72c4-dc0a-b5904b3d3691
---

# What are lifecycle workflows? - Microsoft Entra ID Governance | Microsoft Learn

Lifecycle workflows (LCW) are identity governance capabilities that enable organizations to manage Microsoft Entra users across the three phases of a user's lifecycle with an organization:

- **Joiner**: When an individual enters the scope of needing access. An example is a new employee joining a company or organization.
- **Mover**: When an individual moves between boundaries within an organization. This movement might require more access or authorization. An example is a user who was in marketing and is now a member of the sales organization.
- **Leaver**: When an individual leaves the scope of needing access. This movement might require the removal of access. Examples are an employee who's retiring or an employee who's terminated.

Workflows contain specific processes that run automatically against users as they move through their lifecycle. Workflows consist of [tasks](lifecycle-workflow-tasks) and [execution conditions](understanding-lifecycle-workflows#understanding-lifecycle-workflows).

Tasks are specific actions that run automatically when a workflow is triggered. An execution condition defines the scope of who's affected and the trigger of when a workflow will be performed. For example, sending a manager an email seven days before the value in the `employeeHireDate` attribute of new employees can be described as a workflow. It consists of:

- Task: Send email.
- Who (scope): New employees.
- When (trigger): Seven days before the `employeeHireDate` attribute value.

An automatic workflow schedules a [trigger](understanding-lifecycle-workflows#trigger-details) based on user attributes. Scoping of automatic workflows is possible through a wide range of user and extended attributes, such as the department that a user belongs to.

Lifecycle workflows can even [integrate with the ability of logic apps tasks to extend workflows](lifecycle-workflow-extensibility) for more complex scenarios through your existing logic apps.

[![Diagram of lifecycle workflows.](media/what-are-lifecycle-workflows/intro-2.png)](media/what-are-lifecycle-workflows/intro-2.png#lightbox)

## Why to use lifecycle workflows

Anyone who wants to modernize an identity lifecycle management process for employees needs to ensure:

- That when users join the organization, they're ready to go on day one. They have the correct access to information, group memberships, and applications that they need.
- That users who are no longer tied to the company for various reasons (termination, separation, leave of absence, or retirement) have their access revoked in a timely way.
- That the process for providing or revoking access isn't overly burdensome or time consuming for administrators.
- That administrators and other authorized users can easily troubleshoot problems, and that logging is sufficient to help with troubleshooting, auditing, and compliance.

Key reasons to use lifecycle workflows include:

- Extend your HR-driven provisioning process with other workflows that simplify and automate tasks.
- Centralize your workflow process so you can easily create and manage workflows in one location.
- Easily troubleshoot workflow scenarios with the workflow history and audit logs.
- Manage user lifecycle at scale. As your organization grows, the need for other resources to manage user lifecycle decreases.
- Reduce or remove manual tasks.
- Apply logic apps to extend workflows for more complex scenarios with your existing logic apps.
- Use [Microsoft Security Copilot to create and manage lifecycle workflows](../security-copilot/entra-lifecycle-workflows) using natural language.

Those capabilities can help ensure a holistic experience by allowing you to remove other dependencies and applications to achieve the same result. You can then increase efficiency in new employee orientation and in removal of former employees from the system.

## When to use lifecycle workflows

You can use lifecycle workflows to address any of the following conditions:

- **Automating and extending user orientation and HR provisioning**: Use lifecycle workflows when you want to extend your HR provisioning scenarios by automating tasks such as generating temporary passwords and emailing managers. If you currently have a manual process for orientation, use lifecycle workflows as part of an automated process.
- **Automating dynamic group memberships**: When groups in your organization are well defined, you can automate user membership in those groups. Benefits and differences from dynamic group memberships include:
    - Lifecycle workflows manage static groups, where you don't need a dynamic group rule.
    - There's no need to have one rule per group. Lifecycle workflow rules determine the scope of users to execute workflows against, not which group.
    - Lifecycle workflows help manage users' lifecycle beyond attributes supported in dynamic group memberships--for example, a certain number of days before the `employeeHireDate` attribute value.
    - Lifecycle workflows can perform actions on the group, not just the membership.
- **Workflow history and auditing**: Use lifecycle workflows when you need to create an audit trail of user lifecycle processes. By using the Microsoft Entra admin center, you can view history and audits for orientation and departure scenarios.
- **Automating user account management**: A key part of the identity lifecycle process is making sure that users who are leaving have their access to resources revoked. You can use lifecycle workflows to automate the disabling and removal of user accounts.
- **Automating Access Package Assignment**: Lifecycle workflows can be used to automate assigning, and removing, access packages for users.
- **Integrating with logic apps**: You can apply logic apps to extend workflows for more complex scenarios.

## License requirements

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

With Lifecycle Workflows, you can:

- Create, manage, and delete workflows up to the total limit of 100 workflows.
- Trigger on-demand and scheduled workflow execution.
- Manage and configure existing tasks to create workflows that are specific to your needs.
- Create up to 100 custom task extensions to be used in your workflows.