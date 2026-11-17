---
layout: Conceptual
title: Microsoft Entra Agent ID sign-in process | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/sign-in-process
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn about the Microsoft Entra Agent ID sign-in process, including consent pages, trust criteria, and how to manage agent permissions for secure access to AI agents using work accounts.
ms.topic: concept-article
ms.date: 2026-11-06T00:00:00.0000000Z
ai-usage: ai-assisted
ms.reviewer: dastrock
locale: en-us
document_id: 18bdae10-5562-7e2f-bfb2-fc5d1541fc38
document_version_independent_id: 18bdae10-5562-7e2f-bfb2-fc5d1541fc38
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/sign-in-process.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/sign-in-process
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/sign-in-process.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: edc9ebeb-a224-63f5-7d87-b7dd92b16c61
---

# Microsoft Entra Agent ID sign-in process | Microsoft Learn

When you sign in to an AI agent that uses Microsoft Entra Agent ID, a consent page explains the permissions the agent requests. Review the publisher and requested access before you approve.

This article explains how to assess that request, decide whether to approve it, and get help if the agent looks suspicious. The following image shows an example consent page:

![Screenshot of a sample consent page for signing in to an AI agent.](media/sign-in-process/consent-page.png)

## Sign-in to an agent

An AI agent is software that can perform tasks for you or your team. It might summarize information, watch for issues, send alerts, or prepare drafts you can review. Unlike a regular app that waits for you to select or type, an agent can act on its own within the limits you approve.

To sign you in, AI agents must register their product or service with Microsoft by creating an Agent ID. Each AI agent has a unique Agent ID.

An Agent ID allows the AI agent to:

- Sign you in and identify you.
- Request access to data and actions you allow.

## Consent pages

Agents need permissions before they can access your organization's data. Depending on your organization's policies and previous approvals, you might see requests to:

- **Add this agent to your organization.** This makes the agent available in your organization. If the agent is already added, you don't need to add it again.
- **Allow the agent to access data.** This request lists the information or actions the agent needs, such as reading your profile or email. You can allow or deny the request. Your organization might require administrator approval.

This page gives you control over how AI agents use your accounts and data you have access to.

## Trust an agent

The consent page includes information to help you assess the trustworthiness of an agent that you sign in to:

- The name of the agent, product, or service
- Whether the agent has completed Microsoft's publisher verification process
- The organization that published the agent
- Whether the agent is built by Microsoft

For details about the consent page, see [Application consent experience](../identity-platform/application-consent-experience).

**If you did not intentionally sign-in to this agent, always deny access. Never sign-in to apps or agents you're unfamiliar with.**

## Add agent to your organization

AI agents can't participate in your organization unless a member approves them. When you add an agent to your organization, the agent becomes available to you and other employees or members to use. The agent is able to sign-in other members and request access to their data and information.

An agent might also use a dedicated agent account to access resources that require a user account, such as a mailbox. Adding the agent doesn't give it unlimited permission to create accounts or access resources. Account creation and resource access remain subject to the permissions and policies approved by your administrator. For more information, see [Agent's user accounts](agent-users).

**If you're uncertain whether to add an agent to your organization, pause and contact your administrator.**

## Allow an agent to access data

Approving the agent to access data means the following:

- The agent can use the listed permissions without asking again each time.
- The agent can run in the background to carry out tasks you or your organization configured.

It doesn't give the agent unlimited access. It only gets the specific items shown and can't go outside them unless you or an administrator later grant more permissions.

**When in doubt, pause and ask your administrator if permissions are safe to grant to an agent**.

## Disable an agent or its permissions

You (or an administrator) can remove or disable the agent or its permissions. For more information, see [Manage agents in the end-user experience](manage-agent-identities-end-user). For global removal, administrators can delete the agent identity using Microsoft Graph API or Microsoft Entra PowerShell.

## Criteria to report a suspicious agent

Report an agent if:

- The publisher name looks wrong or suspicious.
- Permissions seem far too broad for the described task.
- You were prompted unexpectedly and no recent change explains it.
- The agent appears to misuse data.

Use the **report it here** link on the consent screen or notify your security desk.

## Need help?

If you're unsure, don't approve. Capture a screenshot, note the agent name, and contact your helpdesk or security team for guidance.