---
layout: Conceptual
title: Resource dashboards for access reviews in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-resource-roles-overview-dashboards
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Describes how to use a resource dashboard to perform an access review in Microsoft Entra Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: pim
locale: en-us
document_id: ff7b03fc-e485-c395-b26d-73ba1d3dfe89
document_version_independent_id: 3b42cf62-c730-4828-a699-e2e397b226be
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-resource-roles-overview-dashboards.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-resource-roles-overview-dashboards
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-resource-roles-overview-dashboards.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6a744f2c-d12e-5ba9-5b4c-a1140350227b
---

# Resource dashboards for access reviews in PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

You can use a resource dashboard to perform an access review in Privileged Identity Management (PIM). The Admin View dashboard in Microsoft Entra ID, part of Microsoft Entra, has three primary components:

- A graphical representation of resource role activations.
- Charts that display the distribution of role assignments by assignment type.
- A data area containing information about new role assignments.

![Screenshot of the Admin View dashboard, showing graphs and charts.](media/pim-resource-roles-overview-dashboards/rbac-overview-top.png)

![Screenshot of the Admin View dashboard, showing data lists.](media/pim-resource-roles-overview-dashboards/role-settings.png)

The graphical representation of resource role activations covers the past seven days. This data is scoped to the selected resource, and displays activations for the most common roles (Owner, Contributor, User Access Administrator), and for all roles combined.

On one side of the activations graph, two charts display the distribution of role assignments by assignment type, for both users and groups. You can change the value to a percentage (or vice versa), by selecting a slice of the chart.

Below the charts are listed the number of users and groups with new role assignments over the last 30 days, and roles sorted by total assignments in descending order.