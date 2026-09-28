---
layout: Conceptual
title: Manage inactive users using Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/lifecycle-workflow-inactive-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article walks you through managing inactive users with Lifecycle Workflows.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
locale: en-us
document_id: 3dd3bbce-0df7-7639-8f1b-49bb83a0f430
document_version_independent_id: 3dd3bbce-0df7-7639-8f1b-49bb83a0f430
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/lifecycle-workflow-inactive-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/lifecycle-workflow-inactive-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/lifecycle-workflow-inactive-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fed0aeca-ab72-8751-ecb3-f3c257f78f65
---

# Manage inactive users using Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn

As part of supporting users no matter where they fall in the Joiner-Mover-Leaver (JML) model of their lifecycle within your organization, Lifecycle Workflows support automating the disabling and deleting of users once they are inactive for a set period of time. This [sign-in inactivity](lifecycle-workflow-execution-conditions#sign-in-inactivity-trigger) allows you to set a workflow to run when a user is inactive for a set number of days. This feature allows you to seamlessly maintain a secure environment by automating the removal of inactive users based on criteria you set for your organization.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Manage inactive users using the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **workflows**.
3. On the workflow screen, select the specific workflow you want to add the inactive user task to, or create a new workflow based on a template.

    Note

    To use any of the leaver tasks, you must select a leaver workflow template.
4. On the **Basics** tab, after entering a unique display name and description for the workflow, select the **Sign-in inactivity** trigger.
5. Once you select your desired workflow template enter basic details, and then select the **Sign-in inactivity** trigger.
6. Under the **Days of inactivity**, enter the number of days you want the trigger to run for if exceeded, and then select **Next**. ![Screenshot of days of inactivity.](media/lifecycle-workflow-inactive-users/inactivity-trigger.png)

    Note

    Sign-in inactivity is determined by the `lastSuccessfulSignInDateTime` attribute.
7. On the **Scope** page, enter the scope you want for the trigger, and then select **Next**.
8. On the **Review Tasks** page, select the task you want to run for the users who you consider to be inactive and select **Review + Create**.

    Note

    Lifecycle Workflows comes with a built-in task, [Send email about user inactivity](lifecycle-workflow-tasks#send-email-about-user-inactivity), that is directly related to helping manage inactive users.