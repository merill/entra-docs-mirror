---
layout: Conceptual
title: Discover Azure resources to manage in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-resource-roles-discover-resources
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to discover Azure resources to manage in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: sfi-ga-nochange
locale: en-us
document_id: bef8c4d4-c8f5-aaf2-c1e8-4da44f9fdee0
document_version_independent_id: 4850f3f9-10ce-78c3-9f6d-8e037e5f3de1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-resource-roles-discover-resources.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-resource-roles-discover-resources
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-resource-roles-discover-resources.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: e79f3d33-9c09-a194-bc85-8088eaadec64
---

# Discover Azure resources to manage in PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

You can use Privileged Identity Management (PIM) in Microsoft Entra ID, to improve the protection of your Azure resources. This helps:

- Organizations that already use Privileged Identity Management to protect Microsoft Entra roles
- Management group and subscription owners who are trying to secure production resources

When you first set up Privileged Identity Management for Azure resources, you need to discover and select the resources you want to protect with Privileged Identity Management. When you discover resources through Privileged Identity Management, PIM creates the PIM service principal (MS-PIM) assigned as User Access Administrator on the resource. There's no limit to the number of resources that you can manage with Privileged Identity Management. However, start with your most critical production resources.

Note

PIM can now automatically manage Azure resources in a tenant with no onboarding required. The updated user experience uses the latest PIM ARM API, allowing for improved performance and granularity in choosing the correct scope you want to manage. The new experience is the default when you navigate to **Azure resources** in PIM. The steps in this article describe the legacy experience. To switch between the new and legacy experiences, use the banner link at the top of the Azure resources page.

## Required permissions

You can view and manage the management groups or subscriptions to which you have Microsoft.Authorization/roleAssignments/write permissions, such as User Access Administrator or Owner roles. If you aren't a subscription owner, but are a Global Administrator and don't see any Azure subscriptions or management groups to manage, then you can [elevate access to manage your resources](/en-us/azure/role-based-access-control/elevate-access-global-admin).

## Discover resources

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Azure resources**.

    If it is your first time using Privileged Identity Management for Azure resources, you see a **Discover resources** page.

    ![Screenshot of the Discover resources pane with no resources listed for first time experience.](media/pim-resource-roles-discover-resources/discover-resources-first-run.png)

    If another administrator in your organization is already managing Azure resources in Privileged Identity Management, you see a list of the resources that are currently being managed.

    ![Screenshot of the Discover resources pane listing resources that are currently being managed.](media/pim-resource-roles-discover-resources/discover-resources.png)
3. Select **Discover resources** to launch the discovery experience.

    ![Screenshot showing the discovery pane lists resources that can be managed, such as subscriptions and management groups](media/pim-resource-roles-discover-resources/discovery-pane.png)
4. On the **Discovery** page, use **Resource state filter** and **Select resource type** to filter the management groups or subscriptions you have write permission to. It's probably easiest to start with **All** initially.

    You can search for and select management group or subscription resources to manage in Privileged Identity Management. When you manage a management group or a subscription in Privileged Identity Management, you can also manage its child resources.

    Note

    When you add a new child Azure resource to a PIM-managed management group, you can bring the child resource under management by searching for it in PIM.
5. Select any unmanaged resources that you want to manage.
6. Select **Manage resource** to start managing the selected resources. The PIM service principal (MS-PIM) is assigned as User Access Administrator on the resource.

    Note

    Once a management group or subscription is managed, it can't be unmanaged. This prevents another resource administrator from removing Privileged Identity Management settings.

    ![Discovery pane with a resource selected and the Manage resource option highlighted](media/pim-resource-roles-discover-resources/discovery-manage-resource.png)
7. If you see a message to confirm the onboarding of the selected resource for management, select **Yes**. PIM will then be configured to manage all the new and existing child objects under the resource.

    ![Screenshot showing a Message confirming to onboard the selected resources for management.](media/pim-resource-roles-discover-resources/discovery-manage-resource-message.png)