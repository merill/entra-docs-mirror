---
layout: Conceptual
title: Create a User Flow - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-user-flow-sign-up-sign-in-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Add sign-up and sign-in user flows for your consumer and business customers. Create a branded, customized user experience for apps in your external tenant.
ms.topic: how-to
ms.date: 2025-09-16T00:00:00.0000000Z
ms.reviewer: kengaderdus
ms.custom: it-pro, seo-july-2024, sfi-image-nochange
locale: en-us
document_id: 1a5b75b2-1997-a166-40b6-243d0b1d8e66
document_version_independent_id: 53180cc2-558c-8861-6967-66de977ff8c4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-user-flow-sign-up-sign-in-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-user-flow-sign-up-sign-in-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-user-flow-sign-up-sign-in-customers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 28a36c1a-9663-b792-83ad-fd1d151af74a
---

# Create a User Flow - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Tip

User flows are created in the Microsoft Entra admin center the same way for both authentication approaches. The instructions in this article apply whether your app uses **browser-delegated authentication** (Microsoft-hosted sign-in pages) or **native authentication** (sign-in UI built into your app). How your app integrates with the user flow at runtime differs by approach. To learn more, see [Choose an authentication approach](concept-choose-authentication-approach).

You can create a simple sign-up and sign-in experience for your customers by adding a user flow to your application. The user flow defines the series of sign-up steps customers follow and the sign-in methods they can use (such as email and password, one-time passcodes, or social accounts from [Google](how-to-google-federation-customers), [Facebook](how-to-facebook-federation-customers), [Apple](how-to-apple-federation-customers)) or a custom [OIDC federation](how-to-custom-oidc-federation-customers). You can also collect information from customers during sign-up by selecting from a series of built-in user attributes or adding your own custom attributes.

This article describes how to create a sign-in and sign-up user flow. After you create the user flow, the next step is to [add your application to the user flow](how-to-user-flow-add-application). You can create multiple user flows if you have multiple applications that you want to offer to customers. Or, you can use the same user flow for many applications. However, an application can have only one user flow.

## Prerequisites

- **A Microsoft Entra external tenant**: Before you begin, create your Microsoft Entra external tenant. You can set up a [free trial](https://aka.ms/ciam-free-trial?wt.mc_id=ciamcustomertenantfreetrial_linkclick_content_cnl), or you can create a new external tenant in Microsoft Entra ID.
- **Email one-time passcode enabled (optional)**: If you want customers to use their email address and a one-time passcode each time they sign in, make sure Email one-time passcode is enabled at the tenant level (in the [Microsoft Entra admin center](https://entra.microsoft.com/), navigate to **External Identities** &gt; **All Identity Providers** &gt; **Email One-time-passcode**).
- **Custom attributes defined (optional)**: User attributes are values collected from the user during self-service sign-up. Microsoft Entra ID comes with a built-in set of attributes, but you can [define custom attributes to collect during sign-up](how-to-define-custom-attributes). Define custom attributes in advance so they're available when you set up your user flow. Or you can create and add them later.
- **Identity providers defined (optional)**: You can set up federation with [Google](how-to-google-federation-customers), [Facebook](how-to-facebook-federation-customers) or an [OIDC identity provider](how-to-custom-oidc-federation-customers) in advance, and then select them as sign-in options as you create the user flow.

## Create and customize a user flow

Follow these steps to create a user flow a customer can use to sign in or sign up for an application. These steps describe how to add a new user flow, select the attributes you want to collect, and change the order of the attributes on the sign-up page.

### To add a new user flow

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
4. Select **New user flow**.

    ![Screenshot of the new user flow option.](media/how-to-user-flow-sign-up-sign-in-customers/new-user-flow.png)
5. On the **Create** page, enter a **Name** for the user flow (for example, "SignUpSignIn").
6. Under **Identity providers**, select the **Email Accounts** check box, and then select one of these options:

    - **Email with password**: Allows new users to sign up and sign in using an email address as the sign-in name and a password as their first-factor authentication method. You can also configure options for showing, hiding, or customizing the self-service password reset link on the sign-in page ([learn more](how-to-customize-branding-customers#to-customize-self-service-password-reset)). If you plan to require multifactor authentication, this option lets you choose from email one-time passcodes, SMS text codes, or both as second-factor methods.
    - **Email one-time passcode**: Allows new users to sign up and sign in using an email address as the sign-in name and email one-time passcode as their first-factor authentication method. If you plan to require multifactor authentication, you can enable SMS text codes as a second-factor method.

    Note

    The **Microsoft Entra ID Sign up** option is unavailable because although customers can sign up for a local account using an email from another Microsoft Entra organization, Microsoft Entra federation isn't used to authenticate them. **[Google](how-to-google-federation-customers)** and **[Facebook](how-to-facebook-federation-customers)** become available only after you set up federation with them. [Learn more about authentication methods and identity providers](concept-authentication-methods-customers).

    ![Screenshot of Identity provider options on the Create a user flow page.](media/how-to-user-flow-sign-up-sign-in-customers/create-user-flow-identity-providers.png)
7. Under **User attributes**, choose the attributes you want to collect from the user during sign-up.

    [![Screenshot of the user attribute options on the Create a user flow page.](media/how-to-user-flow-sign-up-sign-in-customers/user-attributes.png)](media/how-to-user-flow-sign-up-sign-in-customers/user-attributes.png#lightbox)
8. Select **Show more** to choose from the full list of attributes, including **Job Title**, **Display Name**, and **Postal Code**.

    This list also includes any [custom attributes you defined](how-to-define-custom-attributes). Select the checkbox next to each attribute you want to collect from the user during sign-up

    [![Screenshot of the user attribute pane after selecting Show more.](media/how-to-user-flow-sign-up-sign-in-customers/user-attributes-show-more.png)](media/how-to-user-flow-sign-up-sign-in-customers/user-attributes-show-more.png#lightbox)
9. Select **OK**.
10. Select **Create** to create the user flow.

## Control the 'Stay signed in?' prompt

By default, after a customer signs in to an app that uses your user flow, they see a **Stay signed in?** prompt asking whether to stay signed in across browser sessions. If the user selects **Yes**, a persistent authentication cookie is issued and they remain signed in across browser sessions. If they select **No**, a non-persistent cookie is issued.

This prompt is the default behavior for every user flow. Applying custom branding to the user flow or requiring multifactor authentication doesn't change whether the prompt appears. It's shown in all cases unless you override it with a Conditional Access policy.

The prompt isn't a user flow setting. To change or suppress it, configure the **Persistent browser session** session control in a Conditional Access policy that targets your customers and apps:

- **Always persistent**: The browser session is always persisted. The **Stay signed in?** prompt isn't shown.
- **Never persistent**: The browser session ends when the browser is closed. The **Stay signed in?** prompt isn't shown.

For details about the session control and how to apply it, see [Conditional Access: Session - Persistent browser session](../../identity/conditional-access/concept-conditional-access-session#persistent-browser-session) and [Configure authentication session management](../../identity/conditional-access/concept-session-lifetime#persistence-of-browsing-sessions).