---
layout: Conceptual
title: Update a governance relationship - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-update-governance-relationship
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to update an existing governance relationship between a governing and governed tenant in Microsoft Entra Tenant Governance
ms.topic: how-to
ms.date: 2026-03-10T00:00:00.0000000Z
locale: en-us
document_id: c5e5386f-774d-8fe6-eb12-2d906051a517
document_version_independent_id: c5e5386f-774d-8fe6-eb12-2d906051a517
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-update-governance-relationship.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-update-governance-relationship
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-update-governance-relationship.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8a843513-5bc9-2111-bd8c-08590e52cf44
---

# Update a governance relationship - Microsoft Entra ID Governance | Microsoft Learn

This article describes how to update an existing governance relationship between a governing tenant and a governed tenant. You might need to update a governance relationship to add or modify delegated administration roles or multitenant application configurations.

## Prerequisites

- You must have an active governance relationship between a governing tenant and a governed tenant.
- You must have access to the governance policy template you used to create the existing relationship. If you deleted the policy template, you need to create a new relationship.
- You need the **Tenant Governance Administrator** role.
- Review license requirements for sending governance requests in [Microsoft Entra licensing](../../fundamentals/licensing#microsoft-entra-tenant-governance).

## Update the governance policy template

Before you can update a governance relationship, you must first modify the governance policy template you used to establish the existing relationship. When you update the template, its version number automatically increments by one.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the governing tenant.
2. Browse to **Tenant Governance** &gt; **Templates**, and select the policy template you used to set up the relationship.
3. Modify the template as needed. Update one or more of these configurations:

    - **Delegated administration roles**: Add or change the Microsoft Entra built-in roles assigned to security groups in the governing tenant. These roles determine the access level that users in those groups have when they sign in to the governed tenant.
    - **Multitenant application management**: Add or update custom, multitenant applications. When you update the relationship, Tenant Governance creates or updates a service principal with the corresponding permissions in the governed tenant.
4. Save the updated governance policy template. The version number of the template increments by one.

Note

Updating the governance policy template doesn't automatically update the governance relationship. The tenant admins must complete the governance request and approval process described in the sections that follow for the policy template changes to take effect.

## Send a new governance request with the updated template

After updating the governance policy template, send a new governance request from the governing tenant to the governed tenant using the updated template.

1. In the governing tenant, create a new governance request.
2. Select the governed tenant that has the existing relationship you want to update.
3. Select the updated governance policy template.
4. Submit the governance request. The governed tenant receives an email notification about the new governance request.

## Accept the governance request

An admin in the governed tenant must accept the governance request to complete the update.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a **Tenant Governance Administrator** in the governed tenant.
2. Browse to **Tenant Governance** &gt; **Received requests**.
3. Review the updated governance request, including the changes in the policy template.
4. Accept the governance request. The system updates the existing governance relationship with the new policy template configuration. The governing tenant receives an email confirming the accepted request and the updated governance relationship.

When the governed tenant accepts the governance request, these changes take effect:

- Tenant Governance updates the policy snapshot of the existing governance relationship to reflect the latest version of the policy template.
- If you updated delegated administration roles, Tenant Governance updates the GDAP role assignments in the governed tenant accordingly.
- If you updated multitenant application management, Tenant Governance updates the corresponding service principal and its permissions in the governed tenant.