---
layout: Conceptual
title: Quickstart - Get started - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/quickstart-get-started-guide
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to get started with Microsoft Entra External ID. Customize your apps' look and feel, set up a user to test the sign-up flow, and configure a sample app in just a few minutes.
ms.topic: quickstart
ms.date: 2024-11-28T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: cd7ba452-b133-e192-45ca-8fd16d336538
document_version_independent_id: 04f684d9-d348-5d80-f05f-8b71ac477221
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/quickstart-get-started-guide.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/quickstart-get-started-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/quickstart-get-started-guide.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 02fb3f6d-afd3-785c-599b-4225a5f1c460
---

# Quickstart - Get started - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this quickstart, we'll guide you through customizing the look and feel of your apps in the external tenant. We'll also help you set up a user to test the sign-up flow and configure a sample app in just a few minutes. With these built-in external configuration features, Microsoft Entra External ID can serve as the identity provider and access management service for your customers.

## Prerequisites

- An external tenant. If you don't already have one, [sign up for a free trial](https://aka.ms/ciam-free-trial?wt.mc_id=ciamcustomertenantfreetrial_linkclick_content_cnl) or [create a tenant with external configurations in the Microsoft Entra admin center](quickstart-tenant-setup).

Note

You can also use the [Microsoft Entra External ID extension for Visual Studio Code](https://aka.ms/ciamvscode/quickstarts/marketplace) to create your external tenant, customize your sign-in experience, and set up a sample app directly within Visual Studio Code ([learn more](https://aka.ms/ciamvscode/quickstartguide)).

## Customize your sign-in experience

When you set up an external tenant free trial, the guide will start automatically as part of the configuration of your new external tenant. If you created your external tenant with an Azure subscription, you can start the guide manually by following the steps below.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **Overview**.
4. On the **Get started** tab, select **Start the guide**.

    ![Screenshot that shows how to start the guide.](media/how-to-create-external-tenant-portal/guide-link.png)

You can customize your customer's sign-in and sign-up experience in the external tenant. Follow the guide that will help you set up the tenant in three easy steps. First you must specify how would you like your customer to sign in. At this step you can choose between two options: **Email and password** or **Email and one-time passcode**. You can configure external accounts later, which would allow your customers to sign in using their [Google](how-to-google-federation-customers), [Facebook](how-to-facebook-federation-customers), [Apple](how-to-apple-federation-customers), [Microsoft Entra ID](how-to-entra-id-federation-customers), or [custom OIDC](how-to-custom-oidc-federation-customers) account. You can also [define custom attributes](how-to-define-custom-attributes) to collect from the user during sign-up.

If you prefer, you can add your company logo, change the background color or adjust the sign-in layout. These optional changes will apply to the look and feel of all your apps in this tenant with external configurations. After you have the created tenant, other branding options are available. You can [customize the default branding](how-to-customize-branding-customers) and [add languages](how-to-customize-languages-customers). Once you're finished with the customization, select **Continue**.

![Screenshot of customizing the sign-in experience in the guide.](media/quickstart-get-started-guide/customize-branding-in-trial-wizard.png)

## Try out the sign-up experience and create your first user

1. The guide will configure your tenant with the options you have selected. Once the configuration is complete, the button will change its text from **Setting up...** to **Run it now**.
2. Select the **Run it now** button. A new browser tab will open with the sign-in page for your tenant that can be used to create and sign in users.
3. Select **No account? Create one** to create a new user in the tenant.
4. Add your new user's email address and select **Next**.

Note

Use a different email address than the one used to create your trial. If you use your tenant admin email to create a customer account through [self-service sign-up](/en-us/entra/external-id/self-service-sign-up-overview) or by [adding a new external user](/en-us/entra/external-id/customers/how-to-manage-customer-accounts#create-a-customer-account) in the Microsoft Entra admin center, the system creates a second account with the same email address. This new account has customer-level privileges, which can cause conflicts.

1. Complete the sign-up steps on the screen. Typically, once the user has signed in, they're redirected back to your app. However, since you haven’t set up an app at this step, you'll be redirected to JWT.ms instead, where you can view the contents of the token issued during the sign-in process.
2. Go back to the guide tab. At this stage, you can either exit the guide and go to the admin center to explore the full range of configuration options for your tenant. Or you can **Continue** and set up a sample app. We recommend setting up the sample app, so that you can use it to test any further configuration changes you make

    ![Screenshot that shows the successful creation of the sign-up experience.](media/quickstart-get-started-guide/successful-trial-setup.png)

## Set up a sample app

The get started guide will automatically configure sample apps for the following app types and languages:

- Single Page Application (SPA): JavaScript, React, Angular
- Web app: Node.js (Express), ASP.NET Core
- Desktop app: .NET (MAUI)
- Mobile app: .NET (MAUI)

Follow the next steps, to download and run the sample app.

1. Proceed to set up the sample app by selecting the app type.
2. Select your language and **Download sample app** on your machine.
3. Follow the instructions to install and run the app. Sign into the sample app.

    ![Screenshot of the sample app setup.](media/quickstart-get-started-guide/sample-app-setup.png)
4. You've completed the process of creating a trial tenant, configuring the sign-in experience, creating your first user, and setting up a sample app. Select **Continue** to go to the summary page, where you can either go to the admin center or you can restart the guide to choose different options.

Note

The next time you return to your tenant, you might be prompted to set up additional authentication factors for added security of your tenant admin account.

## Explore Microsoft Entra External ID

Explore the features set up by the get started guide in the detailed article on the [get started guide features](/en-us/entra/external-id/customers/concept-guide-explained). You can always come back to the [admin center](https://entra.microsoft.com/) to customize your tenant and try the full range of configuration options for your tenant. For the latest developer content and resources, see the [External ID developer center](https://aka.ms/ciam/dev).