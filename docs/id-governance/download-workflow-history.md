---
layout: Conceptual
title: Download workflow history reports - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/download-workflow-history
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article guides a user on downloading the history of a Lifecycle workflow.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: 6f64ab26-e63e-3223-613e-79feaba0abe3
document_version_independent_id: 6f64ab26-e63e-3223-613e-79feaba0abe3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/download-workflow-history.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/download-workflow-history
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/download-workflow-history.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 2ce42e21-be94-fe36-15ca-b0a23a482ea5
---

# Download workflow history reports - Microsoft Entra ID Governance | Microsoft Learn

The Lifecycle Workflows history feature allows you to view details about the actions of a workflow such as when it runs, processes a task, or processes a user. From the Microsoft Entra admin center, you're able to filter this information up to 30 days from when the action was taken. To store this information for a longer period of time, you can save the history as a CSV report. This article walks you through how you can download these reports.

## Download the history report of a workflow by using the Microsoft Entra admin center

To download the history report of a workflow by using the Microsoft Entra admin center, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. Select the workflow you want to download the history of.
4. On the workflow overview screen, select **Workflow history** under the **Activity** bar on the left.
5. The Workflow history screen shows the history of a workflow from the view of Users, runs, and Tasks. For more information on workflow history, see [Lifecycle Workflows history](lifecycle-workflow-history). ![Screenshot of the workflow history screen.](media/download-workflow-history/workflow-history-screen.png)
6. On the workflow history page that you want to download a report of, the applied filters are included in your report. When these selected filters match what you want in your report, select **Download**. ![Screenshot of download location on workflow history screen.](media/download-workflow-history/workflow-history-screen-download.png)
7. On the download pane, you see the type of report you're downloading at the top, and it's also present in the default name of the CSV report.

    ![Screenshot of the workflow history download pane.](media/download-workflow-history/history-download-pane.png)
8. Select **Download**.

Note

You can download up to 100,000 records in a report. If you want to download more, use the [Lifecycle Workflow reporting API](/en-us/graph/api/resources/identitygovernance-lifecycleworkflows-reporting-overview).