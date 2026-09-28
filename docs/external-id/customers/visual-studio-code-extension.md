---
layout: Conceptual
title: Visual Studio Code extension for External ID - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/visual-studio-code-extension
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to use the Microsoft Entra External ID extension for Visual Studio Code. Use the application samples provided to set up a customized, branded sign-in experience for external users of your application without leaving the development environment.
ms.topic: quickstart
ms.date: 2024-09-16T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: dd8131b2-2198-2530-c667-235eb2027804
document_version_independent_id: dd8131b2-2198-2530-c667-235eb2027804
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/visual-studio-code-extension.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/visual-studio-code-extension
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/visual-studio-code-extension.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/911a44a7-2f6c-477c-810f-dc8b7d425cce
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/14f2b9d5-6f06-45a8-ac5f-313eaa351153
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 61ab8f3b-ac37-83ae-4704-62eaf9f48c5b
---

# Visual Studio Code extension for External ID - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Integrating authentication into your consumer and business customer applications is essential for securing resources and customer data. The Microsoft Entra External ID extension for Visual Studio Code lets you quickly create external tenants, configure sign-in experiences for external users, and set up an External ID sample, all directly within Visual Studio Code. Using the extension walkthrough, you can learn how to set up a customized, branded sign-in experience for external users of your application and bootstrap your projects with preconfigured sample applications.

![Screenshot showing an overview of the extension.](media/visual-studio-code-extension/extension-overview.png)

This extension provides a basic setup that automatically creates a tenant for applications and prepares it for users. It also streamlines your workflow by automatically populating values such as application IDs into your configuration file for a smoother setup process.

## Install the extension

The Microsoft Entra External ID extension is available in the Visual Studio Code Marketplace.

1. If you don’t already have Visual Studio Code installed, [download Visual Studio Code](https://code.visualstudio.com/Download) and complete the installation steps.
2. Install the Microsoft Entra External ID Extension for Visual Studio Code from https://aka.ms/vscodequickstart/marketplace.

After the extension is installed, you can access it using the icon on the activity bar.

![Screenshot showing the open extension walkthrough options.](media/visual-studio-code-extension/open-extension-walkthrough.png)

You can also open the extension from Visual Studio Code **Welcome** page: Select **Help** &gt; **Welcome**, and then under **Walkthroughs**, select **Get started with Microsoft Entra External ID**. You might need to select **More…** to expand the list of extensions.

## Get started with your External ID setup

The Microsoft Entra External ID extension creates a tenant in an external configuration, which contains your app and directory of external users. You can add this new tenant to your existing Azure subscription.

- On the Get Started with Microsoft Entra External ID welcome page, choose an option:

    - If you don't already have an Azure Account, select **Set up a free trial**.
    - If you already have an Azure account, select **Use my subscription**.

    ![Screenshot of the get started options.](media/visual-studio-code-extension/get-started-step.png)

### Set up a free trial (preview)

1. Select **Set up a free trial**.
2. In the sign-in confirmation message, select **Allow**.
3. A new browser window opens. Sign in using your personal account, Microsoft account (MSA), or GitHub account. Once you’re signed in, close the browser window.
4. Return to Visual Studio Code. In the **Where should the tenant be located?** menu, select a location for your tenant data. This selection can't be changed later.
5. Enter a unique name for the tenant.

    ![Screenshot of the tenant name field.](media/visual-studio-code-extension/name-tenant.png)
6. The extension creates your trial tenant. You can view the progress by opening the **View** &gt; **Output** window. When the process is complete, **The tenant is created** appears.

### Use your subscription

1. Select **Use my subscription**.
2. If there are multiple tenants associated with your account, the **Choose a directory** menu appears. Select the directory (tenant) associated with the subscription you want to use.

    ![Screenshot of the directory field.](media/visual-studio-code-extension/choose-directory.png)

    Note

    If the message **No subscriptions available** appears, you can set up a free trial instead.
3. A browser page opens where you can sign in to your account. After you sign in, return to Visual Studio Code.
4. In the **Add a subscription** menu, select your subscription.
5. In the **Select a resource group** menu, choose a resource group.
6. In the **Where should the tenant be located?** menu, select a location for your tenant data. This selection can't be changed later.
7. Enter a name for the tenant, and then select **Enter** to create the tenant.

    ![Screenshot of the trial tenant name field.](media/visual-studio-code-extension/name-tenant.png)

    Note

    The tenant creation process can take up to 30 minutes. Once the tenant is created, you can access it in both the Microsoft Entra admin center and the Azure portal.

## Set up sign-in for your users

You can configure your app to allow users to sign in with their email and a password or a one-time passcode. You can also design the look and feel of the user experience by adding your company logo, changing the background color, or adjusting the sign-in layout. These changes apply to the look and feel of all your apps in this new tenant.

1. Under **Set up sign-in for your users**, select **Set up sign-in and branding**.

    ![Screenshot showing the set up sign-in and branding step.](media/visual-studio-code-extension/set-up-sign-in-step.png)
2. You’re prompted to sign in to the new tenant. Select **Allow**, and in the browser window that opens, choose the account you’re currently using and sign in. Return to Visual Studio Code.
3. In the **How would you like your users to sign in?** menu at the top, choose the sign-in method you want to make available to your users: **Email and password** or **Email and one-time passcode**.

    ![Screenshot showing sign-in methods.](media/visual-studio-code-extension/select-sign-in-method.png)
4. Select **OK**.
5. Choose where you want the sign-in page to appear in the browser window, either **Center-aligned** or **Right-aligned**.

    ![Screenshot showing the sign-in layout selections.](media/visual-studio-code-extension/select-alignment.png)
6. Select a background color for your sign-up page.

    ![Screenshot showing background colors.](media/visual-studio-code-extension/select-background.png)
7. Next, a File Explorer window opens so you can add your company logo. Browse to your company logo file, and then select **Upload**.

    Note

    Image requirements are as follows:

    - Image size 245 x 36 px
    - Maximum file size 50 KB
    - File type: Transparent PNG or JPEG
8. The message **Configuring sign-in flow** appears. You can view the progress in the Output window. When configuration is finished, the message **User flow setup is complete** appears.

## Try out your sign-in experience

The **Try out your sign-in experience** step in the walkthrough allows you to preview the sign-in experience you configured.

![Screenshot of option to try out your sign-in experience.](media/visual-studio-code-extension/try-out.png)

1. Select the **Run it now** button. A new browser tab opens with the sign-up page for your tenant that can be used to create and sign in users.
2. Select **No account? Create one** to create a new user in the tenant.
3. Add your new user's email address and select **Next**.

Note

Use a different email address than the one used to create your trial. If you use your tenant admin email to create a customer account through [self-service sign-up](/en-us/entra/external-id/self-service-sign-up-overview) or by [adding a new external user](/en-us/entra/external-id/customers/how-to-manage-customer-accounts#create-a-customer-account) in the Microsoft Entra admin center, the system creates a second account with the same email address. This new account has customer-level privileges, which can cause conflicts.

1. Complete the sign-up steps on the screen. Typically, once the user signs in, they're redirected back to your app. However, since you haven’t set up an app at this step, you're redirected to JWT.ms instead, where you can view the contents of the token issued during the sign-in process.

To find the user you created during this step, you can go to the [Microsoft Entra admin center](https://entra.microsoft.com/) and look for the user in the users list.

## Set up and run a sample app

The extension contains several code samples that demonstrate how authentication is implemented in different application types and development languages. Samples are included for single page apps (JavaScript, React, Angular) and web apps [Node.js (Express), ASP.NET Core, Python Django, Python Flask, Java Servlet]. Choose a sample from within the extension, and the extension automatically configures the application with your sign-in experience.

1. Under **Set up and run a sample app**, select the **Set up sample app** button.

    ![Screenshot of the Set up and run a sample app step.](media/visual-studio-code-extension/set-up-sample-app.png)
2. In the menu, select the type of app you want to download. If you're prompted to select your account again, choose the same account you’ve been using.

    ![Screenshot of the app selection.](media/visual-studio-code-extension/select-app-type.png)
3. A File Explorer window opens so you can choose where you want to save the sample repository. Select a folder, and then select **Download repository here**.
4. When the download completes, a new Visual Studio Code project workspace opens with the downloaded app folder displayed in the Explorer.
5. Open a new terminal in the Visual Studio Code window.
6. In the top menu, select **Run** &gt; **Run without debugging**. The Debug Console shows the launch script progress. There's a short delay while the project is set up and the build script runs.

When the extension downloads the application, it automatically updates the Microsoft Authentication Library (MSAL) configuration to connect to your new tenant and to use the experience you set up. No further configuration is needed; you can run the application as soon as the project is built. For example in the authConfig file, the **clientId** is set to your application ID and the **authority** is set to the subdomain for your new tenant.

![Screenshot of an auth-config file.](media/visual-studio-code-extension/auth-config-file.png)

## Run the experience

After setup is complete, try out the sign-in experience by entering the local host redirect URI for the application in a browser. The redirect URL is available in the application’s README.md file.

## Use the Explorer view

The Explorer view displays **Manage resources**, **Getting started** and **Help and Feedback** sections. To open the Explorer view, select the extension icon visible in the activity bar of Visual Studio Code.

## Manage resources

In the **Manage resources** section, you can view and manage your external tenants, registered applications, user flows, and company branding. To view project resources, expand the nodes in the left panel under **Manage Resources**.

![Screenshot of the explorer view.](media/visual-studio-code-extension/explorer-manage-resources.png)

In the **Manage resources** section, you can select a resource and go directly to the Microsoft Entra admin center to manage or configure it. For example, right-click an application and select **Open in admin center**. You’re prompted to sign in, and then the Microsoft Entra admin center opens directly to the app registration page for that application.

![Screenshot of the open in admin center option.](media/visual-studio-code-extension/explorer-open-admin-center.png)

## Getting Started actions

In the Getting Started section, you can access documentation for the free trial, or go directly to the sign-in experience configuration or sample app download pages without opening the extension walkthrough.

![Screenshot of the left menu option for starting the walkthrough.](media/visual-studio-code-extension/left-menu-configure-sign-in.png)