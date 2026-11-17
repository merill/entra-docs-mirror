---
layout: Conceptual
title: Security Fundamentals - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/concept-security-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about security features and fundamentals for Microsoft Entra External ID customer identity and access management (CIAM) in external tenant configurations.
ms.topic: concept-article
ms.date: 2026-11-11T00:00:00.0000000Z
ms.custom: it-pro, msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: f1a16c3b-ff82-cb66-b338-cdf8107f2f87
document_version_independent_id: 6d769ec1-2de4-3b21-8fc7-ff3d5d75554c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/concept-security-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/concept-security-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/concept-security-customers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/e8fdebed-2921-4997-a75a-fa863723a535
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf1e63a8-325f-42be-b60c-d84a95a42b1f
platformId: 3cf94d84-78e9-9501-6eab-f1a3eac08867
---

# Security Fundamentals - Microsoft Entra External ID | Microsoft Learn

Customer identity and access management (CIAM) systems face threats such as credential stuffing, automated bot sign-ups, account takeover attempts, and high-volume traffic spikes. Microsoft Entra External ID provides security capabilities you can build on to address these threats. Use this guide to prioritize controls and integrations that help protect your customer-facing applications.

**Applies to external tenants:** Feature support varies by authentication approach and API or SDK version. Compare Microsoft-hosted authentication, Embedded native authentication, and Bring Your Own UX (BYO UX) in the [authentication approach overview](concept-choose-authentication-approach). Check feature availability in the [authentication support matrix](concept-supported-features-customers#authentication-approach-supportability).

This article outlines:

- The attack vectors that commonly target CIAM systems.
- The security controls that can help you address them.
- A prioritized roadmap to guide implementation.
- Available third-party integrations for fraud, bot, and distributed denial-of-service (DDoS) protection.
- Known limitations specific to external tenants.

## Security model for external tenants

A defense‑in‑depth strategy requires combining multiple control layers:

- Front-door protection through a web application firewall (WAF), bot mitigation, and IP controls.
- Identity security through multifactor authentication (MFA), Conditional Access, and access control.
- Fraud prevention through third-party sign-up and sign-in detection providers.
- Application-level authorization.
- Monitoring and alerting.

Each layer addresses a different class of attacks, reducing the likelihood of compromise and limiting the blast radius.

Important

Confirm control and method availability for your integration in the [authentication approach comparison](concept-supported-features-customers#authentication-approach-supportability). Review the [security considerations in Choose an authentication approach](concept-choose-authentication-approach#security-considerations) before implementing your integration.

### Priority 1: Immediate implementation

Start with these protections to establish a security baseline for your external identity flows. Priority 2 adds protections against fraud, bots, DDoS, and more advanced attack patterns.

| **Security feature** | **Description** | **Threats addressed** | **User impact** | **Implementation effort** |
| --- | --- | --- | --- | --- |
| **[Brute force protection](/en-us/entra/identity/authentication/howto-password-smart-lockout)** | Mitigates brute force attacks by limiting the number of sign-in attempts to prevent unauthorized access through repeated password guessing. **Note:** Smart lockout focuses on password misuse; broader bot and fraud activity is addressed through additional controls later in this article. | Prevents brute force, account takeover. | None — No end-user impact | None – Enabled by default |
| **[Common networking HTTP protection](/en-us/entra/external-id/customers/reference-service-limits)** | These built‑in protections help filter malformed traffic, limit abusive request patterns, and mitigate common protocol‑level attacks.**Note:** These safeguards support application stability, but high‑volume DDoS and sophisticated bots require WAF or bot‑mitigation integrations described later. | Protects against common network attacks. | Low – Sensitive actions only | None – Enabled by default |
| **[Access Control](/en-us/entra/external-id/customers/how-to-use-app-roles-customers)** | Limits user access by applying app roles and authorization rules.**Note:** Access control enforces authorization, not user verification. Combine it with MFA and adaptive controls to strengthen security. | Enforces authorization in applications. | Medium– User adoption | Medium – Setup required |
| **[Enable multifactor authentication (MFA) for all users](concept-multifactor-authentication-customers)** | MFA adds a second verification step beyond passwords, significantly reducing the risk of account takeover.**Note:** MFA limits stolen‑credential attacks but must be paired with fraud detection and monitoring to prevent automated or malicious sign‑up attempts. | Adds second factor authentication. | High – User adoption | Medium – Setup required |
| **[Passkeys (FIDO2)](how-to-sign-in-with-passkey)** | Phishing-resistant, passwordless authentication that uses face, fingerprint, PIN, or a security key. A passkey satisfies MFA in a single gesture and can also serve as a primary, passwordless sign-in method. | Prevents phishing, password theft, and credential replay. | Low – Familiar gestures | Medium – Setup and credential management UX required |
| **[Activity logging](/en-us/entra/identity/monitoring-health/concept-sign-ups) & [User insights](/en-us/entra/external-id/customers/how-to-user-insights)** | Activity logs and insights provide visibility into sign-ups, sign-ins, error patterns, and anomalies. They help you identify unusual trends and investigate issues quickly, supporting early detection, and informed decision making. | Enables threat detection. | None — No end-user impact | Medium – Setup required |

### Priority 2: Short-term implementation

Once baseline controls are in place, implement protections that materially improve threat resilience.

| **Security feature** | **Description** | **Threats addressed** | **User impact** | **Implementation effort** |
| --- | --- | --- | --- | --- |
| **[Conditional Access](/en-us/entra/external-id/customers/concept-supported-features-customers#conditional-access)** | Configure policies to require MFA and manage sessions. Check control availability for your authentication integration, including [sign-in frequency (SIF)](../../identity/conditional-access/concept-session-lifetime#user-sign-in-frequency). See [What is Conditional Access?](../../identity/conditional-access/overview) and [Developer guide to Conditional Access authentication context](../../identity-platform/developer-guide-conditional-access-authentication-context) for more information. | Provides access control. | Medium – User adoption | Medium – Setup required |
| **[Credential and secret management](/en-us/entra/architecture/deployment-external-operations#application-security-credential-and-secret-management)** | Prefer certificates over client secrets for app authentication to External ID because certificates are more secure and harder to compromise. | Secures app credentials. | None — No end-user impact | Medium – Setup required |
| **[Token lifetime management](/en-us/entra/architecture/deployment-external-operations#risk-reduction-with-token-lifetime-management)** | Configure the token lifetime to reduce your app’s exposure to compromised tokens. | Limits exposure. | High – Requires frequent refreshes | Medium – Setup required |
| **Custom Domain with Web Application Firewall (WAF)** | Use [Cloudflare](/en-us/entra/external-id/customers/how-to-configure-waf-integration), [Akamai](/en-us/entra/external-id/customers/how-to-configure-akamai-integration) or [Azure WAF](/en-us/entra/external-id/customers/tutorial-configure-external-id-web-app-firewall) for tenant security against DDoS attacks. | Provides DDoS and bot protection. | Medium – User adoption | High – WAF integration |
| **Sign-up fraud protection** | Use [Arkose Labs](/en-us/entra/external-id/customers/how-to-integrate-fraud-protection?pivots=arkose) and [HUMAN Security](/en-us/entra/external-id/customers/how-to-integrate-fraud-protection?pivots=human) to protect against sign-up fraud and block automated bot attacks. | Provides fraud protection. | Medium – User adoption | High – Sign-up protection integration |
| **Enhanced monitoring and alerting** | Use [Azure Monitor and Microsoft Sentinel](/en-us/entra/external-id/customers/how-to-azure-monitor) to enable built-in monitoring, log analytics, and advanced threat detection. | Provides early threat detection. | None — No end-user impact | High – Azure Monitor integration |

### Priority 3: Long-term implementation

These are iterative, ongoing improvements to strengthen posture over time.

| **Security feature** | **Description** | **Threats addressed** | **User impact** | **Implementation effort** |
| --- | --- | --- | --- | --- |
| **[Monitoring and alerting](/en-us/entra/external-id/customers/how-to-azure-monitor)** | Fine-tune monitoring and alert thresholds to improve accuracy. | Provides accurate monitoring. | None — No end-user impact | Medium – Setup required |
| **Continuous security enhancements and new features** | Use the 3–12 month period to iterate on your security controls and adopt [new enhancements](/en-us/entra/external-id/whats-new-docs?tabs=external-tenants). | Helps prevent security threats and vulnerabilities. | Depends on the new feature. | Depends on the new feature. |
| **[Zero Trust Assessment](/en-us/security/zero-trust/assessment/overview)** | Tests hundreds of security settings based on Secure Future Initiative (SFI) and Zero Trust principles. | Provides thorough security configuration testing. | None — No end-user impact | Medium – Setup required |

## Known limitations

These security features have limitations or are unavailable in external tenants. The following table lists these limitations and suggests possible workarounds.

| **Feature** | **Current limitation** | **Workaround** |
| --- | --- | --- |
| **[ID Protection](/en-us/entra/id-protection/overview-identity-protection)** | ID Protection isn’t supported in external tenants. | Not available in external tenants. |