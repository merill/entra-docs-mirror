---
layout: Conceptual
title: Microsoft Entra roles Discovery and insights (preview) in Privileged Identity Management former Security Wizard - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-security-wizard
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Discovery and insights (formerly Security Wizard) help you convert permanent Microsoft Entra role assignments to just-in-time assignments with Privileged Identity Management.
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: pim, H1Hack27Feb2017, sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: 35205d31-e185-704a-9adb-58302cfe0f59
document_version_independent_id: b621d6e3-30b6-f56d-bb3f-c6c8e54a13ee
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-security-wizard.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-security-wizard
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-security-wizard.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8c51d61e-7c8f-0241-b6d1-8a5ac05f51e1
---

# Microsoft Entra roles Discovery and insights (preview) in Privileged Identity Management former Security Wizard - Microsoft Entra ID Governance | Microsoft Learn

## Overview

If you're starting out using Privileged Identity Management (PIM) in Microsoft Entra ID to manage role assignments in your organization, you can use the **Discovery and insights (preview)** page to get started. This feature shows you who is assigned to privileged roles in your organization and how to use PIM to quickly change permanent role assignments into just-in-time assignments. You can view or make changes to your permanent privileged role assignments in **Discovery and insights (preview)**. It's an analysis tool and an action tool.

## Discovery and insights (preview)

Before your organization starts using Privileged Identity Management, all role assignments are permanent. Users are always in their assigned roles even when they don't need their privileges. Discovery and insights (preview), which replaces the former Security Wizard, shows you a list of privileged roles and how many users are currently in those roles. You can list out assignments for a role to learn more about the assigned users if one or more of them are unfamiliar.

✔️ Microsoft recommends that organizations have two cloud-only emergency access accounts permanently assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role. These accounts are highly privileged and aren't assigned to specific individuals. The accounts are limited to emergency or "break glass" scenarios where normal accounts can't be used or all other administrators are accidentally locked out. These accounts should be created following the [emergency access account recommendations](/en-us/entra/identity/role-based-access-control/security-emergency-access).

Also, keep role assignments permanent if a user has a Microsoft account (in other words, an account they use to sign in to Microsoft services like Skype, or Outlook.com). If you require multifactor authentication for a user with a Microsoft account to activate a role assignment, the user is locked out.

## Open Discovery and insights (preview)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Microsoft Entra roles** &gt; **Discovery and insights (preview)**.
3. Opening the page begins the discovery process to find relevant role assignments.

    ![Screenshot showing Microsoft Entra roles Discovery and insights page.](media/pim-security-wizard/new-preview-link.png)
4. Select **Reduce Global Administrators**.

    ![Screenshot that shows the Discovery and insights (Preview) with the Reduce Global Administrators action selected.](media/pim-security-wizard/new-preview-page.png)
5. Review the list of Global Administrator role assignments.

    ![Screenshot showing the Roles pane showing all Global Administrators.](media/pim-security-wizard/new-global-administrator-list.png)
6. Select **Next** to select the users or groups you want to make eligible, and then select **Make eligible** or **Remove assignment**.

    ![Screenshot showing how to convert members to eligible page with options to select members you want to make eligible for roles.](media/pim-security-wizard/new-global-administrator-buttons.png)
7. Optionally, require all Global Administrators to review their own access.

    ![Screenshot showing the Global Administrators page showing the access reviews section.](media/pim-security-wizard/new-global-administrator-access-review.png)
8. After you select any of these changes, you'll see an Azure notification.
9. Select **Eliminate standing access** or **Review service principals** to repeat the above steps on other privileged roles and on service principal role assignments. For service principal role assignments, you can only remove role assignments.

    ![Screenshot showing additional insights options to eliminate standing access and review service principals.](media/pim-security-wizard/new-preview-page-service-principals.png)