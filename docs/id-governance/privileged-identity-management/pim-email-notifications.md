---
layout: Conceptual
title: Email notifications in Privileged Identity Management (PIM) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-email-notifications
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id-governance
ms.subservice: privileged-identity-management
manager: dougeby
description: Describes email notifications in Microsoft Entra Privileged Identity Management (PIM).
ms.topic: concept-article
ms.date: 2026-04-23T00:00:00.0000000Z
ms.reviewer: shaunliu
ms.custom: pim, sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: f5a932ce-6046-f6a9-9b85-188c8530174c
document_version_independent_id: 196cb921-fbf8-6819-e0e2-8cd03fda4505
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/privileged-identity-management/pim-email-notifications.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/privileged-identity-management/pim-email-notifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/privileged-identity-management/pim-email-notifications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7fba8e88-56fd-5900-37a1-27df01d6cce9
---

# Email notifications in Privileged Identity Management (PIM) - Microsoft Entra ID Governance | Microsoft Learn

## Overview

Privileged Identity Management (PIM) lets you know when important events occur in your Microsoft Entra organization, such as when a role is assigned or activated. Privileged Identity Management keeps you informed by sending you and other participants email notifications. These emails might also include links to relevant tasks, such as activating or renewing a role. This article describes what these emails look like, when they are sent, and who receives them.

Note

One event in Privileged Identity Management can generate email notifications to multiple recipients – assignees, approvers, or administrators. The maximum number of notifications sent per one event is 1,000. If the number of recipients exceeds 1,000 – only the first 1,000 recipients receive an email notification. This doesn't prevent other assignees, administrators, or approvers from using their permissions in Microsoft Entra ID and Privileged Identity Management.

## Sender email address and subject line

Emails sent from Privileged Identity Management for both Microsoft Entra ID and Azure resource roles have the following sender email address:

- Email address: `MSSecurity-noreply@microsoft.com`
- Display name: **Microsoft Security**

Important

The `azure-noreply@microsoft.com` has been deprecated and should no longer be sending PIM email notifications.

These emails include a **PIM** prefix in the subject line. Here's an example:

- PIM: Alain Charon was permanently assigned the Backup Reader role

## Email timing for activation approvals

When users activate their role and the role setting requires approval, approvers receive two emails for each approval:

- Request to approve or deny the user's activation request (sent by the request approval engine)
- The user's request is approved (sent by the request approval engine)

Also, Global Administrators and Privileged Role Administrators receive an email for each approval:

- The user's role is activated (sent by Privileged Identity Management)

The first two emails sent by the request approval engine can be delayed. Currently, 90% of emails take three to 10 minutes, but for 1% of customers it can be longer, up to 15 minutes.

If an approval request is approved in the Azure portal before the first email is sent, the first email isn't triggered and other approvers don't receive email notifications of the approval request. It might appear as if they didn't get an email but it's the expected behavior.

## Notifications for Microsoft Entra roles

Privileged Identity Management sends emails when the following events occur for Microsoft Entra roles:

- When a privileged role activation is pending approval
- When a privileged role activation request is completed
- When Microsoft Entra Privileged Identity Management is enabled

Who receives these emails for Microsoft Entra roles depends on your role, the event, and the notifications setting.

| User | Role activation is pending approval | Role activation request is completed | PIM is enabled |
| --- | --- | --- | --- |
| Privileged Role Administrator(Activated) | Yes(only if no explicit approvers are specified) | Yes\* | Yes |
| Security Administrator(Activated) | No | Yes\* | Yes |
| Global Administrator(Activated) | No | Yes\* | Yes |

\* If the [**Notifications** setting](pim-how-to-change-default-settings) is set to **Enable**.

The following shows an example email that is sent when a user activates a Microsoft Entra role for the fictional Contoso organization.

![Screenshot showing the new Privileged Identity Management email for Microsoft Entra roles.](media/pim-email-notifications/email-directory-new.png)

### Weekly Privileged Identity Management digest email for Microsoft Entra roles

A weekly Privileged Identity Management summary email for Microsoft Entra roles is sent to Privileged Role Administrators, Security Administrators, and Global Administrators that have enabled Privileged Identity Management. This weekly email provides a snapshot of Privileged Identity Management activities for the week and privileged role assignments. It's only available for Microsoft Entra organizations on the public cloud. Here's an example email:

![Screenshot showing the weekly Privileged Identity Management digest email for Microsoft Entra roles.](media/pim-email-notifications/email-directory-weekly.png)

The email includes:

| Tile | Description |
| --- | --- |
| **Users activated** | Number of times users activated their eligible role inside the organization. |
| **Users made permanent** | Number of times users with an eligible assignment is made permanent. |
| **Role assignments in Privileged Identity Management** | Number of times users are assigned an eligible role inside Privileged Identity Management. |
| **Role assignments outside of PIM** | Number of times users are assigned a permanent role outside of Privileged Identity Management (inside Microsoft Entra ID). This alert and the accompanying email can be enabled or disabled by opening the alert settings. |

The **Overview of your top roles** section lists the top five roles in your organization based on total number of permanent and eligible administrators for each role. The **Take action** link opens [Discovery & Insights](pim-security-wizard) where you can convert permanent administrators to eligible administrators in batches.

## Notifications for Azure resource roles

Note

In PIM, an *eligible* Owner is someone who has just-in-time (JIT) privileged access to perform certain tasks for managing groups, which can be activated when needed. This is different from a *permanent* Owner, who has ongoing access to manage groups. For more information about JIT ownership of a group, see [Assign eligibility for a group in Privileged Identity Management](groups-assign-member-owner).

Group owners can manage the group, including adding or removing members, renewing groups that are about to expire, and approving requests to join the group. PIM sends emails to *permanent* Owners, *eligible* Owners, and User Access Administrators when the following events occur for Azure resource roles:

- When a role assignment is pending approval
- When a role is assigned
- When a role is soon to expire
- When a role is eligible to extend
- When a role is renewed by an end user
- When a role activation request is completed

Privileged Identity Management sends emails to end users when the following events occur for Azure resource roles:

- When a role is assigned to the user
- When a user's role is expired
- When a user's role is extended
- When a user's role activation request is completed

The following shows an example email that is sent when a user is assigned an Azure resource role for the fictional Contoso organization.

![Screenshot showing the new Privileged Identity Management email for Azure resource roles.](media/pim-email-notifications/email-resources-new.png)

## Notifications for PIM for Groups

Privileged Identity Management sends emails to *permanent* Owners only when the following events occur for PIM for Groups assignments:

- When an Owner or Member role assignment is pending approval
- When an Owner or Member role is assigned
- When an Owner or Member role is soon to expire
- When an Owner or Member role is eligible to extend
- When an Owner or Member role is being renewed by an end user
- When an Owner or Member role activation request is completed

Privileged Identity Management sends emails to end users when the following events occur for PIM for Groups role assignments:

- When an Owner or Member role is assigned to the user
- When a user's Owner or Member role is expired
- When a user's Owner or Member role is extended
- When a user's Owner or Member role activation request is completed