---
layout: Conceptual
title: ID Protection for Agents - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/concept-risky-agents
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Learn about how Microsoft Entra ID Protection identifies risky agents.
ms.topic: how-to
ms.date: 2026-06-17T00:00:00.0000000Z
ms.reviewer: etbasser, owinfrey
locale: en-us
document_id: 7475c386-a4ff-f645-bf9a-555dc62f5085
document_version_independent_id: 7475c386-a4ff-f645-bf9a-555dc62f5085
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/concept-risky-agents.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/concept-risky-agents
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/concept-risky-agents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e6a48e57-c926-471c-ca6e-f4b3ad4edd99
---

# ID Protection for Agents - Microsoft Entra ID Protection | Microsoft Learn

As organizations adopt, build, and deploy autonomous AI agents, the need to monitor and protect those agents becomes critical. Microsoft Entra ID Protection helps protect your organization by automatically detecting and responding to identity-based risks on agents that have agent identities provided by [Microsoft Entra Agent ID](../agent-id/what-is-microsoft-entra-agent-id).

## Prerequisites

### Roles

To use our Risky Agent reports, you must have one of the following administrator roles assigned.

- [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator)
- [Security Operator](../identity/role-based-access-control/permissions-reference#security-operator)
- [Security Reader](../identity/role-based-access-control/permissions-reference#security-reader)

To configure policies that use Agent Risk as a condition, you must have the [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) role assigned.

### Licensing

Starting soon, ID Protection for agents will require a [Microsoft Agent 365 license](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing) to extend protection to agents through [Microsoft Entra Agent ID](../agent-id/what-is-microsoft-entra-agent-id#how-to-get-started).

## How it works

Because agents can operate autonomously and on behalf of a user, they can display unique sign-in behavior. Agents can take initiative, interact with sensitive data, and operate at scale. Microsoft Entra ID Protection for agents identifies and mitigates risks associated with these capabilities. **Learning Mode** automatically suppresses behavioral alerts for agents that lack sufficient activity history, preventing false positives during onboarding and after periods of inactivity. A separate detection runs in parallel to ensure genuinely malicious early-life behavior is still caught. Once an agent exhibits suspicious behavior, ID Protection flags the activity as risky.

## Activities contributing to risk

The following table provides the anomalous activities that can contribute to the agent being flagged for risk. At this time, all risk detections for risky agents are offline.

Note

In on-behalf-of (OBO) flows, where an agent acts using a user's delegated permissions, risky activity is attributed to the **user** rather than the agent. This approach targets remediation at the compromised user session without disrupting the agent for other users. Unless noted otherwise, risk detections in this table apply only to autonomous agent activity.

| Agent risk detection | Description | riskEventType |
| --- | --- | --- |
| Confirmed compromised | Admin confirmed agent compromised | adminConfirmedAgentCompromised |
| Early life malicious activity | Newly created agent immediately exhibited multiple suspicious behavior patterns, acting like an attacker. | earlyLifeMaliciousActivity |
| Entra Directory Reconnaissance | Agent performed suspicious reconnaissance or high-risk directory operations. | entraDirectoryReconnaissance |
| Failed access attempt | Agent attempted and failed to access resources for which it isn't authorized. This detection can indicate an attacker is attempting to replay an agent's token against an unauthorized resource. | failedAccessAttempt |
| Microsoft Entra threat intelligence | Microsoft identified activity that is consistent with known attack patterns based on its internal and external threat intelligence sources. | threatIntelligenceAccount |
| Sign-in spike | Agent made a higher number of sign-ins compared to its usual sign-in frequency. This spike can be an indicator that an attacker is using automation or a toolkit. | signInSpike |
| Suspicious credential usage | This detection flags when new credentials are added to agent blueprints and then actually used. | suspiciousCredentialUsage |
| Unfamiliar resource access | Agent targeted resources that it doesn't usually access. This detection can mean that an attacker is trying to access sensitive resources beyond the agent's intended purpose. | unfamiliarResourceAccess |

## View the risky agent report

The **Risky Agents** report provides a list of all agents that were flagged for risky behavior. A summary of risky agents appears on the [ID Protection Dashboard](id-protection-dashboard). This snapshot view provides an overview of the number of agents flagged for risk by risk level. Select **View risky agents** to open the full report.

You can also navigate directly to the **Risky Agents** report from the ID Protection navigation menu. Filter and sort to find specific agents, risk states, or risk levels.

[![Screenshot showing the Risky agents report.](media/concept-risky-agents/risky-agents-report.png)](media/concept-risky-agents/risky-agents-report.png#lightbox)

You can take action on agents directly from the report, including:

- **Confirm compromise**: Select after manual investigation or automated detection confirms the account is compromised. This step is useful as part of incident response to prevent further damage. Confirm compromise automatically sets the risk level to High and creates an event in the agent's **Risk detections**. This action triggers risk-based Conditional Access policies that are configured to block access on High Agent Risk.
- **Confirm safe**: Marks the user as safe after investigation and clears any active risk state for that user by setting risk level to None. Use this option when you want to mark a false positive and for the system to avoid flagging similar activity.
- **Dismiss risk**: Tells the system that the detected risk for an agent is no longer relevant after investigation, or is a benign true positive where you want the system to continue to flag similar activity.
- **Disable**: Prevents all sign-ins for that agent across Microsoft Entra ID and connected apps.

## View the risky agent details

In the risky agent report, select an entry to view the full details including the corresponding risk detections for that agent. Just like with all ID Protection risk reports, you can take action on the agent directly from the report or from the details view.

**Risky agent details** include:

- Agent display name and ID
- Risk state and risk level
- Agent type and sponsors (if specified)

You can also navigate to the **Risk Detections** report and select the **Agent detections** tab to view a full list of the detection risk events from up to the past 90 days. Risk detections are retained for up to 90 days for investigation purposes.

[![Screenshot showing the Risky agent details.](media/concept-risky-agents/risky-agent-details.png)](media/concept-risky-agents/risky-agent-details.png#lightbox)

## Risk-based Conditional Access for agents

Use [Conditional Access for agents](../identity/conditional-access/agent-id) to set risk policies that block risky agents from accessing resources or other agents. Use this [Conditional Access template](https://aka.ms/CreateAgentRiskPolicy) to simplify deploying this policy in your organization.

## Microsoft Graph

You can also query risky agents [using the Microsoft Graph API](/en-us/graph/use-the-api). There are two collections in the [ID Protection APIs](/en-us/graph/api/resources/identityprotection-overview).

- `riskyAgents`
- `agentRiskDetections`

## Export risk data

You can export data by configuring [diagnostic settings in Microsoft Entra ID](howto-export-risk-data) to send risk data to a Log Analytics workspace, archive it to a storage account, stream it to an event hub, or send it to a SIEM solution.