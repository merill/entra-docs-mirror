---
layout: Conceptual
title: Microsoft Entra ID Protection to Self-Remediate User Risk - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/id-protection-guide-remediate
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra-id-protection
manager: martinco
description: Learn how IT administrators use Microsoft Entra ID Protection to identify and remediate identity risks for users that access enterprise-managed resources.
ms.reviewer: gasinh
ms.topic: concept-article
ms.date: 2025-10-31T00:00:00.0000000Z
locale: en-us
document_id: 19430a8c-6c90-fc26-cb92-8132f5322d40
document_version_independent_id: 19430a8c-6c90-fc26-cb92-8132f5322d40
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/id-protection-guide-remediate.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/id-protection-guide-remediate
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/id-protection-guide-remediate.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c618e0c5-a1ba-40b8-37f6-2ae50acb160b
---

# Microsoft Entra ID Protection to Self-Remediate User Risk - Microsoft Entra | Microsoft Learn

The proof-of-concept (PoC) guidance in this series of articles helps you to learn, deploy, and test Microsoft Entra ID Protection to detect, investigate, and remediate identity-based risks.

An overview of the guidance begins with [Introduction to Microsoft Entra ID Protection proof-of-concept guidance](id-protection-guide-introduction).

Detailed guidance continues with these scenarios:

- [Use real-time risk detection to grant access to protected resources](id-protection-guide-detect)
- [Master risk analysis for effective remediation](id-protection-guide-analyze)
- [Bring identity risk-related telemetry into security investigations](id-protection-guide-investigate)

This article helps administrators to identify and remediate identity risks for users accessing enterprise-managed resources, including Microsoft 365. Use real-time and offline risk detections to evaluate sign-ins and user behavior. Apply automated responses such as multifactor authentication (MFA), password resets, or block access based on risk levels. Risk-based conditional access policies that scale across large environments enforce these protections.

Configure the following features for user self-remediation of identity risk for enterprise-managed resources with Microsoft Entra ID Protection:

- Configure risky sign-in self-remediation
- Configure password reset protection and self-service
- Enforce Conditional Access
- Configure visibility into account health
- [Integrate with Microsoft Defender for incident correlation and investigation](/en-us/defender-xdr/incidents-overview)

## Configure risky sign-in self-remediation

Prompt Microsoft 365 users that you enroll in Microsoft Entra ID Protection to complete multifactor authentication (MFA) upon [risky sign-in detection](../id-protection/howto-identity-protection-remediate-unblock).

## Configure password reset protection and self-service

Configure password protection features, especially in large Microsoft 365 environments where password hygiene and autonomy are critical.

1. Configure [password protection policies](../identity/authentication/concept-password-ban-bad) that block weak or banned passwords.
2. To allow users to securely recover access with multiple authentication methods, configure [self-service password reset (SSPR)](../id-protection/howto-identity-protection-configure-risk-policies#user-risk-policy-in-conditional-access).
3. [Move to phishing-resistant passwordless authentication.](../identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication)

## Enforce Conditional Access

Configure Conditional Access policies for users with dynamic enforcement based on:

1. [Sign-in risk](../id-protection/concept-identity-protection-risks) such as from an unfamiliar location or device.
2. [User risk](../id-protection/concept-identity-protection-risks#user-risk-detections) such as leaked credentials or suspicious behavior.

Require users to verify their identity or restrict access to sensitive apps until after risk mitigation.

## Configure visibility into account health

Configure user alerts and notifications for the following scenarios:

1. Suspicious activity on their account.
2. Required actions to maintain access such as reauthentication or device compliance.