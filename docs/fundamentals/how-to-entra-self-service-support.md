---
layout: Conceptual
title: Microsoft Entra Self-Service Support - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/how-to-entra-self-service-support
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Discover how Microsoft Entra Self-Service Support uses AI and Microsoft Graph data to analyze product logs, resolve issues, and enhance IT admin workflows.
ms.reviewer: tychusnyanga
ms.date: 2026-03-09T00:00:00.0000000Z
ms.topic: how-to
locale: en-us
document_id: a8988d49-0493-bf97-2dc4-4335d448eda1
document_version_independent_id: a8988d49-0493-bf97-2dc4-4335d448eda1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/how-to-entra-self-service-support.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/how-to-entra-self-service-support
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/how-to-entra-self-service-support.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8450e751-78d9-2667-a5f0-8dc4c13dd947
---

# Microsoft Entra Self-Service Support - Microsoft Entra | Microsoft Learn

Microsoft Entra Self-Service Support is an AI-driven conversational support experience that enables IT admins to troubleshoot identity and access issues and get answers to product questions. This feature uses Microsoft public documentation from [learn.microsoft.com](/en-us/) as its knowledge base.

Self-Service Support analyzes product logs accessed with the Microsoft Graph API to identify the root cause of issues and provide relevant resolution guidance. The assistant is offered at no cost to Microsoft Entra customers. This article describes how to use Self-Service Support.

## Key features

Self-Service Support provides a conversational chat interface where users in the Microsoft Entra admin center can interact using natural language prompts. The chat experience can be initiated through the **Diagnose and solve problems** page.

Self-Service Support uses Microsoft Graph data and public documentation from [learn.microsoft.com](/en-us/) as a knowledge base to analyze failures and suggest step-by-step resolutions through guided troubleshooting. As you interact with Self-Service Support, it uses this knowledge base to provide context, explanations, and guidance.

If issues remain unresolved, you can seamlessly escalate them to Microsoft support. The assistant includes a feedback loop that lets you submit ratings and comments to help enhance the quality of responses.

## Prerequisites

Self-Service Support is available to users with permissions to create and manage support tickets, such as [Helpdesk Administrator](../identity/role-based-access-control/permissions-reference#helpdesk-administrator) and [Reports Reader](../identity/role-based-access-control/permissions-reference#reports-reader).

For a full list of roles, see [Least privileged role by task](../identity/role-based-access-control/delegate-by-task).

## How to work with the Microsoft Entra Support Assistant

1. Sign in to the Microsoft Entra admin center as at least a [Reports Reader](../identity/role-based-access-control/permissions-reference#reports-reader).
2. Go to **Diagnose and solve problems**.
3. Select **Self-Service Support**.

    [![Screenshot of the Microsoft Entra Support Assistant interface.](media/how-to-entra-support-assistant/support-assistant-button.png)](media/how-to-entra-support-assistant/support-assistant-button.png#lightbox)
4. Either select one of the prebuilt prompts or enter a natural language question in the text box.
5. Some responses provide the option to answer more questions or select a specific event to troubleshoot. Select an option to troubleshoot further.

    [![Screenshot of the Microsoft Entra Support Assistant with event option buttons highlighted.](media/how-to-entra-support-assistant/support-assistant-event-options.png)](media/how-to-entra-support-assistant/support-assistant-event-options.png#lightbox)
6. As you continue to provide further clarification or select specific events to troubleshoot, Self-Service Support uses Microsoft public documentation to provide context, explanations, and guidance. Select the appropriate option or enter more natural language prompts to continue.
7. After your initial question, you can ask follow-up questions to refine the troubleshooting process. On the third response (after two follow-up questions), the option to create a support request appears at the top of the window.

    [![Screenshot of the Microsoft Entra Support Assistant with the create support requestion option highlighted.](media/how-to-entra-support-assistant/support-assistant-support-request.png)](media/how-to-entra-support-assistant/support-assistant-support-request.png#lightbox)

### Special considerations

As you use the Microsoft Entra Support Assistant, keep in mind the following details:

- Self-Service Support conversation flow is dynamic and flexible, so each experience can vary slightly.
- Select **New chat** at the top of the window to refresh the conversation.
- At this time, Self-Service Support provides identity-related troubleshooting for the following types of scenarios:
    - Authentication and multifactor authentication failures
    - Device registration and sync issues
    - Microsoft Entra Connect provisioning errors
    - Conditional Access misconfigurations
    - Application SSO errors
- Self-Service Support can't perform actions in your tenant - it only provides guidance.
- Select **Switch to classic experience** at the top of the window to switch to the non-AI legacy search experience.

## Provide feedback

Each assistant response includes a feedback prompt for rating, comments, or suggestions. Use the "thumbs up" or "thumbs down" buttons to provide feedback on the responses. This feedback is important and is used to improve the accuracy of Self-Service Support.

​Self-Service Support might make mistakes or provide incomplete information. Always verify important actions and consult the official Microsoft documentation when needed. ​