---
layout: Conceptual
title: What is single sign-on in Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/what-is-single-sign-on
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn about single sign-on for enterprise applications in Microsoft Entra ID, including SAML and OpenID Connect protocols.
ms.topic: overview
ms.date: 2026-06-04T00:00:00.0000000Z
ms.reviewer: alamaral
ms.custom: enterprise-apps-article, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 9edfc165-8727-4f35-1be0-b570ee716673
document_version_independent_id: b41dd96e-4a97-6f83-0b31-9ce17d1de42c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/what-is-single-sign-on.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/what-is-single-sign-on
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/what-is-single-sign-on.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4ec4860b-ee66-a9fb-195e-fcbf62f636e4
---

# What is single sign-on in Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn

Single sign-on (SSO) lets users sign in once and reach many applications. This article explains what SSO is, why it helps ISVs and organizations, the SSO options in Microsoft Entra ID, and how the sign-in process works.

With SSO, users sign in with one set of credentials. They can then open every assigned application without signing in again.

SSO matters to two audiences. **Independent software vendors (ISVs)** build applications for enterprise customers. **Organizations** manage application access for their users. You might be a developer who integrates an app with Microsoft Entra ID, or an admin who plans an SSO rollout. In both roles, SSO basics help you improve security and the user experience.

When Microsoft Entra ID is the identity provider, users sign in once with their work credentials. Microsoft Entra ID verifies each user and confirms their identity to the app. Apps no longer manage separate usernames and passwords.

## Why use single sign-on?

SSO offers clear benefits for two groups: ISVs and the people who use and manage apps.

### For ISV application providers

For ISVs, SSO makes an application easier to sell and support:

- **Enterprise readiness**: SSO makes your app a fit for enterprise customers.
- **Faster onboarding**: Customers deploy your app without managing extra credentials.
- **Competitive advantage**: Enterprise buyers often require SSO.
- **Simpler user management**: Your app relies on the customer's identity system instead of its own user database.

### For end users and organizations

For users and admins, SSO improves daily access and security:

- **Better user experience**: Users keep fewer credentials and sign in less often.
- **Stronger security**: Central sign-in limits credential exposure and applies consistent policies.
- **Easier access management**: Admins control access from one identity provider.
- **Less support overhead**: Fewer password resets and account tasks reach the help desk.

## Single sign-on options

The right SSO method depends on how an app authenticates and where it runs. Microsoft Entra ID supports several approaches.

### Federation-based SSO

Federation-based SSO gives the richest integration. Microsoft Entra ID authenticates users and sends identity information to apps through standard protocols.

**Security Assertion Markup Language (SAML) 2.0**: A mature, XML-based standard used widely in enterprises. SAML suits traditional web apps and cases that need detailed user attributes.

**OpenID Connect (OIDC)**: A modern protocol built on OAuth 2.0 that uses JSON-based tokens. OIDC suits modern web apps, mobile apps, and APIs that need both authentication and authorization.

**Protocol considerations**:

- **For ISV developers**: OIDC is usually simpler to build with modern frameworks. SAML offers broader enterprise compatibility.
- **For administrators**: Both protocols work with your identity infrastructure, though SAML might fit established enterprise systems better.

### Password-based SSO

Password-based SSO works with apps that use username and password sign-in. Microsoft Entra ID securely stores the credentials and replays them to the app. This method helps with apps that don't support federation protocols, especially on-premises apps that use Application Proxy. Application Proxy publishes on-premises apps for secure remote access.

### Linked SSO

Linked SSO keeps a consistent experience while you migrate apps. It adds app links in user portals, but it doesn't provide true single sign-on. Use it for phased migrations, where full SSO comes later.

### Disabled SSO

When SSO is disabled, users sign in to each app separately. Use this setting during testing, or for apps that don't need integrated sign-in.

## How SSO works with Microsoft Entra ID

The SSO process has three parts: the user, the app, and Microsoft Entra ID as the identity provider.

1. **User requests access**: A user opens an app.
2. **Redirect to sign-in**: The app sends the user to Microsoft Entra ID.
3. **Identity check**: Microsoft Entra ID verifies the user's work credentials.
4. **Access granted**: Microsoft Entra ID confirms the user's identity, and the app grants access.

This four-step process happens automatically, so apps don't manage user credentials directly.

## Planning SSO deployment

A successful SSO rollout depends on app hosting, user needs, and integration options. Apps can run on-premises, in the cloud as software as a service (SaaS), or in hybrid environments. Each hosting model shapes your SSO approach.

- **Cloud apps** usually use federation protocols like SAML or OpenID Connect.
- **On-premises apps** can use federation protocols or password-based SSO through Application Proxy.
- **Hybrid scenarios** might combine approaches, based on each app's needs.

For comprehensive planning guidance, see [Plan a single sign-on deployment](plan-sso-deployment) for organizations and [Plan SSO integration for ISV applications](plan-sso-integration-isv) for application developers.

## User experience: My Apps portal

End users access their SSO-enabled applications through the My Apps portal, which provides a centralized location for all assigned applications. Users can find and launch applications without remembering multiple credentials. For more information, see [Sign in and start apps from the My Apps portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).