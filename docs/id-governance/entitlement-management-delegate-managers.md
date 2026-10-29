---
layout: Conceptual
title: Delegate access governance to access package managers in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-delegate-managers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to delegate access governance from IT administrators to access package managers and project managers so that they can manage access themselves.
editor: markwahl-msft
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2024-07-15T00:00:00.0000000Z
ms.reviewer: mwahl
locale: en-us
document_id: acccbc4c-b763-c203-3361-16a84e103379
document_version_independent_id: 4f0fde66-e215-a47e-a663-169bb68207eb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-delegate-managers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-delegate-managers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-delegate-managers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 6f27ce72-b2e8-8962-cf9c-fbbd71572570
---

# Delegate access governance to access package managers in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

To delegate the creation and management of access packages in a catalog, you add users to the access package manager role. Access package managers must be familiar with the need for users to request access to resources in a catalog. For example, if a catalog is used for a project, then a project lead might be an access package manager for that catalog. Access package managers can't add resources to a catalog, but they can manage the access packages and policies in a catalog. When delegating to an access package manager, that person can then be responsible for:

- What roles a user has to the resources in a catalog
- Who will need access
- Who needs to approve the access requests
- How long the project lasts

They can create access packages and policies, including policies referencing existing [connected organizations](entitlement-management-organization). Once their access packages are created, then they can have other users request or be assigned to those access packages.

This video provides an overview of how to delegate access governance from catalog owner to access package manager.

In addition to the catalog owner and access package manager roles, you can also add users to the catalog reader role, which provides view-only access to the catalog, or to the access package assignment manager role, which enables the users to change assignments but not access packages or policies.

## As a catalog owner, delegate to an access package manager

Follow these steps to assign a user to the access package manager role:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner.
2. Browse to **ID Governance** &gt; **Catalogs**.
3. On the Catalogs page, open the catalog you want to add administrators to.
4. In the left menu, select **Roles and administrators**.

    ![Catalogs roles and administrators](media/entitlement-management-shared/catalog-roles-administrators.png)
5. Select **Add access package managers** to select the members for these roles.
6. Select **Select** to add these members.

## Remove an access package manager

Follow these steps to remove a user from the access package manager role:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner.
2. Browse to **ID Governance** &gt; **Catalogs**.
3. On the Catalogs page, open the catalog you want to add administrators to.
4. In the left menu, select **Roles and administrators**.
5. Add a checkmark next to an access package manager you want to remove.
6. Select **Remove**.