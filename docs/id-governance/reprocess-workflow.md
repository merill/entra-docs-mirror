---
layout: Conceptual
title: Reprocess workflow runs using Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/reprocess-workflow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article guides a user on reprocessing workflow runs using Lifecycle Workflows
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: 3453e21f-9f62-cec5-59e0-3b68987e8c9f
document_version_independent_id: 3453e21f-9f62-cec5-59e0-3b68987e8c9f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/reprocess-workflow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/reprocess-workflow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/reprocess-workflow.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: a23c2d06-2fa6-53ae-fe46-b9d754fb26c1
---

# Reprocess workflow runs using Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn

Reprocessing workflows is a feature that allows workflows created using lifecycle workflows to be run again to ensure workflows operate as intended. This is useful when dealing with runs that failed for some reason. This article provides step-by-step instructions for reprocessing workflows using the Microsoft Entra admin center, enabling you to quickly and efficiently manage workflow runs for users or specific runs.

## Reprocess a workflow using the Microsoft Entra admin center

To reprocess a workflow using the Microsoft Entra admin center, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. On the workflow list screen, select the workflow you want to reprocess.
4. On the workflow overview page, select **Workflow history**.
5. On the workflow history screen, the **Users** tab is automatically open, allowing you to see a list of users processed by the workflow.
6. To reprocess a workflow for a user, select the user you want to reprocess a workflow for, and select **Reprocess**. ![Screenshot of reprocessing a workflow.](media/reprocess-workflow/reprocess-workflow.png)

    Note

    You're able to reprocess up to 10 users at a time.
7. If you want to reprocess a workflow based on a run, select the **Runs** tab.
8. On the **Runs** tab, you can see a full list of workflow runs. Select the run you want to reprocess and select **Reprocess**.

    Note

    Only a single run can be reprocessed at a time.