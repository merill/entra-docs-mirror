---
layout: Conceptual
title: Perform an access review of Azure resource and Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-perform-roles-and-resource-roles-review
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to review access of Azure resource and Microsoft Entra roles in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.custom: pim
locale: en-us
document_id: ffaca0d4-06ac-5130-f692-13ada81ad4e3
document_version_independent_id: 30182913-7bb0-c62a-3495-cd27cbfac187
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-perform-roles-and-resource-roles-review.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-perform-roles-and-resource-roles-review
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-perform-roles-and-resource-roles-review.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: aedee303-974d-71bf-c4c7-2608e563225d
---

# Perform an access review of Azure resource and Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Privileged Identity Management (PIM) simplifies how enterprises manage privileged access to resources in Microsoft Entra ID, and other Microsoft online services like Microsoft 365 or Microsoft Intune. Follow the steps in this article to perform reviews of access to roles.

If you're assigned to an administrative role, your organization's Privileged Role Administrator may ask you to regularly confirm that you still need that role for your job. You might get an email that includes a link, or you can go straight to the [Microsoft Entra admin center](https://entra.microsoft.com) and begin.

If you're at least a Privileged Role Administrator interested in access reviews, get more details at [How to start an access review](pim-create-roles-and-resource-roles-review).

## Approve or deny access

You can approve or deny access based on whether the user still needs access to the role. Choose **Approve** if you want them to stay in the role, or **Deny** if they don't need the access anymore. The users' assignment status doesn't change until the review closes and the administrator applies the results. Common scenarios in which certain denied users can't have results applied to them might include the following:

- **Reviewing members of a synced on-premises Windows AD group**: If the group is synced from an on-premises Windows AD, the group can't be managed in Microsoft Entra ID, and therefore membership can't be changed.
- **Reviewing a role with nested groups assigned**: For users who have membership through a nested group, the access review doesn't remove their membership to the nested group and therefore they retain access to the role being reviewed.
- **User not found or other errors**: These might also result in an apply result not being supported.

Follow these steps to find and complete the access review:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Review access**.
3. If you have any pending access reviews, they appear in the access reviews page.

    [![Screenshot of Privileged Identity Management application, with Review access pane selected for Microsoft Entra roles.](media/pim-perform-azure-ad-roles-and-resource-roles-review/rbac-access-review-azure-ad-complete.png)](media/pim-perform-azure-ad-roles-and-resource-roles-review/rbac-access-review-azure-ad-complete.png#lightbox)
4. Select the review you want to complete.
5. Choose **Approve** or **Deny**. In the **Provide a reason box**, enter a business justification for your decision as needed.

    [![Screenshot of Privileged Identity Management application, with the selected Access Review for Microsoft Entra roles.](media/pim-perform-azure-ad-roles-and-resource-roles-review/rbac-access-review-azure-ad-completed.png)](media/pim-perform-azure-ad-roles-and-resource-roles-review/rbac-access-review-azure-ad-completed.png#lightbox)