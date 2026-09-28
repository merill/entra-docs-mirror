---
layout: Conceptual
title: Manage unsponsored guests using Lifecycle Workflows (Preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/how-to-lifecycle-workflow-unsponsored-guest-removal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to manage unsponsored guest removal in your organization using Lifecycle Workflows.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-07-31T00:00:00.0000000Z
ms.custom: template-how-to
ai-usage: ai-assisted
locale: en-us
document_id: 8dc9876d-cf0f-a604-8049-433a5306c5c8
document_version_independent_id: 8dc9876d-cf0f-a604-8049-433a5306c5c8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/how-to-lifecycle-workflow-unsponsored-guest-removal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/how-to-lifecycle-workflow-unsponsored-guest-removal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/how-to-lifecycle-workflow-unsponsored-guest-removal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 47ccafab-c2eb-09bb-b461-48a3181d956c
---

# Manage unsponsored guests using Lifecycle Workflows (Preview) - Microsoft Entra ID Governance | Microsoft Learn

Unsponsored guests—guest users without a valid sponsor assigned—represent a security and compliance risk in your organization. Lifecycle Workflows help you automate the management and removal of unsponsored guests. Microsoft Entra ID Governance includes a built-in **Unsponsored guest cleanup (Preview)** workflow template that automates the detection and management of unsponsored guests.

This article walks you through managing unsponsored guests using the **Unsponsored guest cleanup (Preview)** workflow template.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

Important

This functionality is subject to the guest billing model. For details, see [Microsoft Entra ID Governance licensing for guest users](microsoft-entra-id-governance-licensing-for-guest-users).

## Manage unsponsored guests using the Microsoft Entra admin center

To create a workflow for managing unsponsored guests:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. On the workflow screen, select **Create new workflow**.
4. On the template selection screen, find and select the **Unsponsored guest cleanup (Preview)** workflow template.

    Note

    This template is specifically designed for leaver workflows.
5. Enter basic details for your workflow:

    - **Display name**: A descriptive name for your workflow
    - **Description**: Information about the workflow's purpose
6. Configure the workflow execution conditions. The trigger type is set to **Guest sponsor status (Preview)** by the template and can't be changed.

    ![Screenshot that shows the trigger details section with Guest sponsor status trigger type and number of sponsors set to equal to zero.](media/lifecycle-workflow-unsponsored-guest-removal/trigger-details.png)

    Note

    The **Number of sponsors** condition is set to **Equal to 0** and is not currently configurable. This workflow targets users with no sponsors assigned.
7. Configure the workflow tasks based on your organization's requirements.
8. Select **Review + Create** to finalize and enable the workflow.

## Add email notifications for unsponsored guest removal (optional)

The **Unsponsored guest cleanup (Preview)** template includes the **Delete User Account** task by default. You can optionally add the **Send email about unsponsored guest removal (Preview)** task to notify specified recipients when unsponsored guests are being removed from your organization.

Note

For detailed information about adding and configuring the email task, including recipient options, email customization, and dynamic attributes, see [Lifecycle Workflow tasks and definitions - Send email about unsponsored guest removal (Preview)](lifecycle-workflow-tasks#send-email-about-unsponsored-guest-removal-preview).