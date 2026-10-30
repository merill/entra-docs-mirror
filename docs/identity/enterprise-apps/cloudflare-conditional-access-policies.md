---
layout: Conceptual
title: Tutorial to configure Conditional Access policies in Cloudflare Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/cloudflare-conditional-access-policies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: martinco
description: Configure Conditional Access to enforce application and user policies in Cloudflare Access.
ms.topic: tutorial
ms.date: 2024-04-18T00:00:00.0000000Z
ms.reviewer: gasinh
ms.collection: M365-identity-device-management
ms.custom: not-enterprise-apps
locale: en-us
document_id: 8520fbb6-e432-5b8b-e8e1-5f869eaf41aa
document_version_independent_id: cb432966-2268-eb99-dde4-d4d9becdf42a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/cloudflare-conditional-access-policies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/cloudflare-conditional-access-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/cloudflare-conditional-access-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2860b147-f8b4-8914-fff7-1d8ad14b1080
---

# Tutorial to configure Conditional Access policies in Cloudflare Access - Microsoft Entra ID | Microsoft Learn

With Conditional Access, administrators enforce policies on application and user policies in Microsoft Entra ID. Conditional Access brings together identity-driven signals, to make decisions, and enforce organizational policies. Cloudflare Access creates access to self-hosted, software as a service (SaaS), or nonweb applications.

Learn more: [What is Conditional Access?](../conditional-access/overview)

## Prerequisites

- A Microsoft Entra subscription
    - If you don't have one, get an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)
- A Microsoft Entra tenant linked to the Microsoft Entra subscription
    - See, [Quickstart: Create a new tenant in Microsoft Entra ID](../../fundamentals/create-new-tenant)
- One of the following roles: Cloud Application Administrator, or Application Administrator.
- Configured users in the Microsoft Entra subscription
- A Cloudflare account
    - Go to `dash.cloudflare.com` to [Get started with Cloudflare](https://dash.cloudflare.com/sign-up)

## Scenario architecture

- **Microsoft Entra ID** - Identity Provider (IdP) that verifies user credentials and Conditional Access
- **Application** - You created for IdP integration
- **Cloudflare Access** - Provides access to applications

## Set up an identity provider

Go to developers.cloudflare.com to [set up Microsoft Entra ID as an IdP](https://developers.cloudflare.com/cloudflare-one/identity/idp-integration/entra-id/#set-up-entra-id-as-an-identity-provider).

Note

It's recommended you name the IdP integration in relation to the target application. For example, **Microsoft Entra ID - Customer management portal**.

## Configure Conditional Access

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **App registrations** &gt; **All applications**
3. Select the application you created.
4. Go to **Branding & properties**.
5. For **Home page URL**, enter the application hostname.

    ![Screenshot of options and entries for branding and properties.](media/cloudflare-conditional-access-policies/branding-properties.png)
6. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
7. Select your application.
8. Select **Properties**.
9. For **Visible to users**, select **Yes**. This action enables the app to appear in App Launcher and in [My Apps](https://myapplications.microsoft.com/).
10. Under **Security**, select **Conditional Access**.
11. See, [Building a Conditional Access policy](../conditional-access/concept-conditional-access-policies).
12. Create and enable other policies for the application.

## Create a Cloudflare Access application

Enforce Conditional Access policies on a Cloudflare Access application.

1. Go to `dash.cloudflare.com` to [sign in to Cloudflare](https://dash.cloudflare.com/login).
2. In **Zero Trust**, go to **Access**.
3. Select **Applications**.
4. See, [Add a self-hosted application](https://developers.cloudflare.com/cloudflare-one/applications/configure-apps/self-hosted-apps/).
5. In **Application domain**, enter the protected application target URL.
6. For **Identity providers**, select the IdP integration.
7. Create an Access policy. See, [Access policies](https://developers.cloudflare.com/cloudflare-one/policies/access/) and the following example.

    Note

    Reuse the IdP integration for other applications if they require the same Conditional Access policies. For example, a baseline IdP integration with a Conditional Access policy requiring multifactor authentication and a modern authentication client. If an application requires specific Conditional Access policies, set up a dedicated IdP instance for that application.