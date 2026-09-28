---
layout: Conceptual
title: Lifecycle workflow execution conditions and scheduling - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/lifecycle-workflow-execution-conditions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Conceptual article about Lifecycle workflows execution conditions.
ms.subservice: lifecycle-workflows
ms.workload: identity
ms.topic: concept-article
ms.date: 2026-08-21T00:00:00.0000000Z
ms.custom: template-concept
locale: en-us
document_id: ca38dcce-eb09-ac58-1727-134948364daf
document_version_independent_id: ca38dcce-eb09-ac58-1727-134948364daf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/lifecycle-workflow-execution-conditions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/lifecycle-workflow-execution-conditions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/lifecycle-workflow-execution-conditions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 3554de14-f76e-2c2d-7093-e8b249b712c8
---

# Lifecycle workflow execution conditions and scheduling - Microsoft Entra ID Governance | Microsoft Learn

Workflows created using Lifecycle workflows allow you to automate common tasks for users based on where they fall in the joiner, mover, and leaver model of their lifecycle within your organization. These workflows are able to run in two ways, manually (on-demand) for specific users, or based on a schedule if a user meets the defined execution conditions of a workflow. These execution conditions are defined by two parts: a trigger and a scope. This article describes execution conditions, the difference between the workflow triggers and scopes, and the conditions for when a scheduled workflow runs for users.

## Workflow execution conditions

For a workflow to run for users based on a schedule, they must first meet its execution conditions. The execution conditions consist of:

- Trigger: Defines the conditions for when a workflow runs for users.
- Scope: Defines which users the workflow runs for.

The trigger you choose depends on what type of workflow you want to run for users, and the scope you choose is based on the trigger selected. There are currently four types of triggers supported:

![Screenshot of the trigger details section of a workflow's execution conditions.](media/lifecycle-workflow-execution-conditions/trigger-details.png)

- **Time based attribute**: The workflow is triggered on schedule when a time value is met.
- **Attribute changes**: The workflow is triggered on schedule when a change to an attribute happens.
- **Group membership change**: The workflow is triggered on schedule when a group membership change is met.
- **Sign-in activity**: The workflow is triggered on schedule when a minimum number of days since the user last signed in is met.
- **On-demand only**: The workflow is only triggered manually.

Note

The **On-demand only** trigger is the default trigger of workflow templates that are on-demand only. For the full list of workflow templates, and their compatible triggers, see: [Lifecycle workflows templates and categories](lifecycle-workflow-templates).

## Time based attribute trigger

The **time based attribute** trigger allows you to set a trigger based on when a time value is met.

![Screenshot of the time based workflow trigger.](media/lifecycle-workflow-execution-conditions/time-based-trigger.png)

When setting a workflow where the trigger type is **Time based attribute**, the following details are defined:

| Trigger detail | Description |
| --- | --- |
| Days from Event | The days from the event user attribute for when the workflow is triggered. Value can be from 0-180. |
| Event timing | Defines when the *Days from Event* detail for a workflow is triggered. For example, a workflow that is scheduled to run for a user before they start working would have an event timing value of **Before**, while a workflow scheduled to run for a user after they leave your organization would have an event timing value of **After**. If selecting a template for a workflow that runs on the same day as the event user attribute, the value is **On**. |
| Event user attribute | The attribute defining the change that triggers the workflow. The type of workflow being used determines the attributes available. A joiner workflow can have the attribute value of "*employeeHireDate*" or "*createdDateTime*", while a leaver workflow has an attribute value of "*employeeLeaveDate*". For a list of templates, and their event user attributes, see: [Lifecycle Workflows templates and categories](lifecycle-workflow-templates). You are also able to set custom attribute triggers. For more information, see [Use Custom Attribute Triggers in Lifecycle Workflows (Preview)](workflow-custom-triggers). |

Note

The event user attribute must be set within Microsoft Entra ID for users. For more information on this process, see: [How to synchronize attributes for Lifecycle workflows](how-to-lifecycle-workflow-sync-attributes).

### Relative time-based comparisons (preview)

Important

Relative time-based comparisons are in public preview. During public preview, the Microsoft Entra admin center temporarily shows **Time based attribute** and **Time based attribute V2 (Preview)** as separate choices. Both choices represent the time-based attribute trigger. When this capability becomes generally available, customers will see only one time-based trigger choice that includes relative comparisons. For more information about previews, see [Universal License Terms for Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all).

The preview experience expands the time-based attribute trigger with relative comparisons. It includes the functionality of the standard time-based option and can also match users across a relative period. To configure these comparisons in a new or existing workflow, open [Lifecycle Workflows in the Microsoft Entra admin center](https://aka.ms/LCWRelativeTimeBasedTrigger), and then select **Time based attribute V2 (Preview)** under **Trigger details**.

Configure the following trigger timing details:

| Trigger detail | Description |
| --- | --- |
| Operator | Select **Exactly**, **Between**, or **Less than or equal to**. |
| Days from event | Enter an offset from 0 through 365 days. When you select **Between**, also enter an offset from 0 through 365 days in **Days to event**. |
| Event timing | Select **Before** or **After** the event attribute date. To use the standard time-based behavior on the attribute date, select **Exactly**, enter 0 days, and select **On**. |
| Event attribute | Select any user attribute supported by the time-based trigger, including `employeeHireDate`, `employeeLeaveDateTime`, and `createdDateTime`. |

After configuring the trigger, continue through **Configure scope**, **Review tasks**, and **Review + create**. The workflow and its schedule must both be enabled for the trigger to be evaluated.

Workflow evaluation, scheduling, and processing work the same for both preview choices, except the **Time based attribute V2 (Preview)** choice doesn't have a three-day catch-up window. Workflows created during preview transition to the unified generally available experience without reconfiguration. Microsoft communicates any schema changes in advance.

### Time based attribute scope

The time based attribute scope allows you to define for whom the workflow runs when the time trigger is met.

![Screenshot of the scope screen for time based attribute trigger.](media/lifecycle-workflow-execution-conditions/time-based-scope.png)

When setting the scope of the time based attribute trigger, the following details are defined:

| Scope detail | Description |
| --- | --- |
| Scope type | Rule based. |
| Rule | Defines the rule for who meets the scope of the time based attribute trigger. |

Note

The rule evaluation is case-sensitive.

## Attribute change trigger

The **Attribute change** trigger allows you to set a trigger based on when an attribute changes for users.

![Screenshot of the attribute changes trigger for a workflow.](media/lifecycle-workflow-execution-conditions/attribute-changes-trigger.png)

When setting a workflow where the trigger type is **Attribute change**, the following details are defined:

| Trigger detail | Description |
| --- | --- |
| Trigger Attribute | The trigger attribute defines the attribute that's being changed to trigger the workflow to run. You are also able to set custom attribute triggers. For more information, see [Use Custom Attribute Triggers in Lifecycle Workflows (Preview)](workflow-custom-triggers). |
| Action/Operator | Defines the change to the attribute that triggers the workflow to run. |
| Value | The value of the trigger attribute. |

### Attribute changes trigger scope

The attribute changes trigger scope allows you to define for whom the workflow runs when the attribute change trigger is met.

When setting the scope of the attribute changes trigger, the following details are defined:

| Scope detail | Description |
| --- | --- |
| Scope type | Rule based. |
| Rule | Defines the rule for who meets the scope of the attribute changes trigger. |

Note

The rule evaluation is case-sensitive.

## Group membership change trigger

For workflows that are triggered based on a group membership change, the workflow runs on a schedule when a user is added to, or removed from, a group.

![Screenshot of the group membership change trigger.](media/lifecycle-workflow-execution-conditions/group-membership-trigger.png)

When setting a workflow where the trigger type is **Group membership change**, the following details are defined:

| Trigger detail | Description |
| --- | --- |
| Action | Describes which group membership change triggers the execution condition. Can be **Added to group** or **Removed from group**. |

### Group membership change scope

The group membership change scope allows you to define for whom the workflow runs when the group membership change trigger is met.

![Screenshot of setting scope for group membership change.](media/lifecycle-workflow-execution-conditions/group-membership-scope.png)

When setting the scope of the group membership change trigger, the following details are defined:

| Trigger detail | Description |
| --- | --- |
| Scope type | Group based. |
| Selected group | Defines the group on which the trigger action is based. |

## Sign-in inactivity trigger

The **Sign-in inactivity** trigger allows you to set a trigger based on when a certain number of days has passed since the user last signed in.

![Screenshot of the sign-in inactivity trigger.](media/lifecycle-workflow-execution-conditions/sign-in-inactivity-trigger.png)

When setting the scope of the sign-in inactivity trigger, the following details are defined:

| Scope detail | Description |
| --- | --- |
| Days of inactivity | The number of days since the user last signed in. |

### Sign-in inactivity scope

The sign-in inactivity scope allows you to define for whom the workflow runs when the sign-in inactivity trigger is met.

| Scope detail | Description |
| --- | --- |
| Scope type | Rule based. |
| Rule | Defines the rule for who meets the scope of the attribute changes trigger. |

## On-demand only trigger

The **On-demand only** trigger is set to run the workflow for users you manually select. Workflows with these triggers don't run on a schedule. The users are selected within the scope details section of the workflow.

![Screenshot of selecting users for manual workflow execution.](media/lifecycle-workflow-execution-conditions/on-demand-select-users.png)

When setting a workflow where the trigger type is **On-demand only**, the following details are defined:

| Trigger detail | Description |
| --- | --- |
| Scope type | The scope type determines how the scope of the workflow is defined to run. The default for this is *User selection*. |
| Selection type | The selection type of the workflow can be set as to either allow you to choose users during its creation for who it runs as soon as the workflow is created, or by allowing you to choose which users to run the workflow for at a later date. |

For a detailed guide on running a workflow on-demand for users, see: [Run a workflow on-demand](on-demand-workflow).

## Execution user scope

After the execution conditions are set for an enabled workflow, you're able to see a list of users who currently meet its execution conditions. This user list is made up of users who the workflow runs for the next time it executes, and is based on the last time the workflow engine evaluated users within your tenant.

![Screenshot of a list of users in scope of the workflow's execution conditions.](media/lifecycle-workflow-execution-conditions/execution-user-scope.png)

If the execution conditions recently changed for the workflow, then the execution user scope list might not be current. When the execution conditions are recently changed, the list refreshes with users meeting the latest execution conditions after the workflow engine evaluates the users again. Before the workflow runs for the users, it also checks to make sure the list of users still meet the current execution conditions.

For a detailed guide on viewing the execution user scope of a specific workflow, see: [Check execution user scope of a workflow](check-workflow-execution-scope).

## Lifecycle workflow catch-up window

By design, Lifecycle workflows provide a three day catch up window to help customers process users that could have been missed due to delays in HR user data updates. This means when the workflow engine evaluates users that meet the current execution conditions for the scheduled workflow, it includes users for whom the expected trigger date has already passed but wasn't more than three days past the original trigger date. Once the user is processed, it would only be considered again if there was a change for the user or workflows that allowed it to meet the execution conditions again.

The following table shows examples of Lifecycle Workflows' catch-up window:

| Workflow Scenario | User Data | Lifecycle workflow behavior |
| --- | --- | --- |
| A [pre-hire template](lifecycle-workflow-templates#onboard-pre-hire-employee) workflow is scheduled to run for users 7 days before their **EmployeeHireDate**. | A user is provisioned by HR in Microsoft Entra ID with an **EmployeeHireDate** in 10 days. | The workflow runs for the new user as the date is before the offset. |
| A [pre-hire template](lifecycle-workflow-templates#onboard-pre-hire-employee) workflow is scheduled to run for users 7 days before their **EmployeeHireDate**. | A new user is provisioned by HR in Microsoft Entra ID with an **EmployeeHireDate** in 5 days. | The workflow runs for the new user as the date is within 3 days of the offset. |
| A [pre-hire template](lifecycle-workflow-templates#onboard-pre-hire-employee) workflow is scheduled to run for users 7 days before their **EmployeeHireDate**. | A new user is provisioned by HR in Microsoft Entra ID with an **EmployeeHireDate** in 3 days. | The workflow **does not** run for the new user, as the date is more than 3 days from the offset. |
| A new hire workflow runs on Feb 23 for in scope users with **EmployeeHireDate** of Feb 23. | A new user is provisioned by HR in Microsoft Entra ID on Feb 24 with an EmployeeHireDate set as Feb 23. | The workflow runs again on Feb 24 for the new user, as the date is within 3 days of the offset. |

## Workflow scheduling

While newly created workflows are enabled by default, scheduling is an option that must be enabled manually. To verify whether the workflow is scheduled, you can view the **Scheduled** column on the workflow overview page.

Once scheduling is enabled, the workflow is evaluated either every three hours (by default), or by the interval you select in **workflow settings**, to determine whether or not it should run.

Note

Once the user meets the execution conditions, and is in scope of the workflow, the Lifecycle workflow engine evaluates the user once again before the workflow starts to process them. If the user no longer meets the execution conditions of the workflow, then they won't be processed.

For a detailed guide on setting the execution conditions for a workflow, see: [Create a lifecycle workflow](create-lifecycle-workflow).