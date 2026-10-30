---
layout: Conceptual
title: 'How to: Change the account types supported by an application - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/howto-modify-supported-accounts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this how-to, you configure an application registered with the Microsoft identity platform to change who, or what accounts, can access the application.
manager: pmwongera
ms.custom: 
ms.date: 2023-09-15T00:00:00.0000000Z
ms.reviewer: sureshja
ms.topic: how-to
locale: en-us
document_id: 63b31cc2-b6a1-a7b4-985c-072fab9ac083
document_version_independent_id: 36e85b2b-6c57-9485-ac5f-f0cfc5c98485
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/howto-modify-supported-accounts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/howto-modify-supported-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/howto-modify-supported-accounts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ca8f6c63-e00c-9ce0-3374-3a5fb1a5148f
---

# How to: Change the account types supported by an application - Microsoft identity platform | Microsoft Learn

When you registered your application with the Microsoft identity platform, you specified who--which account types--can access it. For example, you might've specified accounts only in your organization, which is a *single-tenant* app. Or, you might've specified accounts in any organization (including yours), which is a *multi-tenant* app.

In the following sections, you learn how to modify your app's registration to change who, or what types of accounts, can access the application.

## Prerequisites

- An [application registered in your Microsoft Entra tenant](quickstart-register-app)

## Change the application registration to support different accounts

To specify a different setting for the account types supported by an existing app registration:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Developer](../identity/role-based-access-control/permissions-reference#application-developer).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the tenant containing the app registration from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **App registrations**.
4. Select your application, and then select **Manifest** to use the manifest editor.
5. Download the manifest JSON file locally.
6. Now, specify who can use the application, sometimes referred to as the *sign-in audience*. Find the *signInAudience* property in the manifest JSON file and set it to one of the following property values:

    | Property value | Supported account types | Description |
    | --- | --- | --- |
    | **AzureADMyOrg** | Accounts in this organizational directory only (Microsoft only - Single tenant) | All user and guest accounts in your directory can use your application or API. Use this option if your target audience is internal to your organization. |
    | **AzureADMultipleOrgs** | Accounts in any organizational directory (Any Microsoft Entra directory - Multitenant) | All users with a work or school account from Microsoft can use your application or API. This includes schools and businesses that use Office 365. Use this option if your target audience is business or educational customers and to enable multitenancy. |
    | **AzureADandPersonalMicrosoftAccount** | Accounts in any organizational directory (Any Microsoft Entra directory - Multitenant) and personal Microsoft accounts (such as Skype, Xbox) | All users with a work or school, or personal Microsoft account can use your application or API. It includes schools and businesses that use Office 365 as well as personal accounts that are used to sign in to services like Xbox and Skype. Use this option to target the widest set of Microsoft identities and to enable multitenancy. |
    | **PersonalMicrosoftAccount** | Personal Microsoft accounts only | Personal accounts that are used to sign in to services like Xbox and Skype. Use this option to target the widest set of Microsoft identities. |
7. Save your changes to the JSON file locally, then select **Upload** in the manifest editor to upload the updated manifest JSON file.

### Why changing to multi-tenant can fail

Switching an app registration from single- to multi-tenant can sometimes fail due to Application ID URI (App ID URI) name collisions. An example App ID URI is `https://contoso.onmicrosoft.com/myapp`.

The App ID URI is one of the ways an application is identified in protocol messages. For a single-tenant application, the App ID URI need only be unique within that tenant. For a multi-tenant application, it must be globally unique so Microsoft Entra ID can find the app across all tenants. Global uniqueness is enforced by requiring that the App ID URI's host name matches one of the Microsoft Entra tenant's [verified publisher domains](howto-configure-publisher-domain).

For example, if the name of your tenant is *contoso.onmicrosoft.com*, then `https://contoso.onmicrosoft.com/myapp` is a valid App ID URI. If your tenant has a verified domain of *contoso.com*, then a valid App ID URI would also be `https://contoso.com/myapp`. If the App ID URI doesn't follow the second pattern, `https://contoso.com/myapp`, converting the app registration to multi-tenant fails.

For more information about configuring a verified publisher domain, see [Configure a verified domain](howto-configure-publisher-domain).