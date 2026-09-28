---
layout: Conceptual
title: Extend or renew PIM for groups assignments - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/groups-renew-extend
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to extend or renew PIM for groups assignments.
ms.reviewer: markwahl-msft
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.custom: pim, sfi-image-nochange
locale: en-us
document_id: 57209f67-28d5-ca2d-4c9d-0fdf2b36b096
document_version_independent_id: 9600398a-e766-ab14-6977-0d036faddea4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/groups-renew-extend.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/groups-renew-extend
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/groups-renew-extend.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 99989270-a7d3-015f-0699-5ddd902f9089
---

# Extend or renew PIM for groups assignments - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Privileged Identity Management (PIM) in Microsoft Entra ID provides controls to manage the access and assignment lifecycle for group membership and ownership. Administrators can assign start and end date-time properties for group membership and ownership. When the assignment end approaches, Privileged Identity Management sends email notifications to the affected users or groups. It also sends email notifications to administrators of the resource to ensure that appropriate access is maintained. Assignments might be renewed and remain visible in an expired state for up to 30 days, even if access isn't extended.

## Who can extend and renew

Only users with permissions to manage groups can extend or renew time-bound group membership or ownership assignments. The assignee can request to extend assignments that are about to expire and request to renew assignments that are already expired.

- To manage ownership of a role-assignable group, you need a Microsoft Entra role with the `microsoft.directory/groupsAssignableToRoles/owners/update` permission, such as Privileged Role Administrator or Global Administrator, or be an active owner of the group.
- To manage membership in a role-assignable group, you need a Microsoft Entra role with the `microsoft.directory/groupsAssignableToRoles/members/update` permission, such as Privileged Role Administrator or Global Administrator, or be an active owner of the group.
- To manage ownership of a non-role-assignable group, you need a Microsoft Entra role with the `microsoft.directory/groups/owners/update` permission, such as Groups Administrator or Identity Governance Administrator, or be an active owner of the group.
- To manage membership in a non-role-assignable group, you need a Microsoft Entra role with the `microsoft.directory/groups/members/update` permission, such as Groups Administrator or Identity Governance Administrator, or be an active owner of the group.

Role assignments for administrators can be scoped at directory level or administrative unit level. Built-in and custom Microsoft Entra roles are supported.

Privileged Identity Management doesn't support permissions that start with `microsoft.directory/groups.security/` or `microsoft.directory/groups.unified/`. Use permissions that start with `microsoft.directory/groups/` instead.

Privileged Identity Management doesn't support groups in Restricted Management Administrative Units (RMAU).

Note

Administrators and group owners can manage groups through the Groups experience and other interfaces, overriding changes made in Microsoft Entra PIM.

## When notifications are sent

Privileged Identity Management sends email notifications to administrators and affected users of PIM for Groups assignments that are expiring:

- Within 14 days prior to expiration
- One day prior to expiration
- When an assignment expires

Administrators receive notifications when a user or group requests to extend or renew an expiring or expired assignment. When an administrator resolves the request, all administrators and the requesting user are notified of the approval or denial.

## Extend group assignments

The following steps outline the process for requesting, resolving, or administering an extension or renewal of a group membership or ownership assignment.

### Self-extend expiring assignments

Users assigned group membership or ownership can extend expiring group assignments directly from the **Eligible** or **Active** tab on the **Assignments** page for the group. Users or groups can request to extend eligible and active assignments that expire in the next 14 days.

[![Screenshot of where to self-extend expiring assignments.](media/pim-for-groups/pim-group-11.png)](media/pim-for-groups/pim-group-11.png#lightbox)

When the assignment end date-time is within 14 days, the **Extend** command is available. To request an extension of a group assignment, select **Extend** to open the request form.

[![Screenshot of where to extend group assignment pane with a Reason box and details.](media/pim-for-groups/pim-group-12.png)](media/pim-for-groups/pim-group-12.png#lightbox)

Note

Include the details of why the extension is necessary, and for how long the extension should be granted (if you have this information).

Administrators receive an email notification requesting that they review the extension request. If a request to extend has already been submitted, an Azure notification appears in the portal.

To view the status of or cancel your request, open the **Pending requests** page for the group assignment.

[![Screenshot of the pending requests page showing the link to Cancel.](media/pim-for-groups/pim-group-13.png)](media/pim-for-groups/pim-group-13.png#lightbox)

### Admin approved extension

When a user or group submits a request to extend a group assignment, administrators receive an email notification that contains the details of the original assignment and the reason for the request. The notification includes a direct link to the request for the administrator to approve or deny.

In addition to following the link from the email, administrators can approve or deny requests by going to the Privileged Identity Management administration portal and selecting **Approve requests** in the left pane.

[![Screenshot of the Approve requests page listing requests and links to approve or deny.](media/pim-for-groups/pim-group-14.png)](media/pim-for-groups/pim-group-14.png#lightbox)

When an administrator selects **Approve** or **Deny**, the details of the request are shown, along with a field to provide a business justification for the audit logs.

[![Screenshot of where to approve group assignment request with requestor reason, assignment type, start time, end time, and reason.](media/pim-for-groups/pim-group-15.png)](media/pim-for-groups/pim-group-15.png#lightbox)

When approving a request to extend a group assignment, resource administrators can choose a new start date, end date, and assignment type. Changing assignment type might be necessary if the administrator wants to provide limited access to complete a specific task (one day, for example). In this example, the administrator can change the assignment from **Eligible** to **Active**. This means they can provide access to the requestor without requiring them to activate.

### Admin initiated extension

If a user assigned to a group doesn't request an extension for the group assignment, an administrator can extend an assignment on behalf of the user. Administrative extensions of group assignment don't require approval, but notifications are sent to all other administrators after the assignment has been extended.

To extend a group assignment, browse to the assignment view in Privileged Identity Management. Find the assignment that requires an extension. Then select **Extend** in the action column.

[![Screenshot of the assignments page listing eligible group assignments with links to extend.](media/pim-for-groups/pim-group-16.png)](media/pim-for-groups/pim-group-16.png#lightbox)

## Renew group assignments

While conceptually similar to the process for requesting an extension, the process to renew an expired group assignment is different. Using the following steps, assignments and administrators can renew access to expired assignments when necessary.

### Self-renew

Users who can no longer access resources can access up to 30 days of expired assignment history. To do this, they browse to **My Roles** in the left pane, and then select the **Expired assignments** tab.

The list of assignments shown defaults to **Eligible assignments**. Use the drop-down menu to toggle between Eligible and Active assignments.

To request renewal for any of the group assignments in the list, select the **Renew** action. Then provide a reason for the request. It's helpful to provide a duration in addition to any other context or a business justification that can help the resource administrator decide to approve or deny.

After the request is submitted, resource administrators are notified of a pending request to renew a group assignment.

### Admin approves

Resource administrators can access the renewal request from the link in the email notification or by accessing Privileged Identity Management from the Microsoft Entra admin center and selecting **Approve requests** from the left pane.

When an administrator selects **Approve** or **Deny**, the details of the request are shown along with a field to provide a business justification for the audit logs.

When approving a request to renew a group assignment, resource administrators must enter a new start date, end date, and assignment type.