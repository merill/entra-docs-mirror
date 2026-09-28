---
layout: Conceptual
title: Microsoft Entra ID Protection to Detect Protected Resource Risks - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/id-protection-guide-detect
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra-id-protection
manager: martinco
description: Learn how identity administrators use real-time risk detection features in Microsoft Entra ID Protection to grant user access to protected resources.
ms.reviewer: gasinh
ms.topic: concept-article
ms.date: 2025-10-31T00:00:00.0000000Z
locale: en-us
document_id: bfbc77ae-805e-6e1a-3e3a-bf67241abc96
document_version_independent_id: bfbc77ae-805e-6e1a-3e3a-bf67241abc96
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/id-protection-guide-detect.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/id-protection-guide-detect
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/id-protection-guide-detect.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d452e224-e132-305d-b9b6-39849d07c8c3
---

# Microsoft Entra ID Protection to Detect Protected Resource Risks - Microsoft Entra | Microsoft Learn

The proof-of-concept (PoC) guidance in this series of articles helps you to learn, deploy, and test Microsoft Entra ID Protection to detect, investigate, and remediate identity-based risks.

An overview of the guidance begins with [Introduction to Microsoft Entra ID Protection proof-of-concept guidance](id-protection-guide-introduction).

Detailed guidance continues with these scenarios:

- [Master risk analysis for effective remediation](id-protection-guide-analyze)
- [Bring identity risk-related telemetry into security investigations](id-protection-guide-investigate)
- [Allow users to self-remediate identity risk for enterprise-managed resources](id-protection-guide-remediate)

This article helps identity administrators use real-time risk detection features in Microsoft Entra ID Protection to grant user access to protected resources. To set up your PoC for this scenario, begin with [Introduction to Microsoft Entra ID Protection proof-of-concept guidance](id-protection-guide-introduction). Then follow the detailed guidance in this article.

Perform the following steps for real-time risk detection with Microsoft Entra ID Protection:

1. Configure risk policies.
2. Investigate and remediate risks.
3. Monitor and tune policies.

## Configure risk policies

To [configure and enable risk policies](../id-protection/howto-identity-protection-configure-risk-policies), factor Sign-in risk and User [risk policies](../id-protection/concept-identity-protection-policies) in Microsoft Entra Conditional Access. If you enabled legacy risk policies in Microsoft Entra ID Protection, plan to [migrate them to Conditional Access](../id-protection/howto-identity-protection-configure-risk-policies#migrate-to-conditional-access).

1. Set up the following key foundational policies.

    - [User risk policy](../id-protection/howto-identity-protection-configure-risk-policies): Trigger actions such as require a secure password change for high-risk users.
    - [Sign-in risk policy](../id-protection/howto-identity-protection-configure-risk-policies#sign-in-risk-policy-in-conditional-access): Evaluate each sign-in attempt and enforce controls such as multifactor authentication (MFA) or block access.
    - [MFA registration policy](../id-protection/howto-identity-protection-configure-mfa-policy): Ensure user enrollment in MFA before they become risky.
2. Test policies with nonadmin test users before you fully deploy your solution.
3. Automate your solution with Conditional Access and Microsoft-managed Conditional Access policies. Automation is critical for scaling protection across large environments.
4. Risk signals from Microsoft Entra ID Protection feed into [Conditional Access policies](../identity/conditional-access/policy-all-users-mfa-strength) and [Microsoft-managed Conditional Access policies](../identity/conditional-access/managed-policies). Consider these options for your scenario:

    - Require [MFA](../identity/authentication/tutorial-enable-azure-mfa) for sign-in risk or secure password reset for user risk [based on risk level](../identity/authentication/tutorial-risk-based-sspr-mfa).
    - To prevent lockouts, [exclude emergency access accounts](../identity/role-based-access-control/security-emergency-access).
    - [Apply policies to workload identities](../identity/conditional-access/workload-identity) like service principals.

## Investigate and remediate risks

To [investigate and remediate risks](../id-protection/howto-identity-protection-remediate-unblock), use the Microsoft Entra ID Protection dashboards and reports.

1. Review reports for [risky users](../id-protection/concept-risk-reports#risky-users), [risky sign-ins](../id-protection/concept-risk-reports#risky-sign-ins), and [risk detections](../id-protection/concept-risk-reports#risk-detections).
2. To immediately view impact in sign-in logs, use the [Impact analysis of risk-based access policies workbook](../id-protection/workbook-risk-based-policy-impact). It helps you understand your environment before you enable policies that might block your users from signing in, require MFA, or perform a secure password change. It also provides you with a breakdown for the date range of the sign-ins that you select.
3. Begin [initial triage](../id-protection/howto-identity-protection-investigate-risk#initial-triage) of your findings. Take manual actions such as dismissing false positives or confirming compromise.
4. Make decisions based on the [investigation and risk remediation framework](../id-protection/howto-identity-protection-investigate-risk#investigation-and-risk-remediation-framework).
5. Use [Microsoft Graph PowerShell](../id-protection/howto-identity-protection-graph-api) or APIs for bulk actions.

For deeper analysis, [export risk data](../id-protection/howto-export-risk-data) to security information and event management (SIEM) tools such as Microsoft Sentinel or [Log Analytics](../id-protection/howto-export-risk-data#log-analytics).

## Monitor and tune policies

Monitor the impact of policies using these features:

1. Use the [Impact analysis of risk-based access policies workbook](../id-protection/workbook-risk-based-policy-impact) for trend analysis.
2. To simulate policy effects, enable [report-only mode in Conditional Access](../identity/conditional-access/concept-conditional-access-report-only).
3. To manage user risk and risk detections, configure automated [Microsoft Entra ID Protection notifications](../id-protection/howto-identity-protection-configure-notifications), such as the users at risk detected email or weekly digest email.
4. To reduce false positives and improve the accuracy of Microsoft Entra ID Protection risk calculations for a specific tenant, configure named locations such as VPN IP ranges.