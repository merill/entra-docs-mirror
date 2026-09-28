---
layout: Conceptual
title: Start using PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-getting-started
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to enable and get started using Privileged Identity Management (PIM) in the Microsoft Entra admin center.
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: pim, sfi-ga-nochange
locale: en-us
document_id: f720f767-871a-b92b-0efa-e0e35d3ccca8
document_version_independent_id: ee84f58e-7791-40cf-9b38-1d5b416303af
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-getting-started.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-getting-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-getting-started.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bbb9c816-bb69-af67-ac31-73386f4dc3dc
---

# Start using PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Use Privileged Identity Management (PIM) to manage, control, and monitor access within your Microsoft Entra organization. With PIM you can provide as-needed and just-in-time access to Azure resources, Microsoft Entra resources, and other Microsoft online services like Microsoft 365 or Microsoft Intune.

This article describes how to enable Privileged Identity Management (PIM) and get started using it.

## Prerequisites

To use Privileged Identity Management, you must have a Microsoft Entra ID P2 or Microsoft Entra ID Governance license. For more information on licensing, see [Microsoft Entra ID Governance licensing fundamentals](../licensing-fundamentals).

## Activation of role assignments

When a Microsoft Entra tenant has a Microsoft Entra ID P2 or Microsoft Entra ID Governance license, users with active role assignments can do the following:

- Open the **Roles and administrators** page in Microsoft Entra ID and select a role.
- Open the **Privileged Identity Management** page.
- Make calls to PIM using the [Microsoft Entra roles API](/en-us/graph/identity-network-access-overview/).

Microsoft Entra enables PIM for the tenant in the following ways:

- Starting immediately, you can create eligible or time-bound assignments for Microsoft Entra roles;
- Global Administrators or Privileged Role Administrators may start receiving other emails, such as the PIM weekly digest;
- The PIM service principal name (MS–PIM) may get mentioned in audit log events related to role assignment management.

These behaviors are expected and shouldn't affect your workflows.

## Prepare PIM for Microsoft Entra roles

Here are the recommended tasks to prepare Privileged Identity Management to manage Microsoft Entra roles:

1. [Configure Microsoft Entra role settings](pim-how-to-change-default-settings)
2. [Give eligible assignments](pim-how-to-add-role-to-user)
3. [Allow eligible users to activate their Microsoft Entra role just-in-time](pim-how-to-activate-role)

## Prepare PIM for Azure roles

Here are the recommended tasks to prepare Privileged Identity Management to manage Azure roles for a subscription:

1. [Discover Azure resources](pim-resource-roles-discover-resources)
2. [Configure Azure role settings](pim-resource-roles-configure-role-settings)
3. [Give eligible assignments](pim-resource-roles-assign-roles)
4. [Allow eligible users to activate their Azure roles just-in-time](pim-resource-roles-activate-your-roles)

## Navigate to your tasks

Once Privileged Identity Management is set up, you can learn your way around.

[![Screenshot showing the navigation window in Privileged Identity Management showing Tasks, Manage, Activity, and Troubleshooting + Support options.](media/pim-getting-started/pim-quickstart-tasks.png)](media/pim-getting-started/pim-quickstart-tasks.png#lightbox)

| Menu item | Description |
| --- | --- |
| **My roles** | Displays a list of eligible and active roles assigned to you. **My roles** is where you can activate any assigned eligible roles. |
| **My requests** | Displays your pending requests to activate eligible role assignments. |
| **Approve requests** | Displays a list of requests to activate eligible roles by users in your directory that you can approve. |
| **Review access** | Lists active access reviews you're assigned to complete, whether you're reviewing access for yourself or someone else. |
| **Microsoft Entra roles** | Displays a dashboard and settings for Privileged Role Administrators to manage Microsoft Entra role assignments. This dashboard is disabled for anyone who isn't a Privileged Role Administrator. These users have access to a special dashboard titled **My view**. The **My view** dashboard only displays information about the user accessing the dashboard, not the entire organization. |
| **Groups** | Manage just-in-time membership in the group or just-in-time ownership of the group. Groups can be used to provide access to Microsoft Entra roles, Azure roles, and various other scenarios. To manage a Microsoft Entra group in PIM, you must bring it under management in PIM. |
| **Azure resources** | Displays a dashboard and settings for Privileged Role Administrators to manage Azure resource role assignments. This dashboard is disabled for anyone who isn't a Privileged Role Administrator. These users have access to a special dashboard titled **My view**. The **My view** dashboard only displays information about the user accessing the dashboard, not the entire organization. |
| **My audit history** | View your PIM audit history, including all role activations and assignments. |
| **Troubleshoot** | Get help diagnosing and resolving common PIM issues. |
| **New support request** | Create a support request for PIM-related issues. |