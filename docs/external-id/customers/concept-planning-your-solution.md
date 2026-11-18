---
layout: Conceptual
title: Plan a Deployment - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/concept-planning-your-solution
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Plan a Microsoft Entra External ID deployment, from creating an external tenant and choosing an authentication approach to integrating and securing sign-in.
ai-usage: ai-assisted
ms.topic: concept-article
ms.date: 2026-11-17T00:00:00.0000000Z
ms.custom: it-pro, seo-july-2024, msecd-doc-authoring-1030
locale: en-us
document_id: 4cd23bdf-a161-ab3b-4940-f42726aaefe7
document_version_independent_id: e68e8f00-c2ec-7885-4139-cf6c9455c159
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/concept-planning-your-solution.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/concept-planning-your-solution
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/concept-planning-your-solution.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 27db9af4-115d-f993-c845-abc6ebf82201
---

# Plan a Deployment - Microsoft Entra External ID | Microsoft Learn

Microsoft Entra External ID adds customer identity and access management (CIAM) to your app on the Microsoft Entra platform, so you get consistent app integration, tenant management, and operations across workforce and customer scenarios.

**Applies to external tenants:** Feature support varies by authentication approach and API or SDK version. Compare Microsoft-hosted authentication, Embedded native authentication, and Bring Your Own UX (BYO UX) in the [authentication approach overview](concept-choose-authentication-approach). Check feature availability in the [authentication support matrix](concept-supported-features-customers#authentication-approach-supportability).

Use this guide to plan your deployment in six steps. Each section summarizes the key choices and links to setup instructions and reference documentation.

![Diagram of six setup steps: create a tenant, choose authentication, register an app, integrate a user flow, secure sign-in, and customize sign-in.](media/concept-planning-your-solution/planning-flow-horizontal.png)

Jump to a step for details, or go straight to the **How-to guides**.

| Step | How-to guides |
| --- | --- |
| **Step 1: Create an external tenant** | • [Create an external tenant](how-to-create-external-tenant-portal)• [Or start a free trial](https://aka.ms/ciam-free-trial?wt.mc_id=ciamcustomertenantfreetrial_linkclick_content_cnl) |
| **Step 2: Choose an authentication approach** | • [Choose an authentication approach](concept-choose-authentication-approach) |
| **Step 3: Register your application** | • [Register your application](/en-us/entra/identity-platform/quickstart-register-app) |
| **Step 4: Integrate a sign-in flow with your app** | • [Create a user flow](how-to-user-flow-sign-up-sign-in-customers)• [Add your app to the user flow](how-to-user-flow-add-application) |
| **Step 5: Secure your sign-in** | • [Add multifactor authentication (MFA)](concept-multifactor-authentication-customers)• [Review security and governance](concept-security-customers) |
| **Step 6: Customize your sign-in** | • [Customize branding](concept-branding-customers)*(Microsoft-hosted pages)*• [Use a custom URL domain](concept-custom-url-domain)• [Add custom authentication extensions](concept-custom-extensions) |

## Step 1: Create an external tenant

![Diagram showing the setup flow with step 1, create an external tenant, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-1.png)

Your external tenant is the resource where you register apps and manage customer identities, separate from your workforce tenant. When you create it, you choose its geographic location and domain name. If you're migrating from Azure AD B2C, review the [Azure AD B2C migration planning guidance](plan-your-migration-from-b2c-to-external-id). For other identity deployments, review [user migration guidance](how-to-migrate-users).

The directory contains both [admin accounts](how-to-manage-admin-accounts) and customer accounts. Customers usually self-register; you can also [create local accounts](how-to-manage-customer-accounts). Customer accounts have a restricted [default permission set](reference-user-permissions) and can't see other users, groups, or devices.

### How to create an external tenant

- [Create an external tenant](how-to-create-external-tenant-portal) in the Microsoft Entra admin center.
- Don't have a tenant yet? [Start a free trial](https://aka.ms/ciam-free-trial?wt.mc_id=ciamcustomertenantfreetrial_linkclick_content_cnl).
- Using Visual Studio Code? Use the [Microsoft Entra External ID extension](https://aka.ms/ciamvscode/quickstarts/marketplace) and its [quickstart guide](https://aka.ms/ciamvscode/quickstartguide).

## Step 2: Choose an authentication approach

![Diagram showing the setup flow with step 2, choose an authentication approach, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-2.png)

Decide how to build the sign-in experience before you register your app. This choice drives the rest of your integration.

- **Microsoft-hosted authentication** — Microsoft hosts the sign-in page, and your app redirects users to it. You can apply company branding or application-specific branding themes.
- **Embedded native authentication** — Your app presents the sign-in interface and calls an SDK or the Native Authentication API. Your team manages the interface and integration.
- **Bring Your Own UX (BYO UX)** — Your team hosts a separate authentication website within a browser-based authorization flow. Microsoft Entra External ID applies authentication policies and verifies credentials.

### How to choose an authentication approach

- [Choose an authentication approach](concept-choose-authentication-approach) — feature comparison and trade-offs.
- [Embedded native authentication overview](../../identity-platform/concept-native-authentication) — integration guidance for an interface in your app.

## Step 3: Register your application

![Diagram showing the setup flow with step 3, register your application, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-3.png)

Register your app in your external tenant to establish its application identity. Follow the registration guide for your platform and authentication approach.

| Setting | Microsoft-hosted | Embedded native authentication | BYO UX |
| --- | --- | --- | --- |
| Redirect URI | Register a callback URI for your app. | Configure the redirect required by your platform or browser integration, separately from direct native code redemption. | Register a web-type redirect URI, including for public clients. |
| Client type | Choose the registration for your app's platform. | Public client; enable public client flows. | Public or confidential client. |
| Service API authority | Default tenant domain or a custom URL domain. | The Native Authentication API V2 requires a tenant-verified custom domain for browser-based apps, not for non-browser clients using native HTTP transports. | Tenant-verified custom domain for API calls. |
| Integration setup | Configure hosted sign-in. | Enable native authentication for the app. | Use Microsoft Graph beta to configure your self-hosted authentication page. |

After registration, configure your application and tenant identifiers. Keep confidential-client credentials on the server; don't place client secrets in mobile apps or browser code.

### How to register your application

- Find platform-specific guidance on the [Samples by app type and language page](samples-ciam-all).
- If your platform isn't listed, follow the general [register an application](../../identity-platform/quickstart-register-app) quickstart.
- For Embedded native authentication app settings, see [Configure an app for Embedded native authentication](../../identity-platform/how-to-native-authentication-configure-app).

## Step 4: Integrate a sign-in flow with your app

![Diagram showing the setup flow with step 4, integrate a sign-in flow with your app, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-4.png)

Create a sign-up and sign-in user flow that defines the sign-in methods, attributes to collect, and identity providers for your app. Use the [authentication support matrix](concept-supported-features-customers#authentication-approach-supportability) to check which configured features are available through your integration.

For the Native Authentication API integrations, follow the [attribute collection contract](../../identity-platform/concept-native-authentication-user-attributes).

### Plan your user flow

- **Number of user flows.** Each app uses one user flow. You can share one flow across apps or create up to 10 per tenant for differentiated experiences.
- **Attributes to collect.** Decide which built-in attributes you need and whether you need [custom attributes](how-to-define-custom-attributes).
- **Terms and conditions consent.** Use custom attributes to capture consent with links to your terms and privacy policies.
- **Token claims.**[Add required attributes to the token](how-to-add-attributes-to-token) if your app depends on them.
- **Sign-in methods.** Configure local account methods and identity providers for each user flow. With Microsoft-hosted authentication, configured federated providers can include [Google](how-to-google-federation-customers), [Facebook](how-to-facebook-federation-customers), [Apple](how-to-apple-federation-customers), [another Microsoft Entra tenant](how-to-entra-id-federation-customers), or [custom OpenID Connect (OIDC)](how-to-custom-oidc-federation-customers). Federation isn't supported through the Native Authentication API. Confirm method and journey availability in the [methods and journeys comparison](concept-supported-features-customers#methods-and-journeys-by-approach).

### How to integrate a user flow with your app

- [Define custom attributes](how-to-define-custom-attributes) (if needed).
- [Create the sign-up and sign-in user flow](how-to-user-flow-sign-up-sign-in-customers).
- [Add your application to the user flow](how-to-user-flow-add-application).
- Integrate your app code:
    - **Microsoft-hosted:** Follow a [sample or quickstart](samples-ciam-all) for your app type.
    - **Embedded native authentication:** Start with the [application configuration guide](../../identity-platform/how-to-native-authentication-configure-app), [SDK quickstart](../../identity-platform/quickstart-native-authentication), or [Native Authentication API reference](../../identity-platform/reference-native-authentication). Confirm platform and SDK coverage in the [native authentication overview](../../identity-platform/concept-native-authentication#how-to-use-native-authentication). For an existing V1 integration, use the [V1 API reference](../../identity-platform/reference-native-authentication-api-v1) and [migration guide](../../identity-platform/how-to-migrate-native-authentication-v1-v2).
    - **Bring Your Own UX:** Review the [Bring Your Own UX overview](concept-bring-your-own-ux) for architecture, requirements, and implementation guidance.

## Step 5: Secure your sign-in

![Diagram showing the setup flow with step 5, secure your sign-in, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-5.png)

Plan MFA and review security for your customer-facing apps. Configure tenant policies and protect application sessions, tokens, and any credentials or state your integration handles. Assign ownership for the interface, integration, and hosting components your team operates. For responsibility boundaries, see [authentication integration responsibilities](concept-choose-authentication-approach#security-considerations).

- **Enable MFA.** Review [available MFA methods](concept-multifactor-authentication-customers).
- **Review security and governance.** Plan for Conditional Access, risk-based policies, and auditing. See [Security and governance](concept-security-customers).

## Step 6: Customize your sign-in

![Diagram showing the setup flow with step 6, customize your sign-in, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-6.png)

Customize the sign-in look and feel and extend it with your own business logic. You can configure Microsoft-hosted pages, manage the interface in your app with Embedded native authentication, or host your own page with BYO UX.

- **Customize branding***(Microsoft-hosted pages)*. Apply your logo, colors, and language strings to the sign-in pages. See [Customize the sign-in look and feel](concept-branding-customers).
- **Use a custom URL domain where required.** The Native Authentication API V2 requires a tenant-verified custom domain for browser-based apps, such as SPAs, but not for non-browser clients, such as iOS and Android apps using native HTTP transports. BYO UX requires a tenant-verified custom domain. See [Custom URL domain](concept-custom-url-domain).
- **Add custom authentication extensions.** Extend the flow with server-side logic. Event availability can differ by approach and API or SDK version. See [Custom authentication extensions](concept-custom-extensions).