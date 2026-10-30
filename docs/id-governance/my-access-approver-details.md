---
layout: Conceptual
title: Configure Requestor Visibility of Approver Details - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/my-access-approver-details
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to configure whether requestors can see approver details for pending access package requests in the My Access portal at the tenant or package level.
ms.topic: how-to
ms.date: 2026-06-17T00:00:00.0000000Z
ms.reviewer: owinfrey
locale: en-us
document_id: 3f3c8f6e-aff3-070e-537d-33fb3efeb656
document_version_independent_id: 3f3c8f6e-aff3-070e-537d-33fb3efeb656
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/my-access-approver-details.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/my-access-approver-details
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/my-access-approver-details.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e57d79eb-b346-dbcb-bca8-005965d1ac1b
---

# Configure Requestor Visibility of Approver Details - Microsoft Entra ID Governance | Microsoft Learn

Note

This feature will be widely available beginning in September 2025.

Admins can control whether requestors see approver details for pending access package requests in the [My Access](https://myaccess.microsoft.com) portal. You can set this option at the access package level, or at the tenant level (default for all packages). The access package setting overrides the tenant setting when explicitly set to Yes or No.

## Tenant-level setting (applies to all access packages by default)

Use this setting to define the default behavior for all access packages in your tenant. This setting applies to **members only** and can be overridden by the access package-level setting.

1. In the Microsoft Entra admin center, go to **Identity Governance** &gt; **Entitlement management** &gt; **Control configurations**.
2. Under **My Access settings for end users**, find **Show approver details to members on pending access package requests.**
3. Choose the desired behavior:

    - **Checked** – All members (excluding guests) will see their approver’s name and email address on pending access package requests in My Access.
    - **Unchecked** – Members won’t see approver details by default.
4. Select **Save**.

Note

- The tenant setting applies to all access packages by default but can be overridden on a per-package basis via Advanced request settings.
- To show approver details to guests and connected organization users, set the access package-level setting to Yes.