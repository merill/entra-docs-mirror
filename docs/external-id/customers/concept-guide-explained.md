---
layout: Conceptual
title: Get started guide features - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/concept-guide-explained
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about the features you set up with the get started guide.
ms.topic: concept-article
ms.date: 2025-02-06T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 172dcd2f-b812-ebb6-db87-dac36185026f
document_version_independent_id: 172dcd2f-b812-ebb6-db87-dac36185026f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/concept-guide-explained.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/concept-guide-explained
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/concept-guide-explained.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 0a84a9e1-3221-6d51-7039-40542d82e95b
---

# Get started guide features - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

After completing the [get started guide](/en-us/entra/external-id/customers/quickstart-get-started-guide), you can recreate, edit, and customize the initial configuration to meet your company’s needs. This helps you become familiar with the features and functions of Microsoft Entra External ID, better understand how to use them, and appreciate the value they provide. During this process, you might even discover new features that you want to use.

The get started guide set up the below features for you automatically. This article explains these features and guides you on how to configure them manually.

![Flowchart that shows the steps in the guide.](media/concept-guide-explained/guide-flow.png)

## Trial tenant creation

![Flowchart that shows the trial tenant creation step in the guide.](media/concept-guide-explained/trial-creation.png)

An external tenant is the first resource you need to create to get started with Microsoft Entra External ID. If you have an Azure subscription, you can create your new tenant in the Microsoft Entra admin center by following [these steps](how-to-create-external-tenant-portal).

## App registration

![Flowchart that shows the app registration step in the guide.](media/concept-guide-explained/app-registration.png)

To enable your application to sign in with Microsoft Entra External ID, you need to register your app with Microsoft Entra External ID. The get started guide creates this trusted relationship between the sample app and your tenant. It not only registers the app but also creates an endpoint, the redirect URI, and adds basic delegated permissions to the app for you to test the sign-in process.

If you register your app manually, you can also grant API permission if your app needs to call an API. Based on your app type, you have to choose the right registration process. You can find more information on how to register your app [here](/en-us/entra/identity-platform/quickstart-register-app).

## User flow

![Flowchart that shows the user flow step in the guide.](media/concept-guide-explained/user-flow.png)

The get started guide automatically creates the user flow for you. A user flow defines the authentication methods a customer can use to sign in to your application and the information they need to provide during sign-up. You can configure the existing user flow or create a new one. If you want the same sign-in experience for all of your apps, you can add multiple apps to the same user flow. However, only one sign-in experience is needed for an application, so you can add each application to just one user flow.

You can find more information on how to create a user flow [here](how-to-user-flow-sign-up-sign-in-customers) and how to add an application to the user flow [here](how-to-user-flow-add-application). After you create the user flow, you can test your sign-up and sign-in experience with the [Run user flow feature](how-to-test-user-flows).

If your app requires more information than the built-in user attributes provide, you can add your own attributes. We refer to these attributes as custom user attributes. You can create custom user attributes manually and add them to your user flow. You can find more information on how to create custom attributes [here](how-to-define-custom-attributes#create-custom-user-attributes).

## Branding

![Flowchart that shows the branding step in the guide.](media/concept-guide-explained/branding.png)

The get started guide provided you with several basic options to customize the sign-in page, including adding your company logo, changing the background color, and adjusting the layout.

After the initial setup, you can manually edit these settings and add more branding options. You can refine the layout, add headers and footers, configure text, images, and hyperlinks, and add languages to your sign-in and sign-up pages. For more details about the various branding options available in your new external tenant, visit the [Branding options](how-to-customize-branding-customers) page.

## Sign-in preview with your first user

![Flowchart that shows the sign-in preview step in the guide.](media/concept-guide-explained/sign-in-preview.png)

The get started guide allowed you to preview the sign-in experience with your first user. At this step in the guide, you had to create a new user only to test the sign-up steps. In the guide, your newly created user was redirected to JWT.ms instead of your app.

To find the user you created during the guide setup, you can go to the [admin center](https://entra.microsoft.com/) and look for the user in the users list. You can find the user in the users list as a [customer user](how-to-manage-customer-accounts) and also manage your own account as a [tenant admin](how-to-manage-admin-accounts). If you’d like to see data on user activity and engagement for registered applications in your tenant, you can use the [Application user activity dashboards](how-to-user-insights). The Application user activity dashboards are being retired on August 31, 2026; for new deployments, use [Azure Monitor](how-to-azure-monitor). For more information, see [Migrate from User Insights](how-to-user-insights#migrate-from-user-insights).

The guide set up the authentication method for your customer users; you choose between email and password, or one-time passcode sign-in. You can also manually configure other options for authenticating users of your applications, including enabling sign-in with social accounts like Facebook, Google, Apple, or using a custom OpenID Connect identity provider. For more information on how to configure these options, visit the [Authentication methods and identity providers](concept-authentication-methods-customers) page. You can also [enable self-service password reset](how-to-enable-password-reset-customers) for your customers.

## App samples

![Flowchart that shows the app sample step in the guide.](media/concept-guide-explained/app-sample.png)

The get started guide provides a downloadable sample app to test the features of your new tenant. When you register your app manually, Microsoft Entra ID generates a unique identifier known as an **Application (client) ID**. This value is used to identify your app when creating authentication requests, enabling a trusted relationship between your app and your tenant. The samples are automatically configured with your **clientId** and the **authority** is set to `<trialtenant>.ciamlogin.com`.

You can find the comprehensive list of app samples and guides [here](samples-ciam-all) that explains the process in detail.

The **Code sample guide** links point to the relevant sample articles and guide you through the process of registering your app, creating a user flow, associating your app with the user flow, and running your project to sign in. In some cases, it also guides you on how to call an API.

For more information on configuring your app for authentication, see the **Build and integrate guide** links. These tutorials assist you in building and integrating your own apps with Microsoft Entra External ID. You can also add [custom authentication extensions](concept-custom-extensions) at specific points within the authentication flow.