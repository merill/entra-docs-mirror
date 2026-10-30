---
layout: Conceptual
title: App consent permissions for custom roles in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/custom-consent-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: App consent permissions for custom Microsoft Entra roles in the Microsoft Entra admin center, PowerShell, or Graph API.
ms.topic: overview
ms.date: 2025-03-30T00:00:00.0000000Z
ms.reviewer: psignoret
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done
locale: en-us
document_id: d2dd7b19-7c4b-3349-6810-2a9834570b62
document_version_independent_id: 732d7b03-7f42-2cff-449b-a05ee1bfd9a9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/custom-consent-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/custom-consent-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/custom-consent-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 42dc2032-0d3c-b6b7-68ca-d712c86b4c94
---

# App consent permissions for custom roles in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article contains the currently available app consent permissions for custom role definitions in Microsoft Entra ID. In this article, you'll find the permissions required for some common scenarios related to app consent and permissions.

## License requirements

Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## App consent permissions

Use the permissions listed in this article to manage app consent policies, as well as the permission to grant consent to apps.

Note

The Microsoft Entra admin center does not yet support adding the permissions listed in this article to a custom role definition. You must [use Microsoft Graph PowerShell to create a custom role](custom-create) with the permissions listed in this article.

#### Granting delegated permissions to apps on behalf of self (user consent)

To allow users to grant consent to applications on behalf of themselves (user consent), subject to an app consent policy.

- microsoft.directory/servicePrincipals/managePermissionGrantsForSelf.{id}

Where `{id}` is replaced by the ID of an [app consent policy](../enterprise-apps/manage-app-consent-policies) which will set the conditions which must be met for this permission to be active.

For example, to allow users to grant consent on their own behalf, subject to the built-in app consent policy with ID `microsoft-user-default-low`, you would use the permission `...managePermissionGrantsForSelf.microsoft-user-default-low`.

#### Granting permissions to apps on behalf of all (admin consent)

To delegate tenant-wide admin consent to apps, for both delegated permissions and application permissions (app roles):

- microsoft.directory/servicePrincipals/managePermissionGrantsForAll.{id}

Where `{id}` is replaced by the ID of an [app consent policy](../enterprise-apps/manage-app-consent-policies) which will set the conditions which must be met for this permission to be usable.

For example, to allow role assignees to grant tenant-wide admin consent to apps subject to a custom [app consent policy](../enterprise-apps/manage-app-consent-policies) with ID `low-risk-any-app`, you would use the permission `microsoft.directory/servicePrincipals/managePermissionGrantsForAll.low-risk-any-app`.

#### Managing app consent policies

To delegate the creation, update and deletion of [app consent policies](../enterprise-apps/manage-app-consent-policies).

- microsoft.directory/permissionGrantPolicies/create
- microsoft.directory/permissionGrantPolicies/standard/read
- microsoft.directory/permissionGrantPolicies/basic/update
- microsoft.directory/permissionGrantPolicies/delete

## Full list of permissions

| Permission | Description |
| --- | --- |
| microsoft.directory/servicePrincipals/managePermissionGrantsForSelf.{id} | Grants the ability to consent to apps on behalf of self (user consent), subject to app consent policy `{id}`. |
| microsoft.directory/servicePrincipals/managePermissionGrantsForAll.{id} | Grants the permission to consent to apps on behalf of all (tenant-wide admin consent), subject to app consent policy `{id}`. |
| microsoft.directory/permissionGrantPolicies/standard/read | Read standard properties of permission grant policies |
| microsoft.directory/permissionGrantPolicies/basic/update | Update basic properties of permission grant policies |
| microsoft.directory/permissionGrantPolicies/create | Create permission grant policies |
| microsoft.directory/permissionGrantPolicies/delete | Delete permission grant policies |