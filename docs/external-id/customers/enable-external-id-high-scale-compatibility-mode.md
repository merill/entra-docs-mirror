---
layout: Conceptual
title: Enable External ID High Scale Compatibility (HSC) mode - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/enable-external-id-high-scale-compatibility-mode
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Enable HSC mode on your Azure AD B2C tenant to adopt Microsoft Entra External ID endpoints while keeping existing users and credentials in place.
ms.topic: how-to
ms.date: 2026-03-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 3b46ea7e-f0b4-536e-acac-e062a56e5bd1
document_version_independent_id: 3b46ea7e-f0b4-536e-acac-e062a56e5bd1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/enable-external-id-high-scale-compatibility-mode.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/enable-external-id-high-scale-compatibility-mode
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/enable-external-id-high-scale-compatibility-mode.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: cae49f94-dda9-6c93-17c0-c372ed8e307f
---

# Enable External ID High Scale Compatibility (HSC) mode - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Enable High Scale Compatibility (HSC) mode to transition applications from Azure AD B2C to Microsoft Entra External ID with minimal disruption while keeping existing B2C user credentials in place. New customers evaluating Microsoft Entra External ID at scale should refer to [Planning your solution](concept-planning-your-solution).

If you're an Azure AD B2C customer and haven't yet reviewed the available options for migration, refer to [Plan your migration from Azure AD B2C to External ID](plan-your-migration-from-b2c-to-external-id).

In this article, you’ll learn how to:

- Enable HSC mode by using Microsoft Graph
- Review identity schema for coexistence
- Onboard and validate your first applications on External ID endpoints
- Roll out additional applications and prepare for Azure AD B2C retirement

## Prerequisites

This article assumes you've already chosen the **High Scale Compatibility (HSC) mode migration approach**. If you still need to decide between approaches (standard vs. HSC mode), start with [Plan your migration from Azure AD B2C to External ID](plan-your-migration-from-b2c-to-external-id).

Important

Enabling HSC mode is a significant tenant-level change and can only be reversed by contacting Microsoft support. Before you call the enable API, confirm you've reviewed the [HSC mode limitations](plan-your-migration-from-b2c-to-external-id#hsc-mode-limitations) — including gaps for social identity providers, passkeys, age gating, admin portal experience, and Conditional Access — and validated that your scenarios are supported.

Before you begin, contact your Microsoft account team or raise a support ticket to request allowlisting for HSC mode. This process can take a few days to complete. You can't proceed to Stage 1 until your tenant is allowlisted.

If your Azure AD B2C tenant uses custom attributes, verify that every custom attribute has a nonempty `description` value before enabling HSC mode. The enable API syncs custom attributes to the External ID context and fails if any attribute has a null or empty description. To check and fix attribute descriptions, see [Custom attribute sync fails](troubleshoot-high-scale-compatibility-mode#custom-attribute-sync-fails).

## Stage 1: Enable HSC mode

Once your tenant is allowlisted for HSC mode, you can turn on HSC mode by calling the following Microsoft Graph API. The calling account needs the [`Policy.ReadWrite.AuthenticationFlows`](/en-us/graph/permissions-reference#policyreadwriteauthenticationflows) permission:

**POST**: `https://graph.microsoft.com/beta/policies/authenticationFlowsPolicy/externalIdHybridModeConfiguration`**Body**: `{}`

Important

After you enable HSC mode, allow up to 1 hour for the changes to take effect across all services before proceeding to Stage 2. If you need to disable HSC mode, contact Microsoft support.

## Stage 2: Review token claims for coexistence

During coexistence, applications authenticate users through either B2C or External ID endpoints. Before migrating applications, review how token claims are populated to avoid breaking changes.

Most tenants don't need to make any identity data changes. However, if your applications rely on specific claims — most commonly `email` or `sub` — verify that those attributes are correctly populated and emitted. Applications can break if expected claims are missing or use different claim names in External ID.

**Common scenarios to check**

- Applications that rely on `email` or `sub`
- Local accounts where `mail` isn't populated
- Claims populated only via sign-in names or custom policies

Important

In External ID, the `sub` claim isn't set to the same value as `oid`. If your applications depend on the `sub` claim matching the user's `oid`, request the `profile` scope to retrieve the `oid` claim and use it as the stable user identifier instead.

Before migrating applications, validate how attributes map to token claims used by your applications. You can configure optional claims using [JWT claims customization](/en-us/entra/identity-platform/jwt-claims-customization), or use [custom extensions](/en-us/entra/identity-platform/custom-extension-overview) to add external user data to tokens before they're issued.

If your applications don't depend on specific token claims, continue to Stage 3.

## Stage 3: Build your first External ID application (with existing B2C users)

Use the following steps to create and configure an application that uses External ID endpoints while continuing to use the existing Azure AD B2C user base. Native authentication is optional and applies only to apps that use the native auth APIs.

### Register your application

Follow the instructions in [Register an application](/en-us/entra/identity-platform/quickstart-register-app) to register your application.

When registering an application in your External ID tenant, choose *Accounts in this organizational directory only*. When registering an application in your B2C tenant, choose *Accounts in any organizational directory*.

Note

Existing Azure AD B2C app registrations can't be reused for External ID endpoints due to differences in application properties, single‑tenant requirements, and Native Authentication support, which requires dedicated app registrations.

### (Optional) Native authentication

If you're using native authentication, enable it by following the guidance in [Native authentication](/en-us/entra/identity-platform/concept-native-authentication).

### Configure user flows

Next, create an External ID user flow and associate it with your application. You can use the Microsoft Graph API to do this. For more information, see [Create authentication event flows](/en-us/graph/api/identitycontainer-post-authenticationeventsflows?view=graph-rest-beta&amp;tabs=http&amp;preserve-view=true).

### (Optional) Configure a custom URL domain and Azure Front Door

External ID supports custom authentication domains (for example, `login.contoso.com`) to maintain branding and consistency. [Custom URL domains](/en-us/entra/external-id/customers/concept-custom-url-domain) are implemented using a reverse proxy such as Azure Front Door, which routes traffic from the custom domain to the underlying External ID endpoints.

Important

When using Azure Front Door, routing rules must be clearly defined to ensure authentication traffic is sent to the correct identity platform. Azure Front Door routes requests based on hostnames and paths, and each custom domain is associated with a specific backend origin.

If an application needs to support authentication traffic for both Azure AD B2C and Microsoft Entra External ID at the same time, sharing the same custom authentication domain isn't recommended. Because [Azure Front Door routing methods](/en-us/azure/frontdoor/routing-methods) can route a custom domain to only one origin at a time, this scenario typically requires a separate custom domain for External ID endpoints (for example, `login.contoso.com` for B2C and `login-ext.contoso.com` for External ID) to avoid routing conflicts and unintended traffic mixing.

### (Optional) Add custom authentication extensions

Some applications require lightweight logic during authentication, such as attribute validation or token enrichment. Custom authentication extensions let you invoke an external REST API at specific points in the authentication flow without building full custom policies. For more information, see [Custom authentication extensions](/en-us/entra/external-id/customers/concept-custom-extensions) and [Custom extensions overview](/en-us/entra/identity-platform/custom-extension-overview).

## Stage 4: Validate end-to-end scenarios

Before you roll out broadly, validate the External ID–enabled application across critical authentication scenarios.

**Recommended validation**

- Sign in to the new app using existing B2C credentials.
- Inspect the issued token and verify:
    - `oid` remains the same as B2C.
    - `issuer` and `sub` differ from B2C.
- Sign up a new user in the new app using External ID auth endpoints (web or native authentication APIs).
- Sign in with the same user on a legacy B2C app and confirm the same `oid`.
- After validation, use the new app with hosted web flows and External ID features.

**What to verify**

- Existing users and newly created users.
- Token claims consumed by backend APIs.
- Sign‑in logs and error handling.

## Stage 5: Expand application adoption incrementally and prepare for retirement

After the initial application is validated:

- Onboard additional applications to External ID one at a time.
- Keep remaining applications on Azure AD B2C until they're ready.
- Maintain coexistence between B2C and External ID applications as needed.
- Ensure all Azure AD B2C applications are migrated to Microsoft Entra External ID on or before Azure AD B2C service retirement.
- Once all applications are running on External ID endpoints, no further action is required.