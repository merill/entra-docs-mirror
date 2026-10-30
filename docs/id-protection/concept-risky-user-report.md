---
layout: Conceptual
title: Risky user report - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/concept-risky-user-report
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Learn about the risky user report in Microsoft Entra ID Protection
ms.topic: concept-article
ms.date: 2025-11-05T00:00:00.0000000Z
ms.reviewer: chuqiaoshi
locale: en-us
document_id: 0a2824d3-a83e-9df9-ad21-7f8bd55012d9
document_version_independent_id: 0a2824d3-a83e-9df9-ad21-7f8bd55012d9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/concept-risky-user-report.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/concept-risky-user-report
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/concept-risky-user-report.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4bae6ee4-f28a-b4fe-d4b7-07e3ed1241d0
---

# Risky user report - Microsoft Entra ID Protection | Microsoft Learn

Knowing which users are at risk and *why* they're at risk is a key responsibility of security and identity administrators. The Risky user report in Microsoft Entra ID Protection provides the full report, along with a risk data summary, and an activity timeline.

The Risky user report is also integrated with the Identity Risk Management Agent (Preview) for enhanced agent suggestions and insights. If you have the Identity Risk Management Agent enabled, you can switch between the standard view and the agent view of the report.

This article provides an overview of the information and actions available in the Risky user report.

## Prerequisites

To access this report, you need:

- Microsoft Entra ID Free, Microsoft Entra ID P1 for limited data on users.
- Microsoft Entra ID P2 licenses for full access to the risky user data.
- [Security Reader](../identity/role-based-access-control/permissions-reference#security-reader) and [Security Operator](../identity/role-based-access-control/permissions-reference#security-operator) are the least privileged roles required to use the *standard view* of the report.
- [Security Administrator](../identity/role-based-access-control/permissions-reference#search-administrator) is required to use the *agent view* of the report and access the Identity Risk Management Agent features.
- [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator) is required to reset passwords.

## Risky user report

The standard view of the Risky user report contains three main sections: The summary chart of risky users at each level, new risky users per day, and the full list of risky users. If you have the [Identity Risk Management Agent](identity-risk-management-agent-risky-user-report) turned on, you can use the **Agent view** to see agent suggestions and insights.

The **Percentage of risky users at each risk level** chart shows a visual representation of your user and their risk levels. This visual summary allows you to quickly see the state of things in your organization. Hover over each segment of the chart to see the percentage of users at each risk level.

[![Screenshot of the Percentage of risky users at each risk level chart.](media/concept-risky-user-report/risky-users-pie-chart.png)](media/concept-risky-user-report/risky-users-pie-chart.png#lightbox)

The **New risky users per day** chart shows a timeline of when risky users were detected in your organization. The chart also indicates if risk was remediated by the user or an administrator. Hover over any point in the chart to see the breakdown of the risky users and remediation activity.

[![Screenshot of the New risky users per day chart.](media/concept-risky-user-report/risky-users-bar-graph.png)](media/concept-risky-user-report/risky-users-bar-graph.png#lightbox)

The lower half of the report contains the full list of risky users.

- Select the name of a risky user to see their risk details.
- Select the checkbox next to one or more users to take action, such as confirm compromise or dismiss the risk.
- If action options are greyed out, you need a higher privileged role. For more information, see [What is Microsoft Entra ID Protection](overview-identity-protection#required-roles).

[![Screenshot of the risky users list.](media/concept-risky-user-report/risky-users-list.png)](media/concept-risky-user-report/risky-users-list-expanded.png#lightbox)

## Risky user details

From the Risky User Details page, you can take actions such as dismissing the risk or resetting the user's password.

From the **Risky users report**, select a user to view more details about their risk events and even take action on that user.

The details include basic information about the user and a timeline of recent risk activities. The **Timeline** section provides a chronological view of risk events associated with the user. The timeline shows when the risk was detected, the risk level, and the type of risk detected.

To see risk sign-in events together with risky user events, select the **Aggregate risk signals by risky sign-ins** checkbox.

### Unified risk signals

Microsoft Entra ID Protection correlates signals from Microsoft Defender and other sources to provide unified risk signals for user risk detections. This capability calculates a comprehensive Identity Risk Score based on multiple identity signals from across your identity fabric, including linked accounts and account sets.

You can view unified risk signals in both the standard view and agent view of the Risky user report. Select a user from the list to see details for each linked account associated with a risky user, helping you understand the full scope of risk across a user's identity. When the Identity Risk Score is raised, the Microsoft Entra score is also raised, which can automatically trigger your risk-based Conditional Access policies.

The Identity Risk Score appears within the context of a selected user from the risky user report. The score, risk summary, and links to investigate further are provided to help you understand the risk and take appropriate action. Select the **View full report in Microsoft Defender** link to see the correlated signals in Microsoft Defender for Identity and investigate the risky user further.

For full details on how unified risk works, prerequisites, how to enable the feature, and troubleshooting, see [Unified risk signals in Microsoft Entra ID Protection](concept-identity-protection-unified-risk).

## Take action on a risky user

Taking action on the user level applies to all the detections currently associated with that user. If the action buttons are greyed out, you need a higher privileged role. Administrators can take action on users and choose to:

- **Reset password** - This action revokes user's current sessions.
- **Confirm user compromised** - This action is taken on a true positive. ID Protection sets the user risk to high and adds a new detection, Admin confirmed user compromised. The user is considered risky until remediation steps are taken.
- **Confirm user safe** - This action is taken on a false positive. Doing so removes risk and detections on this user and places it in learning mode to relearn the usage properties. You might use this option to mark false positives.
- **Dismiss user risk** - This action is taken on a benign positive user risk. This user risk we detected is real, but not malicious, like those from a known penetration test. Similar users should continue being evaluated for risk going forward.
- **Block user** - This action blocks a user from signing in if attacker has access to password or ability to perform MFA.
- **Investigate with Microsoft 365 Defender** - This action takes administrators to the Microsoft Defender portal to allow an administrator to investigate further.