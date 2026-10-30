---
layout: Conceptual
title: Build resilience with credential management in Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-in-credentials
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: A guide for architects and IT administrators on building a resilient credential strategy.
ms.topic: best-practice
ms.date: 2026-04-03T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 92961258-34e1-6d50-2a10-59ee91431c01
document_version_independent_id: fc109608-de90-1f41-fb5b-75a48571d243
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-in-credentials.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-in-credentials
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-in-credentials.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: 8c8b5d54-b27f-eb98-4d75-5470d8091d7d
---

# Build resilience with credential management in Microsoft Entra ID - Microsoft Entra | Microsoft Learn

When a credential is presented to Microsoft Entra ID in a token request, there can be multiple dependencies that must be available for validation. The first authentication factor relies on Microsoft Entra authentication and, in some cases, on external (non-Entra ID) dependency, such as on-premises infrastructure. For more information on hybrid authentication architectures, see [Build resilience in your hybrid infrastructure](resilience-in-hybrid).

The most secure and resilient credential strategy is to use passwordless authentication. [Windows Hello for Business](../identity/authentication/concept-authentication-passkeys-fido2) and [Passkey (FIDO 2.0)](../identity/authentication/concept-authentication-passkeys-fido2) security keys have fewer dependencies than other MFA methods. For macOS users customers can enable [Platform Credential for macOS](../identity/authentication/concept-authentication-passkeys-fido2). When you implement these methods users are able to perform strong passwordless and **phishing-resistant** Multi-Factor authentication (MFA).

![Image of preferred authentication methods and dependencies](media/resilience-in-credentials/passwordless-pr.png)

Tip

For a video series deep dive on deploying these authentication methods, see [Phishing-resistant authentication in Microsoft Entra ID](../identity/authentication/phishing-resistant-authentication-videos)

If you implement a second factor, the dependencies for the second factor are added to the dependencies for the first. For example, if your first factor is via [Pass Through Authentication (PTA)](../identity/hybrid/connect/how-to-connect-pta) and your second factor is [SMS](../identity/authentication/howto-authentication-sms-signin), your dependencies are as follows.

- Microsoft Entra authentication services
- Microsoft Entra multifactor authentication service
- On-premises infrastructure
- Phone carrier
- The user's device (not pictured)

![Image of remaining authentication methods and dependencies.](media/resilience-in-credentials/updated-admin-resilience-credentials.png)

Your credential strategy should consider the dependencies of each authentication type and provision methods that avoid a single point of failure.

Because authentication methods have different dependencies, it's a good idea to enable users to register for as many second factor options as possible. Be sure to include second factors with different dependencies, if possible. For example, Voice call and SMS as second factors share the same dependencies, so having them as the only options doesn't mitigate risk.

For second factors, the Microsoft Authenticator app or other authenticator apps using time-based one time passcode (TOTP) or OAuth hardware tokens have the fewest dependencies and are, therefore, more resilient.

## Additional Detail on External (Non-Entra) Dependencies

| Authentication Method | External (Non-Entra) Dependency | More Information |
| --- | --- | --- |
| Certificate Based Authentication (CBA) | In most cases (depending on configuration) CBA will require a revocation check. This adds an external dependency on the CRL distribution point (CDP) | [Understanding the certificate revocation process](../identity/authentication/concept-certificate-based-authentication-certificate-revocation-list#enforce-crl-validation-for-cas) |
| Pass Through Authentication (PTA) | PTA uses on-premise agents to process the password authentication. | [How does Microsoft Entra pass-through authentication work?](../identity/hybrid/connect/how-to-connect-pta-how-it-works#how-does-microsoft-entra-pass-through-authentication-work) |
| Federation | Federation server(s) must be online and available to process the authentication attempt | [High availability cross-geographic AD FS deployment in Azure with Azure Traffic Manager](/en-us/windows-server/identity/ad-fs/deployment/active-directory-adfs-in-azure-with-azure-traffic-manager) |
| External Multifactor Authentication (External MFA) | External MFA provides a path for customers to use external MFA providers. | [Manage external MFA in Microsoft Entra ID](../identity/authentication/how-to-authentication-external-method-manage) |

## How do multiple credentials help resilience?

Provisioning multiple credential types gives users options that accommodate their preferences and environmental constraints. As a result, interactive authentication where users are prompted for multifactor authentication will be more resilient to specific dependencies being unavailable at the time of the request. You can [optimize reauthentication prompts for multifactor authentication](../identity/authentication/concepts-azure-multi-factor-authentication-prompts-session-lifetime).

In addition to individual user resiliency described above, enterprises should plan contingencies for large-scale disruptions such as operational errors that introduce a misconfiguration, a natural disaster, or an enterprise-wide resource outage to an on-premises federation service (especially when used for multifactor authentication).

## How do I implement resilient credentials?

- Deploy [Passwordless credentials](../identity/authentication/howto-authentication-passwordless-deployment). Prefer phishing-resistant methods such as Windows Hello for Business, Passkeys (both Authenticator Passkey Sign-in and FIDO2 security keys) and certificate based authentication (CBA) to increase security while reducing dependencies.
- Deploy the [Microsoft Authenticator App](https://support.microsoft.com/account-billing/how-to-use-the-microsoft-authenticator-app-9783c865-0308-42fb-a519-8cf666fe0acc) as a second factor.
- [Migrate from federation to cloud authentication](../identity/hybrid/connect/migrate-from-federation-to-cloud-authentication) to remove reliance on federated identity provider.
- Turn on [password hash synchronization](../identity/hybrid/connect/whatis-phs) for hybrid accounts that are synchronized from Windows Server Active Directory. This option can be enabled alongside federation services such as Active Directory Federation Services (AD FS) and provides a fallback in case the federation service fails.
- [Analyze usage of multifactor authentication methods](../identity/authentication/howto-authentication-methods-activity) to improve user experience.
- [Implement a resilient access control strategy](../identity/authentication/concept-resilient-controls)