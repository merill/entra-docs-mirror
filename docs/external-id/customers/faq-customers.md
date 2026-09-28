---
layout: Conceptual
title: Frequently asked questions - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/faq-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Find answers to frequently asked questions about Microsoft Entra External ID. Learn about pricing, features, and the future of Azure AD B2C and External Identities.
ms.topic: faq
ms.date: 2026-05-20T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: it-pro
locale: en-us
document_id: e407c207-e1d7-f901-e184-f0daa7bd3d02
document_version_independent_id: a503616f-3fb2-4530-589b-9c421fd829c0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/faq-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/faq-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/faq-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3f086b6d-c4b0-394a-f5ca-44204587b2b9
---

# Frequently asked questions - Microsoft Entra External ID | Microsoft Learn

This article answers frequently asked questions about Microsoft Entra External ID. It offers guidance to help customers better understand Microsoft’s current external identities capabilities and the journey for our next generation platform (Microsoft Entra External ID).

This FAQ references customer identity and access management (CIAM). CIAM is an industry recognized category that covers solutions that manage identity, authentication, and authorization for external identity use cases (partners, customers, and citizens). Common functionality includes self-service capabilities, adaptive access, single sign-on (SSO), and bring your own identity (BYOI).

## External ID pricing

### How is External ID billed?

Microsoft Entra External ID pricing is based on monthly active users (MAU), which is the count of unique users with authentication activity within a calendar month. External ID consists of a core offer and premium add-ons. The Microsoft Entra External ID core offering is free for the first 50,000 MAU. For the latest information about usage billing and pricing, see [Billing model for Microsoft Entra External ID](../external-identities-pricing).

Note

If you previously subscribed to Azure Active Directory B2C (Azure AD B2C) or to B2B collaboration under an Azure AD External Identities P1/P2 SKU, see the [External ID pricing](../external-identities-pricing) page for information about current pricing options and any available upgrade paths.

### Does the 50,000 MAU free tier apply to add-ons?

No, External ID add-ons don't have a free tier. To learn more about pricing visit the [External ID pricing page](/en-us/entra/external-id/external-identities-pricing).

### Does External ID have phone authentication via SMS?

Currently, SMS isn't available for first-factor authentication or self-service password reset in external tenants. However, SMS is now available for second-factor verification in external tenants at additional cost. [Learn more](concept-multifactor-authentication-customers#sms-based-authentication)

### I linked my external tenant to a subscription, but the license status still shows "free"

After you link your external tenant to a subscription, you can view it on your external tenant home page (**Home** &gt; **Billing**). However, the license on your external tenant overview page (**Home** &gt; **Tenant overview** &gt; **Overview**) still shows **Microsoft Entra ID Free**. We're working to resolve this known issue.

### Why does my Azure AD External Identities bill show phone charges named "Microsoft Entra External ID?"

Following the new [billing model](https://azure.microsoft.com/pricing/details/active-directory-b2c/) for Azure AD External Identities SMS Phone Authentication, you might notice a new name for Phone MFA on your bill. Now you see the following names based on your [country or region pricing tier](https://aka.ms/ExternalIDSMSCountries):

- Microsoft Entra External ID - Phone Authentication Low Cost 1 Transaction
- Microsoft Entra External ID - Phone Authentication Mid Low Cost 1 Transaction
- Microsoft Entra External ID - Phone Authentication Mid High Cost 1 Transaction
- Microsoft Entra External ID - Phone Authentication High Cost 1 Transaction

Although the new bill mentions Microsoft Entra External ID, if you're an Azure AD External Identities customer, **you’re still billed for Azure AD B2B based on your core MAU count**.

## About External ID

### What is Microsoft Entra External ID?

Microsoft Entra External ID is our next generation CIAM platform. It represents an evolutionary step in unifying secure and engaging experiences across all external identities including customers, partners, citizens, and others, within a single, integrated platform.

### Is Microsoft Entra External ID a new name for Azure AD B2C?

No, it's not a new name for Azure AD B2C. Microsoft Entra External ID is our next generation CIAM solution that combines CIAM use cases and B2B collaboration features into one unified platform.

### I notice some name changes, both in the admin center and on the website

Yes, we rebranded some items in the admin center and in our messaging to best match our vision for External ID. The following table summarizes the changes.

| Previous name | New name |
| --- | --- |
| Azure AD External Identities | Azure AD B2C |
| Azure AD B2B | Now part of Microsoft Entra External ID |
| Azure AD for customers | Microsoft Entra External ID |
| Azure AD B2B collaboration | External ID B2B collaboration |
| Azure AD B2B direct connect | External ID B2B direct connect |
| Customer tenant | External tenant |

Note

A Microsoft Entra tenant can be created in either a workforce tenant configuration or an external tenant configuration. [Learn more about tenant configurations](../tenant-configurations).

### How can I get started with External ID?

Get started with securing your consumer and business customer apps by [creating an external tenant](quickstart-tenant-setup) in the Microsoft Entra admin center.

## Azure AD B2C and Azure AD External Identities

### What's happening to Azure AD B2C and Azure AD External Identities?

Effective May 1, 2025 Azure AD B2C P1 and P2 will no longer be available to purchase for new customers, but current Azure AD B2C customers can continue using the product. The product experience, including creating new tenants or user flows, remains unchanged. The operational commitments, including service level agreements (SLAs), security updates, and compliance, also remain unchanged. We'll continue supporting Azure AD B2C until at least May 2030. For detailed migration guidance, see [Plan your migration from Azure AD B2C to External ID](plan-your-migration-from-b2c-to-external-id). Contact your account representative for more information and to learn more about Microsoft Entra External ID.

### What's happening to Azure AD B2B collaboration and B2B direct connect?

Azure AD B2B collaboration and B2B direct connect are now part of Microsoft Entra External ID as External ID B2B collaboration and B2B direct connect. They remain in the same location in the Microsoft Entra admin center within the workforce tenant.

### I have a substantial investment in custom policies, including code artifacts and CI/CD pipelines. How should I view the upcoming converged platform?

We recognize the large investments in building and managing custom policies. We listened to customers who told us custom policies are too hard to build and manage. With the new External ID platform, we're simplifying experiences so that custom policies are no longer needed. We'll provide a migration path for existing custom policies in B2C when it becomes available.

## Product Features

### What's the difference between external and workforce tenants?

Both are Microsoft Entra tenants, but with different default configurations. [Learn more about the tenant configurations](../tenant-configurations).

### Are there custom policies in External ID?

Our next-generation CIAM platform is designed to accommodate equivalent capabilities without the need for complex custom policies.

### What identity providers does External ID support?

External ID supports various identity providers, including Microsoft Entra accounts (via invite), Facebook, Google, Apple, Microsoft Entra ID federation, custom OIDC, and SAML/WS-Fed identity provider federation. Identity providers are based on the tenant configuration and whether the external user is invited or uses self-service sign-up. [Learn more about identity providers](../identity-providers) in External ID, and refer to our [supported feature comparison](concept-supported-features-customers).

### Where can I find a list of External ID features?

For a detailed list of the External ID features and capabilities, see [Supported features in workforce and external tenants](concept-supported-features-customers).

### Will External ID support Microsoft Entra US Government Cloud?

External ID currently supports public clouds only. External ID in the public cloud is accredited for [Federal Risk and Authorization Management Program](/en-us/azure/compliance/offerings/offering-fedramp) (FedRAMP) High and [Department of Defense (DoD) Impact Level 2 (IL2)](/en-us/azure/compliance/offerings/offering-dod-il2).

## Developer Experiences

### I'm a developer, where can I get started with External ID?

You can find the latest resources and information for developers in our [Developer Center](https://aka.ms/ciam/dev).

- [Create an external tenant](quickstart-tenant-setup) and follow a guide to set up your tenant and run your first sample.
- Use our tutorials to learn how to build and integrate your consumer and business customer apps with External ID.
- Sign up for [Identity blog](https://devblogs.microsoft.com/identity/tag/external-id/) email updates to keep up with the latest news and insights.
- Follow us on [YouTube](https://www.youtube.com/playlist?list=PL3ZTgFEc7Lythpts59O9KOVuEDLWJLLmA) for video overviews, tutorials, and deep dives.

In addition to those resources, we have some developer-focused features in public preview:

- Use Microsoft Entra External ID as an identity provider for [Azure App Service’s built-in authentication](https://devblogs.microsoft.com/identity/app-service-external-id/).
- Use the [Microsoft Entra External ID extension for Visual Studio Code](https://aka.ms/ciam/vscode/marketplace). This extension offers a seamless, guided experience that enables you to create and configure a sample External ID application entirely from within VS Code. Read our [blog](https://devblogs.microsoft.com/identity/external-id-extension/) and [documentation](visual-studio-code-extension) to learn more.

### How do I add authentication with External ID to my app code?

We have a single, unified [Microsoft Authentication Library (MSAL)](../../identity-platform/msal-overview) where the same application code works for workforce and customer scenarios. In three steps, you can sign up or sign in a user:

1. Configure MSAL to use to your tenant and application
2. Create a sign-in function that calls MSAL to start the web-based sign in flow
3. Create a response handler which can extract customer information from the returned token

You can see example code for each of these steps in our [sample applications](samples-ciam-all).

### Can I build a fully custom authentication sign-in experience?

Yes. Microsoft Entra External ID supports two authentication approaches: **browser-delegated authentication**, which redirects users to a Microsoft-hosted sign-in page, and **native authentication**, which lets you build the sign-in UI directly into your app. Native authentication gives you full control over the sign-in experience for mobile and single-page applications but requires more development effort and shared security responsibility. To compare both approaches and decide which is right for your app, see [Choose an authentication approach](concept-choose-authentication-approach).

### What integrations does External ID support for developers?

External ID supports server-side integrations with external systems via [custom authentication extensions](../../identity-platform/custom-extension-overview). This capability allows developers to implement their own logic and invoke it via real-time API calls during sign-in/up flows.