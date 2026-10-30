---
layout: Conceptual
title: Validate rules for dynamic membership groups - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/groups-dynamic-rule-validation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how to test members against a rule for dynamic membership groups in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2024-12-19T00:00:00.0000000Z
ms.reviewer: yukarppa
ms.custom: it-pro
locale: en-us
document_id: 16bafb84-ba6f-71f3-c674-2a1a9cba6f83
document_version_independent_id: f00b8319-0e21-c357-644c-dc68bd7751c9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/groups-dynamic-rule-validation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/groups-dynamic-rule-validation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/groups-dynamic-rule-validation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a7e4100a-ec62-0152-d3b9-75b1744f7d6a
---

# Validate rules for dynamic membership groups - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra ID provides the means to validate rules for dynamic membership groups. On the **Validate rules** tab, you can validate a rule against sample group members to confirm that the rule is working as expected.

When you create or update rules for dynamic membership groups, you want to know whether a user or a device is a member of the group. This knowledge helps you evaluate whether a user or device meets the rule criteria. It also helps you troubleshoot when membership isn't expected.

## Prerequisites

To evaluate the rule for dynamic membership groups, the administrator must be at least a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).

Warning

Assigning one of the required roles via indirect role assignment isn't supported.

## Validate a rule for dynamic membership groups

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a Groups Administrator.
2. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
3. Select an existing dynamic group or create a new dynamic group, and then select **Dynamic membership rules**.

    ![Screenshot of selections for viewing details of dynamic membership rules.](media/groups-dynamic-rule-validation/validate-tab.png)
4. On the **Validate Rules** tab, select users to validate their memberships. You can select 20 users or devices at one time.

    ![Screenshot of the button for adding users in the process of validating a rule.](media/groups-dynamic-rule-validation/validate-tab-add-users.png)
5. After you finish selecting users or devices, choose **Select**. Validation automatically starts. The validation results show whether a user is a member of the group or not.

    ![Screenshot that shows the results of rule validation.](media/groups-dynamic-rule-validation/validate-tab-results.png)
6. If the rule isn't valid or if there's a network problem, the results show **Unknown**. If the value is **Unknown**, select **View details**. The detailed error message describes the problem and the necessary actions.

    ![Screenshot that shows detailed results of rule validation.](media/groups-dynamic-rule-validation/validate-tab-view-details.png)
7. You can modify the rule to trigger a new validation of memberships. To see why a user isn't a member of the group, select **View details**. Verification details show the result of each expression that composes the rule. Select **OK** to close the details.