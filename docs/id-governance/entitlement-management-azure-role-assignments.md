---
layout: Conceptual
title: Assign Azure Role-based access control (RBAC) Roles - Entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-azure-role-assignments
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Assign Azure RBAC roles to access packages and catalogs in Microsoft Entra Entitlement Management. Learn how to manage access with least privilege principles.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2026-04-07T00:00:00.0000000Z
locale: en-us
document_id: 506e8c4b-d163-7ed9-56aa-28944d273dee
document_version_independent_id: 506e8c4b-d163-7ed9-56aa-28944d273dee
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-azure-role-assignments.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-azure-role-assignments
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-azure-role-assignments.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 3a185826-092d-eef9-67fa-a31942a54351
---

# Assign Azure Role-based access control (RBAC) Roles - Entitlement management - Microsoft Entra ID Governance | Microsoft Learn

Entitlement Management supports access lifecycle for various resource types such as Applications, SharePoint sites, Groups, Teams, and [Microsoft Entra Roles](entitlement-management-roles). To manage access to Azure resources, You can assign access to Azure RBAC roles directly to Access packages and Catalogs.

By assigning Azure RBAC roles to employees, and guests, using Entitlement Management, you can look at an identity's entitlements to quickly determine which Azure roles are assigned to that identity. Following the security principle of [least privilege access](../identity-platform/secure-least-privileged-access), you're able to assign both **Active** and **Eligible** role types allowing privilege to be activated just in time when access to Azure resources are needed.

By assigning Azure resources, administrators can:

- Choose the target scope that aligns with the catalog resource options (Management Group, Subscription, or Resource Group).
- Select eligible or active role type that a user receives when assigned to the access package.
- Select the appropriate Azure RBAC role (supports custom Azure roles and built-in roles). End users who request and are approved, or are assigned, to the access package receive the Azure role assignment automatically.

## Supported Scenarios

| Catalog scope where the resource is added | Access Package scope allowed | What end users can receive |
| --- | --- | --- |
| Management Group | Management Group | Eligible or active Azure roles assigned at the Management Group scope |
| Subscription | Subscription | Eligible or active Azure roles assigned at the Subscription scope |
| Subscription | Resource Group (tied to the subscription) | Eligible or active Azure roles assigned at the Resource Group scope |

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

### Azure RBAC requirements for catalog onboarding

To onboard an Azure Subscription or Management Group into an Entitlement Management catalog, the administrator performing this action must have Azure RBAC permissions that allow role assignment management at that scope.

Specifically, Entitlement Management performs an Azure RBAC check for:

- `Microsoft.Authorization/roleassignments/read`
- `Microsoft.Authorization/roleassignments/write`
- `Microsoft.Authorization/roleassignments/delete`

at the selected Management Group or Subscription. This check ensures that the administrator has sufficient permissions for Entitlement Management to later assign Azure RBAC roles at that scope on behalf of approved access package assignments.

If any of these checks fail, onboarding of the Azure resource into the catalog fails.

### Azure RBAC requirements for adding a role to an access package

After a Subscription or Management Group has been onboarded into a catalog, an Access Package administrator can add Azure RBAC roles at:

- Management Group
- Subscription
- Resource Group (within an onboarded Subscription)

When adding an Azure RBAC role to an access package, Entitlement Management dynamically enumerates available role definitions at the selected assignment scope. As a result, the administrator configuring the access package must have:

- `Microsoft.Authorization/roleDefinitions/read`

at the specific scope selected for role assignment (Management Group, Subscription, or Resource Group) to query role visibility.

## Add an Azure RBAC role to a Catalog

To assign an Azure RBAC role to a catalog within entitlement management, you'd do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator) or [Privileged Role Administrator](../identity/role-based-access-control/permissions-reference#privileged-role-administrator) with Catalog Owner permissions.
2. Browse to **ID Governance** &gt; **Catalogs**.
3. On the Catalogs page, open the catalog you want to add the Azure resource role to and select **Add Resources**.
4. On the add resources page, select **Azure Resources**. ![Screenshot of Azure resources within the available resources on the catalog add resources page.](media/entitlement-management-azure-role-assignments/azure-resources-catalog.png)
5. On the **Select Azure Resources** pane, select either **Subscription** or **Management Group**. ![Screenshot of selecting the Azure resource type.](media/entitlement-management-azure-role-assignments/select-azure-resource-type.png)
6. From the list, select which Azure subscription or management group that you want to add to the catalog. ![Screenshot of list of available Azure subscriptions.](media/entitlement-management-azure-role-assignments/azure-subscription-list.png)
7. With the resource selected, select **Add**. ![screenshot of Azure resource added to catalog.](media/entitlement-management-azure-role-assignments/azure-catalog-selection.png)

## Add an Azure RBAC role to an access package

After you add an Azure resource to a catalog, you're now able to add it as a resource to access packages within that catalog. Azure resources can be added to both new, and existing, access packages. This section walks you through how to add an Azure RBAC role to an existing access package. To add an Azure RBAC role to an existing access package, you'd do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner or Access Package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. Select an existing access package you want to add the Azure RBAC roles to.
4. On the access package overview page, select **Resources**. ![Screenshot of resource role option on an existing access package.](media/entitlement-management-azure-role-assignments/access-package-resource-roles.png)
5. On the add resources page, select **Azure Resources**.
6. On the **Select Azure Resources** pane, select either **Subscription** or **Management Group**. ![Screenshot of selecting the Azure resource type.](media/entitlement-management-azure-role-assignments/select-azure-resource-type.png)
7. From the list, select which Azure subscription or management group that you want to add to the access package. ![Screenshot of list of available Azure subscriptions.](media/entitlement-management-azure-role-assignments/azure-subscription-list.png)
8. If choosing subscription, under Scope, choose where the role assignment applies. ![Screenshot of Azure scope.](media/entitlement-management-azure-role-assignments/azure-scope.png)
9. For **Role Type**, you can select the following types: **Active**: For roles that should be permanently assigned. **Eligible**: For roles that require elevation via [Privileged Identity Management (PIM)](privileged-identity-management/pim-configure) when needed. ![Screenshot of selecting the role type for the Azure role.](media/entitlement-management-azure-role-assignments/azure-role-type.png)
10. Select the Azure RBAC Role to assign. Both built-in roles and Azure Custom roles are available. ![Screenshot of selecting the Azure role.](media/entitlement-management-azure-role-assignments/azure-role-list.png)
11. With the resource selected, select **Add** to add it to the access package.