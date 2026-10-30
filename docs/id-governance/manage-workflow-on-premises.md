---
layout: Conceptual
title: Manage users synchronized from Active Directory Domain Services with workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/manage-workflow-on-premises
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: A how to article on how to edit a user account related task to run for users synchronized from Active Directory Domain Services (AD DS) with Lifecycle workflows.
ms.workload: identity
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.subservice: lifecycle-workflows
ms.custom: template-how-to, sfi-image-nochange
locale: en-us
document_id: 903b7edc-5f15-740b-9dda-b7e3dd2db311
document_version_independent_id: 903b7edc-5f15-740b-9dda-b7e3dd2db311
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/manage-workflow-on-premises.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/manage-workflow-on-premises
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/manage-workflow-on-premises.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4dd9eb41-54b3-b846-601b-06cee217e61f
---

# Manage users synchronized from Active Directory Domain Services with workflows - Microsoft Entra ID Governance | Microsoft Learn

Workflows created by Lifecycle workflows can be used to manage the lifecycle of users synchronized from Active Directory Domain Services (AD DS). Synced AD DS support allows you to use workflow tasks to enable, disable, and delete synchronized users. In this article, you're walked through the steps of enabling a user account task to be run for users synchronized from AD DS.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

While most Lifecycle workflow tasks can manage users synchronized from Active Directory Domain Services without any extra configuration, certain tasks such as enabling, disabling, and deleting tasks require some extra configuration. For more information on setting these prerequisites, see: [User account tasks](lifecycle-workflow-on-premises#user-account-tasks).

## Configure a user account task to manage users synchronized from Active Directory Domain Services using the Microsoft Entra admin center

Account related tasks within workflows can be quickly edited to apply to users synchronized from Active Directory Domain Services. To edit a task in such a way using the Microsoft Entra admin center, do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. Select the workflow you want to edit the task within.
4. On the workflow screen, select **Tasks**.
5. On the Tasks screen, either select an existing task you want to run for users synchronized from Active Directory Domain Services, or create a new one by selecting **Add task**.
6. On the individual task screen, enable the checkbox that corresponds to running for a synchronized Active Directory Domain Services user. The following image shows it being enabled for a delete user account task. ![Screenshot of setting on-premises flag to delete account.](media/manage-workflow-on-premises/delete-user-account-task-flag.png)
7. Select **Save**.

## Edit a user account task to be compatible with users synchronized from Active Directory Domain Services using Microsoft Graph

To manage user tasks to be compatible with users synchronized from Active Directory Domain Services via API using Microsoft Graph, see: [Configure the arguments for built-in Lifecycle Workflow tasks](/en-us/graph/identitygovernance-lifecycleworkflows-task-arguments).