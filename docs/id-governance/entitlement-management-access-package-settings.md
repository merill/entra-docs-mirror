---
layout: Conceptual
title: Share link to request an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-access-package-settings
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to share link to request an access package in entitlement management.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-06-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5a3b8b61-463f-e439-a894-4c67977a57f1
document_version_independent_id: ff886517-c264-6e49-dbd2-c0a6388f4428
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-access-package-settings.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-access-package-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-access-package-settings.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 8a4ec78b-6655-996b-413a-a74cdc62d081
---

# Share link to request an access package in entitlement management - Microsoft Entra ID Governance | Microsoft Learn

This article explains how to share a link for a specific access package that will direct a user straight into the access package request flow in the My Access portal, skipping the need for the user to locate and select the access package within the My Access portal.

When you create access packages, they're discoverable by default. This means that if a policy allows a user to request the access package, they'll automatically see the access package listed in their My Access portal. However, You can also change the Hidden setting so that the access package isn't listed in the user's My Access portal. Users can only view hidden access packages if they have the direct My Access portal link mentioned in this article. For more details please refer to, [hide or delete access package in entitlement management](entitlement-management-access-package-edit).

A user will only see the access packages from a given tenant in their My Access portal. The link outlined in this article includes a tenant hint which ensures the My Access portal loads for the correct tenant. If users are accessing the My Access portal without a tenant hint in their URL, they can also use the organization/tenant switcher which is located on the top right of the My Access portal.

For the external user from another tenant to use the My Access portal link to request the access package, the catalog for the access package must be [enabled for external users](entitlement-management-catalog-create) and there must be a [policy for the external user's directory](entitlement-management-access-package-request-policy) in the access package.

## Share link to request an access package

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and the Access package manager.
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. On the **Access packages** page, open the access package you want to share a link to request an access package for.
4. On the Overview page, check the **Hidden** setting. If the **Hidden** setting is **Yes**, then even users who don't have the My Access portal link can browse and request the access package. If you don't wish to have them browse for the access package, then change the setting to **No**.
5. On the Overview page, copy the **My Access portal link**.

    ![Access package overview - My Access portal link](media/entitlement-management-shared/my-access-portal-link.png)

    It's important that you copy the entire My Access portal link when sending it to an internal business partner. This ensures that the partner gets access to your directory's portal to make their request. The link starts with `myaccess`, includes a directory hint, and ends with an access package ID. For US Government, the domain in the My Access portal link will be `myaccess.microsoft.us`.

    `https://myaccess.microsoft.com/@<directory_hint>#/access-packages/<access_package_id>`
6. Email or send the link to your external business partner. They can share the link with their users in their organization to request the access package.