---
layout: Conceptual
title: Cancel workflow runs using Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/cancel-workflow-runs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to cancel in-progress or queued workflow runs in Lifecycle Workflows to prevent the impact of automation errors and misconfigurations.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-07-27T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: fde75c03-03ee-1c1b-8e46-b155707c6af3
document_version_independent_id: fde75c03-03ee-1c1b-8e46-b155707c6af3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/cancel-workflow-runs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/cancel-workflow-runs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/cancel-workflow-runs.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 00ba78da-acec-f51f-2831-2d374299efa6
---

# Cancel workflow runs using Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn

Lifecycle Workflows allows administrators to cancel in-progress or queued workflow runs to prevent or mitigate the widespread impact of automation errors and misconfigurations.

When you cancel a workflow run, keep the following behavior in mind:

- **In-progress runs**: Canceling an in-progress workflow run cancels any tasks that haven't been processed yet. Tasks that already completed aren't affected.
- **Queued runs**: Queued workflows are runs where execution hasn't started yet. Canceling a queued run cancels the upcoming execution of all tasks for that run.
- **No rollback**: Previously completed changes aren't reversed. Only execution of upcoming changes is halted.
- **Single run selection**: Currently, you can only select a single run to cancel at a time.
- **Run-level cancellation only**: You can't cancel specific tasks or specific users within a run. Cancellation applies to the entire run.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Cancel a workflow run in the Microsoft Entra admin center

To cancel a workflow run:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. Select the workflow that contains the run you want to cancel.
4. On the workflow page, select **Workflow History**.

    ![Screenshot of the workflow overview page with the Workflow history link highlighted in the left navigation.](media/cancel-workflow-runs/workflow-history-cancel.png)
5. Select the **Runs** tab.
6. Select a run that has a status of **In progress** or **Queued**.

    Note

    The **Cancel** button is only enabled after you select a run that has a status of **In progress** or **Queued**. The **Cancel** button isn't available on the **Users** or **Tasks** tabs because only runs can be canceled.
7. Select **Cancel**.