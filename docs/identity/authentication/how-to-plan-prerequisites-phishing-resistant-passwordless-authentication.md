---
layout: Conceptual
title: Get started with a phishing-resistant passwordless authentication deployment in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Detailed guidance for planning the prerequisites to deploy passwordless and phishing-resistant authentication for organizations that use Microsoft Entra ID.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: miepping, sipower
ms.collection: M365-identity-device-management
locale: en-us
document_id: e3ae287e-2043-de17-766e-8bde34e5a4c3
document_version_independent_id: e3ae287e-2043-de17-766e-8bde34e5a4c3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 64eb1632-78aa-5b43-d79b-1cd1c247a358
---

# Get started with a phishing-resistant passwordless authentication deployment in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Passwords are the primary attack vector for modern adversaries, and a source of friction for users and administrators. As part of an overall [Zero Trust security strategy](https://www.microsoft.com/security/business/zero-trust), Microsoft recommends [moving to phishing-resistant passwordless](https://www.microsoft.com/security/business/solutions/passwordless-authentication) in your authentication solution. This guide helps you select, prepare, and deploy the right phishing-resistant passwordless credentials for your organization. Use this guide to plan and execute your phishing-resistant passwordless project.

Features like multifactor authentication (MFA) are a great way to secure your organization. But users often get frustrated with the extra security layer on top of their need to remember passwords. Phishing-resistant passwordless authentication methods are more convenient. For example, an analysis of Microsoft consumer accounts shows that sign-in with a password can take up to 24 seconds on average, but passkeys only take around 8 seconds in most cases, with synced passkeys only taking 3 seconds. The speed and ease of passkey sign-in is even greater when compared with traditional password and MFA sign in. Passkey users don't need to remember their password, or wait around for SMS messages.

Note

This data is based on analysis of Microsoft consumer account sign-ins.

Phishing-resistant passwordless methods also have extra security baked in. They automatically count as MFA by using something that the user has (a physical device or security key) and something the user knows or is, like a biometric or PIN. And unlike traditional MFA, phishing-resistant passwordless methods deflect phishing attacks against your users by using hardware-backed credentials that can’t be easily compromised.

Microsoft Entra ID offers the following phishing-resistant passwordless authentication options:

- Passkeys (FIDO2)
    - Windows Hello for Business
    - Microsoft Entra passkey on Windows
    - Platform credential for macOS (preview)
    - Entra Passkey on Windows
    - Microsoft Authenticator app passkeys
    - FIDO2 security keys
    - Synced passkeys (synced via providers such as Google Password Manager or iCloud Keychain)
- Certificate-based authentication/smart cards

## Prerequisites

Before you start your Microsoft Entra phishing-resistant passwordless deployment project, complete these prerequisites:

- Review license requirements
- Review the roles needed to perform privileged actions
- Identify stakeholder teams that need to collaborate

### License requirements

Registration and passwordless sign in with Microsoft Entra doesn't require a license, but we recommend at least a Microsoft Entra ID P1 license for the full set of capabilities associated with a passwordless deployment. For example, a Microsoft Entra ID P1 license helps you enforce passwordless sign in through Conditional Access, and track deployment with an authentication method activity report. Refer to the licensing requirements guidance for features referenced in this guide for specific licensing requirements.

### Integrate apps with Microsoft Entra ID

Microsoft Entra ID is a cloud-based Identity and Access Management (IAM) service that integrates with many types of applications, including Software-as-a-Service (SaaS) apps, line-of-business (LOB) apps, on-premises apps, and more. You need to integrate your applications with Microsoft Entra ID to get the most benefit from your investment in passwordless and phishing-resistant authentication. As you integrate more apps with Microsoft Entra ID, you can protect more of your environment with Conditional Access policies that enforce the use of phishing-resistant authentication methods. To learn more about how to integrate apps with Microsoft Entra ID, see [Five steps to integrate your apps with Microsoft Entra ID](../../fundamentals/five-steps-to-full-application-integration).

When you develop your own applications, follow the developer guidance for supporting passwordless and phishing-resistant authentication. For more information, see [Support passwordless authentication with FIDO2 keys in apps you develop](../../identity-platform/support-fido2-authentication).

### Required roles

The following table lists least privileged role requirements for phishing-resistant passwordless deployment. We recommend that you enable phishing-resistant passwordless authentication for all privileged accounts.

| Microsoft Entra role | Description |
| --- | --- |
| [User Administrator](../role-based-access-control/permissions-reference#user-administrator) | To implement combined registration experience |
| [Authentication Administrator](../role-based-access-control/permissions-reference#authentication-administrator) | To implement and manage authentication methods |
| [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator) | To implement and manage the Authentication methods policy |
| User | To configure Authenticator app on device; to enroll security key device for web or Windows 10/11 sign-in |

### Customer stakeholder teams

To ensure success, make sure that you engage with the right stakeholders, and that they understand their roles before you begin your planning and rollout. The following table lists commonly recommended stakeholder teams.

| Stakeholder team | Description |
| --- | --- |
| Identity and Access Management (IAM) | Manages day-to-day operations of the IAM system |
| Information Security Architecture | Plans and designs the organization’s information security practices |
| Information Security Operations | Runs and monitors information security practices for Information Security Architecture |
| Security Assurance and Audit | Helps ensure IT processes are secure and compliant. They conduct regular audits, assess risks, and recommend security measures to mitigate identified vulnerabilities and enhance the overall security posture. |
| Help Desk and Support | Assists end users who encounter issues during deployments of new technologies and policies, or when issues occur |
| End-User Communications | Messages changes to end users in preparation to aid in driving user-facing technology rollouts |