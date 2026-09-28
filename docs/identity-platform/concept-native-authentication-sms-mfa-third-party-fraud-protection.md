---
layout: Conceptual
title: Third-party fraud protection for native authentication with SMS MFA - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/concept-native-authentication-sms-mfa-third-party-fraud-protection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how third-party fraud protection integrates with native authentication flows to assess risk and protect SMS-based multifactor authentication.
manager: pmwongera
ms.date: 2026-03-03T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: 30dce2c9-d665-4ce0-0ae3-00b42eec883f
document_version_independent_id: 30dce2c9-d665-4ce0-0ae3-00b42eec883f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/concept-native-authentication-sms-mfa-third-party-fraud-protection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/concept-native-authentication-sms-mfa-third-party-fraud-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/concept-native-authentication-sms-mfa-third-party-fraud-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e8fdebed-2921-4997-a75a-fa863723a535
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf1e63a8-325f-42be-b60c-d84a95a42b1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 55b65744-3484-f8a6-4405-d7f0e49ab576
---

# Third-party fraud protection for native authentication with SMS MFA - Microsoft identity platform | Microsoft Learn

Native authentication allows you to have full control over the design of your mobile and desktop application sign-in experience. While this model provides flexibility and control over the user experience, it also introduces fraud prevention risks, especially for SMS-based multifactor authentication (MFA).

This article explains the fraud risks associated with native authentication, then provides guidance for integrating third-party fraud protection solutions to secure native authentication applications.

## Prerequisites

- Your native application integrates with a third‑party fraud protection provider to securely evaluate risk signals before issuing an SMS one‑time passcode (OTP).
- You deploy a customer‑managed web application firewall (WAF) to enforce fraud decisions and to support any increase in SMS throttling limits.
- You enable [regional opt‑in for SMS‑based MFA in supported geographies by using Microsoft Graph](../external-id/customers/how-to-region-code-opt-in).
- Your native application has the required [permissions to access Microsoft Graph on behalf of a signed‑in user](/en-us/graph/auth-v2-service?tabs=http).

## Fraud risk in native authentication

Microsoft Entra External ID provides baseline fraud protections for native authentication application, including:

- Regional blocking for known high‑fraud regions
- Basic throttling of SMS one‑time passcode (OTP) requests
- A phone number reputation signal

Native authentication applications that use SMS‑based MFA remain exposed to extra risks, including:

- **International Revenue Share Fraud (IRSF)** which occurs when attackers artificially inflate SMS traffic to premium‑rate international destinations in order to extract revenue through telecom termination and revenue‑sharing mechanisms.
- **Account takeover (ATO)** is a common attack pattern in which attackers use automated, scripted techniques to attempt sign‑ins with compromised or valid‑looking credentials. Although ATO is not specific to SMS or MFA, in environments where SMS verification is enabled these attempts can result in SMS challenges being issued as if the activity were legitimate.

In browser‑delegated authentication flows, Microsoft Entra External ID mitigates these risks by using rich device telemetry and CAPTCHA challenges. Native authentication applications don't use the Microsoft‑hosted, browser‑delegated sign‑in experience, so the risk profiling doesn't benefit from rich device telemetry. Because of this, native authentication scenarios that use SMS by default are less protected by extensive risk profiling than browser-delegated flows. Customers are therefore recommended to set up extra risk detection and protection using third party providers.

To effectively, mitigate fraud in native authentication scenarios that use SMS:

- Native authentication applications owners need to implement extra fraud detection and mitigation
- Fraud decisions must occur before SMS one‑time passcodes (OTPs) are sent
- Third‑party fraud providers assess risk using device, behavioral, and network signals collected outside of Microsoft Entra External ID

## Recommended fraud prevention architecture

Microsoft recommends a high-level architecture for securing native authentication applications that user SMS-based MFA consisting of the native authentication applications, third-party fraud protection provider, web application firewall (WAF), and Microsoft Entra External ID.

The third-party fraud protection provider evaluates risk before an SMS MFA challenge is issued. By incorporating external risk signals, such as device intelligence and phone number reputation, the system can block high-risk sign-in attempts earlier and reduce exposure to fraud.

| Component | Notes |
| --- | --- |
| **Native applications** | The native application integrates a third-party fraud detection SDK. The applications collect limited, privacy‑preserving device and behavioral signals using the third‑party provider’s tooling and associate those signals with the current authentication session |
| **Third‑party fraud protection provider** | The third‑party fraud provider evaluates the signals collected from the native application and determines the risk level of the authentication attempt. Based on the evaluation, one of the following outcomes occurs: - **Low or acceptable risk**: The authentication flow proceeds, and Microsoft Entra External ID is triggered to issue the SMS one-time passcode (OTP).  - **High risk requiring extra verification**: Device possession is verified before allowing the flow to continue. - **High risk with failed evaluation**: The sign-in attempt is blocked immediately, and no SMS challenge is sent.  You can use third‑party fraud providers such as [Human security](https://www.humansecurity.com/) and [Prove](https://www.prove.com/). |
| **Web application firewall (WAF)** | The WAF is a customer‑managed enforcement layer that sits in front of Microsoft Entra External ID endpoints. The WAF consumes the fraud decision from the third‑party provider and enforces it consistently. Microsoft doesn't configure or operate the WAF; its behavior, including fail‑open or fail‑closed policies, is owned by the customer. |
| **Microsoft Entra External ID** | Microsoft Entra External ID processes only those requests that have passed upstream fraud checks. It doesn't receive raw device telemetry or third‑party risk scores. It issues SMS OTPs only after upstream approval and relies on its built‑in controls, such as throttling, regional restrictions, and phone number reputation signals to provide protection. |

### Sign-in flow protection example

This diagram shows how a native application integrates third‑party fraud protection into an SMS‑based MFA sign‑in flow. The native app coordinates with Microsoft Entra External ID, a web application firewall (WAF), and an external fraud provider to evaluate risk before an SMS OTP is sent. By gating SMS MFA on real‑time risk signals, the flow helps block high‑risk sign‑in attempts while allowing legitimate users to complete authentication.

![Diagram of End-to-end native authentication flow showing how third-party risk evaluation gates SMS-based MFA before a sign-in completes or is blocked.](media/reference-native-auth-api/native-app-sms-mfa-third-party-fraud-protection-flow.svg)

In native authentication flows that use SMS‑based MFA, the application evaluates fraud risk before Microsoft Entra External ID sends an SMS one‑time passcode (OTP). The native app initializes a third‑party fraud protection SDK early in the sign‑in process using provider‑specific mechanisms.

Microsoft Entra External ID drives the authentication state and determines when MFA is required. When SMS MFA is triggered, the native app performs a real‑time risk evaluation through the third‑party provider. As part of this evaluation, the app retrieves the user’s registered phone number from Microsoft Graph to validate it with the fraud provider to assess reputation and abuse signals.

A customer‑managed web application firewall (WAF) enforces the fraud decision returned by the third‑party provider. If the provider allows the request, the WAF forwards it to Microsoft Entra External ID, which issues the SMS OTP and completes authentication after the user submits the code. If Microsoft detects high risk for the SMS challenge, the service blocks the request. The sign-in attempt stops, and Microsoft doesn’t send an SMS. If the provider requires additional verification, the app completes the provider‑specific challenge before allowing the flow to continue.

By gating SMS MFA on upstream risk evaluation, this flow reduces exposure to telephony fraud, account takeover and other related threats while allowing legitimate users to complete authentication.