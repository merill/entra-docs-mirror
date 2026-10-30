---
layout: Conceptual
title: Review agent findings in the Risky user report - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/identity-risk-management-agent-risky-user-report
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Learn about how the Identity Risk Management Agent works with the Risky user report in Microsoft Entra ID Protection
ms.topic: how-to
ms.date: 2025-11-08T00:00:00.0000000Z
ms.reviewer: chuqiaoshi
locale: en-us
document_id: 314240b4-909b-9344-16a8-ee922c1bcca8
document_version_independent_id: 314240b4-909b-9344-16a8-ee922c1bcca8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/identity-risk-management-agent-risky-user-report.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/identity-risk-management-agent-risky-user-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/identity-risk-management-agent-risky-user-report.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 12c84b96-6af7-cf96-131d-5883a0543219
---

# Review agent findings in the Risky user report - Microsoft Entra ID Protection | Microsoft Learn

The Identity Risk Management Agent (Preview) in Microsoft Entra ID Protection provides proactive risk management capabilities by analyzing the risky identities and suggesting actions to remediate them. By using a Large Language Model, the agent helps security administrators review and respond to risky activities before they lead to security incidents.

Note

The Identity Risk Management Agent is currently being deployed and in preview. This information relates to a prerelease product that might be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

- You must have at least the [Microsoft Entra ID P2](overview-identity-protection#license-requirements) license.
- You must have available [security compute units (SCU)](/en-us/copilot/security/manage-usage).
    - On average, each agent run consumes less than one SCU.
- You must have the appropriate Microsoft Entra role.
    - [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator) is required to *activate the agent the first time* and *view the agent and take action on the suggestions*.
    - [Security Reader](../identity/role-based-access-control/permissions-reference#security-reader) and [Global Reader](../identity/role-based-access-control/permissions-reference#global-reader) roles can *view the agent and any suggestions, but can't take any actions*.
    - For more information, see [Assign Security Copilot access](/en-us/copilot/security/authentication#assign-security-copilot-access).
- Review [Privacy and data security in Microsoft Security Copilot](/en-us/copilot/security/privacy-data-security).

## Review agent findings in the Risky users report

The Identity Risk Management Agent is integrated directly into the Risky users report in Microsoft Entra ID Protection to support your existing workflow.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **ID Protection** &gt; **Risky users**.
3. Select the **Agent view** option at the top of the report.

The top half of the agent view of the risky user report contains a summary of recent agent activity. This tile provides quick access to the **Chat with agent** feature, an option to trigger a one-time run, and a link to the agent settings. The lower half of the report contains the full list of risky users. Select a user from the list to view agent insights and suggestions specific to that user.

## Agent summary

An agent summary appears at the top of the Agent view, showing recent agent activities. This tile provides quick access to the **Chat with agent** feature and a **Manage agent** button, which lets you trigger a one-time run or open agent settings.

## Agent suggestions

Agent suggestions are displayed below the agent summary. Hover over a suggestion to highlight impacted users in the table. Selecting a suggestion filters the table to show only those users for review. Each suggestion includes a bulk action button, so you can apply the action with one click.

Currently, the following remediation actions are available in agent suggestions:

- Dismiss risk
- Reset password

## Risky users table with agent suggestions

The lower half of the report lists all risky users. Select a user to view agent findings, risk factors, and suggestions specific to that user. The **Agent** suggestion column also shows recommended remediation actions directly in the table. Select the action button to apply a remediation to individual users.

## Risky user details

The **Risky user details** page provides a new **Agent view**, which presents agent findings specific to a risky user. This view includes the following information:

- **Basic user information**: Username, current risk level, and UPN
- **Agent findings**: The agent provides a verdict of *Compromised* or *Not compromised* based on its investigation.
- **Risk summary**: A detailed explanation of the agent's findings, based on analysis of the user's sign-ins and behaviors.
- **Risk factors**: Key risk indicators summarized for easy review.
- **Suggested remediation action**: A call-to-action button that allows you to quickly start remediating the risk.

**Standard view**[![Screenshot of the standard view of the risky user details.](media/identity-risk-management-agent-risky-user-report/risky-user-details-standard-view.png)](media/identity-risk-management-agent-risky-user-report/risky-user-details-standard-view-expanded.png#lightbox)

**Agent view**[![Screenshot of the agent view of the risky user details.](media/identity-risk-management-agent-risky-user-report/risky-user-details-agent-view.png)](media/identity-risk-management-agent-risky-user-report/risky-user-details-agent-view-expanded.png#lightbox)

The agent findings, summary, and risk factors are AI-generated and therefore dynamic. Language might vary between runs.

The bottom half of the agent view of the risky user details provides a visual of recent activity. This section includes the following visualizations:

- **User's risk level graph**: A historical trend of the user's risk level over the past 7 days to help you understand changes.
- **User's past sign-in counts**: The number of sign-ins for this user in the past 7 days.
- **Risky sign-in map**: A map showing the locations of risky sign-ins for this user.