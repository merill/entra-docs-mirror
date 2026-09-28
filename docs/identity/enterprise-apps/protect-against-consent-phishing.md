---
layout: Conceptual
title: Protect against consent phishing - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/protect-against-consent-phishing
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn ways of mitigating against application-based consent phishing attacks using Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2023-12-11T00:00:00.0000000Z
ms.custom: template-concept, enterprise-apps-article
ms.reviewer: tilarso
locale: en-us
document_id: d59d4ab6-a86e-8827-1a35-5cb95d9901c0
document_version_independent_id: 39d3bc60-deaa-8ae3-513a-d1d7013291c1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/protect-against-consent-phishing.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/protect-against-consent-phishing
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/protect-against-consent-phishing.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/486161dc-fa28-4625-9b1c-1a21d690bc8d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/5dd28c86-729c-4723-ab5a-57e26fcec2a8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e3473643-c73b-5aee-9b07-ea33b3ec2193
---

# Protect against consent phishing - Microsoft Entra ID | Microsoft Learn

Productivity is no longer confined to private networks, and work is shifting dramatically toward cloud services. While cloud applications enable employees to be productive remotely, attackers can also use application-based attacks to gain access to valuable organization data. You might be familiar with attacks focused on users, such as email phishing or credential compromise. Consent phishing is another threat vector to be aware of.

This article explores what consent phishing is, what Microsoft does to protect an organization, and what steps organizations can take to stay safe.

## What is consent phishing?

Consent phishing attacks trick users into granting permissions to malicious cloud applications. These malicious applications can then gain access to legitimate cloud services and data of users. Unlike credential compromise, *threat actors* who perform consent phishing target users who can grant access to their personal or organizational data directly. The consent screen displays all permissions the application receives. Because a legitimate provider (such as the Microsoft identity platform) hosts the application, unsuspecting users accept the terms. This action grants a malicious application the requested permissions to the data. The following image shows an example of an OAuth app that is requesting access to a wide variety of permissions.

![Screenshot showing permissions requested window requiring user consent.](media/protect-consent-phishing/permissions-requested.png)

## Mitigating consent phishing attacks

Administrators, users, or Microsoft security researchers might flag OAuth applications that appear to behave suspiciously. Microsoft reviews a flagged application to determine whether it violates the terms of service. If a violation is confirmed, Microsoft Entra ID disables the application and prevents further use across all Microsoft services.

When Microsoft Entra ID disables an OAuth application, the following actions occur:

- The malicious application and related service principals are placed into a fully disabled state. Any new token requests or requests for refresh tokens are denied, but existing access tokens are still valid until their expiration.
- These applications show `DisabledDueToViolationOfServicesAgreement` on the `disabledByMicrosoftStatus` property on the related [application](/en-us/graph/api/resources/application) and [service principal](/en-us/graph/api/resources/serviceprincipal) resource types in Microsoft Graph. To prevent them from being instantiated in your organization again in the future, you can't delete these objects.
- An email is sent to a Privileged Role Administrator when a user in an organization consented to an application before it was disabled. The email specifies the action taken and recommended steps they can do to investigate and improve their security posture.

## Recommended response and remediation

If a Microsoft disabled application impacts the organization, the organization should take the following steps to keep the environment secure:

1. Investigate the application activity for the disabled application, including:
    - The delegated permissions or application permissions requested by the application.
    - The Microsoft Entra audit logs for activity by the application and sign-in activity for users authorized to use the application.
2. Review and use the [guidance for defending against illicit consent grants](/en-us/microsoft-365/security/office-365-security/detect-and-remediate-illicit-consent-grants). The guidance includes auditing permissions and consent for disabled and suspicious applications found during review.
3. Implement best practices for hardening against consent phishing, described in the following section.

## Best practices for hardening against consent phishing attacks

Administrators should be in control of application use by providing the right insights and capabilities to control how applications are allowed and used within organizations. While attackers never rest, there are steps organizations can take to improve the security posture. Some best practices to follow include:

- Educate your organization on how our permissions and consent framework works:
    - Understand the data and the permissions an application is asking for and understand how [permissions and consent](../../identity-platform/permissions-consent-overview) works within the platform.
    - Make sure that administrators know how to [manage and evaluate consent requests](manage-consent-requests).
    - Routinely [audit applications and consented permissions](/en-us/azure/security/fundamentals/steps-secure-identity#audit-apps-and-consented-permissions) in the organization to make sure that applications are accessing only the data they need and are adhering to the principles of least privilege.
- Know how to spot and block common consent phishing tactics:
    - Check for poor spelling and grammar. If an email message or the consent screen of the application has spelling and grammatical errors, it's likely a suspicious application. In that case, report it directly on the [consent prompt](../../identity-platform/application-consent-experience#building-blocks-of-the-consent-prompt) with the **Report it here** link and Microsoft investigates if it's a malicious application and disable it, if confirmed.
    - Don't rely on application names and domain URLs as a source of authenticity. Attackers like to spoof application names and domains that make it appear to come from a legitimate service or company to drive consent to a malicious application. Instead, validate the source of the domain URL and use applications from [verified publishers](../../identity-platform/publisher-verification-overview) when possible.
    - Block [consent phishing emails with Microsoft Defender for Office 365](/en-us/microsoft-365/security/office-365-security/anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365) by protecting against phishing campaigns where an attacker is impersonating a known user in the organization.
    - Configure Microsoft Defender for Cloud Apps policies to help manage abnormal application activity in the organization. For example, [activity policies](/en-us/defender-cloud-apps/user-activity-policies), [anomaly detection](/en-us/defender-cloud-apps/anomaly-detection-policy), and [OAuth app policies](/en-us/defender-cloud-apps/app-permission-policy).
    - Investigate and hunt for consent phishing attacks by following the guidance on [advanced hunting with Microsoft 365 Defender](/en-us/microsoft-365/security/defender/advanced-hunting-overview).
- Allow access to trusted applications that meet certain criteria and protect against those applications that don't:
    - [Configure user consent settings](configure-user-consent?tabs=azure-portal) to allow users to only consent to applications that meet certain criteria. Such applications include applications developed by your organization or from verified publishers and only for low risk permissions you select.
    - Use applications that are publisher verified. [Publisher verification](../../identity-platform/publisher-verification-overview) helps administrators and users understand the authenticity of application developers through a Microsoft supported vetting process. Even if an application does have a verified publisher, it's still important to review the consent prompt to understand and evaluate the request. For example, reviewing the permissions being requested to ensure they align with the scenario the app is requesting them to enable, other app and publisher details on the consent prompt, and so on.
    - Create proactive [application governance](/en-us/defender-cloud-apps/app-governance-manage-app-governance) policies to monitor third-party application behavior on the Microsoft 365 platform to address common suspicious application behaviors.
    - With [Microsoft Security Copilot](/en-us/copilot/security/microsoft-security-copilot), you can use natural language prompts to get insights from your Microsoft Entra data. This helps you identify and understand risks related to applications or workload identities. Learn more about how to [Assess application risks using Microsoft Security Copilot in Microsoft Entra](/en-us/entra/fundamentals/copilot-security-entra-investigate-risky-apps).