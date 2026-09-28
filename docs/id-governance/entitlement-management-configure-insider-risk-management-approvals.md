---
layout: Conceptual
title: Configure Insider risk management-based approvals for access package requests in Entitlement Management (Preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-configure-insider-risk-management-approvals
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article describes how to configure Insider risk management-based approvals for access package requests.
ms.subservice: entitlement-management
ms.topic: how-to
ms.date: 2025-11-04T00:00:00.0000000Z
locale: en-us
document_id: 6b282c8f-77b7-3154-eb43-5d57ea58b017
document_version_independent_id: 6b282c8f-77b7-3154-eb43-5d57ea58b017
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-configure-insider-risk-management-approvals.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-configure-insider-risk-management-approvals
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-configure-insider-risk-management-approvals.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2dd3324d-dff7-6ee1-a8c3-6404f88c5f1d
---

# Configure Insider risk management-based approvals for access package requests in Entitlement Management (Preview) - Microsoft Entra ID Governance | Microsoft Learn

Making sure risky users don't gain access to sensitive resources is an important part of securing your environment. You can further secure the entitlement management request process by integrating [Microsoft Purview Insider Risk Management (IRM)](/en-us/purview/insider-risk-management-configure) signals into the access package approval workflow in Microsoft Entra ID Governance’s Entitlement Management. With risk management-based approvals, Entitlement Management automatically adds a new first approval stage when a user flagged as risky requests access to an access package. This ensures that users identified as potentially compromised or at-risk are reviewed by authorized security or compliance approvers before access requests are routed for standard approval routing. This article describes how to further secure your entitlement request process with Insider risk management.

## License requirements

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals). You must also have [appropriate licensing for Microsoft Purview](/en-us/purview/insider-risk-management-configure#subscriptions-and-licensing).

## Prerequisites

To use Insider Risk Management approvals with Entitlement management, you must first [Create an Insider Risk Management policy](/en-us/purview/insider-risk-management-plan).

## How risk-based approvals work

When a user requests access to an access package through the **My Access** portal:

1. **Risk evaluation**: Entitlement Management queries Microsoft Purview Insider Risk Management for the user’s current userRiskLevel
2. **Configuration check**: If the user’s risk level matches one of the administrator-selected thresholds (for example, Moderate or Elevated), Entitlement Management automatically adds an additional risk-based approval stage before the standard approval process.
3. **Automatic approver assignment**:

    - The request is routed to users assigned the Compliance Administrator role in Microsoft Entra ID.
4. **Compliance review**: The assigned approvers review the user’s risk details and decide whether to approve or deny this stage of the request approval routing.

    - If approved, the request continues through the rest of the regular access package approval steps.
    - If denied, the request is closed, recorded in the audit logs, and no further approval routing takes place.
5. **Audit logging**: All actions (approval and denial) and outcomes are captured in [Entitlement Management logs](entitlement-management-logs-and-reporting) for reporting and compliance visibility.

## Configure Insider Risk Management-based approvals for an access package using the Microsoft Entra admin center

To configure Insider Risk Management-based approvals for an access package in the Microsoft Entra admin center, you'd do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Control configurations**.
3. On the control configurations screen, you're able to see the options[![Screenshot of the control configuration cards in Entitlement Management.](media/entitlement-management-configure-risk-approvals/control-configurations-cards.png)](media/entitlement-management-configure-risk-approvals/control-configurations-cards.png#lightbox)
4. On the card **Risk-based approval (Preview)**, select **View settings**.
5. On the risk-based approval page, next to **Require approval for users with insider risk level (Preview)**, select **Customize**. (See the separate article to configure [ID Protection-based approvals](entitlement-management-configure-id-protection-approvals).) ![Screenshot of the risk-based approval overview screen.](media/entitlement-management-configure-risk-approvals/risk-based-approval-overview.png)
6. You can set the insider risk level and then select **Save**.![Screenshot of the insider risk level settings in entitlement management.](media/entitlement-management-configure-risk-approvals/insider-risk-levels-settings.png)

## Reviewing a risky user's request

To review the pending request from a risky user, the approver must have the [Compliance Administrator](../identity/role-based-access-control/permissions-reference#compliance-administrator) role.

When a risky user submits a request for an access package, administrators are able to see their pending status via the requests page within the access package:

![Screenshot of a pending request for an access package by a risky user.](media/entitlement-management-configure-risk-approvals/insider-risky-user-pending-request.png)

A user set as an approver, or fallback approver, for risky users can view the request to approve or deny via the my access portal: [![Screenshot of approving a risky user from insider risk management.](media/entitlement-management-configure-risk-approvals/insider-risky-user-approvals.png)](media/entitlement-management-configure-risk-approvals/insider-risky-user-approvals.png#lightbox)

Note

Approvers have a maximum of 14 days to take action. If they don't take action within that time frame, requests are automatically denied.