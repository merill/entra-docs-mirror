---
layout: Conceptual
title: Plan a CIAM Deployment - Microsoft Entra External ID | Microsoft Learn
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
description: Discover the steps for setting up a customer identity and access management (CIAM) solution in an external tenant, including creating a tenant, registering apps, and setting up user flows for sign-in.
ai-usage: ai-assisted
ms.topic: concept-article
ms.date: 2026-05-21T00:00:00.0000000Z
ms.custom: it-pro, seo-july-2024
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
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 27db9af4-115d-f993-c845-abc6ebf82201
---

# Plan a CIAM Deployment - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Microsoft Entra External ID adds customer identity and access management (CIAM) to your app on the Microsoft Entra platform, so you get consistent app integration, tenant management, and operations across workforce and customer scenarios.

This article is a decision-making guide for the six planning steps. Each section summarizes the key choices and links to the canonical how-tos and reference docs.

![Diagram showing the six setup steps as a horizontal flow: create an external tenant, choose an authentication approach, register your application, integrate a sign-in flow, secure your sign-in, and customize your sign-in.](media/concept-planning-your-solution/planning-flow-horizontal.png)

Jump to a step for details, or go straight to the **How-to guides**.

| Step | How-to guides |
| --- | --- |
| **Step 1: Create an external tenant** | • [Create an external tenant](how-to-create-external-tenant-portal)• [Or start a free trial](https://aka.ms/ciam-free-trial?wt.mc_id=ciamcustomertenantfreetrial_linkclick_content_cnl) |
| **Step 2: Choose an authentication approach** | • [Choose an authentication approach](concept-choose-authentication-approach) |
| **Step 3: Register your application** | • [Register your application](/en-us/entra/identity-platform/quickstart-register-app) |
| **Step 4: Integrate a sign-in flow with your app** | • [Create a user flow](how-to-user-flow-sign-up-sign-in-customers)• [Add your app to the user flow](how-to-user-flow-add-application) |
| **Step 5: Secure your sign-in** | • [Add multifactor authentication (MFA)](concept-multifactor-authentication-customers)• [Review security and governance](concept-security-customers)• [Integrate third-party bot protection](tutorial-third-party-bot-protection-native-api-sign-up)*(native authentication)*• [Integrate third-party ATO protection](tutorial-third-party-account-take-over-protection-native-api)*(native authentication)* |
| **Step 6: Customize your sign-in** | • [Customize branding](concept-branding-customers)*(browser-delegated)*• [Use a custom URL domain](concept-custom-url-domain)• [Add custom authentication extensions](concept-custom-extensions) |

## Step 1: Create an external tenant

![Diagram showing the setup flow with step 1, create an external tenant, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-1.png)

Your external tenant is the resource where you register apps and manage customer identities, separate from your workforce tenant. When you create it, you choose its geographic location and domain name. If you currently use Azure AD B2C, your existing B2C tenants aren't affected; see [Plan your migration from Azure AD B2C to External ID](plan-your-migration-from-b2c-to-external-id).

Important

Effective May 1, 2025, Azure Active Directory B2C (Azure AD B2C) is no longer available for new customers to purchase. To learn more, see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

The directory contains both [admin accounts](how-to-manage-admin-accounts) and customer accounts. Customers usually self-register; you can also [create local accounts](how-to-manage-customer-accounts). Customer accounts have a restricted [default permission set](reference-user-permissions) and can't see other users, groups, or devices.

### How to create an external tenant

- [Create an external tenant](how-to-create-external-tenant-portal) in the Microsoft Entra admin center.
- Don't have a tenant yet? [Start a free trial](https://aka.ms/ciam-free-trial?wt.mc_id=ciamcustomertenantfreetrial_linkclick_content_cnl).
- Using VS Code? Use the [Microsoft Entra External ID extension](https://aka.ms/ciamvscode/quickstarts/marketplace) ([learn more](https://aka.ms/ciamvscode/quickstartguide)).

## Step 2: Choose an authentication approach

![Diagram showing the setup flow with step 2, choose an authentication approach, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-2.png)

Decide how to build the sign-in experience before you register your app. This choice drives the rest of your integration.

- **Browser-delegated authentication** — Microsoft hosts the sign-in page; your app redirects users to it. Broad platform support, system-browser SSO, lower maintenance.
- **Native authentication** — your app hosts the sign-in UI and calls MSAL or the native authentication API directly. Full UI control, more development and security responsibility.

### How to choose an authentication approach

- [Choose an authentication approach](concept-choose-authentication-approach) — feature comparison and trade-offs.
- [Native authentication overview](/en-us/entra/identity-platform/concept-native-authentication) — detail if you're considering native.

## Step 3: Register your application

![Diagram showing the setup flow with step 3, register your application, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-3.png)

Register your app in your external tenant to establish a trust relationship with Microsoft Entra ID. The settings you configure depend on the authentication approach you chose in Step 2:

| Setting | Browser-delegated | Native authentication |
| --- | --- | --- |
| Redirect URI | Required (matches your app's sign-in callback) | Required only as a [web fallback](/en-us/entra/identity-platform/concept-native-authentication-web-fallback) |
| Public client flows | Not required | Enabled |
| Native authentication | Not required | Enabled |

After you register the app, update your code with the application (client) ID, tenant subdomain, and (if applicable) client secret.

### How to register your application

- Find platform-specific guidance on the [Samples by app type and language page](samples-ciam-all).
- If your platform isn't listed, follow the general [register an application](/en-us/entra/identity-platform/quickstart-register-app) quickstart.
- For native authentication app settings, see [How to enable native authentication](/en-us/entra/identity-platform/concept-native-authentication#how-to-enable-native-authentication).

## Step 4: Integrate a sign-in flow with your app

![Diagram showing the setup flow with step 4, integrate a sign-in flow with your app, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-4.png)

Create a sign-up and sign-in user flow that defines the sign-in methods, attributes to collect, and identity providers for your app. You create the user flow the same way for both authentication approaches; the difference is how your app drives it at runtime:

| - | Browser-delegated | Native authentication |
| --- | --- | --- |
| Runtime behavior | App redirects to the Microsoft-hosted sign-in page | App calls MSAL native authentication APIs from your own UI |
| Supported app types | Web, SPA, mobile, daemon | Mobile, SPA |
| Federated identity providers (social, external IdPs) | Supported | Not supported — use browser-delegated if needed |
| Company branding | Applies to Microsoft-hosted pages | Managed in your app's UI/localization |
| Attribute collection | Configured in the user flow | Configured in the user flow; submitted via the MSAL [user attribute builder](/en-us/entra/identity-platform/concept-native-authentication-user-attribute-builder) |

### Plan your user flow

- **Number of user flows.** Each app uses one user flow. You can share one flow across apps or create up to 10 per tenant for differentiated experiences.
- **Attributes to collect.** Decide which built-in attributes you need and whether you need [custom attributes](how-to-define-custom-attributes).
- **Terms and conditions consent.** Use custom attributes to capture consent with links to your terms and privacy policies.
- **Token claims.**[Add required attributes to the token](how-to-add-attributes-to-token) if your app depends on them.
- **Sign-in methods.** Local accounts (email OTP, email + password) work with both approaches. Federated providers ([Google](how-to-google-federation-customers), [Facebook](how-to-facebook-federation-customers), [Apple](how-to-apple-federation-customers), [another Microsoft Entra tenant](how-to-entra-id-federation-customers), [custom OIDC](how-to-custom-oidc-federation-customers)) require browser-delegated authentication.

### How to integrate a user flow with your app

- [Define custom attributes](how-to-define-custom-attributes) (if needed).
- [Create the sign-up and sign-in user flow](how-to-user-flow-sign-up-sign-in-customers).
- [Add your application to the user flow](how-to-user-flow-add-application).
- Wire up your app code:
    - **Browser-delegated:** follow a [sample or quickstart](samples-ciam-all) for your app type.
    - **Native authentication:** follow the [native authentication overview and tutorials](/en-us/entra/identity-platform/concept-native-authentication).

## Step 5: Secure your sign-in

![Diagram showing the setup flow with step 5, secure your sign-in, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-5.png)

Every customer-facing app needs MFA and a baseline security review. Native authentication apps have extra work: because your app is the exposed sign-in surface, you front it with a web application firewall (WAF). Browser-delegated apps inherit Microsoft's platform-level protections on the hosted sign-in pages.

- **Enable MFA.**[Available MFA methods](concept-multifactor-authentication-customers).
- **Review security and governance.** Conditional Access, risk-based policies, auditing. See [Security and governance](concept-security-customers).
- **Add bot protection***(native authentication only)*. Requires a [custom URL domain](concept-custom-url-domain). See [Integrate third-party bot protection](tutorial-third-party-bot-protection-native-api-sign-up).
- **Add account takeover (ATO) protection***(native authentication only)*. Requires a [custom URL domain](concept-custom-url-domain). See [Integrate third-party ATO protection](tutorial-third-party-account-take-over-protection-native-api).

## Step 6: Customize your sign-in

![Diagram showing the setup flow with step 6, customize your sign-in, highlighted.](media/concept-planning-your-solution/planning-flow-horizontal-step-6.png)

Customize the sign-in look and feel and extend it with your own business logic. With native authentication, your app owns the UI, so the Microsoft Entra company-branding feature doesn't apply — manage visuals and localization in your app code.

- **Customize branding***(browser-delegated only)*. Apply your logo, colors, and language strings to the Microsoft-hosted sign-in pages. See [Customize the sign-in look and feel](concept-branding-customers).
- **Use a custom URL domain.** Replace the default `ciamlogin.com` host with your own domain. Also a prerequisite for native authentication bot/ATO protection in Step 5. See [Custom URL domain](concept-custom-url-domain).
- **Add custom authentication extensions.** Extend the flow with server-side logic. Token-issuance extensions work with both approaches; attribute-collection extensions are browser-delegated only. See [Custom authentication extensions](concept-custom-extensions).