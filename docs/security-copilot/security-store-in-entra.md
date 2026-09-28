---
layout: Conceptual
title: Discover and deploy agents and solutions in Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/security-store-in-entra
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Learn how to use Security Store in Microsoft Entra to discover, purchase, and deploy AI agents and security solutions for identity and access management.
ms.date: 2026-03-17T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: how-to
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
ai-usage: ai-assisted
locale: en-us
document_id: b209108c-d0b9-b655-58ab-0db5e3ce7f12
document_version_independent_id: b209108c-d0b9-b655-58ab-0db5e3ce7f12
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/security-store-in-entra.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/security-store-in-entra
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/security-store-in-entra.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: dce1e1aa-500b-cf63-9bdf-b9ab355892ec
---

# Discover and deploy agents and solutions in Microsoft Entra | Microsoft Learn

[Security Store](/en-us/security/store/what-is-security-store) in the Microsoft Entra admin center offers agents and integrated solutions that can help you perform identity and access management tasks efficiently. These offerings include [Microsoft Security Copilot agents](/en-us/copilot/security/agents-overview) published by Microsoft and approved partners. Security Store also provides non-agentic solutions that integrate with Microsoft Entra products and can deliver capabilities such as advanced fraud prevention directly into your identity workflows.

This article explains how to discover and deploy AI agents and solutions in Microsoft Entra.

Note

To learn more about publishing agents to Security Store, see [Publish agents to Microsoft Security Store](/en-us/security/store/publish-a-security-copilot-agent-or-analytics-solution-in-security-store).

## Prerequisites

To purchase and deploy agents and solutions from Security Store, you need:

- [Access to a Security Copilot workspace provisioned with SCU capacity](/en-us/copilot/security/get-started-security-copilot).
- For partner-published agents and solutions, you need the [Azure subscription contributor or owner role](/en-us/marketplace/roles-permissions).

## Agents in the Security Store

Security Store includes Microsoft Entra agents that automate identity and access management tasks. For a complete list of available agents, their capabilities, required permissions, and setup instructions, see [Microsoft Entra agents](entra-agents).

## Solutions in the Security Store

The following solutions are available through Security Store in the Microsoft Entra admin center.

- **Verified ID solutions**: [Microsoft Entra Verified ID](/en-us/entra/verified-id/) solutions available in the Security Store provide advanced fraud prevention capabilities. These solutions integrate directly into your identity verification workflows, enabling enhanced trust and security for credential issuance and verification scenarios.
- **External ID solutions**: [Microsoft Entra External ID](/en-us/entra/external-id/) solutions available in the Security Store deliver WAF and bot defense to strengthen your organization's edge protection. These solutions help secure customer-facing applications and protect against automated threats targeting your external identity infrastructure.

## Discover and deploy agents and solutions in the Microsoft Entra admin center

Security Store is embedded in the Microsoft Entra admin center, so you can discover and deploy agents and solutions without leaving your identity management workflow.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Security Store**.
3. Browse or search for the agent or solution you want to deploy.

    - Use the **All** and **Agent** tabs to filter results.
4. Select the agent or solution to view its details, including capabilities, requirements, and setup instructions.
5. To purchase and deploy the agent or solution:

    - Select **Get agent** or **Get solution** to begin the deployment process if you have sufficient permissions.
    - Select **Copy link** to copy the details page URL and share it with a security administrator, if you don't have permissions to deploy agents or solutions.
    - For partner-published agents, complete the purchase and deploy on the [Security Store website](https://securitystore.microsoft.com/), as described in the [Microsoft Security Store documentation](/en-us/security/store/get-agents-in-security-store).

    Tip

    You can manage centralized purchases for partner-published agents through public offers, or through private offers, as described in [How to purchase SaaS solutions (private offers)](/en-us/security/store/how-to-purchase-saas-solutions-private-offers).
6. After purchasing an agent, select **Security Copilot** &gt; **Agents**, find your agent in the **Ready for setup** section, and then select **Set up** to begin agent setup.

After setup, the agent appears in the **Agents in use** section.

## Manage and remove agents

Agents deployed from Security Store are managed through [Microsoft Security Copilot](/en-us/copilot/security/microsoft-security-copilot).

- To manage agent settings, go to **Security Copilot** &gt; **Agents** and select the agent you want to configure.
- To remove an agent, perform the removal in Security Copilot. Removing the agent in Security Copilot stops entitlement checks and billing.
- For partner-published agents, review billing and entitlement details in **Security Store** &gt; **Management** &gt; **My Solutions**.

For more information, see [Manage Security Copilot agents](/en-us/copilot/security/agents-manage).