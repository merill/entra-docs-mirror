---
layout: Conceptual
title: Microsoft Security Copilot scenarios in Microsoft Entra Internet and Private Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-internet-access-private-access-scenarios
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Learn how to use Microsoft Security Copilot with Microsoft Entra Internet Access and Private Access
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: concept-article
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: 99c766a5-5d08-eaca-0c8f-9eff82a698a0
document_version_independent_id: 99c766a5-5d08-eaca-0c8f-9eff82a698a0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-internet-access-private-access-scenarios.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-internet-access-private-access-scenarios
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-internet-access-private-access-scenarios.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: 1c213fe9-f33c-a849-86b5-76ada4c53f6a
---

# Microsoft Security Copilot scenarios in Microsoft Entra Internet and Private Access | Microsoft Learn

[Microsoft Security Copilot](/en-us/security-copilot/microsoft-security-copilot) gets insights from your Microsoft Entra data through Global Secure Access network traffic analysis skills, enabling administrators to investigate and monitor network traffic usage and behavior using natural language queries. Network traffic analysis skills allow network administrators and security teams to analyze user, device, and branch network usage, identify network issues, and detect threats or policy violations in real time without the need to write complex queries.

## Microsoft Entra Internet Access and Private Access scenarios supported by Microsoft Security Copilot

Security Copilot is integrated into the Microsoft Entra admin center and works seamlessly with Microsoft Entra ID Protection features. The following table provides an overview of the scenarios supported by Security Copilot:

| Scenario | Role(s) | License | Tenant |
| --- | --- | --- | --- |
| Global Secure Access | [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator)[Global Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader)[Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator)[Global Secure Access Log Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-log-reader) | [Microsoft Entra ID P1 or P2 license](/en-us/entra/id-protection/overview-identity-protection#license-requirements)Entra Private Access License (for private access traffic)Entra Internet Access License (for general internet traffic outside Microsoft services) | Global Secure Access configured |

Using Security Copilot, you can apply its capabilities with Global Secure Access in the following use cases:

- Monitor data consumption and bandwidth usage
- Investigate blocked traffic and security threats
- Analyze user application access patterns
- Monitor cross-tenant access and external connections

## Global Secure Access

For example, as a security analyst or network administrator, you can use Security Copilot to investigate and monitor network traffic usage and behavior using natural language queries. You can analyze user, device, and branch network usage, identify network issues, and detect threats or policy violations in real time. As a result, your investigation process is streamlined and more effective.

Note

If an action is blocked by insufficient permissions, a recommended role is displayed. You can use the following prompt in the Security Copilot chat to activate the required role. This is dependent on having an eligible role assignment that provides the necessary access.

- *Activate the {required role} so that I can perform {the desired task}.*

### Monitor data consumption and bandwidth usage

You can begin your investigation by analyzing overall network traffic patterns and identifying users with high data consumption. Understanding bandwidth usage and traffic distribution are crucial for capacity planning, identifying potential security issues, and detecting unusual usage patterns that might indicate compromised accounts or policy violations. Use the following example prompts to get the information you need:

- *Show the top 5 users with the highest data consumption in the last day.*
- *List the top 10 accessed applications names in the last week based on network traffic logs.*

### Investigate blocked traffic and security threats

Next, you should investigate blocked traffic and security threats to identify potential security incidents and ensure that your organization's security policies are effectively enforced. Analyzing blocked traffic can help you detect malicious activities, misconfigurations, or policy violations that could compromise your network's security. Use the following example prompts to get the information you need:

- *Show all blocked traffic for user david.analyst@woodgrovebank.com in the last 24 hours.*
- *List all applications with high-risk scores accessed in the last 24 hours based on network traffic logs.*

### Analyze user application access patterns

You can analyze specific user access patterns to understand application usage, identify unusual behavior, and ensure compliance with corporate access policies. This analysis helps identify potential insider threats, compromised accounts, or unauthorized application usage that could pose security risks. Use the following example prompt to get the information you need:

- *List all applications names that user sarah.manager@woodgrovebank.com has accessed in the last 24 hours based on network traffic logs.*

### Monitor cross-tenant access and external connections

Finally, you should monitor cross-tenant traffic to identify any unauthorized external connections, to prevent unauthorized data access and movement. Use the following example prompt to get the information you need:

- *Show all cross-tenant traffic to tenant aaaabbbb-0000-cccc-1111-dddd2222eeee in the last 7 days based on network traffic logs.*