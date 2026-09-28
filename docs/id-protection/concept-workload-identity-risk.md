---
layout: Conceptual
title: Securing workload identities with Microsoft Entra ID Protection - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/concept-workload-identity-risk
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-workload-id
manager: dougeby
description: Workload identity risk in Microsoft Entra ID Protection
ms.topic: concept-article
ms.date: 2025-08-06T00:00:00.0000000Z
ms.reviewer: etbasser
ms.custom: sfi-image-nochange
locale: en-us
document_id: 179f3992-c493-9074-20f7-a15ee804d9d2
document_version_independent_id: dcaab75f-1aca-45c7-4b43-6faddda1bfbb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/concept-workload-identity-risk.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/concept-workload-identity-risk
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/concept-workload-identity-risk.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 829b161f-4a7e-ba9e-f0c6-edaa17465471
---

# Securing workload identities with Microsoft Entra ID Protection - Microsoft Entra ID Protection | Microsoft Learn

Microsoft Entra ID Protection can detect, investigate, and remediate workload identities to protect applications and service principals in addition to user identities.

A [workload identity](../workload-id/workload-identities-overview) is an identity that allows an application access to resources, sometimes in the context of a user. These workload identities differ from traditional user accounts as they:

- Can’t perform multifactor authentication.
- Often have no formal lifecycle process.
- Need to store their credentials or secrets somewhere.

These differences make workload identities harder to manage and put them at higher risk for compromise.

Important

Full risk details and risk-based access controls are available to Workload Identities Premium customers; however, customers without the [Workload Identities Premium](https://entra.microsoft.com/#view/Microsoft_Azure_ManagedServiceIdentity/WorkloadIdentitiesBlade) licenses still receive all detections with limited reporting details.

Note

ID Protection detects risk on single tenant, non-Microsoft SaaS, and multitenant apps. Managed Identities aren't currently in scope.

## Prerequisites

To make use of workload identity risk reports, including **Risky workload identities** and the **Workload identity detections** tab in the **Risk detections** in the admin center, you must have the following.

- One of the following administrator roles assigned

    - [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator)
    - [Security Operator](../identity/role-based-access-control/permissions-reference#security-operator)
    - [Security Reader](../identity/role-based-access-control/permissions-reference#security-reader)
- Users assigned the [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) role can create policies that use risk as a condition.
- To take action on risky workload identities we recommend setting up risk-based Conditional Access policies, which requires [Workload Identities Premium](https://www.microsoft.com/security/business/identity-access/microsoft-entra-workload-identities#office-StandaloneSKU-k3hubfz) licensing: You can view, start a trial, and acquire licenses on the [Workload Identities](https://portal.azure.com/#view/Microsoft_Azure_ManagedServiceIdentity/WorkloadIdentitiesBlade).

Note

With [Microsoft Security Copilot](/en-us/copilot/security/microsoft-security-copilot), you can use natural language prompts to get insights on risky workload identities. Learn more about how to [Assess application risks using Microsoft Security Copilot in Microsoft Entra](/en-us/entra/fundamentals/copilot-security-entra-investigate-risky-apps).

## Workload identity risk detections

We detect risk on workload identities across sign-in behavior and offline indicators of compromise.

| Detection name | Detection type | Description | riskEventType |
| --- | --- | --- | --- |
| Microsoft Entra threat intelligence | Offline | This risk detection indicates some activity that is consistent with known attack patterns based on Microsoft's internal and external threat intelligence research. | investigationsThreatIntelligence |
| Suspicious Sign-ins | Offline | This risk detection indicates sign-in properties or patterns that are unusual for this service principal. The detection learns the baselines sign-in behavior for workload identities in your tenant. This detection takes between 2 and 60 days, and fires if one or more of the following unfamiliar properties appear during a later sign-in: IP address / ASN, target resource, user agent, hosting/non-hosting IP change, IP country, credential type. Because of the programmatic nature of workload identity sign-ins, we provide a timestamp for the suspicious activity instead of flagging a specific sign-in event. Sign-ins that are initiated after an authorized configuration change might trigger this detection. | suspiciousSignins |
| Admin confirmed service principal compromised | Offline | This detection indicates an admin selected 'Confirm compromised' in the Risky Workload Identities UI or using riskyServicePrincipals API. To see which admin confirmed this account compromised, check the account’s risk history (via UI or API). | adminConfirmedServicePrincipalCompromised |
| Leaked Credentials | Offline | This risk detection indicates that the account's valid credentials leaked. This leak can occur when someone checks in the credentials in public code artifact on GitHub, or when the credentials are leaked through a data breach. When the Microsoft leaked credentials service acquires credentials from GitHub, the dark web, paste sites, or other sources, they're checked against current valid credentials in Microsoft Entra ID to find valid matches. | leakedCredentials |
| Malicious application | Offline | This detection combines alerts from ID Protection and Microsoft Defender for Cloud Apps to indicate when Microsoft disables an application for violating our terms of service. We recommend [conducting an investigation](https://go.microsoft.com/fwlink/?linkid=2208429) of the application. Note: These applications show `DisabledDueToViolationOfServicesAgreement` on the `disabledByMicrosoftStatus` property on the related [application](/en-us/graph/api/resources/application) and [service principal](/en-us/graph/api/resources/serviceprincipal) resource types in Microsoft Graph. To prevent them from being instantiated in your organization again in the future, you can't delete these objects. | maliciousApplication |
| Suspicious application | Offline | This detection indicates that ID Protection or Microsoft Defender for Cloud Apps identified an application that might be violating our terms of service but hasn't disabled it. We recommend [conducting an investigation](https://go.microsoft.com/fwlink/?linkid=2208429) of the application. | suspiciousApplication |
| Anomalous service principal activity | Offline | This risk detection baselines normal administrative service principal behavior in Microsoft Entra ID, and spots anomalous patterns of behavior like suspicious changes to the directory. The detection is triggered against the administrative service principal making the change or the object that was changed. | anomalousServicePrincipalActivity |
| Suspicious API Traffic | Offline | This risk detection is reported when abnormal GraphAPI traffic or directory enumeration of a service principal is observed. The Suspicious API Traffic detection might indicate abnormal reconnaissance or data exfiltration by a service principal. | suspiciousAPITraffic |

## Identify risky workload identities

Organizations can find workload identities flagged for risk in one of two locations:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Reader](../identity/role-based-access-control/permissions-reference#security-reader).
2. Browse to **ID Protection** &gt; **Risky workload identities**.

[![Screenshot showing risks detected against workload identities in the report.](media/concept-workload-identity-risk/workload-identity-detections-in-risk-detections-report.png)](media/concept-workload-identity-risk/workload-identity-detections-in-risk-detections-report.png#lightbox)

### Microsoft Graph APIs

You can also query risky workload identities [using the Microsoft Graph API](/en-us/graph/use-the-api). There are two new collections in the [ID Protection APIs](/en-us/graph/api/resources/identityprotection-overview).

- `riskyServicePrincipals`
- `servicePrincipalRiskDetections`

### Export risk data

Organizations can export data by configuring [diagnostic settings in Microsoft Entra ID](howto-export-risk-data) to send risk data to a Log Analytics workspace, archive it to a storage account, stream it to an event hub, or send it to a SIEM solution.

## Enforce access controls with risk-based Conditional Access

Using [Conditional Access for workload identities](../identity/conditional-access/workload-identity), you can block access for specific accounts you choose when ID Protection marks them "at risk." Policy can be applied to single-tenant service principals registered in your tenant. Non-Microsoft SaaS, multi-tenanted apps, and managed identities are out of scope.

For improved security and resilience of your workload identities, Continuous Access Evaluation (CAE) for workload identities is a powerful tool that offers instant enforcement of your Conditional Access policies and any detected risk signals. CAE-enabled non-Microsoft workload identities accessing CAE-capable first party resources are equipped with 24 hour Long Lived Tokens (LLTs) that are subject to continuous security checks. For more information on configuring workload identity clients for CAE and current feature scope, see [CAE for workload identities documentation](../identity/conditional-access/concept-continuous-access-evaluation-workload).

## Investigate risky workload identities

ID Protection provides organizations with two reports they can use to investigate workload identity risk. These reports are the risky workload identities, and risk detections for workload identities. All reports allow for downloading of events in .CSV format for further analysis.

Some of the key questions to answer during your investigation include:

- Do accounts show suspicious sign-in activity?
- Were there unauthorized changes to the credentials?
- Were there suspicious configuration changes to accounts?
- Did the account acquire unauthorized application roles?

The [Microsoft Entra security operations guide for Applications](../architecture/security-operations-applications) provides detailed guidance on investigation areas.

Once you determine if the workload identity was compromised, you should dismiss the account’s risk or confirm the account as compromised in the Risky workload identities report. You can also select "Disable service principal" if you want to block the account from further sign-ins.

[![Confirm workload identity compromise or dismiss the risk.](media/concept-workload-identity-risk/confirm-compromise-or-dismiss-risk.png)](media/concept-workload-identity-risk/confirm-compromise-or-dismiss-risk.png#lightbox)

## Remediate risky workload identities

1. Inventory any credentials assigned to the risky workload identity, whether for the service principal or application objects.
2. Add a new credential. Microsoft recommends using x509 certificates.
3. Remove the compromised credentials. If you believe the account is at risk, we recommend removing all existing credentials.
4. Remediate any Azure KeyVault secrets that the Service Principal has access to by rotating them.

The [Microsoft Entra Toolkit](https://github.com/microsoft/AzureADToolkit) is a PowerShell module that can help you perform some of these actions.