---
layout: Conceptual
title: Integrate third-party bot protection with Native API sign-up - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/tutorial-third-party-bot-protection-native-api-sign-up
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to integrate third-party bot protection providers with Native API sign-up flows in Microsoft Entra External ID by using a Web Application Firewall.
ms.topic: tutorial
ms.date: 2026-02-24T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 2eb9a3c4-635e-2226-ebfb-409eda04bb90
document_version_independent_id: 2eb9a3c4-635e-2226-ebfb-409eda04bb90
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/tutorial-third-party-bot-protection-native-api-sign-up.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/tutorial-third-party-bot-protection-native-api-sign-up
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/tutorial-third-party-bot-protection-native-api-sign-up.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e8fdebed-2921-4997-a75a-fa863723a535
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf1e63a8-325f-42be-b60c-d84a95a42b1f
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 4f38d585-668c-c2cc-4acf-f506a0fa6839
---

# Integrate third-party bot protection with Native API sign-up - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial guides you through integrating third-party bot protection providers with Native API sign-up flows in Microsoft Entra External ID. By using a Web Application Firewall (WAF) to intercept sign-up requests, you can implement risk-based challenge mechanisms during user registration to protect against automated bot attacks and fake account creation.

Note

This integration applies to native authentication API flows only. The WAF intercepts the native authentication `/start` endpoint to evaluate the request before user registration proceeds. Browser-delegated (web-hosted) sign-up flows aren't covered by this tutorial and use a different integration model.

Note

This tutorial assumes you manually make raw HTTP requests to execute the sign-up flow. When possible, use a Microsoft-built and supported authentication SDK. See [Tutorial: Prepare your Android mobile app for native authentication](tutorial-native-authentication-prepare-android-app) and [Tutorial: Prepare your iOS/macOS mobile app for native authentication](tutorial-native-authentication-prepare-ios-macos-app).

## Prerequisites

- An external tenant. If you don't already have one, [create an external tenant](how-to-create-external-tenant-portal).
- A [registered application](/en-us/entra/identity-platform/quickstart-register-app)in the Microsoft Entra admin center with the following configuration:
    - Application (client) ID and Directory (tenant) ID recorded.
    - [Admin consent granted](/en-us/entra/identity-platform/quickstart-register-app#grant-admin-consent-external-tenants-only).
    - [Public client and native authentication flows enabled](/en-us/entra/identity-platform/concept-native-authentication#how-to-enable-native-authentication).
- A [user flow](how-to-user-flow-sign-up-sign-in-customers) created in the Microsoft Entra admin center and [associated with your application](how-to-user-flow-add-application).
- A [custom domain](how-to-custom-url-domain) associated with your external tenant.
- A third-party bot protection provider account (this tutorial uses HUMAN Security as an example) with the following configuration values:
    - Enforcer API credentials
    - SDK integration details
- A WAF platform account (this tutorial uses Cloudflare) with domain administrator privileges.

## How bot protection works

When a user attempts to sign up using Native Authentication, the sign-up request flows through a Web Application Firewall (WAF) that intercepts the /start endpoint. The WAF evaluates the request with your third-party bot protection provider using their detection APIs. If the request is flagged as suspicious based on device fingerprinting, behavioral analysis, or bot signatures, the WAF can block the request or present a challenge to verify the user is human.

This approach allows you to apply bot protection during the native sign-up flow without requiring browser-based redirects, maintaining the native app user experience while protecting against automated account creation and bot attacks.

## Architecture components

This integration involves several key components working together to provide bot protection:

- **External tenant:** A dedicated Microsoft Entra ID instance for managing external identities and customer access.
- **Native application:** A mobile or desktop application that uses Microsoft Entra External ID (native authentication) to sign users up and sign them in.
- **Native APIs:** Service endpoints that enable mobile and desktop apps to perform sign-up, sign-in, and self-service password reset (SSPR) flows in-app, without a browser redirect.
- **Web Application Firewall (WAF):** A firewall that inspects incoming and outgoing HTTP traffic, intercepts sign-up requests, and coordinates with the third-party provider for bot detection.
- **Third-party bot protection provider:** A third-party provider that delivers bot detection, device fingerprinting, and risk-assessment services to identify automated attacks.

[![Diagram of risk-based authentication flow showing native app, WAF, third-party provider, and OTP-based MFA steps.](media/tutorial-third-party-bot-protection-native-api-sign-up/native-app-sign-up-flow-waf.png)](media/tutorial-third-party-bot-protection-native-api-sign-up/native-app-sign-up-flow-waf.png#lightbox)

## Configuration steps

1. Create a sign-up flow for your external tenant.
2. Create a WAF configuration.
3. Update the WAF layer to intercept specific API requests during sign-up flow.
4. Update the native app sign-up API call flow.

## Create a sign-up flow for your external tenant

Before integrating bot protection, ensure you have a working sign-up flow configured. If you've already completed this setup as part of the prerequisites, you can skip to the next section.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. If you haven't already done so, [register an application in the Microsoft Entra admin center](/en-us/entra/identity-platform/quickstart-register-app). Make sure to:
    - Record the **Application (client) ID** and **Directory (tenant) ID** for later use.
    - [Grant admin consent](/en-us/entra/identity-platform/quickstart-register-app#grant-admin-consent-external-tenants-only) to the application.
    - [Enable public client and native authentication flows](/en-us/entra/identity-platform/concept-native-authentication#how-to-enable-native-authentication).
3. If you haven't already done so, [create a user flow in the Microsoft Entra admin center](how-to-user-flow-sign-up-sign-in-customers#to-add-a-new-user-flow). When you create the user flow, take note of the user attributes you configure as required. These attributes are the ones that Microsoft Entra expects your app to submit.
4. [Associate your app registration with the user flow](how-to-user-flow-add-application).
5. Test the sign-up flow by [registering a customer user](how-to-manage-customer-accounts#create-a-customer-account). Alternatively, you can test after completing the integration.

## Configure WAF to intercept sign-up requests

Configure a WAF to intercept sign-up requests for bot detection. This tutorial uses Cloudflare as an example, but you can use any WAF that supports request interception and custom logic execution.

Important

A custom domain must be associated with your external tenant before configuring WAF. Without a custom domain, the WAF can't intercept sign-up requests.

For detailed Cloudflare WAF setup instructions, see [Configure Cloudflare WAF with Microsoft Entra External ID](how-to-configure-waf-integration).

## Configure WAF worker for bot detection

This section configures the WAF to intercept sign-up /start requests and perform bot detection with your third-party provider.

### Update the WAF layer to intercept specific API requests during sign-up flow

Use the Cloudflare WAF that you created in the previous section.

1. Sign in to the **Cloudflare account** for the external domain (mentioned in the Create a WAF configuration step) associated with the external tenant with at least **Domain Administrator** privilege.
2. Go to **Workers Routes**, and select **Create application**.

    ![Screenshot showing the Workers Routes page in Cloudflare.](media/tutorial-third-party-bot-protection-native-api-sign-up/workers-pages-create-application.png)

    ![Screenshot of Cloudflare dashboard sidebar with Workers Routes selected, showing Access, Speed, Caching, Rules, and Error Pages menu options.](media/tutorial-third-party-bot-protection-native-api-sign-up/workers-routes-page.png)
3. Select **Start with Hello World**.

    [![Screenshot showing the Start with Hello World template option.](media/tutorial-third-party-bot-protection-native-api-sign-up/create-application-template.png)](media/tutorial-third-party-bot-protection-native-api-sign-up/create-application-template.png#lightbox)
4. Name the worker and select **Deploy**.

    [![Screenshot of Cloudflare Workers deployment screen showing worker name, code preview, and Deploy button.](media/tutorial-third-party-bot-protection-native-api-sign-up/deploy-hello-world-worker.png)](media/tutorial-third-party-bot-protection-native-api-sign-up/deploy-hello-world-worker.png#lightbox)
5. Once the worker is deployed, select the **Settings** tab. Select **+Add** in **Domains & Routes**.

    [![Screenshot of the Settings tab with Domains &amp; Routes section and Add button for configuring worker routes.](media/tutorial-third-party-bot-protection-native-api-sign-up/settings-domains-routes.png)](media/tutorial-third-party-bot-protection-native-api-sign-up/settings-domains-routes.png#lightbox)
6. Select **Route**.

    [![Screenshot showing the Route option.](media/tutorial-third-party-bot-protection-native-api-sign-up/domains-routes-settings.png)](media/tutorial-third-party-bot-protection-native-api-sign-up/domains-routes-settings.png#lightbox)
7. Select the domain from **Zone**. Add the following in the **Route** field:

    `*<custom_domain>/<external_tenant_id(guid)>/*signup/v1.0/start*`

    Select **Fail Closed** for failure mode.

    [![Screenshot showing the Route configuration with Zone and Route fields.](media/tutorial-third-party-bot-protection-native-api-sign-up/route-configuration-screen.png)](media/tutorial-third-party-bot-protection-native-api-sign-up/route-configuration-screen.png#lightbox)
8. Select **Add Route**.

If the WAF setup was configured properly, all requests to the external tenant /start endpoint are intercepted by the worker.

### Configure worker logic for bot detection

The worker logic must be configured to:

- Extract relevant information from the sign-up request (device fingerprint, IP address, user agent, behavioral data).
- Send this data to your third-party bot protection provider's detection API.
- Evaluate the bot detection score returned by the provider.
- If the request is identified as a bot based on your threshold, block the request or present a challenge.
- If the request appears legitimate, forward it to the Microsoft Entra /start endpoint.

#### Third-party provider integration

This tutorial uses [HUMAN Security](https://docs.humansecurity.com/home) as the third-party bot protection provider. The Enforcer API provided by HUMAN Security is used for bot detection. Refer to the following HUMAN Security documentation:

- [Enforce an HTTP request | HUMAN Documentation](https://docs.humansecurity.com/applications/reference/request)
- SDK documentation: [Overview | HUMAN Documentation](https://docs.humansecurity.com/applications/mobile-sdk-intro)

Note

The worker code implementation is specific to your chosen bot protection provider's API and your detection thresholds. Contact Microsoft support for guidance on implementing the worker logic for your specific provider.

## Update the native app sign-up API call flow

The standard sign-up flow using Native API endpoints is described in the [Native authentication API reference documentation](/en-us/entra/identity-platform/reference-native-authentication-api?tabs=emailOtp#api-reference-for-sign-up). With bot protection enabled, your native app's sign-up flow interacts with the WAF layer transparently.

### Sign-up flow with bot protection

When the WAF intercepts a `/start` request and determines it's from a bot, it can either block the request entirely or present a challenge. The flow works as follows:

1. **App initiates sign-up:** The native app calls the `/start` endpoint to begin the sign-up flow.
2. **WAF intercepts request:** The WAF receives the request and extracts device and behavioral signals.
3. **Bot detection evaluation:** The WAF sends the signals to the bot protection provider for analysis.
4. **Decision point:**
    - If legitimate: Request is forwarded to Microsoft Entra `/start` endpoint.
    - If suspicious: Request is blocked or challenged based on your configuration.
5. **Sign-up continues:** If allowed, the standard sign-up flow proceeds with `/challenge`, `/continue`, and other endpoints.

Tip

To enhance bot detection accuracy, integrate your provider's SDK into your native app to collect device fingerprinting and behavioral signals. Pass these signals to the WAF through custom headers or request parameters.

Tip

For a complete Android SDK implementation example using WAF-based bot protection, see the [HUMAN Security bot protection sample app](https://github.com/Azure-Samples/ms-identity-ciam-native-auth-android-sample/tree/feature/integrate-human-signup-bot-protection).