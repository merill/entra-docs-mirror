---
layout: Conceptual
title: Customize a workflow schedule - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/customize-workflow-schedule
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to customize the schedule of a lifecycle workflow.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: krbain
locale: en-us
document_id: 630a7e46-8320-09e1-ea99-d44f82400331
document_version_independent_id: 55c068fb-7afb-7a25-584c-7f226abc61c1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/customize-workflow-schedule.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/customize-workflow-schedule
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/customize-workflow-schedule.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4c411d92-5fb4-35c6-cbfb-f712858cde51
---

# Customize a workflow schedule - Microsoft Entra ID Governance | Microsoft Learn

When you create workflows by using lifecycle workflows, you can fully customize them to match the schedule that fits your organization's needs. By default, workflows are scheduled to run every 3 hours. But you can set the interval to be as frequent as 1 hour or as infrequent as 24 hours.

## Customize the schedule of workflows by using the Microsoft Entra admin center

Workflows that you create within lifecycle workflows follow the same schedule that you define on the **Workflow settings** pane. To adjust the schedule, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows**.
3. On the **Lifecycle workflows** overview page, select **Workflow settings**.
4. On the **Workflow settings** pane, set the schedule of workflows as an interval of 1 to 24.

    ![Screenshot of the settings for a workflow schedule.](media/customize-workflow-schedule/workflow-schedule-settings.png)
5. Select **Save**.

## Customize the schedule of workflows by using Microsoft Graph

To schedule workflow settings by using the Microsoft Graph API, see [`lifecycleManagementSettings` resource type](/en-us/graph/api/resources/identitygovernance-lifecyclemanagementsettings).