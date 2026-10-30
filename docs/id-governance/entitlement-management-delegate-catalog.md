---
layout: Conceptual
title: Delegate access governance to catalog creators in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-delegate-catalog
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to delegate access governance from IT administrators to catalog creators and project managers so that they can manage access themselves.
editor: markwahl-msft
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-03-10T00:00:00.0000000Z
ms.reviewer: mwahl
ms.custom: sfi-image-nochange
locale: en-us
document_id: c41a43cf-7468-4524-c0e2-fda8fc7d81b6
document_version_independent_id: 2e825df4-2597-1dd9-6a6c-017b3e1ce993
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-delegate-catalog.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-delegate-catalog
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-delegate-catalog.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 20d71443-9b32-d366-5857-f2eef7daac54
---

# Delegate access governance to catalog creators in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

A catalog is a container of resources and access packages. You create a catalog when you want to group related resources and access packages. By default the role Identity Governance Administrator is the least privileged role that can [create a catalog](entitlement-management-catalog-create), and can add other users as catalog owners as an even further least privilege option.

Note

Following least privilege access, it is recommended to use the Identity Governance Administrator role when possible in entitlement management.

There are three ways an organization can delegate with catalogs:

- When getting started in a pilot project, Identity Governance Administrators can [create](entitlement-management-catalog-create) and manage the catalog. Later, when moving from pilot to production, they could delegate a catalog by [assigning nonadministrators as owners to the catalog](entitlement-management-catalog-create#add-more-catalog-owners), so that those users could maintain the policies going forward.
- If there are resources that don't have owners, then administrators can create catalogs, add those resources to each catalog, and then [assign nonadministrators as owners to a catalog](entitlement-management-catalog-create#add-more-catalog-owners). This allows users who aren't administrators and aren't resource owners to manage their own access policies for those resources.
- If resources have owners, then administrators can assign a collection of users, such as an `All Employees` dynamic group, to the catalog creators role, so a user who are in that group and own resources can create a catalog for their own resources.

This article illustrates how to delegate to users who aren't administrators, so that they can create their own catalogs. You can add those users to the Microsoft Entra entitlement management-defined catalog creator role. You can add individual users, or you can add a group whose members are then able to create catalogs. After you create a catalog, you can add resources they own to their catalog. They can create access packages and policies, including policies referencing existing [connected organizations](entitlement-management-organization).

If you have existing catalogs to delegate, then continue at the [create and manage a catalog of resources](entitlement-management-catalog-create#add-more-catalog-owners) article.

## As an IT administrator, delegate to a catalog creator

Follow these steps to assign a user to the catalog creator role.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **settings**.
3. Select **Edit**.

    ![Settings to add catalog creators](media/entitlement-management-delegate-catalog/settings-delegate.png)
4. In the **Delegate entitlement management** section, select **Add catalog creators** to select the users or groups that you want to delegate this entitlement management role to.
5. Select **Select**.
6. Select **Save**.

## Allow delegated roles to access the Microsoft Entra admin center

To allow delegated roles, such as catalog creators and access package managers, to access the Microsoft Entra admin center to manage access packages, you should check the administration portal setting.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **Entra ID** &gt; **Users** &gt; **User settings**.
3. Make sure **Restrict access to Microsoft Entra administration portal** is set to **No**.

    ![Microsoft Entra user settings - Administration portal](media/entitlement-management-delegate-catalog/user-settings.png)

## Manage role assignments programmatically

You can also view and update catalog creators and entitlement management catalog-specific role assignments using Microsoft Graph. A user in an appropriate role with an application that has the delegated `EntitlementManagement.ReadWrite.All` permission can call the Graph API to [list the role definitions](/en-us/graph/api/rbacapplication-list-roledefinitions) of entitlement management, and [list role assignments](/en-us/graph/api/rbacapplication-list-roleassignments) to those role definitions.

To retrieve a list of the users and groups assigned to the catalog creators role, the role with definition ID `ba92d953-d8e0-4e39-a797-0cbedb0a89e8`, use the Graph query:

```http
GET https://graph.microsoft.com/v1.0/roleManagement/entitlementManagement/roleAssignments?$filter=roleDefinitionId eq 'ba92d953-d8e0-4e39-a797-0cbedb0a89e8'&$expand=principal
```