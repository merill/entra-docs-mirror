---
layout: Conceptual
title: Security Copilot in Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/security-copilot-in-entra
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Use Security Copilot in Microsoft Entra to investigate identity risks and troubleshoot identity tasks quickly.
ms.reviewer: ptyagi
ms.date: 2026-04-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: concept-article
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
ai-usage: ai-assisted
locale: en-us
document_id: 976e3de7-1e47-0954-1b21-3d2e97e3e6b0
document_version_independent_id: 976e3de7-1e47-0954-1b21-3d2e97e3e6b0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/security-copilot-in-entra.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/security-copilot-in-entra
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/security-copilot-in-entra.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bbdf32c0-cf08-9cc3-ec0d-21ce4ab333e1
---

# Security Copilot in Microsoft Entra | Microsoft Learn

[Microsoft Security Copilot](/en-us/security-copilot/microsoft-security-copilot) is a platform that brings together the power of AI and human expertise to help administrators and security teams respond to attacks faster and more effectively. Microsoft Entra is one of the Microsoft plugins that enable the Security Copilot platform to generate accurate and relevant information. Through this plugin, Security Copilot can help you investigate and resolve identity risks, assess identities and access with AI-driven intelligence, and complete complex tasks quickly. Security Copilot gets insights from your Microsoft Entra users, groups, sign-in logs, audit logs, and more, while also providing contextualized insights and recommendations in security best practices.

You can explore sign-ins and risky users, get contextualized insights on how to resolve incidents, learn how to protect accounts using natural language. Built on top of real-time machine learning, Security Copilot can help you find gaps in access policies, generate identity workflows, and troubleshoot faster. Security Copilot can assist with scenarios across different products in the Microsoft Entra admin center, such as an incident investigation that includes the Microsoft Entra ID Protection risky user reports and Microsoft Entra sign-in logs.

## Security Copilot experiences

Security Copilot in Microsoft Entra includes the standalone Security Copilot experience, embedded experiences in the Microsoft Entra admin center, specialized agents that can perform tasks, and natural language prompts that can be used in several end-to-end scenarios.

For more information, see:

- [Microsoft Security Copilot experiences](/en-us/security-copilot/experiences-security-copilot)
- [Microsoft Security Copilot agents](/en-us/security-copilot/agents-overview)
- [Microsoft Security Copilot scenarios](entra-security-scenarios)

## Get started

In the Security Copilot platform, Microsoft Entra is a plugin that provides access to your organization's identity data and insights. To use Security Copilot in Microsoft Entra, you need to onboard to Security Copilot and turn on the Microsoft Entra plugin.

1. Onboard to Security Copilot by following the [Get started with Microsoft Security Copilot](/en-us/security-copilot/get-started-security-copilot)guide.
    - This guide contains guidance around subscription requirements, billing, and capacity.
    - Take a moment to [understand authentication in Microsoft Security Copilot](/en-us/security-copilot/authentication).
2. In the Security Copilot standalone experience, select the **Sources** icon from the prompt bar and turn on the Microsoft Entra plugin for Security Copilot, if it's not already on.

Once you're all set up in Security Copilot, you can start using [natural language prompts](/en-us/security-copilot/prompting-security-copilot) to help remediate identity-based incidents. You can always check the **Promptbook library** in the standalone [Security Copilot](https://securitycopilot.microsoft.com/) experience for more examples.

- *Give me all user details for karita@woodgrovebank.com and extract the user Object ID.*
- *Does karita@woodgrovebank.com have any registered devices in Microsoft Entra?*
- *List the recent risky sign-ins for karita@woodgrovebank.com.*
- *Can you give me sign-in logs for karita@woodgrovebank.com for the past 48 hours? Put this information in a table format.*
- *Get Microsoft Entra audit logs for karita@woodgrovebank.com for the past 72 hours. Put information in table format.*

## Access Copilot chat in the Microsoft Entra admin center

Copilot chat is available directly from the left side navigation in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Reader](../identity/role-based-access-control/permissions-reference#security-reader).
2. Select **Copilot chat** from the side navigation menu.

    [![Screenshot of the Copilot chat option in the Microsoft Entra admin center.](media/security-copilot-in-entra/copilot-chat-left-nav.png)](media/security-copilot-in-entra/copilot-chat-left-nav-expanded.png#lightbox)
3. Enter a question or task in the chat prompt bar, or select one of the suggestion cards to get started.

The **Entra Copilot** panel opens with the following options:

- **New chat**: Start a new conversation with Copilot.
- **Agent chat**: Select a specialized agent, such as the **Identity Risk Management Agent** or the **Conditional Access Optimization Agent**, to get targeted assistance.
- **Recent sessions**: View and resume previous Copilot chat sessions.

The Microsoft Entra Copilot chat experience is designed to meet you where you are in your workflow and stay with you when needed. You can expand or collapse the chat history pane on the left and switch between "sidecar mode" and "fullscreen mode" in the upper-right corner.

[![Screenshot of the Copilot chat buttons to expand and collapse the views.](media/security-copilot-in-entra/copilot-chat-collapse-buttons.png)](media/security-copilot-in-entra/copilot-chat-collapse-buttons.png#lightbox)

In addition, when you navigate around the Microsoft Entra admin center from the Copilot chat experience, the sidecar remains open in the new page, allowing you to continue your conversation with Copilot without interruption.

## Provide feedback

Copilot in Microsoft Entra uses AI and machine learning to process data and generate responses for each of the key features. However, AI-generated content might be incorrect. Your feedback on the generated responses helps improve the accuracy of Copilot and Microsoft Entra over time.

All key features have an option for providing feedback, but the exact steps vary based on the feature. Look for the thumbs up and thumbs down icons to let us know if the response was helpful or not.

![Screenshot of the Copilot thumbs up and thumbs down icons for providing feedback.](media/copilot-security-entra/thumbs-up-thumbs-down.png)

## Privacy and data security in Security Copilot

To understand how Security Copilot handles your prompts and the data that’s retrieved from the service(prompt output), see [Privacy and data security in Microsoft Security Copilot](/en-us/security-copilot/privacy-data-security).