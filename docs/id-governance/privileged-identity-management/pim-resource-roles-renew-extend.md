---
layout: Conceptual
title: Renew Azure resource role assignments in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-resource-roles-renew-extend
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to extend or renew Azure resource role assignments in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: pim, sfi-image-nochange
locale: en-us
document_id: de486759-f16f-4bd9-5639-2bd9bfe8feb1
document_version_independent_id: 4e26e9ef-0d42-f6b2-3441-f66d99f2aa89
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-resource-roles-renew-extend.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-resource-roles-renew-extend
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-resource-roles-renew-extend.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 4c7fc529-6edb-988d-940a-db05a09e505c
---

# Renew Azure resource role assignments in PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Microsoft Entra Privileged Identity Management (PIM) provides controls to manage the access and assignment lifecycle for Azure resources. Administrators can assign roles using start and end date-time properties. When the assignment end approaches, Privileged Identity Management sends email notifications to the affected users or groups. It also sends email notifications to administrators of the resource to ensure that appropriate access is maintained. Assignments might be renewed and remain visible in an expired state for up to 30 days, even if access isn't extended.

## Who can extend and renew?

Only administrators of the resource can extend or renew role assignments. The affected user or group can request to extend roles that are about to expire and request to renew roles that are already expired.

## When are notifications sent?

Privileged Identity Management sends email notifications to administrators and affected user or groups of roles that are expiring within 14 days and one day prior to expiration. It sends an additional email when an assignment officially expires.

Administrators receive notifications when a user or group assigned an expiring or expired role requests to extend or renew. When a specific administrator resolves the request, all other administrators are notified of the resolution decision (approved or denied). Then the requesting user or group is notified of the decision.

## Extend role assignments

The following steps outline the process for requesting, resolving, or administering an extension or renewal of a role assignment.

### Self-extend expiring assignments

Users assigned to a role can extend expiring role assignments directly from the **Eligible** or **Active** tab on the **My roles** page of a resource and from the top level **My roles** page of the Privileged Identity Management portal. In the portal, users can request to extend eligible or active (assigned) roles that expire in the next 14 days.

![Screenshot of the My roles page listing eligible roles with an Action column.](media/pim-resource-roles-renew-extend/aadpim-rbac-extend-ui.png)

When the assignment end date-time is within 14 days, the link to **Extend** becomes active in the Microsoft Entra admin center. In the following example, assume the current date is March 27.

Note

For a group assigned to a role, the **Extend** link never becomes available so that a user with an inherited assignment can't extend the group assignment.

![Screenshot of the action column with links to Activate or Extend.](media/pim-resource-roles-renew-extend/aadpim-rbac-extend-within-14.png)

To request an extension of this role assignment, select **Extend** to open the request form.

![Screenshot of the Extend role assignment pane with a Reason box.](media/pim-resource-roles-renew-extend/aadpim-rbac-extend-role-assignment-request.png)

To view information about the original assignment, expand **Assignment details**. Enter a reason for the extension request, and then select **Extend**.

Note

Include the details of why the extension is necessary, and for how long the extension should be granted (if you have this information).

![Screenshot of the Extend role assignment pane with Assignment details expanded.](media/pim-resource-roles-renew-extend/aadpim-rbac-extend-form-complete.png)

In a matter of moments, resource administrators receive an email notification requesting that they review the extension request. If a request to extend has already been submitted, an Azure notification appears in the portal.

![Screenshot of a Notification explaining that there is already an existing pending role assignment extension.](media/pim-resource-roles-renew-extend/aadpim-rbac-extend-failed-existing-request.png)

Go to the **Pending requests** page to view the status of your request or to cancel it.

![Screenshot of Azure resources - Pending requests page listing any pending requested and a link to Cancel.](media/pim-resource-roles-renew-extend/aadpim-rbac-extend-cancel-request.png)

### Admin approved extension

When a user or group submits a request to extend a role assignment, resource administrators receive an email notification that contains the details of the original assignment and the reason for the request. The notification includes a direct link to the request for the administrator to approve or deny.

In addition to following the link from the email, administrators can approve or deny requests by going to the Privileged Identity Management administration portal and selecting **Approve requests** in the left pane.

![Screenshot of Azure resources - Approve requests page listing requests and links to approve or deny.](media/pim-resource-roles-renew-extend/aadpim-rbac-extend-admin-approve-grid.png)

When an administrator selects **Approve** or **Deny**, the details of the request are shown, along with a field to provide a business justification for the audit logs.

![Screenshot of Approve role assignment request with requestor reason, assignment type, start time, end time, and reason.](media/pim-resource-roles-renew-extend/aadpim-rbac-extend-admin-approve-blade.png)

When approving a request to extend role assignment, resource administrators can choose a new start date, end date, and assignment type. Changing assignment type might be necessary if the administrator wants to provide limited access to complete a specific task (one day, for example). In this example, the administrator can change the assignment from **Eligible** to **Active**. This means they can provide access to the requestor without requiring them to activate.

### Admin initiated extension

If a user assigned to a role doesn't request an extension for the role assignment, an administrator can extend an assignment on behalf of the user. Administrative extensions of role assignment don't require approval, but notifications are sent to all other administrators after the role has been extended.

To extend a role assignment, browse to the resource role or assignment view in Privileged Identity Management. Find the assignment that requires an extension. Then select **Extend** in the action column.

![Screenshot of Azure resources - assignments page listing eligible roles with links to extend.](media/pim-resource-roles-renew-extend/aadpim-rbac-extend-admin-extend.png)

## Renew role assignments

While conceptually similar to the process for requesting an extension, the process to renew an expired role assignment is different. Using the following steps, assignments and administrators can renew access to expired roles when necessary.

### Self-renew

Users who can no longer access resources can access up to 30 days of expired assignment history. To do this, browse to **My Roles** in the left pane, and then select the **Expired roles** tab in the Azure resource roles section.

![Screenshot of My roles page - Expired roles tab.](media/pim-resource-roles-renew-extend/aadpim-rbac-renew-from-myroles.png)

The list of roles shown defaults to **Eligible roles**. Use the drop-down menu to toggle between Eligible and Active assigned roles.

To request renewal for any of the role assignments in the list, select the **Renew** action. Then provide a reason for the request. It's helpful to provide a duration in addition to any other context or a business justification that can help the resource administrator decide to approve or deny.

![Screenshot of Renew role assignment pane showing Reason box.](media/pim-resource-roles-renew-extend/aadpim-rbac-renew-request-form.png)

After the request is submitted, resource administrators are notified of a pending request to renew a role assignment.

### Admin approves

Resource administrators can access the renewal request from the link in the email notification or by accessing Privileged Identity Management from the Microsoft Entra admin center and selecting **Approve requests** from the left pane.

![Screenshot of Azure resources - Approve requests page listing requests and links to approve or deny.](media/pim-resource-roles-renew-extend/aadpim-rbac-extend-admin-approve-grid.png)

When an administrator selects **Approve** or **Deny**, the details of the request are shown along with a field to provide a business justification for the audit logs.

![Screenshot of Approve role assignment request with requestor reason, assignment type, start time, end time, and reason.](media/pim-resource-roles-renew-extend/aadpim-rbac-extend-admin-approve-blade.png)

When approving a request to renew role assignment, resource administrators must enter a new start date, end date, and assignment type.

### Admin renew

Resource administrators can renew expired role assignments from the **Members** tab in the left navigation menu of a resource. Resource administrators can also renew expired role assignments from within the **Expired** roles tab of a resource role.

To view a list of all expired role assignments, on the **Members** screen, select **Expired roles**.

![Screenshot of Azure resources - Members page listing expired roles with links to renew.](media/pim-resource-roles-renew-extend/aadpim-rbac-renew-from-member-blade.png)