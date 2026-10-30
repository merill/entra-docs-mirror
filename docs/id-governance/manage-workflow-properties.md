---
layout: Conceptual
title: Manage workflow properties - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/manage-workflow-properties
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article guides a user to editing a workflow's properties using Lifecycle Workflows.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: template-how-to
locale: en-us
document_id: 4e414b3b-3418-103b-be64-c498d2cf7cd7
document_version_independent_id: 114d58f6-1f54-8657-eb7c-ea023c0b9046
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/manage-workflow-properties.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/manage-workflow-properties
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/manage-workflow-properties.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: db916119-df3e-c9e2-1d3c-4f15122b464e
---

# Manage workflow properties - Microsoft Entra ID Governance | Microsoft Learn

Managing workflows can be accomplished in one of two ways:

- Updating the basic properties of a workflow without creating a new version of it
- Creating a new version of the updated workflow

You can update the following basic information without creating a new workflow.

- display name
- description
- [Administrative Unit Scope](manage-delegate-workflow)
- whether or not it's enabled
- whether or not workflow schedule is enabled
- task name
- task description

If you change any other parameters, a new version is required to be created as outlined in the [Managing workflow versions](manage-workflow-tasks) article.

If done via the Microsoft Entra admin center, the new version is created automatically. If done using Microsoft Graph, you must manually create a new version of the workflow. For more information, see Edit the properties of a workflow using Microsoft Graph.

## Edit the properties of a workflow using the Microsoft Entra admin center

To edit the properties of a workflow using the Microsoft Entra admin center, you do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. Here you see a list of all of your current workflows. Select the workflow that you want to edit.

    ![Screenshot of the workflow list.](media/manage-workflow-properties/manage-list.png)
4. To change the display name, description, or the Administrative unit scope, select **Properties**.

    ![Screenshot of the basic properties screen.](media/manage-workflow-properties/manage-properties.png)
5. Update the desired properties.

Note

Display names cannot be the same as other existing workflows. They must have their own unique name.

1. Select **save**.

## Edit the properties of a workflow using Microsoft Graph

To update a workflow via API using Microsoft Graph, see: [Update workflow](/en-us/graph/api/identitygovernance-workflow-update)