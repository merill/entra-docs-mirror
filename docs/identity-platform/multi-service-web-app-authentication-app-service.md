---
layout: Conceptual
title: Tutorial - Add authentication to Azure App Service - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/multi-service-web-app-authentication-app-service
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this tutorial, you learn how to enable authentication for a web app running on Azure App Service. Limit access to the web app to users in your organization​.
manager: pmwongera
ms.date: 2024-02-17T00:00:00.0000000Z
ms.reviewer: stsoneff
ms.subservice: 
ms.topic: tutorial
ms.custom: sfi-image-nochange
locale: en-us
document_id: da98f6cd-4869-689c-9357-accb7ed04591
document_version_independent_id: 3da7391b-a925-fc5e-6b80-03ef5c7f8023
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/multi-service-web-app-authentication-app-service.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/multi-service-web-app-authentication-app-service
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/multi-service-web-app-authentication-app-service.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 79ca9080-667b-75ff-4d13-09317b1b98f1
---

# Tutorial - Add authentication to Azure App Service - Microsoft identity platform | Microsoft Learn

Learn how to enable authentication for your web app running on Azure App Service and limit access to users in your organization.

![Diagram that shows user sign-in.](media/multi-service-web-app-authentication-app-service/web-app-sign-in.svg)

App Service provides built-in authentication support, so you can sign in users and access data by writing minimal or no code in your web app. Using the App Service authentication module isn't required, but helps simplify authentication and for your app. This article shows how to secure your web app with the App Service authentication module by using Microsoft Entra ID as the identity provider.

The authentication module is enabled and configured through the Azure portal and app settings. No SDKs, specific languages, or changes to application code are required.​ A variety of identity providers are supported, which includes Microsoft Entra ID, Microsoft Account, Facebook, Google, and X​​. When the authentication module is enabled, every incoming HTTP request passes through it before being handled by app code.​​ To learn more, see [Authentication and authorization in Azure App Service](/en-us/azure/app-service/overview-authentication-authorization).

In this tutorial, you:

- Configure authentication for the web app.
- Limit access to the web app to users in your organization.

## Prerequisites

If you don't have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create and publish a web app on App Service

For this tutorial, you need a web app deployed to App Service. You can use an existing web app, or you can follow one of the [ASP.NET Core](/en-us/azure/app-service/quickstart-dotnetcore), [Node.js](/en-us/azure/app-service/quickstart-nodejs), [Python](/en-us/azure/app-service/quickstart-python), or [Java](/en-us/azure/app-service/quickstart-java) quickstarts to create and publish a new web app to App Service.

Whether you use an existing web app or create a new one, take note of the following:

- web app name
- name of the resource group that the web app is deployed to

You need these names throughout this tutorial.

## Configure authentication

You now have a web app running on App Service. Next, you enable authentication for the web app. You use Microsoft Entra ID as the identity provider. For more information, see [Configure Microsoft Entra authentication for your App Service application](/en-us/azure/app-service/configure-authentication-provider-aad).

In the [Azure portal](https://portal.azure.com) menu, select **Resource groups**, or search for and select **Resource groups** from any page.

In **Resource groups**, find and select your resource group. In **Overview**, select your app's management page.

![Screenshot that shows selecting your app's management page.](media/multi-service-web-app-authentication-app-service/select-app-service.png)

On your app's left menu, select **Authentication**, and then click **Add identity provider**.

In the **Add an identity provider** page, select **Microsoft** as the **Identity provider** to sign in Microsoft and Microsoft Entra identities.

For **Tenant type**, select **Workforce**.

For **App registration** &gt; **App registration type**, select **Create new app registration**.

For **App registration** &gt; **Supported account types**, select **Current tenant-single tenant**.

In the **App Service authentication settings** section, leave **Authentication** set to **Require authentication** and **Unauthenticated requests** set to **HTTP 302 Found redirect: recommended for websites**.

At the bottom of the **Add an identity provider** page, click **Add** to enable authentication for your web app.

![Screenshot that shows configuring authentication.](media/multi-service-web-app-authentication-app-service/configure-authentication.png)

You now have an app that's secured by the App Service authentication.

Note

To allow accounts from other tenants, change the 'Issuer URL' to 'https://login.microsoftonline.com/common/v2.0' by editing your 'Identity Provider' from the 'Authentication' blade.

## Verify limited access to the web app

When you enabled the App Service authentication module, an app registration was created in your Microsoft Entra tenant. The app registration has the same display name as your web app. To check the settings, sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Developer](../identity/role-based-access-control/permissions-reference#application-developer) and browse to **Entra ID** &gt; **App registrations**. Select the app registration that was created. In the overview, verify that **Supported account types** is set to **My organization only**.

![Screenshot that shows verifying access.](media/multi-service-web-app-authentication-app-service/verify-access.png)

To verify that access to your app is limited to users in your organization, start a browser in incognito or private mode and go to `https://<app-name>.azurewebsites.net`. You should be directed to a secured sign-in page, verifying that unauthenticated users aren't allowed access to the site. Sign in as a user in your organization to gain access to the site. You can also start up a new browser and try to sign in by using a personal account to verify that users outside the organization don't have access.

## Clean up resources

If you're finished with this tutorial and no longer need the web app or associated resources, [clean up the resources you created](multi-service-web-app-clean-up-resources).