---
layout: Conceptual
title: Use custom attribute triggers in lifecycle workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/workflow-custom-triggers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article discusses how to use Custom Attribute Triggers as an attribute change trigger within a workflow in Lifecycle Workflows.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: 816e2c75-b6f2-be66-e47a-d00e2e61c873
document_version_independent_id: 816e2c75-b6f2-be66-e47a-d00e2e61c873
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/workflow-custom-triggers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/workflow-custom-triggers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/workflow-custom-triggers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 6d8288de-5c5c-034b-1db7-4e4f971403bd
---

# Use custom attribute triggers in lifecycle workflows - Microsoft Entra ID Governance | Microsoft Learn

Lifecycle Workflows allows you to trigger workflows to run automatically for users that meet the execution conditions of the workflow. There are many default attributes that you can use to trigger workflows, but sometimes you might require triggering a workflow based on a specific attribute not offered by default. Using custom attribute triggers, you can trigger a workflow to run for users based on when they move within your organization based on:

- [Custom security attributes (CSA)](manage-workflow-custom-security-attribute)
- Directory extension attributes
- On-premises extension attributes (1-15)
- EmployeeOrgData attributes

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Use custom attribute triggers in a new workflow using the Microsoft Entra admin center

To use custom attribute triggers in a new workflow, do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator) and [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Create a workflow**.
3. On the Workflows page, select a workflow template that you want to use a custom security attribute as part of the scope for.
4. Enter the basic information such as display name, description, and administration scope.
5. Under **Trigger type** select **Attribute changes**.
6. For Attribute, select the attribute trigger you want to trigger the workflow to run.
7. Finish configuring the workflow and save it.

    Note

    Attribute changes are only detected for scheduled workflows.

## Add a custom attribute to an existing workflow trigger using the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator) and [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. Select the workflow that you want to add a custom attribute to the trigger of.
4. On the workflow overview page, select **Execution conditions**.
5. Under **Trigger details**, update the trigger with the custom attribute you want to use to trigger the workflow.
6. Select **Save**.

## Custom attribute trigger considerations

Currently the workflow and the workflow schedule must be enabled for attributes changes to be picked up and workflows executions to be scheduled. Once Lifecycle Workflows starts checking for attribute changes, the time it takes for changes to be picked up might be delayed for these custom attributes. While changes should be picked up within minutes, there are upstream processes that will add further delays after the user attribute changes, for example:

- Custom attributes might take up to 4 hours for their changes to be updated by the underlying service, however, once the custom attributes changes are propagated, Lifecycle Workflows should pick up the change within seconds.
- Once changes are picked up by Lifecycle workflows, workflow execution will occur in the next target run, according to the schedule for users that meet the workflow scope.

## Attribute vs custom attribute processing timing

The following image shows the potential differences in processing times for using regular attributes and custom attributes in the workflow trigger.

![Screenshot of a comparison between regular and custom attribute processing timing in a workflow run.](media/workflow-custom-triggers/custom-attribute-timing.png)

In example A, the workflow is scheduled to run when the department attribute changes, it's 12:00 pm and the next target runs are at 1pm and 2pm:

- At 12:10pm, the user department changes
- At 12:15 pm, the user is detected to be in scope of the workflow
- In the 1pm run, the user gets processed by the workflow

In example B, the workflow is scheduled to run when the TestCustomSecurityAttribute1 attribute changes, it's 12:00 pm and the next target runs are at 1pm and 2pm:

- At 12:10pm the TestCustomSecurityAttribute1 attribute changes for a user
- At 3:55 pm the change is passed to Lifecycle Workflows
- At 4:00 pm the user is detected to be in scope of the workflow (too late for the 4pm run)
- In the 5pm run, the user gets processed by the workflow

For frequently asked question about using custom attribute triggers within lifecycle workflows, see: [Lifecycle workflows FAQs](workflows-faqs).