---
layout: Conceptual
title: Plan a Microsoft Entra ID Protection deployment - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/how-to-deploy-identity-protection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Create a plan to deploy Microsoft Entra ID Protection.
ms.topic: how-to
ms.date: 2025-08-06T00:00:00.0000000Z
ms.reviewer: jhenders, tracyyu, chuqiaoshi
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6aeb7867-3185-8c70-65df-91de055d238e
document_version_independent_id: 240705ed-62ca-da0c-5875-92425fe499eb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/how-to-deploy-identity-protection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/how-to-deploy-identity-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/how-to-deploy-identity-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e769806c-71a9-c1cc-eadb-87d8e0ea2d92
---

# Plan a Microsoft Entra ID Protection deployment - Microsoft Entra ID Protection | Microsoft Learn

Microsoft Entra ID Protection detects identity-based risks, reports them, and allows administrators to investigate and remediate these risks to keep organizations safe and secure. Risk data can be further fed into tools like Conditional Access to make access decisions or fed to a security information and event management (SIEM) tool for further analysis and investigation.

This deployment plan extends concepts introduced in the [Conditional Access deployment plan](../identity/conditional-access/plan-conditional-access).

## Prerequisites

- A working Microsoft Entra tenant with Microsoft Entra ID P2, or trial license enabled. If needed, [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
    - Microsoft 365 E5 or Microsoft Enterprise Mobility + Security E5 licenses are needed for some risk detections. For more information, see [What is Microsoft Entra ID Protection?](overview-identity-protection#microsoft-defender).
- Administrators who interact with ID Protection must have one or more of the following role assignments depending on the tasks they're performing. To follow the [Zero Trust principle of least privilege](/en-us/security/zero-trust/), consider using [Privileged Identity Management (PIM)](../id-governance/privileged-identity-management/pim-configure)to just-in-time activate privileged role assignments.
    - Read ID Protection and Conditional Access policies and configurations
        - [Security Reader](../identity/role-based-access-control/permissions-reference#security-reader)
        - [Global Reader](../identity/role-based-access-control/permissions-reference#global-reader)
    - Manage ID Protection
        - [Security Operator](../identity/role-based-access-control/permissions-reference#security-operator)
        - [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator)
    - Create or modify Conditional Access policies
        - [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator)
        - [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator)
- A test user who isn't an administrator to verify policies work as expected before deploying to real users. If you need to create a user, see [Quickstart: Add new users to Microsoft Entra ID](../fundamentals/how-to-create-delete-users).
- A group that the user is a member of. If you need to create a group, see [Create a group and add members in Microsoft Entra ID](/en-us/entra/fundamentals/how-to-manage-groups).

### Engage the right stakeholders

When technology projects fail, they typically do so due to mismatched expectations on affect, outcomes, and responsibilities. To avoid these pitfalls, ensure that you’re engaging the right stakeholders and that stakeholder roles in the project are well understood by documenting the stakeholders, their project input, and accountability.

### Communicating change

Communication is critical to the success of any new functionality. You should proactively communicate with your users how their [experience](concept-identity-protection-user-experience) changes, when it changes, and how to get support if they experience issues.

## Step 1: Review existing reports

It's important to review the [ID Protection reports](howto-identity-protection-investigate-risk) before deploying risk-based Conditional Access policies. This review gives an opportunity to investigate any existing suspicious behavior. You might choose to dismiss the risk or confirm these users as safe if you determine they aren't at risk.

- [Investigate risk detections](howto-identity-protection-investigate-risk)
- [Remediate risks and unblock users](howto-identity-protection-remediate-unblock)
- [Make bulk changes using Microsoft Graph PowerShell](howto-identity-protection-graph-api)

For efficiency, we recommend allowing users to self-remediate through policies that are discussed in Step 3.

## Step 2: Plan for Conditional Access risk policies

ID Protection sends risk signals to Conditional Access, to make decisions and enforce organizational policies. These policies might require users perform multifactor authentication or secure password change. There are several items organizations should plan for before creating their policies.

### Policy exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../identity/role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../identity/managed-identities-azure-resources/overview).

### Multifactor authentication

For users to self-remediate risk though, they must register for Microsoft Entra multifactor authentication before they become risky. For more information, see the article [Plan a Microsoft Entra multifactor authentication deployment](../identity/authentication/howto-mfa-getstarted).

### Known network locations

It's important to configure [named locations in Conditional Access](../identity/conditional-access/concept-assignment-network#how-are-these-locations-defined) and add your VPN ranges to [Defender for Cloud Apps](/en-us/defender-cloud-apps/ip-tags#create-an-ip-address-range). Sign-ins from named locations that are marked as trusted or known, improve the accuracy of ID Protection risk calculations. These sign-ins lower a user's risk when they authenticate from a location marked as trusted or known. This practice reduces false positives for some detections in your environment.

### Report only mode

[Report-only mode](../identity/conditional-access/howto-conditional-access-insights-reporting) is a Conditional Access policy state that allows administrators to evaluate the effect of Conditional Access policies before enforcing them in their environment.

## Step 3: Configure your policies

### ID Protection MFA registration policy

Use the ID Protection multifactor authentication registration policy to help get your users registered for Microsoft Entra multifactor authentication before they need to use it. Follow the steps in the article [How To: Configure the Microsoft Entra multifactor authentication registration policy](howto-identity-protection-configure-mfa-policy) to enable this policy.

### Conditional Access policies

**Sign-in risk** - Most users have a normal behavior that can be tracked, when they fall outside of this norm it could be risky to allow them to just sign in. You might want to block that user or ask them to perform multifactor authentication to prove that they're really who they say they are. You start by scoping these policies to a subset of your users.

**User risk** - Microsoft works with researchers, law enforcement, various security teams at Microsoft, and other trusted sources to find leaked username and password pairs. When these vulnerable users are detected, we recommend requiring users perform multifactor authentication then reset their password.

The article [Configure and enable risk policies](howto-identity-protection-configure-risk-policies) provides guidance to create Conditional Access policies to address these risks.

## Step 4: Monitoring and continuous operational needs

### Email notifications

[Enable notifications](howto-identity-protection-configure-notifications) so you can respond when a user is flagged as at risk. These notifications allow you to start investigating immediately. You can also set up weekly digest emails giving you an overview of risk for that week.

### Monitor and investigate

The [Impact analysis of risk-based access policies workbook](workbook-risk-based-policy-impact) helps administrators understand user impact before creating risk-based Conditional Access policies.

The [ID Protection workbook](../identity/monitoring-health/workbook-risk-analysis) can help monitor and look for patterns in your tenant. Monitor this workbook for trends and also Conditional Access Report Only mode results to see if there are any changes that need to be made, for example, additions to named locations.

Microsoft Defender for Cloud Apps provides an investigation framework organizations can use as a starting point. For more information, see the article [How to investigate anomaly detection alerts](/en-us/defender-cloud-apps/investigate-anomaly-alerts).

You can also use the ID Protection APIs to [export risk information](howto-export-risk-data) to other tools, so your security team can monitor and alert on risk events.

During testing, you might want to [simulate some threats](howto-identity-protection-simulate-risk) to test your investigation processes.