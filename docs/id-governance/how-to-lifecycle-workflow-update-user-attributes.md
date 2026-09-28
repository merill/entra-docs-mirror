---
layout: Conceptual
title: Update user attributes with Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/how-to-lifecycle-workflow-update-user-attributes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to update user attributes using the Update user attributes task in Lifecycle Workflows.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-05-01T00:00:00.0000000Z
ms.custom: template-how-to
ai-usage: ai-assisted
locale: en-us
document_id: 0aa3ab69-438d-5325-046e-b28767cb85a4
document_version_independent_id: 0aa3ab69-438d-5325-046e-b28767cb85a4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/how-to-lifecycle-workflow-update-user-attributes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/how-to-lifecycle-workflow-update-user-attributes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/how-to-lifecycle-workflow-update-user-attributes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 8160ffba-5ec2-9258-d981-6a3c7550751b
---

# Update user attributes with Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn

Lifecycle Workflows allow you to automate the updating of user attributes as part of joiner, mover, and leaver scenarios. The **Update user attributes** task enables you to set or clear attribute values for users in your organization when lifecycle events occur, such as a department change or an employee leaving.

This article walks you through configuring a workflow with the Update user attributes task using the Microsoft Entra admin center and Microsoft Graph.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Supported attributes

The Update user attributes task supports the following attribute types:

- Built-in user attributes for cloud-managed users (for example, `department`, `jobTitle`, `employeeLeaveDateTime`)
- On-premises extension attributes for cloud-managed users (for example, `extensionAttribute1` through `extensionAttribute15`)
- Directory extension attributes for cloud-managed users and users synced from on-premises AD

Note

Custom security attributes are not supported with this task.

Note

For datetime attributes, you can specify either a specific date or use `system.now`. When set to `system.now`, the attribute will be set to the date when the task is processed.

## Limitations

Before configuring this task, be aware of the following limitations:

- **Up to 10 attributes** can be updated per task instance.
- For **users synced from on-premises AD**, this task supports **directory extension attributes only**.

## Configure the Update user attributes task using the Microsoft Entra admin center

To add the Update user attributes task to a workflow using the Microsoft Entra admin center, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. Select an existing workflow or create a new workflow where you want to add the task.
4. On the workflow screen, select **Tasks**.
5. Select **Add task**, and then select **Update user attributes** from the list of available tasks.

    ![Screenshot showing the Select tasks panel with Update user attributes (Preview) selected.](media/how-to-lifecycle-workflow-update-user-attributes/select-update-user-attributes-task.png)
6. Configure the attribute updates:

    - Select the attributes you want to update or clear.
    - Provide the new values for each attribute, or leave the value empty to clear an attribute.

    ![Screenshot showing the attribute configuration panel for the Update user attributes task.](media/how-to-lifecycle-workflow-update-user-attributes/configure-attribute-user-task.png)
7. Select **Save** to add the task to the workflow.

Note

You can configure up to 10 attribute updates within a single task instance.