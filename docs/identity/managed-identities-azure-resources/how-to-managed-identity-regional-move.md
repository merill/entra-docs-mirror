---
layout: Conceptual
title: Move managed identities to another region - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/how-to-managed-identity-regional-move
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Steps involved in getting a managed identity recreated in another region
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2023-05-25T00:00:00.0000000Z
ms.custom: subject-moving-resources
locale: en-us
document_id: ded63343-e92a-4c2c-aa81-7ae2d724da02
document_version_independent_id: cc35513c-7e44-2ac3-4b00-4c6018efeb61
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/how-to-managed-identity-regional-move.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/how-to-managed-identity-regional-move
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/how-to-managed-identity-regional-move.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: d330e24e-d096-374d-a293-5e3e3e10575a
---

# Move managed identities to another region - Managed identities for Azure resources | Microsoft Learn

There are situations in which you'd want to move your existing user-assigned managed identities from one region to another. For example, you may need to move a solution that uses user-assigned managed identities to another region. You may also want to move an existing identity to another region as part of disaster recovery planning, and testing.

Moving User-assigned managed identities across Azure regions isn't supported. You can however, recreate a user-assigned managed identity in the target region.

## Prerequisites

- Permissions to list permissions granted to existing user-assigned managed identity.
- Permissions to grant a new user-assigned managed identity the required permissions.
- Permissions to assign a new user-assigned identity to the Azure resources.
- Permissions to edit Group membership, if your user-assigned managed identity is a member of one or more groups.

## Prepare and move

1. Copy user-assigned managed identity assigned permissions. You can list [Azure role assignments](/en-us/azure/role-based-access-control/role-assignments-list-powershell) but that may not be enough depending on how permissions were granted to the user-assigned managed identity. You should confirm that your solution doesn't depend on permissions granted using a service specific option.
2. Create a [new user-assigned managed identity](how-manage-user-assigned-managed-identities?pivots=identity-mi-methods-powershell#create-a-user-assigned-managed-identity-2) at the target region.
3. Grant the managed identity the same permissions as the original identity that it's replacing, including Group membership. You can review [Assign Azure roles to a managed identity](/en-us/azure/role-based-access-control/role-assignments-portal-managed-identity), and [Group membership](/en-us/entra/fundamentals/how-to-manage-groups).
4. Specify the new identity in the properties of the resource instance that uses the newly created user assigned managed identity.

## Verify

After reconfiguring your service to use your new managed identities in the target region, you need to confirm that all operations have been restored.

## Clean up

Once that you confirm your service is back online, you can proceed to delete any resources in the source region that you no longer use.