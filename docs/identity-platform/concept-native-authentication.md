---
layout: Conceptual
title: Embedded native authentication overview - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/concept-native-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: adamstoffel
ms.author: adamstoffel
ms.service: identity-platform
description: Understand how Embedded native authentication gives your application control of the interface while Microsoft Entra External ID controls authentication.
manager: dougeby
ms.subservice: external
ms.topic: overview
ms.date: 2026-11-13T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1030
ai-usage: ai-assisted
locale: en-us
document_id: 82b9a249-1fd3-f098-b2bf-9ca0a0f7c3fe
document_version_independent_id: 82b9a249-1fd3-f098-b2bf-9ca0a0f7c3fe
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/concept-native-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/concept-native-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/concept-native-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 512d2d52-7152-fe30-f8bd-cccc6c99140e
---

# Embedded native authentication overview - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

**Authentication approach:** Embedded native authentication.

Embedded native authentication is an authentication approach that lets your application present sign-up, sign-in, and password reset while Microsoft Entra External ID validates credentials and enforces authentication requirements. Your app controls the interface and handles the actions, available methods, and links returned by the Native Authentication API.

## API version boundaries

Important

The Native Authentication API V2 is in preview. The [Native Authentication API V1](reference-native-authentication-api-v1) remains generally available. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to preview features.

The primary references describe the response-driven Native Authentication API, with native routes such as `/api/v2.0`. Follow service-returned links without rewriting their versions or paths. The `/oauth2/v2.0` OAuth endpoint path is also used by V1 integrations.

Existing V1 integrations can continue to use the [V1 API reference](reference-native-authentication-api-v1) and its [SDK library references](reference-native-authentication-api-v1#sdk-references). The legacy V1 guides and tutorials have been removed from this documentation. This documentation change doesn't announce retirement of V1 or its SDKs. See [SDK compatibility and migration](how-to-migrate-native-authentication-v1-v2#sdk-compatibility) for platform and package requirements.

## Application-owned experience, service-controlled authentication

With Embedded native authentication, a mobile, desktop, or single-page application (SPA) can present authentication within its own interface. Your application controls layout, interaction, and validation feedback. Microsoft Entra External ID validates credentials, enforces authentication requirements, and issues tokens.

Tenant and Conditional Access policies and the application's user flow apply to Microsoft-hosted authentication, Embedded native authentication, and Bring Your Own UX (BYO UX). Presentation and integration responsibilities differ. With Embedded native authentication, your app handles the required interactions, such as a second-factor challenge after password verification or more attribute collection after email verification.

Microsoft-hosted authentication presents pages on behalf of your app. Choose Embedded native authentication when your team needs control of the interface and can implement response handling and security responsibilities. See [Choose an authentication approach](../external-id/customers/concept-choose-authentication-approach) for the broader comparison.

## Customer journeys

The same authorization transaction surrounds each journey. Your app starts authorization, completes the returned authentication interactions, resumes authorization, and exchanges the authorization code for tokens.

| Journey | Behavior |
| --- | --- |
| **Sign-up** | Create an email-with-password or passwordless email one-time passcode (OTP) account. Collect the attributes and complete the verification steps requested by the user flow. |
| **Sign-in** | Submit the customer's identifier and complete password or email one-time-passcode verification using an offered method. Username-with-password sign-in is also available for configured local accounts. |
| **Password reset** | Verify an offered email or SMS one-time passcode, submit a replacement password, and follow the password-update polling responses. Recovery can start before sign-in discovery or through a password method's `recover` link. |
| **Multifactor authentication (MFA) and inline registration** | Complete email or SMS verification when policy requires MFA. If registration is required, handle the returned `enroll` and `activate` operations. Email OTP first-factor accounts use a different second factor, such as SMS. |
| **Policy requirements after sign-up or password reset** | Continue handling required authentication, including MFA and Conditional Access, before requesting tokens. Completing account creation or a password update doesn't bypass policy. |

Select journeys and methods from those available in the current transaction. Your application can present a choice or apply its flow logic within those options.

The Native Authentication API doesn't support federation, phone numbers as a first factor, time-based one-time passwords (TOTP), passkeys, push authentication, or external MFA methods. Later-operation step-up and using native-issued tokens with profile or credential-management APIs aren't supported. See the [method and integration matrices](../external-id/customers/concept-supported-features-customers#methods-and-journeys-by-approach) for the comparison with Microsoft-hosted authentication and BYO UX.

For supported custom authentication extension events, see the [approach comparison](../external-id/customers/concept-supported-features-customers#custom-authentication-extension-applicability). For configuration, see [Custom authentication extensions](../external-id/customers/concept-custom-extensions).

## Integration responsibilities

Use the configuration guide and API references for a direct integration, or use a documented JavaScript, Android, or Apple SDK. The [SDK quickstart](quickstart-native-authentication) configures a React Next.js sample. SDK entry points and supported continuation interfaces are specific to the package and platform.

| Responsibility | What your application implements |
| --- | --- |
| **Response handling** | Use the latest `state`, `action`, and links to select an allowed operation through user choice or application flow logic. |
| **Method selection** | Select from the returned methods, use masked hints where needed, and follow the selected method's links. |
| **Attribute collection** | Collect values according to the returned field requirements and validation metadata. Don't require page-grouping metadata. |
| **Transaction continuity** | Keep the latest continuation token in memory and use it only with links from the same response. |
| **Authorization** | Request the needed scopes initially and exchange the final authorization code for tokens. |
| **Recovery** | Handle validation failures, throttling, expiration, unsupported interactions, and cancellation without replaying credentials automatically. A separately configured browser sign-in starts a new authentication attempt; it doesn't resume native progress. |

SPAs with Embedded native authentication and BYO UX websites need a proxy or edge cross-origin resource sharing (CORS) policy for cross-origin browser API calls. Android and iOS apps using native HTTP transports don't need CORS or a CORS proxy. See [Native authentication CORS concepts](concept-native-authentication-cors).

All service API calls in the current native authentication integration use a tenant-verified custom domain and the tenant GUID. Configure that authority before starting a journey; see [Configure the API authority](how-to-native-authentication-configure-app#configure-the-api-authority).

## Security boundaries

Your application handles credentials, so protect passwords, one-time passcodes, continuation tokens, authorization codes, and issued tokens. Use HTTPS, don't log authentication bodies, and don't cache credential responses. Validate returned URL authorities before sending transaction data.

Use client-side validation to help customers correct their input. The service validates authentication requests.

## Session boundaries

Embedded native authentication supports single sign-on (SSO) for embedded webviews. A signed-in native app requests an access token for the web resource and includes it in the webview request's `Authorization` header. The resource validates the token and establishes a session, allowing access without another sign-in prompt. See [Authenticate an embedded webview from a native app](how-to-native-authentication-webview-sso).

Signing out of your native app doesn't terminate other application or browser sessions. Clear each application's session separately when your sign-out experience requires it.

## Existing V1 application configuration

For existing V1 applications, [enable public client and native authentication flows](reference-native-authentication-api-v1#enable-public-client-and-native-authentication-flows), then update your platform configuration. The [V1 API reference](reference-native-authentication-api-v1#v1-challenge-types-and-capabilities) describes challenge types and capabilities. For a response-driven integration, follow [Configure an application](how-to-native-authentication-configure-app) to select and configure the V2 entry points.

## Conditional Access and sign-in frequency

Microsoft Entra External ID supports the Conditional Access [sign-in frequency (SIF)](../identity/conditional-access/concept-session-lifetime#user-sign-in-frequency) session control for both Microsoft-hosted and native authentication.

For native authentication, when reauthentication is required by the policy, Microsoft Entra External ID prevents token issuance during refresh token grants (`grant_type=refresh_token`). Your app must handle the failed token refresh and prompt the user to sign in again before it can acquire new tokens. The policy doesn't display the sign-in UI for your app.