---
layout: Conceptual
title: Identity Risk Management Agent Settings - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/identity-risk-management-agent-settings
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Learn how to configure the settings for the Identity Risk Management Agent in Microsoft Entra ID Protection.
ms.topic: concept-article
ms.date: 2025-10-20T00:00:00.0000000Z
ms.reviewer: chuqiaoshi
locale: en-us
document_id: 294524f0-f9fb-bb53-1e95-2cb21da7797d
document_version_independent_id: 294524f0-f9fb-bb53-1e95-2cb21da7797d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/identity-risk-management-agent-settings.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/identity-risk-management-agent-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/identity-risk-management-agent-settings.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8ae182f1-4eab-9072-2980-18be7d89a7ea
---

# Identity Risk Management Agent Settings - Microsoft Entra ID Protection | Microsoft Learn

The Identity Risk Management Agent in Microsoft Entra ID Protection provides proactive risk management capabilities by analyzing user behavior and suggesting actions to mitigate potential identity risks. You can configure the settings to meet your organization's needs, such as how often it runs, and email notifications.

Note

The Identity Risk Management Agent is currently being deployed and in preview. This information relates to a prerelease product that might be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Access the agent settings

Once the agent is enabled, you can adjust a few settings. To review and adjust the settings:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **ID Protection** &gt; **Risky users**.
3. With the **Agent view** selected, select the ellipses in the upper-right corner and then select **Settings**.
4. On the agent page, select the **Settings** tab. The settings are organized into **Controls**, **Communications**, and **Memory**.
5. After making any changes, select **Save** at the bottom of the page.

You can also access the settings from the Microsoft Entra agent library. Select **Agents** from the left-hand navigation, select the **Identity Risk Management Agent**, and then select the **Settings** tab.

### Controls

The **Controls** section provides the roles and permissions required for the agent to run. You can also adjust how the agent is triggered and the scope of the agent.

#### Trigger

By default, the agent continuously monitors your tenant, but you can also change the frequency or set to manual run only. When the agent is set to run daily or manually, the agent can send email notifications to selected recipients after each run.

The following options are available:

- **Continuous monitoring**: The agent checks for new risky users every 5 minutes and automatically investigates them.
- **Daily trigger**: The agent runs automatically every 24 hours.
- **Manual run**: The agent runs only when started manually.

#### Permissions and role-based access

The agent requires specific permissions to read risk detections, risk history, sign-in and audit logs, and user information. These permissions are granted through the [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator) role.

#### Scope

By default, the agent investigates the most recent 100 risky users within the last 90 days. You can control the scope of for agent scan by adjusting several options.

- Select the **Select users and groups** option to search for and select the users and groups you want the agent to scan.
- Set the maximum recent risky users to scan within 1-100.
- Select which risk levels to include in the scan. All risk levels are selected by default.
- Set a specific time frame for the scope:
    - Last 7 days
    - Last 14 days
    - Last 30 days
    - Custom time frame up to 90 days

### Communications

The Identity Risk Management Agent can send email notifications to selected recipients. Notifications aren't turned on by default.

1. Set the **Email notifications** toggle to **On**.
2. Select the **No users selected** link under the **Additional recipients** heading to search for and add more recipients.

### Memory

The Identity Risk Management Agent uses your feedback to refine its suggestions over time. If you mark a false positive as "confirmed safe", the agent remembers that feedback for future runs. The history of the input you and your team provide appears in this list.