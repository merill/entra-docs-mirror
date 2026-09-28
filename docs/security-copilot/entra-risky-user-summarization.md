---
layout: Conceptual
title: Investigate risky users with Copilot | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-risky-user-summarization
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Use Copilot in Microsoft Entra to quickly respond to identity threats by summarizing the risk level for a user and receiving insights relevant to the incident.
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: how-to
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: b98a2c08-7785-bd0b-5614-efdf0e31b71f
document_version_independent_id: b98a2c08-7785-bd0b-5614-efdf0e31b71f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-risky-user-summarization.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-risky-user-summarization
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-risky-user-summarization.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1ed6a876-f728-0df2-90ab-5f06cbba58b8
---

# Investigate risky users with Copilot | Microsoft Learn

Microsoft Entra ID Protection applies the capabilities of [Copilot in Microsoft Entra](/en-us/security-copilot/microsoft-security-copilot) to summarize a user's risk level, provide insights relevant to the incident at hand, and provide recommendations for rapid mitigation. Identity risk investigation is a crucial step to defend an organization. Copilot in Microsoft Entra helps reduce the time to resolution by providing IT admins and security operations center (SOC) analysts the right context to investigate and remediate identity risk and identity-based incidents. Risky user summarization provides admins and responders quick access to the most critical information in context to aid their investigation.

Respond to identity threats quickly:

- Risk summary: summarize in natural language why the user risk level was elevated.
- Recommendations: get guidance on how to mitigate and respond to these types of attacks, with quick links to help and documentation.

This article describes how to access the risky user summary capability of Microsoft Entra ID Protection and Copilot in Microsoft Entra. Using this feature requires [Microsoft Entra ID P2 licenses](/en-us/entra/id-protection/overview-identity-protection#license-requirements).

Note

If the [Identity Risk Management Agent](/en-us/entra/id-protection/identity-risk-management-agent-get-started) is enabled in your tenant, you will see a separate risky user summary in this view.

## Prerequisites

- A tenant with Security Copilot enabled. Refer to [Get started with Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot#option-2-provision-capacity-in-azure) for more information.

## Investigate risky users

To view and investigate a risky user:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as at least a [Security Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#security-reader).
2. Navigate to **ID Protection** &gt; [Risky users](https://aka.ms/entracopilotriskyuser).
3. Select a user from the risky users report.

    ![Screenshot that shows the ID Protection risky users report.](media/copilot-entra-risky-user-summarization/risky-users-report.png)
4. In the **Risky User Details** window, information appears in **Summarize**.

    ![Screenshot that shows the ID Protection risky user summarization details.](media/copilot-entra-risky-user-summarization/risky-user-details.png)

The risky user summary contains three sections:

- Summary by Copilot: summarizes in natural language why ID Protection flagged the user for risk.
- What to do: lists the next steps to investigate this incident and prevent future incidents.
- Help and documentation: lists resources for help and documentation.

In this example, suggested remediations are to:

- Create sign-in risk and user risk based [Conditional Access policies](/en-us/entra/id-protection/howto-identity-protection-configure-risk-policies).

Suggested help and documentation are:

- [What is risk in ID Protection?](/en-us/entra/id-protection/concept-identity-protection-risks)
- [Incident Response Playbooks](/en-us/security/operations/incident-response-playbooks)
- [Risk-based Access Policies](/en-us/entra/id-protection/concept-identity-protection-policies)

## Investigate risky users using Copilot

Launch Security Copilot from the **Copilot** button in the Microsoft Entra admin center. Use natural language questions or prompts to:

- List or identify users based on risk
- Extract user-specific risk information
- Summarize user risk history

### List or identify users based on risk

Using Microsoft Security Copilot, you can easily retrieve and summarize information about user risk status in your system.

For example:

- *List all users currently flagged as risky.*
- *Show users who are currently at risk.*
- *Identify users who have been marked as risky.*
- *List all users who have been compromised.*
- *Show users who are currently considered safe.*
- *How many users are currently flagged as risky?*
- *Provide a count of all risky users.*

### User-specific risk information

Using Microsoft Security Copilot, you can focus in on a specific user and identify their risk level.

For example:

- *Determine if this user is currently high risk*
- *Display detailed risk information for this user*

### User risk history

Using Microsoft Security Copilot, you can retrieve past information about a user over time to establish their risk history.

- *Show the risk history for this user*
- *Has this user ever been flagged as risky*
- *Was this user previously at risk*