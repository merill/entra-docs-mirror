---
layout: Conceptual
title: Identity Risk Management Agent - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/identity-risk-management-agent-get-started
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Learn about the Identity Risk Management Agent and its role in identifying and mitigating risks within Microsoft Entra ID Protection.
ms.topic: concept-article
ms.date: 2025-12-01T00:00:00.0000000Z
ms.reviewer: chuqiaoshi
locale: en-us
document_id: f95b121f-9de1-7517-881f-67c2f355a7cd
document_version_independent_id: f95b121f-9de1-7517-881f-67c2f355a7cd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/identity-risk-management-agent-get-started.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/identity-risk-management-agent-get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/identity-risk-management-agent-get-started.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 29f77155-5534-74a5-6529-6d8dd9f9fba7
---

# Identity Risk Management Agent - Microsoft Entra ID Protection | Microsoft Learn

IT administrators and security analysts face mounting pressure to identify and respond to threats quickly while managing increasingly complex environments. They're often overwhelmed by the sheer volume of alerts, struggle to prioritize which risks need immediate attention, and find it difficult to connect scattered data points across their organization's systems. The Identity Risk Management Agent with Security Copilot in Microsoft Entra helps these professionals investigate potential risks, understand their effect, and take decisive action to protect their organization's critical assets.

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

### Known limitations

- Each agent run currently investigates up to 100 risky users. To customize the scope within this limitation, use the Agent Scope Setting.
- Once an agent run starts, it can't be stopped or paused. It can take 10-15 minutes to finish the run on 100 users.
- The agent currently analyzes user identity only. At this time, agent analysis on Workload Identities isn't supported.
- Agent suggestions require manual admin approval. At this time, automatic remediation isn't supported.
- The agent reasons over Microsoft Entra data, such as sign-in logs, risk detections, risky users, and audit logs.
- Investigation summaries and recommendations are AI-generated and might be incomplete or incorrect. Review before enforcement and use human judgment when applying changes.

## How it works

If the agent identifies new risky identities that weren't previously identified, it takes the following steps. **The initial scanning steps do not consume any SCUs.**

1. The agent checks for new risky users in your tenant who currently have a risk state of "At risk".
2. The agent identifies risky users that are within your defined [scope settings](identity-risk-management-agent-settings#scope).

If the agent identifies something that wasn't previously suggested, it takes the following steps. **These agent action steps consume SCUs.**

1. **Investigate the risky user**: The agent checks the user's risky sign-ins and risk detections to analyze what's risky about this user.
2. **Generate findings and a risk summary:** The agent generates findings based on the investigation, which includes a thorough risk summary explaining the suggestion and defining the key risk factors.
3. **Generate a recommended remediation action**: The agent suggests a remediation action, using the information gathered during the investigation.
4. **Answer questions through chat**: IT administrators ask the agent questions related to the risky users and the risk summary.
5. **Store custom instructions in agent memory**: Customers can give the agent custom instructions through agent chat, which the agent stores in its memory and applies for future runs. Currently, agent memory can store preferred remediation recommendations.

Note

Agent memory currently stores recommended actions only. Remediations are not executed automatically; instead, custom instructions are used to update the agent’s recommendations.

## Getting started

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **ID Protection** &gt; **Risky users**.
3. From the banner message at the top of the report, select **Start agent** to begin your first run.

    - Avoid using an account with a role activated through PIM.
    - A message that says "The agent is starting its first run" appears in the upper-right corner.
    - The first run might take a few minutes to complete.