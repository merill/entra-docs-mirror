---
layout: Conceptual
title: What is Microsoft Entra ID Protection? - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/overview-identity-protection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Automation to detect, remediate, investigate, and analyze risk data with Microsoft Entra ID Protection
ms.topic: overview
ms.date: 2025-10-30T00:00:00.0000000Z
ms.reviewer: chuqiaoshi
locale: en-us
document_id: c2e83171-fd05-9fe1-3ba7-0fb20161ee63
document_version_independent_id: 2e6b2451-5ff8-a277-90ea-49aa70957977
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/overview-identity-protection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/overview-identity-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/overview-identity-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 309fcde9-820d-27b1-b9a4-a3bba0bef9cd
---

# What is Microsoft Entra ID Protection? - Microsoft Entra ID Protection | Microsoft Learn

Microsoft Entra ID Protection helps organizations detect, investigate, and remediate identity-based risks. These risks can be fed into tools like Conditional Access to make access decisions or sent to a security information and event management (SIEM) tool for further investigation and correlation.

![Diagram showing how ID Protection works at a high level.](media/overview-identity-protection/identity-protection-overview.png)

## Detect risks

Microsoft continually adds and updates detections in our catalog to protect organizations. These detections come from our learnings based on the analysis of trillions of signals each day from Active Directory, Microsoft Accounts, and in gaming with Xbox. This broad range of signals helps ID Protection detect risky behaviors like:

- Anonymous IP address usage
- Password spray attacks
- Leaked credentials
- and more...

During each sign-in, ID Protection runs all real-time sign-in detections, generating a sign-in session risk level that indicates how likely the sign-in is compromised. Based on this risk level, policies are applied to protect the user and the organization.

For a full listing of risks and how they're detected, see the article [What is risk](concept-identity-protection-risks).

## Investigate

Any risks detected on an identity are tracked with reporting. ID Protection provides three key reports for administrators to investigate risks and take action:

- **Risk detections:** Each risk detected is reported as a risk detection.
- **Risky sign-ins:** A risky sign-in is reported when there are one or more risk detections reported for that sign-in.
- **Risky users:**A Risky user is reported when either or both of the following are true:
    - The user has one or more Risky sign-ins.
    - One or more risk detections are reported.

For more information about how to use the reports, see the article [How To: Investigate risk](howto-identity-protection-investigate-risk).

## Remediate risks

Automation is critical in security because the scale of signals and attacks requires automation to keep up.

The [Microsoft Digital Defense Report 2024](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/Microsoft%20Digital%20Defense%20Report%202024%20%281%29.pdf) provides the following statistics:

> 
> 78 trillion security signals analyzed per day, an increase of 13 trillion from the previous year
> 
> 600 million attacks on Microsoft customers per day
> 
> 2.75x increase year over year in human-operated ransomware attacks

These statistics continue to trend upwards, with no sign of slowing down. In this environment, automation is the key to identifying and remediating risk so IT organizations can focus on the right priorities.

### Automatic remediation

[Risk-based Conditional Access policies](howto-identity-protection-configure-risk-policies) can be enabled to require access controls such as providing a strong authentication method, perform multifactor authentication, or perform a secure password reset based on the detected risk level. If the user successfully completes the access control, the risk is automatically remediated.

### Manual remediation

When user remediation isn't enabled, an admin must manually review them in the reports in the portal, through the API, or in Microsoft Defender XDR. Admins can perform manual actions to dismiss, confirm safe, or confirm compromise on the risks.

## Making use of the data

Data from ID Protection can be exported to other tools for archive, further investigation, and correlation. The Microsoft Graph based APIs allow organizations to collect this data for further processing in a tool such as their SIEM. Information about how to access the ID Protection API can be found in the article, [Get started with Microsoft Entra ID Protection and Microsoft Graph](howto-identity-protection-graph-api)

Information about integrating ID Protection information with Microsoft Sentinel can be found in the article, [Connect data from Microsoft Entra ID Protection](/en-us/azure/sentinel/data-connectors-reference#microsoft).

Organizations might store data for longer periods by changing the diagnostic settings in Microsoft Entra ID. They can choose to send data to a Log Analytics workspace, archive data to a storage account, stream data to Event Hubs, or send data to another solution. Detailed information about how to do so can be found in the article, [How To: Export risk data](howto-export-risk-data).

## Required roles

ID Protection requires users to be assigned one or more of the following roles.

| Role | Can do | Can't do |
| --- | --- | --- |
| [Global Reader](../identity/role-based-access-control/permissions-reference#global-reader) | Read-only access to ID Protection | Write access to ID Protection |
| [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator) | Reset user passwords | Read or write to ID Protection |
| [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) | Create policies that factor in user or sign-in risk as a condition | Read or write to legacy ID Protection policies |
| [Security Reader](../identity/role-based-access-control/permissions-reference#security-reader) | View all ID Protection reports and Overview | Configure or change policies  Reset password for a user  Configure alerts  Give feedback on detections |
| [Security Operator](../identity/role-based-access-control/permissions-reference#security-operator) | View all ID Protection reports and Overview  Dismiss user risk, confirm safe sign-in, confirm compromise | Configure or change policies  Reset password for a user  Configure alerts |
| [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator) | Full access to ID Protection | Reset password for a user |

## License requirements

Using this feature requires Microsoft Entra ID P2 licenses. To find the right license for your requirements, see [Microsoft Entra plans and pricing](https://www.microsoft.com/en-us/security/business/microsoft-entra-pricing). The following table describes the key capabilities of Microsoft Entra ID Protection and the licensing requirements for each capability. Refer to the Microsoft Entra plans and pricing page for pricing details.

| Capability | Details | Microsoft Entra ID Free / Microsoft 365 Apps | Microsoft Entra ID P1 | Microsoft Entra ID P2 / Microsoft Entra Suite |
| --- | --- | --- | --- | --- |
| Risk policies | Sign-in and user risk policies (via ID Protection or Conditional Access)Includes Microsoft managed remediation policies | No | No | Yes |
| Security reports | Overview | No | No | Yes |
| Security reports | Risky users | Limited Information. Only users with medium and high risk are shown. No details drawer or risk history. | Limited Information. Only users with medium and high risk are shown. No details drawer or risk history. | Full access |
| Security reports | Risky sign-ins | Limited Information. No risk detail or risk level is shown. | Limited Information. No risk detail or risk level is shown. | Full access |
| Security reports | Risk detections | No | Limited Information. No details drawer. | Full access |
| Notifications | Users at risk detected alerts | No | No | Yes |
| Notifications | Weekly digest | No | No | Yes |
| MFA registration policy | Require MFA (via Conditional Access) | No | No | Yes |
| Microsoft Graph | All risk reports | No | No | Yes |

To view the **Risky workload identities** report and the **Workload identity detections** tab in the **Risk detections** report, you need Workload Identities Premium licensing. For more information, see [Securing workload identities](concept-workload-identity-risk).

### Microsoft Defender

Microsoft Entra ID Protection receives signals from Microsoft Defender products for several risk detections, so you also need the appropriate license for the Microsoft Defender product that owns the signal you're interested in.

**Microsoft 365 E5** covers all of the following signals:

- **Microsoft Defender for Cloud Apps**

    - Activity from anonymous IP address
    - Impossible travel
    - Mass access to sensitive files
    - New country
- **Microsoft Defender for Office 365**

    - Suspicious inbox rules
- **Microsoft Defender for Endpoint**

    - Possible attempt to access Primary Refresh Token