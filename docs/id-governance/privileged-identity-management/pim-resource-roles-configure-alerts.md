---
layout: Conceptual
title: Configure security alerts for Azure roles in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-resource-roles-configure-alerts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Learn how to configure security alerts for Azure resource roles in Privileged Identity Management (PIM).
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: rianakarim
ms.custom: pim
locale: en-us
document_id: 9ddcbd2c-5065-a544-db3f-43303c61f319
document_version_independent_id: b08188eb-1abb-41f9-7dc3-d3b1888a7c3e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-resource-roles-configure-alerts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-resource-roles-configure-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-resource-roles-configure-alerts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 25641b58-c778-e524-b647-72ee65f23ded
---

# Configure security alerts for Azure roles in Privileged Identity Management - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Privileged Identity Management (PIM) generates alerts when there's suspicious or unsafe activity in your organization in Microsoft Entra ID. When an alert is triggered, it shows up on the Alerts page.

Note

One event in Privileged Identity Management can generate email notifications to multiple recipients – assignees, approvers, or administrators. The maximum number of notifications sent per one event is 1,000. If the number of recipients exceeds 1,000 – only the first 1,000 recipients receive an email notification. This limit doesn't prevent other assignees, administrators, or approvers from using their permissions in Microsoft Entra ID and Privileged Identity Management.

![Screenshot of the alerts page listing alert, risk level, and count.](media/pim-resource-roles-configure-alerts/rbac-alerts-page.png)

## Review alerts

Select an alert to see a report that lists the users or roles that triggered the alert, along with remediation guidance.

![Screenshot of the alert report showing last scan time, description, mitigation steps, type, severity, security impact, and how to prevent next time.](media/pim-resource-roles-configure-alerts/rbac-alert-info.png)

## Alerts

| Alert | Severity | Trigger | Recommendation |
| --- | --- | --- | --- |
| **Too many owners assigned to a resource** | Medium | Too many users have the owner role. | Review the users in the list and reassign some to less privileged roles. |
| **Too many permanent owners assigned to a resource** | Medium | Too many users are permanently assigned to a role. | Review the users in the list and reassign some to require activation for role use. |
| **Duplicate role created** | Medium | Multiple roles have the same criteria. | Use only one of these roles. |
| **Roles are being assigned outside of Privileged Identity Management** | High | A role is managed directly through the Azure IAM resource, or the Azure Resource Manager API. | Review the users in the list and remove them from privileged roles assigned outside of Privileged Identity Management. |

Note

For the **Roles are being assigned outside of Privileged Identity Management** alerts, you might encounter duplicate notifications. These duplications might primarily be related to a potential live site incident where notifications are being sent again.

### Severity

- **High**: Requires immediate action because of a policy violation.
- **Medium**: Doesn't require immediate action but signals a potential policy violation.
- **Low**: Doesn't require immediate action but suggests a preferred policy change.

## Configure security alert settings

Follow these steps to configure security alerts for Azure roles in Privileged Identity Management:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Azure resources**. Select your subscription &gt; **Alerts** &gt; **Setting**. For information about how to add the Privileged Identity Management tile to your dashboard, see [Start using Privileged Identity Management](pim-getting-started).

    ![Screenshot of the alerts page with settings highlighted.](media/pim-resource-roles-configure-alerts/rbac-navigate-settings.png)
3. Customize settings on the different alerts to work with your environment and security goals.

    ![Screenshot of the alert setting.](media/pim-resource-roles-configure-alerts/rbac-alert-settings.png)

Note

"Roles are being assigned outside of Privileged Identity Management" alert is triggered for role assignments created for Azure subscriptions and isn't triggered for role assignments on Management Groups, Resource Groups, or Resource scope.