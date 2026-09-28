---
layout: Conceptual
title: How to Register an App in Microsoft Entra ID" - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to register your app in Microsoft Entra ID and configure it for single-tenant or multitenant use.
manager: pmwongera
ms.custom: 
ms.date: 2026-05-14T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
locale: en-us
document_id: c9642c47-826b-017f-eff3-ab3b25e4e454
document_version_independent_id: 091f26e7-6543-ef0f-b575-b44519943391
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-register-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-register-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-register-app.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 3c608975-4529-a003-b4c2-84a21d270068
---

# How to Register an App in Microsoft Entra ID" - Microsoft identity platform | Microsoft Learn

In this how-to guide, you learn how to register an application in Microsoft Entra ID. This process is essential for establishing a trust relationship between your application and the Microsoft identity platform. By completing this quickstart, you enable identity and access management (IAM) for your app, allowing it to securely interact with Microsoft services and APIs.

## Prerequisites

- An Azure account that has an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- The Azure account must be at least an [Application Developer](../identity/role-based-access-control/permissions-reference#application-developer).
- A workforce or external tenant. You can use your **Default Directory** for this quickstart. If you need an external tenant, complete [set up an external tenant](/en-us/entra/external-id/customers/quickstart-tenant-setup).

## Register an application

Registering your application in Microsoft Entra establishes a trust relationship between your app and the Microsoft identity platform. The trust is unidirectional. Your app trusts the Microsoft identity platform, and not the other way around. Once created, you can't move the application object between different tenants.

Follow these steps to create the app registration:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Developer](../identity/role-based-access-control/permissions-reference#application-developer).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the tenant in which you want to register the application.
3. Browse to **Entra ID** &gt; **App registrations** and select **New registration**.
4. Enter a meaningful **Name** for your app; for example, *identity-client-app*. App users can see this name, and you can change it at any time. You can have multiple app registrations with the same name.
5. Under **Supported account types**, open the drop-down and select who can use the application. We recommend **Single tenant only - &lt;your tenant&gt;** for most applications. Refer to the table for more information on each option.

    | Supported account types | Description |
    | --- | --- |
    | **Single tenant only - &lt;your tenant&gt;** | For *single-tenant* apps for use only by users (or guests) in *your* tenant. |
    | **Multiple Entra ID tenants** | For *multitenant* apps when you want users in *any* Microsoft Entra tenant to be able to use your application. Ideal for software-as-a-service (SaaS) applications that you intend to provide to multiple organizations. |
    | **Any Entra ID Tenant + Personal Microsoft accounts** | For *multitenant* apps that support both organizational and personal Microsoft accounts (for example, Skype, Xbox, Live, Hotmail). |
    | **Personal accounts only** | For apps used only by personal Microsoft accounts (for example: Xbox, Live, Hotmail). |
6. Select **Register** to complete the app registration.
7. The application's **Overview** page is displayed. Record the **Application (client) ID**, which uniquely identifies your application and is used in your application's code as part of validating the security tokens it receives from the Microsoft identity platform.

Important

New app registrations are hidden to users by default. When you're ready for users to see the app on their [My Apps page](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510) you can enable it. To enable the app, navigate to **Entra ID** &gt; **Enterprise apps** in the Microsoft Entra admin center and select the app. Then set **Visible to users?** to **Yes** on the **Properties** page.

## Grant admin consent (external tenants only)

Once you register your application, it gets assigned the **User.Read** permission. However, for external tenants, the customer users can't consent to permissions themselves. You as the admin must consent to this permission on behalf of all the users in the tenant:

1. Select **API permissions** under **Manage** on your app registration's **Overview** page.
2. Select **Grant admin consent for &lt; tenant name &gt;**, then select **Yes**.
3. Select **Refresh**, then verify that **Granted for &lt; tenant name &gt;** appears under **Status** for the permission.