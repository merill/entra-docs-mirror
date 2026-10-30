---
layout: Conceptual
title: Understand and manage dynamic group processing in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/manage-dynamic-group
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Learn how dynamic group management works.
ms.topic: concept-article
ms.date: 2025-04-08T00:00:00.0000000Z
ms.reviewer: mbhargava
ai-usage: ai-assisted
locale: en-us
document_id: 8be0c533-ce6a-2bec-b9d4-aa658718993b
document_version_independent_id: 8be0c533-ce6a-2bec-b9d4-aa658718993b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/manage-dynamic-group.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/manage-dynamic-group
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/manage-dynamic-group.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ef208121-1b60-4cd7-c5f9-acc2954385c1
---

# Understand and manage dynamic group processing in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

## Overview

Dynamic membership groups in Microsoft Entra ID are a powerful feature that enables administrators to automate the management of group memberships. Changes to memberships are typically processed within a few hours.

However, under certain conditions, customers can experience delays in membership updates. Processing can take more than 24 hours. Understanding the underlying causes can help admins optimize their configurations and avoid unnecessary processing bottlenecks.

## How dynamic group processing works

Dynamic group processing operates in a sequential manner. Changes for a single tenant are evaluated and applied in order, rather than all at once. Large volumes of changes, especially when they affect many users or devices, can lead to long processing queues. The long queues can extend the time required for updates to finish processing.

### Key factors that affect processing time

The three biggest factors that influence processing and can cause membership updates to take longer are:

- **Number of dynamic groups**: Tenants that have a large number of dynamic groups require more evaluations, increasing processing time.
- **Number of object changes**: A high volume of user or device changes can create a long processing queue and extend the processing time. Examples include changes to extension attributes, device additions or removals, and bulk user updates.
- **Rule configuration**: Certain rule configurations can affect processing time. For instance, the choice of inefficient operators like `Match`, `Contains`, or `memberOf` can increase processing time. Rule complexity is also a contributing factor.

Note

Stale devices and inactive user accounts can remain in scope for dynamic membership rules and can be added to groups when they satisfy the rule conditions. Review and clean up [stale devices](/en-us/entra/identity/devices/manage-stale-devices) and [inactive users](/en-us/entra/identity/monitoring-health/howto-manage-inactive-user-accounts) so your dynamic groups include only the objects you intend to manage.

## Best practices for dynamic membership groups in your tenant

To help ensure efficient processing and minimize delays, consider the following best practices.

### Monitor the number of dynamic membership groups in your tenant

Regularly review the number of groups in your tenant. Delete inactive or outdated groups.

### Pause nonessential groups

You can pause nonessential groups to improve processing performance. You might consider pausing group processing in these circumstances:

- **Planned large-scale updates**: You anticipate making a large number of changes to group membership. For example, you plan to make changes to more than 500 groups or make more than 20,000 membership changes.
- **Unexpected delays**: You notice that group membership hasn't changed and you encounter unexpected delays.

To temporarily halt processing, use the **Pause All Groups** script. Allow the service to recover before resuming.

Don't unpause the groups immediately. Wait a minimum of 24 hours to allow group processing to catch up. Then, check your audit logs to see if they're back to baseline. If necessary, unpause groups in phases rather than all at once.

### Optimize rule efficiency

- Avoid the use of the `Match` operator in rules as much as possible. Instead, use the `StartsWith`, `Equals`, or `EndsWith` operator.
- Avoid the use of the `Contains` operator in rules as much as possible. It can lead to increased processing time.
- Use fewer `-or` operators. Instead, use the `-in` operator to group rules into a single criterion. Grouping rules makes them easier to evaluate.
- Avoid the use of the [`memberOf`](groups-dynamic-rule-member-of) operator if possible. It's currently in preview, and it comes with bugs and limitations. It can also introduce more complexity, particularly if a tenant has a large number of groups or frequent updates. The recommendation is to delete existing `memberOf` groups in your tenant.

For more help with optimizing dynamic group processing, review [Create simpler, more efficient rules for dynamic membership groups in Microsoft Entra ID](groups-dynamic-rule-more-efficient).

## Summary

Delays in dynamic group processing primarily happen due to high volumes of changes and large numbers of groups. By following best practices like optimizing rule efficiency, monitoring changes, and pausing nonessential groups when necessary, IT administrators can improve processing performance and avoid unnecessary delays.