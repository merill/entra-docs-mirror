---
layout: Conceptual
title: Audit activity history for group assignments in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/groups-audit
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: View activity and audit activity history for group assignments in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: sfi-image-nochange
locale: en-us
document_id: dc32d928-d9e6-3270-3da1-002f2d0fa125
document_version_independent_id: 98cb3ede-b0ad-ee32-7aa7-0399bbbcf15f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/groups-audit.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/groups-audit
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/groups-audit.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3e16912f-ad2c-a3b0-f302-e941831f2cc7
---

# Audit activity history for group assignments in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn

## Overview

When working with your organization's groups in Privileged Identity Management (PIM), you can view activity, activations, and audit history for Microsoft Entra group membership or ownership changes.

Note

If your organization has outsourced management functions to a service provider who uses [Azure Lighthouse](/en-us/azure/lighthouse/overview), role assignments authorized by that service provider won't be shown here.

Follow these steps to view the audit history for groups in Privileged Identity Management.

## View resource audit history

**Resource audit** gives you a view of all activity associated with groups in PIM.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Groups**.
3. Select the group you want to view audit history for.
4. Select **Resource audit**.

    [![Screenshot of where to select Resource audit.](media/pim-for-groups/pim-group-19.png)](media/pim-for-groups/pim-group-19.png#lightbox)
5. Filter the history using a predefined date or custom range.

## View my audit

**My audit** enables you to view your personal role activity for groups in PIM.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Groups**.
3. Select the group you want to view audit history for.
4. Select **My audit**.

    [![Screenshot of where to select My audit.](media/pim-for-groups/pim-group-20.png)](media/pim-for-groups/pim-group-20.png#lightbox)
5. Filter the history using a predefined date or custom range.