---
layout: Conceptual
title: Choose an Authentication Approach - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/concept-choose-authentication-approach
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Compare Microsoft Entra External ID authentication approaches to choose Microsoft-hosted pages, Embedded native authentication, or Bring Your Own UX.
ai-usage: ai-assisted
ms.topic: concept-article
ms.custom: msecd-doc-authoring-1030
ms.date: 2026-11-17T00:00:00.0000000Z
locale: en-us
document_id: 5f5d53c5-c4f6-c3ae-683c-1ff67284213e
document_version_independent_id: 5f5d53c5-c4f6-c3ae-683c-1ff67284213e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/concept-choose-authentication-approach.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/concept-choose-authentication-approach
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/concept-choose-authentication-approach.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: a3290c41-db73-af3a-cbf2-a07b17177110
---

# Choose an Authentication Approach - Microsoft Entra External ID | Microsoft Learn

Choose how your customer-facing application presents Microsoft Entra External ID authentication. Compare where the interface runs, what your team maintains, and which capabilities you need. Different applications can use different approaches.

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

## Authentication approach options

| Approach | How required authentication steps are presented | What your team controls |
| --- | --- | --- |
| **Microsoft-hosted authentication** | On Microsoft-hosted pages reached through a browser redirect. | **Company branding:** Tenant-wide logos, text, and styling. **Branding themes:** Customization for selected applications. |
| **Embedded native authentication** | In authentication screens your app implements. | Screens and their integration with your app. |
| **Bring Your Own UX (BYO UX)** | On a separate authentication website your team hosts. | The website, its presentation, and its integration. |

### Common policy foundation

All approaches use user flows and authentication policies configured in Microsoft Entra External ID. External ID provides the authentication service; the approaches differ in how the interface is hosted and integrated.

For each application, consider your sign-up, sign-in, account recovery, identity provider, and policy requirements. Confirm that your chosen integration supports those journeys by using the [methods and journeys comparison](concept-supported-features-customers#methods-and-journeys-by-approach). Feature availability can differ by approach and API or SDK version.

## Application and audience requirements

Match each requirement to a candidate, then verify its journeys and integration requirements.

| Requirement | Approach to evaluate | Verification or next step |
| --- | --- | --- |
| **Microsoft-managed authentication pages** | Microsoft-hosted authentication. | Review [company branding](concept-branding-customers), application-specific themes, and [sign-up and sign-in availability](concept-supported-features-customers#methods-and-journeys-by-approach). Plan the app integration and presentation settings. |
| **Authentication screens integrated into your app** | Embedded native authentication. | Review [platform support](../../identity-platform/concept-native-authentication#how-to-use-native-authentication) and [method availability](concept-supported-features-customers#methods-and-journeys-by-approach). Plan the app screens and authentication-state handling. |
| **An authentication website with its own UI and release cycle** | Bring Your Own UX. | Review the website and domain requirements for one or more applications. Plan the website's API and browser integration. |
| **Different interaction requirements across applications** | Combine approaches. | Evaluate each application's interface, integration, session, and journey requirements. |

Important

The Native Authentication API V2 and Bring Your Own UX (BYO UX) are in preview. The Native Authentication API V1 remains generally available. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to preview features.

Plan how your team updates the authentication interface:

- Configure company branding and themes for Microsoft-hosted pages.
- Release Embedded native authentication screens with your application.
- Deploy a BYO UX website on its own release schedule.

## Microsoft-hosted authentication

Evaluate Microsoft-hosted authentication when you want authentication pages hosted and managed by Microsoft. Configure [company branding](concept-branding-customers) across the tenant, or use [branding themes](../../fundamentals/how-to-customize-branding-themes-apps) for selected applications. Your team integrates the app and configures policy.

## Embedded native authentication

Evaluate Embedded native authentication when you want authentication interactions integrated into your application's interface. Your team builds the screens and handles credentials, state, and integration. Confirm platform and SDK support in the [native authentication overview](../../identity-platform/concept-native-authentication). For method and journey support, use the [methods and journeys comparison](concept-supported-features-customers#methods-and-journeys-by-approach) and [browser fallback requirements](../../identity-platform/concept-native-authentication-web-fallback).

The Native Authentication API V2 requires a [tenant-verified custom domain](concept-custom-url-domain) for browser-based apps, such as single-page applications (SPAs), to help protect against cross-site request forgery (CSRF). Also plan a cross-origin resource sharing (CORS) proxy or edge policy for cross-origin browser calls. Non-browser clients, such as Android and iOS apps using native HTTP transports, don't require a custom domain or CORS configuration. Enable the required methods in your tenant and test the journeys your app needs.

## Bring Your Own UX

With Bring Your Own UX (BYO UX), you control and operate the authentication website instead of using Microsoft-hosted pages. Unlike embedded native authentication, the authentication website runs separately from your applications and can serve multiple apps.

Choose BYO UX when you want more control over the presentation and user experience than Microsoft-hosted custom branding provides, or if you want a sign-in website you can share across applications and update independently of their releases. Your team takes responsibility for hosting and maintaining the website. For details, see the [Bring Your Own UX overview](concept-bring-your-own-ux).

## Ownership and security responsibilities

For every approach, your team configures authentication policies, integrates the application, and protects application sessions and tokens. Plan accessibility, testing, monitoring, security updates, incident response, and release coordination for the components your team operates.

Microsoft maintains Microsoft-hosted sign-in pages. With Embedded native authentication, your team maintains app screens and state handling. With BYO UX, your team hosts and manages the website, proxy, and browser integration.

Protect any credentials, continuation state, and tokens your integration handles. Avoid exposing them in URLs or logs. Test what happens when policy requires another verification step and when a session expires. Identify the team responsible for deploying fixes to the components your organization operates.

## Feature comparison

Use the [authentication approach support matrix](concept-supported-features-customers#authentication-approach-supportability) to compare methods, policies, and journeys.

| Requirement | Coverage to review |
| --- | --- |
| **Sign-up, sign-in, and password reset** | Confirm [method and journey availability](concept-supported-features-customers#methods-and-journeys-by-approach) for your approach. For tenant configuration, see [identity providers and authentication methods](concept-authentication-methods-customers). |
| **Additional verification** | Confirm method availability and factor registration requirements in the [multifactor authentication (MFA) guidance](concept-multifactor-authentication-customers). |
| **Session behavior** | Review [Conditional Access](concept-supported-features-customers#conditional-access), [sign-in frequency](../../identity/conditional-access/concept-session-lifetime#user-sign-in-frequency), and [single sign-on](concept-supported-features-customers#single-sign-on). Plan sign-out for each app's session. |
| **Custom business logic** | Confirm which [custom authentication extension events](concept-custom-extensions) your integration supports. |

### Supported languages and frameworks

For Microsoft-hosted integration, see [Samples by app type and language](samples-ciam-all) and [Register an app](../../identity-platform/quickstart-register-app). For Embedded native authentication, confirm platform and SDK requirements in the [native authentication overview](../../identity-platform/concept-native-authentication). For BYO UX, plan a self-hosted browser authorization flow with a web-type redirect URI.