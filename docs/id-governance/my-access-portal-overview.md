---
layout: Conceptual
title: What is the My Access portal? - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/my-access-portal-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: A description of the My Access portal where users can manage access within Microsoft Entra.
ms.topic: overview
ms.date: 2024-12-10T00:00:00.0000000Z
locale: en-us
document_id: d1ee0ddc-e767-7f54-3cad-7e97afb261a2
document_version_independent_id: d1ee0ddc-e767-7f54-3cad-7e97afb261a2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/my-access-portal-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/my-access-portal-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/my-access-portal-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 67fb7744-7e79-6f92-1a9a-c0f910bf0e3c
---

# What is the My Access portal? - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn

My Access is a web-based portal used by users to review or request access to resources within Microsoft Entra, and by Administrators to configure this access. Depending on who is using the My Access portal, a different set of actions can be taken.

Users access the My Access portal to:

- Request access for themselves
- Approve or deny access for themselves or direct reports
- Review access for themselves
- Review access for users
- Manage and review access for agents managed

Administrators, via the Microsoft Entra admin center, can configure:

- Access packages that users can request, or that can be assigned to agents
- Access reviews for access packages
- Access reviews for groups and applications
- The overview page

## License requirements

This feature requires Microsoft Entra ID Governance or Microsoft Entra Suite subscriptions, for your organization's users. Some capabilities, within this feature, may operate with a Microsoft Entra ID P2 subscription. For more information, see the articles of each capability for more details. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

Using [Microsoft Entra ID Governance](licensing-fundamentals) for agent identities requires one of the following license plans:

- **Microsoft 365 E7**, which includes Agent 365 and Microsoft Entra Suite, to provide governance of user and agent identities.
- **Microsoft Agent 365** license paired with at least Microsoft Entra P1 or Microsoft 365 E3.

For more information, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing). For the full list of agent-specific capabilities, refer to the **Microsoft Agent 365** column in the [Microsoft Entra ID Governance licensing table](licensing-fundamentals).

## Overview page

The Overview page shows you key tasks that need your attention such as pending requests and reviews. It's the landing page for the My Access portal.

## Discover access packages

In the My Access portal, you can view the access packages you can request by selecting **Access packages** in the left-hand menu and the **Available** tab. Find the access package you want to request access to in the list. You can search for an access package by name, description, or resources via the search bar. Once you locate the access package, select the row. You might have to answer questions and provide business justification for your request.

Select Request history in the left-hand menu to see a list of your requests and the status.

For more information, see [Request an access package - entitlement management](entitlement-management-request-access).

## Approve or deny a request

In the My Access portal, you can view your pending requests by selecting **Approvals** in the left-hand menu. Select a pending request and review the details. Based on the information provided, approve or deny the request.

For more information, see [Approve or deny access requests - entitlement management](entitlement-management-request-approve).

## Review access

In the My Access portal, you can view your pending access reviews by selecting **Access reviews** in the left-hand menu. On this page, select the specific review, and make a decision based on the information provided.

Microsoft Entra ID will also send you an email with instructions shortly after the review starts. Follow the instructions in the email to complete the review.

For more information about self-reviews, see: [Review your access to resources in access reviews](self-access-review).

For more information about reviews for others, see: [Review access to groups & applications in access reviews](perform-access-review).

## Manage agents

In the My Access portal, you can view a list of agent identities that you own and sponsor. For more about managing and sponsoring agent identities, see: [Administrative relationships for agent identities (Owners, sponsors, and managers)](../agent-id/agent-owners-sponsors-managers).

You're able to manage, approve, review, and enable the agent identities. For all agent identities you own or sponsor you're also able to see general information such as level of access, and agent identities activity. For more information on managing agent identities using the My Access portal, see: [Manage Agent (Preview)](../agent-id/manage-agent).