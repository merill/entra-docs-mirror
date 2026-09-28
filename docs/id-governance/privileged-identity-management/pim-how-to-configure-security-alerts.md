---
layout: Conceptual
title: Security alerts for Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-how-to-configure-security-alerts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Configure security alerts for Microsoft Entra roles in Privileged Identity Management.
ms.topic: how-to
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: pim, sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: 9a8ae82f-6d28-7186-da5a-226a7071c1c1
document_version_independent_id: 4681d5a1-ccd8-1796-7336-9138bf5307cc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-how-to-configure-security-alerts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-how-to-configure-security-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-how-to-configure-security-alerts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: f67d5406-f9b6-effe-1d2c-ba44fec8745a
---

# Security alerts for Microsoft Entra roles in PIM - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Privileged Identity Management (PIM) generates alerts when there's suspicious or unsafe activity in your organization in Microsoft Entra ID. When an alert is triggered, it shows up on the Privileged Identity Management dashboard. Select the alert to see a report that lists the users or roles that triggered the alert.

Note

One event in Privileged Identity Management can generate email notifications to multiple recipients – assignees, approvers, or administrators. The maximum number of notifications sent per one event is 1000. If the number of recipients exceeds 1000 – only the first 1000 recipients will receive an email notification. This doesn't prevent other assignees, administrators, or approvers from using their permissions in Microsoft Entra ID and Privileged Identity Management.

![Screenshot that shows the alerts page with a list of alerts and their severity.](media/pim-how-to-configure-security-alerts/view-alerts.png)

## License requirements

Using Privileged Identity Management requires licenses. For more information on licensing, see [Microsoft Entra ID Governance licensing fundamentals](../licensing-fundamentals) .

## Security alerts

This section lists all the security alerts for Microsoft Entra roles, along with how to fix them and how to prevent them. Severity has the following meaning:

- **High**: Requires immediate action because of a policy violation.
- **Medium**: Doesn't require immediate action but signals a potential policy violation.
- **Low**: Doesn't require immediate action but suggests a preferable policy change.

Note

Only the following roles are able to read PIM security alerts for Microsoft Entra roles: **Global Administrator**, **Privileged Role Administrator**, **Global Reader**, **Security Administrator**, and **Security Reader**.

### Administrators aren't using their privileged roles

Severity: **Low**

| - | Description |
| --- | --- |
| **Why do I get this alert?** | Users that have assigned privileged roles they don't need increase the chances of an attack. It's also easier for attackers to remain unnoticed in accounts that aren't actively being used. |
| **How to fix?** | Review the users in the list and remove them from privileged roles that they don't need. |
| **Prevention** | Assign privileged roles only to users who have a business justification. Schedule regular [access reviews](pim-create-roles-and-resource-roles-review) to verify that users still need their access. |
| **In-portal mitigation action** | Removes the account from their privileged role. |
| **Trigger** | Triggered if a user goes over a specified number of days without activating a role. |
| **Number of days** | This setting specifies the maximum number of days, from 0 to 100, that a user can go without activating a role. |

### Roles don't require multifactor authentication for activation

Severity: **Low**

| - | Description |
| --- | --- |
| **Why do I get this alert?** | Without multifactor authentication, compromised users can activate privileged roles. |
| **How to fix?** | Review the list of roles and [require multifactor authentication](pim-how-to-change-default-settings) for every role. |
| **Prevention** | [Require MFA](pim-how-to-change-default-settings) for every role. |
| **In-portal mitigation action** | Makes multifactor authentication required for activation of the privileged role. |

### The organization doesn't have Microsoft Entra ID P2 or Microsoft Entra ID Governance

Severity: **Low**

| - | Description |
| --- | --- |
| **Why do I get this alert?** | The current Microsoft Entra organization doesn't have Microsoft Entra ID P2 or Microsoft Entra ID Governance. |
| **How to fix?** | Review information about [Microsoft Entra editions](../../fundamentals/licensing). Upgrade to Microsoft Entra ID P2 or Microsoft Entra ID Governance. |

### Potential stale accounts in a privileged role

Severity: **Medium**

| - | Description |
| --- | --- |
| **Why do I get this alert?** | This alert is no longer triggered based on the last password change date of for an account. This alert is for accounts in a privileged role that haven't signed in during the past *n* days, where *n* is a configurable number of days between 1 and 365. These accounts might be service or shared accounts that aren't being maintained and are vulnerable to attackers. |
| **How to fix?** | Review the accounts in the list. If they no longer need access, remove them from their privileged roles. |
| **Prevention** | Ensure that accounts that are shared are rotating strong passwords when there's a change in the users that know the password. Regularly review accounts with privileged roles using [access reviews](pim-create-roles-and-resource-roles-review) and remove role assignments that are no longer needed. |
| **In-portal mitigation action** | Removes the account from their privileged role. |
| **Best practices** | Shared, service, and emergency access accounts that authenticate using a password and are assigned to highly privileged administrative roles such as Global Administrator or Security Administrator should have their passwords rotated for the following cases:<br>- After a security incident involving misuse or compromise of administrative access rights<br>- After any user's privileges are changed so that they're no longer an administrator (for example, after an employee who was an administrator leaves IT or leaves the organization)<br>- At regular intervals (for example, quarterly or yearly), even if there was no known breach or change to IT staffing<br><br>Since multiple people have access to these accounts' credentials, the credentials should be rotated to ensure that people that have left their roles can no longer access the accounts. [Learn more about securing accounts](../../identity/role-based-access-control/security-planning) |

### Roles are being assigned outside of Privileged Identity Management

Severity: **High**

| - | Description |
| --- | --- |
| **Why do I get this alert?** | Privileged role assignments made outside of Privileged Identity Management aren't properly monitored and might indicate an active attack. |
| **How to fix?** | Review the users in the list and remove them from privileged roles assigned outside of Privileged Identity Management. You can also enable or disable both the alert and its accompanying email notification in the alert settings. |
| **Prevention** | Investigate where users are being assigned privileged roles outside of Privileged Identity Management and prohibit future assignments from there. |
| **In-portal mitigation action** | Removes the user from their privileged role. |

Note

PIM sends email notifications for the **Role assigned outside of PIM** alert when the alert is enabled from alert settings. For Microsoft Entra roles in PIM, emails are sent to **Privileged Role Administrators**, **Security Administrators**, and **Global Administrators** that have enabled Privileged Identity Management. For Azure resources in PIM, emails are sent to **Owners** and **User Access Administrators**.

### There are too many Global Administrators

Severity: **Low**

| - | Description |
| --- | --- |
| **Why do I get this alert?** | Global Administrator is the highest privileged role. If a Global Administrator is compromised, the attacker gains access to all of their permissions, which put your whole system at risk. |
| **How to fix?** | Review the users in the list and remove any that don't absolutely need the Global Administrator role. Assign lower privileged roles to these users instead. |
| **Prevention** | Assign users the least privileged role they need. |
| **In-portal mitigation action** | Removes the account from their privileged role. |
| **Trigger** | Triggered if two different criteria are met, and you can configure both of them. First, you need to reach a certain threshold of Global Administrator role assignments. Second, a certain percentage of your total role assignments must be Global Administrators. If you only meet one of these measurements, the alert doesn't appear. |
| **Minimum number of Global Administrators** | This setting specifies the number of Global Administrator role assignments, from 2 to 100, that you consider to be too few for your Microsoft Entra organization. |
| **Percentage of Global Administrators** | This setting specifies the minimum percentage of administrators who are Global Administrators, from 0% to 100%, below which you don't want your Microsoft Entra organization to dip. |

### Roles are being activated too frequently

Severity: **Low**

| - | Description |
| --- | --- |
| **Why do I get this alert?** | Multiple activations to the same privileged role by the same user is a sign of an attack. |
| **How to fix?** | Review the users in the list and ensure that the [activation duration](pim-how-to-change-default-settings) for their privileged role is set long enough for them to perform their tasks. |
| **Prevention** | Ensure that the [activation duration](pim-how-to-change-default-settings) for privileged roles is set long enough for users to perform their tasks.[Require multifactor authentication](pim-how-to-change-default-settings) for privileged roles that have accounts shared by multiple administrators. |
| **In-portal mitigation action** | N/A |
| **Trigger** | Triggered if a user activates the same privileged role multiple times within a specified period. You can configure both the time period and the number of activations. |
| **Activation renewal timeframe** | This setting specifies in days, hours, minutes, and seconds the time period you want to use to track suspicious renewals. |
| **Number of activation renewals** | This setting specifies the number of activations, from 2 to 100, at which you would like to be notified, within the timeframe you chose. You can change this setting by moving the slider, or typing a number in the text box. |

## Customize security alert settings

Follow these steps to configure security alerts for Microsoft Entra roles in Privileged Identity Management:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Privileged Role Administrator](../../identity/role-based-access-control/permissions-reference#privileged-role-administrator).
2. Browse to **ID Governance** &gt; **Privileged Identity Management** &gt; **Microsoft Entra roles** &gt; **Alerts** &gt; **Setting**. For information about how to add the Privileged Identity Management tile to your dashboard, see [Start using Privileged Identity Management](pim-getting-started).

    ![Screenshot of the alerts page with the settings highlighted.](media/pim-how-to-configure-security-alerts/alert-settings.png)
3. Customize settings on the different alerts to work with your environment and security goals.

    ![Screenshot of the alert setting page.](media/pim-how-to-configure-security-alerts/security-alert-settings.png)