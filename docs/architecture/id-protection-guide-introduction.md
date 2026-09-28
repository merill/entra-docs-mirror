---
layout: Conceptual
title: Introduction to Microsoft Entra ID Protection proof-of-concept guidance - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/id-protection-guide-introduction
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra-id-protection
manager: martinco
description: Learn, deploy, and test Microsoft Entra ID Protection so that you can detect, investigate, and remediate identity-based risks.
ms.reviewer: gasinh
ms.topic: concept-article
ms.date: 2025-10-31T00:00:00.0000000Z
locale: en-us
document_id: 2dae6ac4-6490-c1dc-79df-62c507fef9b2
document_version_independent_id: 2dae6ac4-6490-c1dc-79df-62c507fef9b2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/id-protection-guide-introduction.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/id-protection-guide-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/id-protection-guide-introduction.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 98d081cf-e536-79be-0819-9834b09e26b3
---

# Introduction to Microsoft Entra ID Protection proof-of-concept guidance - Microsoft Entra | Microsoft Learn

The proof-of-concept (PoC) guidance in this series of articles helps you to learn, deploy, and test Microsoft Entra ID Protection to detect, investigate, and remediate identity-based risks. Detailed guidance for specific scenarios continues in these articles:

- [Use real-time risk detection to grant access to protected resources](id-protection-guide-detect)
- [Master risk analysis for effective remediation](id-protection-guide-analyze)
- [Bring identity risk-related telemetry into security investigations](id-protection-guide-investigate)
- [Allow users to self-remediate identity risk for enterprise-managed resources](id-protection-guide-remediate)

This guide assumes you're running a PoC in a production environment. Running a PoC in a test environment might give you more flexibility. Follow the guidance in these articles to ensure a successful Microsoft Entra ID Protection PoC launch.

## Understand the products

Understanding the products and their core concepts is the first step toward running a successful PoC. Start with learning about the product features in this section:

- Learn how [Microsoft Entra ID Protection](../id-protection/overview-identity-protection) helps you feed identity-based risks into tools like Conditional Access (CA) to make access decisions. You can send risks to a security information and event management (SIEM) tool for investigation and correlation.

    - Learn about [sign-in and user risk detections](../id-protection/concept-identity-protection-risks) license requirements and whether detections occur in real-time or offline.
    - Learn how Microsoft Entra ID Protection reports help you to [investigate risks](../id-protection/howto-identity-protection-investigate-risk) in your environment.
    - Learn how to allow users to self-remediate detected risks with [sign-in risk and user risk policies](../id-protection/howto-identity-protection-configure-risk-policies).
    - Learn how to manage risky users with [Microsoft Graph data](../id-protection/howto-identity-protection-graph-api).
    - Learn how to [export risk data](../id-protection/howto-export-risk-data) from Microsoft Entra ID Protection for long-term storage and analysis.
- Follow the [step-by-step guidance](../id-protection/how-to-deploy-identity-protection) to plan a Microsoft Entra ID Protection deployment along with the [Conditional Access deployment plan](../identity/conditional-access/plan-conditional-access). Follow detailed instructions for these steps:

    - [Configure Microsoft Entra ID Protection notifications](../id-protection/howto-identity-protection-configure-notifications).
    - [Configure the MFA registration policy](../id-protection/howto-identity-protection-configure-mfa-policy).
    - [Configure and enable risk policies](../id-protection/howto-identity-protection-configure-risk-policies).
    - [Simulate risk detections](../id-protection/howto-identity-protection-simulate-risk).
    - [Provide risk feedback](../id-protection/howto-identity-protection-risk-feedback).
- Learn how to immediately view risk impact from sign-in logs with the [Impact analysis of risk-based access policies workbook](../id-protection/workbook-risk-based-policy-impact).
- Review the [Microsoft Entra ID Protection Power Platform connector reference guide](/en-us/connectors/azureadip/) for these services: Copilot Studio, Logic Apps, Power Apps, and Power Automate.

## Meet prerequisites

To kick off a Microsoft Entra ID Protection PoC, you need these prerequisites.

- An enabled working Microsoft Entra tenant with Microsoft Entra ID P2 or trial license. You can [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Microsoft 365 E5 or Microsoft Enterprise Mobility + Security E5 licenses for some risk detections.
- One or more of the following role assignments, depending on tasks performed. To follow the [Zero Trust principle of least privilege](/en-us/security/zero-trust/), consider using [Privileged Identity Management (PIM)](../id-governance/privileged-identity-management/pim-configure) to just-in-time activate privileged role assignments.

    - Read Microsoft Entra ID Protection and Conditional Access policies and configurations

        - [Security Reader](../identity/role-based-access-control/permissions-reference#security-reader)
        - [Global Reader](../identity/role-based-access-control/permissions-reference#global-reader)
    - Manage Microsoft Entra ID Protection

        - [Security Operator](../identity/role-based-access-control/permissions-reference#security-operator)
        - [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator)
    - Create or modify Conditional Access policies

        - [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator)
        - [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator)
    - A test user who isn't an administrator to verify that policies work as expected before you deploy real users. To create a user, follow the steps in [How to create, invite, and delete users](../fundamentals/how-to-create-delete-users).
- A group, and the user is a member. To create a group, see [Create a group and add members in Microsoft Entra ID](../fundamentals/how-to-manage-groups).

## Identify use cases and plan configuration and testing

While you design your PoC, identify relevant use cases and plan for appropriate configuration and testing.

For all scenarios, plan to include the following steps:

1. Review the [Microsoft Entra ID Protection reports](../id-protection/howto-identity-protection-investigate-risk). Before you deploy risk-based Conditional Access policies, investigate existing suspicious behavior. Determine criteria to dismiss risks or confirm users as safe.

    - [Investigate risk detections](../id-protection/howto-identity-protection-investigate-risk)
    - [Remediate risks and unblock users](../id-protection/howto-identity-protection-remediate-unblock)
    - [Make bulk changes using Microsoft Graph PowerShell](../id-protection/howto-identity-protection-graph-api)
2. Plan for Conditional Access risk policies. Microsoft Entra ID Protection sends risk signals to Conditional Access to make decisions and enforce organizational policies. These policies might require users to perform [multifactor authentication](../identity/authentication/howto-mfa-getstarted) (MFA) or secure password change.

    - Exclude accounts from your policies such as [Emergency Access/Break-Glass](../identity/role-based-access-control/security-emergency-access), [Service accounts/Service principals](../identity/managed-identities-azure-resources/overview), and Microsoft Entra Connect Sync.
    - Deploy MFA so users can self-remediate risk. Users need to be able to perform MFA to self-remediate.
3. Configure [named locations in Conditional Access](../identity/conditional-access/concept-assignment-network#how-are-these-locations-defined).
4. Add your VPN ranges to [Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/ip-tags#create-an-ip-address-range).
5. Scope and define success criteria.
6. Test everything in [Report-only mode](../identity/conditional-access/howto-conditional-access-insights-reporting), a Conditional Access policy state that allows you to evaluate the effect of Conditional Access policies before enforcement.
7. Compile a comprehensive report on PoC results.
8. Make recommendations for full-scale implementation based on PoC findings.
9. Outline a timeline and resource plan for deployment.

## Microsoft Entra ID Protection licensing

Review the following table for licensing requirements for Microsoft Entra ID Protection key capabilities. The [Microsoft Entra plans and pricing](https://www.microsoft.com/security/business/microsoft-entra-pricing) page provides additional information to help you select the best option for your identity needs.

| Capability | Details | Microsoft Entra ID Free / Microsoft 365 Apps | Microsoft Entra ID | Microsoft Entra ID P2 / Microsoft Entra Suite |
| --- | --- | --- | --- | --- |
| Risk policies | Sign-in and user risk policies (via ID Protection or Conditional Access) | No | No | Yes |
| Security reports | Overview | No | No | Yes |
| Security reports | Risky users | Limited information. Shows only users with medium and high risk. No details drawer or risk history. | Limited information. Shows only users with medium and high risk. No details drawer or risk history. | Full access |
| Security reports | Risky sign-ins | Limited information. No risk detail or risk level. | Limited information. No risk detail or risk level. | Full access |
| Security reports | Risk detections | No | Limited information. No details drawer. | Full access |
| Notifications | Users at risk detected alerts | No | No | Yes |
| Notifications | Weekly digest | No | No | Yes |
| MFA registration policy | Require MFA (via Conditional Access) | No | No | Yes |
| Microsoft Graph | All risk reports | No | No | Yes |

If you [secure workload identities](../id-protection/concept-workload-identity-risk), you need Workload Identities Premium licensing to view the Risky workload identities report and the Workload identity detections tab in the Risk detections report.

If you want Microsoft Entra ID Protection to receive signals from Microsoft Defender products, you need the appropriate Microsoft Defender license.

Microsoft 365 E5 covers these signals:

- Microsoft Defender for Cloud Apps

    - Activity from anonymous IP address
    - Impossible travel
    - Mass access to sensitive files
    - New country/region
- Microsoft Defender for Office 365 (suspicious inbox rules)
- Microsoft Defender for Endpoint (possible attempt to access primary refresh token)