---
layout: Conceptual
title: Configure Fluxx Labs for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/fluxxlabs-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to configure single sign-on between Microsoft Entra ID and Fluxx Labs.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: da89d478-1b3e-82ab-127b-75be7ff89642
document_version_independent_id: 06468160-e8a1-2724-9c3d-56335329b32d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/fluxxlabs-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/fluxxlabs-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/fluxxlabs-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f32f9e97-8831-9332-14d6-1e63d9f1efaf
---

# Configure Fluxx Labs for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Fluxx Labs with Microsoft Entra ID. When you integrate Fluxx Labs with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Fluxx Labs.
- Enable your users to be automatically signed-in to Fluxx Labs with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Fluxx Labs single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Fluxx Labs supports **IDP** initiated SSO.

## Add Fluxx Labs from the gallery

To configure the integration of Fluxx Labs into Microsoft Entra ID, you need to add Fluxx Labs from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Fluxx Labs** in the search box.
4. Select **Fluxx Labs** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Fluxx Labs

Configure and test Microsoft Entra SSO with Fluxx Labs using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Fluxx Labs.

To configure and test Microsoft Entra SSO with Fluxx Labs, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Fluxx Labs SSO**- to configure the single sign-on settings on application side.
    1. **Create Fluxx Labs test user** - to have a counterpart of B.Simon in Fluxx Labs that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Fluxx Labs** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Set up Single Sign-On with SAML** page, perform the following steps:

    a. In the **Identifier** text box, type a URL using one of the following patterns:

    | Environment | URL Pattern |
    | --- | --- |
    | Production | `https://<subdomain>.fluxx.io` |
    | Pre production | `https://<subdomain>.preprod.fluxxlabs.com` |

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    | Environment | URL Pattern |
    | --- | --- |
    | Production | `https://<subdomain>.fluxx.io/auth/saml/callback` |
    | Pre production | `https://<subdomain>.preprod.fluxxlabs.com/auth/saml/callback` |

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [Fluxx Labs Client support team](https://fluxx.zendesk.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Fluxx Labs** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Fluxx Labs SSO

1. In a different web browser window, sign in to your Fluxx Labs company site as administrator.
2. Select **Admin** below the **Settings** section.

    ![Screenshot that shows the &quot;Settings&quot; section with &quot;Admin&quot; selected.](media/fluxxlabs-tutorial/configure-1.png)
3. In the Admin Panel, Select **Plug-ins** &gt; **Integrations** and then select **SAML SSO-(Disabled)**

    ![Screenshot that shows the &quot;Integrations&quot; tab with &quot;S A M L S S O- (Disabled) selected.](media/fluxxlabs-tutorial/configure-2.png)
4. In the attribute section, perform the following steps:

    ![Screenshot that shows the &quot;Attributes&quot; section with &quot;S A M L S S O&quot; checked, values entered in fields, and the &quot;Save&quot; button selected.](media/fluxxlabs-tutorial/configure-3.png)

    a. Select the **SAML SSO** checkbox.

    b. In the **Request Path** textbox, type **/auth/saml**.

    c. In the **Callback Path** textbox, type **/auth/saml/callback**.

    d. In the **Assertion Consumer Service Url(Single Sign-On URL)** textbox, enter the **Reply URL** value, which you have entered.

    e. In the **Audience(SP Entity ID)** textbox, enter the **Identifier** value, which you have entered.

    f. In the **Identity Provider SSO Target URL** textbox, paste the **Login URL** value, which you copied previously.

    g. Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.

    h. In **Name identifier Format** textbox, enter the value `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`.

    i. Select **Save**.

    Note

    Once the content saved, the field appears blank for security, but the value has been saved in the configuration.

### Create Fluxx Labs test user

To enable Microsoft Entra users to sign in to Fluxx Labs, they must be provisioned into Fluxx Labs. In the case of Fluxx Labs, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to your Fluxx Labs company site as an administrator.
2. Select the below displayed **icon**.

    ![Screenshot that shows administrator options with the &quot;Plus&quot; icon selected under &quot;Your Dashboard is Empty&quot;.](media/fluxxlabs-tutorial/configure-6.png)
3. On the dashboard, select the below displayed icon to open the **New PEOPLE** card.

    ![Screenshot that shows the &quot;Contact Management&quot; menu with the &quot;Plus&quot; icon next to &quot;People&quot; selected.](media/fluxxlabs-tutorial/configure-4.png)
4. On the **NEW PEOPLE** section, perform the following steps:

    ![Fluxx Labs Configuration](media/fluxxlabs-tutorial/configure-5.png)

    a. Fluxx Labs use email as the unique identifier for SSO logins. Populate the **SSO UID** field with the user’s email address, that matches the email address, which they are using as login with SSO.

    b. Select **Save**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Fluxx Labs for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Fluxx Labs tile in the My Apps, you should be automatically signed in to the Fluxx Labs for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).