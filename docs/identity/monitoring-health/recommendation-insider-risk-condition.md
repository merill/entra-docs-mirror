---
layout: Conceptual
title: Protect your tenant with Insider Risk in Conditional Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/recommendation-insider-risk-condition
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how you can protect your tenant by enabling the Insider Risk condition in Conditional Access integrated with Microsoft Purview Adaptive Protection.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.reviewer: poulomib
locale: en-us
document_id: b360aff2-9c84-9151-5685-b2fa12f75fb0
document_version_independent_id: b360aff2-9c84-9151-5685-b2fa12f75fb0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/recommendation-insider-risk-condition.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/recommendation-insider-risk-condition
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/recommendation-insider-risk-condition.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3c731f93-d08b-feb4-d05f-bb788e1512f8
---

# Protect your tenant with Insider Risk in Conditional Access - Microsoft Entra ID | Microsoft Learn

[Microsoft Entra recommendations](overview-recommendations) is a feature that provides you with personalized insights and actionable guidance to align your tenant with recommended best practices.

This article covers the recommendation to protect your tenant by enabling the Insider Risk condition in Conditional Access paired with Microsoft Purview Adaptive Protection. This recommendation is called `insiderRiskPolicy` in the recommendations API in Microsoft Graph.

## Description

Adaptive protection dynamically assigns appropriate Data Loss Prevention (DLP) policies to users based on the risk levels defined and analyzed by the machine learning models in insider risk management. With this new capability, static DLP policies become adaptive based on user context. The most effective policy, such as blocking data sharing, is applied only to high-risk users while low-risk users can maintain productivity.

These risk signals, when integrated with Conditional Access policies, allow Administrators to take appropriate actions for each risk level. Configuring Conditional Access policies with insider risk allows organizations to respond effectively to changing threat landscapes.

## Value

Implementing a Conditional Access policy that blocks access to resources for high-risk internal users is of high priority due to its critical role in proactively enhancing security, mitigating insider threats, and safeguarding sensitive data in real-time.

## Action plan

1. Enable [Adaptive Protection](https://compliance.microsoft.com/insiderriskmgmt?viewid=dynamicriskprevention&amp;innerviewid=summary) in Microsoft Purview.

    - You must be a member of the Insider Risk Management or Insider Risk Management Admins role group in Microsoft Purview to configure Adaptive Protection.
    - For information, see [Roles and role groups for Microsoft Purview](/en-us/microsoft-365/security/office-365-security/scc-permissions)
2. Create a [Conditional Access policy](https://entra.microsoft.com/#view/Microsoft_AAD_ConditionalAccess/CaTemplates.ReactView/templateIds%7E/%5B%2216aaa400-bfdf-4756-a420-ad2245d4cde8%22%5D) that includes the Insider Risk condition.

    - You must be signed in as a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator) to view this template.
    - For more information, see [Conditional Access conditions: Insider Risk](../conditional-access/concept-conditional-access-conditions#insider-risk).

## License requirements

Using this feature requires Microsoft Entra ID P2 licenses.