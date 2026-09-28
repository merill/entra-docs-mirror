---
layout: Conceptual
title: Microsoft Entra ID Protection to Investigate Risk Telemetry - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/id-protection-guide-investigate
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra-id-protection
manager: martinco
description: Learn how Security Operations Center (SOC) admins use Microsoft Entra ID Protection to bring identity risk-related telemetry into security investigations.
ms.reviewer: gasinh
ms.topic: concept-article
ms.date: 2025-10-31T00:00:00.0000000Z
locale: en-us
document_id: 3cc78883-1d45-51f1-f606-2bbf28eb4c42
document_version_independent_id: 3cc78883-1d45-51f1-f606-2bbf28eb4c42
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/id-protection-guide-investigate.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/id-protection-guide-investigate
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/id-protection-guide-investigate.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: 64d1353f-7331-89b3-cc36-2febffba72c7
---

# Microsoft Entra ID Protection to Investigate Risk Telemetry - Microsoft Entra | Microsoft Learn

The proof-of-concept (PoC) guidance in this series of articles helps you to learn, deploy, and test Microsoft Entra ID Protection to detect, investigate, and remediate identity-based risks.

An overview of the guidance begins with [Introduction to Microsoft Entra ID Protection proof-of-concept guidance](id-protection-guide-introduction).

Detailed guidance continues with these scenarios:

- [Use real-time risk detection to grant access to protected resources](id-protection-guide-detect)
- [Master risk analysis for effective remediation](id-protection-guide-analyze)
- [Allow users to self-remediate identity risk for enterprise-managed resources](id-protection-guide-remediate)

This article helps Security Operations Center (SOC) administrators to bring identity risk-related telemetry into security investigations.

Configure the following features for identity risk-related telemetry with Microsoft Entra ID Protection:

- Investigate identity-based incidents
- Investigate with Microsoft Security Copilot
- Remediate and respond
- Review for audit and compliance
- Configure access in multitenant environments

## Investigate identity-based incidents

Detect and investigate identity threats in the Microsoft Entra admin center or with Microsoft Graph APIs:

1. [Risky sign-ins](../id-protection/concept-risk-reports#risky-sign-ins) such as [impossible travel](../id-protection/howto-identity-protection-investigate-risk#atypical-travel-detections), [anonymous IPs, and malware-linked IPs](../id-protection/howto-identity-protection-investigate-risk#malicious-ip-address-detections).
2. [Risky users](../id-protection/concept-risk-reports#risky-users) such as accounts with [leaked credentials](../id-protection/howto-identity-protection-investigate-risk#leaked-credentials-detections) and [suspicious behavior](../id-protection/howto-identity-protection-investigate-risk#password-spray-detections).
3. [Risk detections](../id-protection/concept-risk-reports#risk-detections) such as [token replay](../id-protection/howto-identity-protection-investigate-risk#anomalous-token-and-token-issuer-anomaly-detections) and unfamiliar sign-in properties.

## Investigate with Microsoft Security Copilot in Microsoft Entra

Microsoft Security in Microsoft Entra brings together the power of artificial intelligence (AI) and human expertise to help admins and security teams to respond to threats and attacks faster. Through the embedded experience, you can investigate and resolve identity risks, assess identities, and quickly access complete complex tasks.

Use natural language prompts in [Microsoft Security Copilot](../security-copilot/entra-investigate-incident):

- Summarize why a user is risky.
- Retrieve sign-in logs, audit trails, and group memberships.
- Get remediation recommendations and links to documentation.

Learn more about [Microsoft Security Copilot scenarios](../security-copilot/entra-security-scenarios) in Microsoft Entra.

## Remediate and respond

After you confirm a threat:

1. Track that [risk-based Conditional Access](../id-protection/concept-identity-protection-policies) was triggered to block or challenge access.
2. Manually dismiss or confirm compromise to [remediate risks and unblock users](../id-protection/howto-identity-protection-remediate-unblock#administrator-manual-remediation).
3. [Initiate secure password resets or MFA re-registration](../id-protection/concept-identity-protection-user-experience).
4. Use response playbooks to guide next steps.

## Review for audit and compliance

Log and audit all SOC actions in Microsoft Entra to perform the following steps:

1. Review logs in the Microsoft Entra admin center.
2. For correlation and storage, export logs to [Azure Monitor Log Analytics](../identity/monitoring-health/howto-analyze-activity-logs-log-analytics), [Microsoft Sentinel](/en-us/azure/sentinel/overview?tabs=defender-portal), or your dedicated security information and event management (SIEM) system.
3. Generate alerts for specific actions such as policy changes, user unblocks.

## Configure access in multitenant environments

For [multitenant environments](../identity/multi-tenant-organizations/defender-xdr-microsoft-entra-mto):

1. Configure [cross-tenant access policies](../external-id/cross-tenant-access-overview).
2. To limit scope, use [role-based access control](../identity/role-based-access-control/custom-overview) (such as Security Reader, Security Operator).
3. Automate deployment with [PowerShell or Microsoft Graph APIs](../id-protection/howto-identity-protection-graph-api).