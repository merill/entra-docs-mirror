---
layout: Conceptual
title: Configure Netskope Administrator Console for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/netskope-cloud-security-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Netskope Administrator Console.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: aa7c3473-a3ff-4660-e232-6c2d1ff259fb
document_version_independent_id: 33f36156-2502-d102-a294-ef31290adff5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/netskope-cloud-security-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/netskope-cloud-security-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/netskope-cloud-security-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 25e50e6a-38b4-a673-69f4-7407385ce212
---

# Configure Netskope Administrator Console for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Netskope Administrator Console with Microsoft Entra ID. When you integrate Netskope Administrator Console with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Netskope Administrator Console.
- Enable your users to be automatically signed-in to Netskope Administrator Console with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Netskope Administrator Console single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Netskope Administrator Console supports **SP and IDP** initiated SSO.
- Netskope Administrator Console supports just-in-time user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Netskope Administrator Console from the gallery

To configure the integration of Netskope Administrator Console into Microsoft Entra ID, you need to add Netskope Administrator Console from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Netskope Administrator Console** in the search box.
4. Select **Netskope Administrator Console** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Netskope Administrator Console

Configure and test Microsoft Entra SSO with Netskope Administrator Console using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Netskope Administrator Console.

To configure and test Microsoft Entra SSO with Netskope Administrator Console, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Netskope Administrator Console SSO**- to configure the single sign-on settings on application side.
    1. **Create Netskope Administrator Console test user** - to have a counterpart of B.Simon in Netskope Administrator Console that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Netskope Administrator Console** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following step:

    In the **Reply URL** text box, type a URL using the following pattern: `https://<tenant_host_name>/saml/acs`

    Note

    The value isn't real. Update the value with the actual Reply URL. You get the value explained later in the article.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<tenantname>.goskope.com`

    Note

    The Sign-on URL values isn't real. Update Sign-on URL value with the actual Sign-on URL. Contact [Netskope Administrator Console Client support team](mailto:support@netskope.com) to get Sign-on URL value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. Netskope Administrator Console application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, Netskope Administrator Console application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | admin-role | user.assignedroles |

    Note

    Select [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui) to know how to create roles in Microsoft Entra ID.
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
10. On the **Set up Netskope Administrator Console** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Netskope Administrator Console SSO

1. Open a new tab in your browser, and sign in to your Netskope Administrator Console company site as an administrator.
2. Select the **Settings** tab from the left navigation pane.

    ![Screenshot shows Setting selected in the navigation pane.](media/netskope-cloud-security-tutorial/configure-settings.png)
3. Select **Administration** tab.

    ![Screenshot shows Administration selected from Settings.](media/netskope-cloud-security-tutorial/administration.png)
4. Select **SSO** tab.

    ![Screenshot shows S S O selected in Administration.](media/netskope-cloud-security-tutorial/tab.png)
5. On the **Network Settings** section, perform the following steps:

    ![Screenshot shows Network Settings where you can enter the values described.](media/netskope-cloud-security-tutorial/network.png)

    a. Copy **Assertion Consumer Service URL** value and paste it into the **Reply URL** textbox in the **Basic SAML Configuration** section.

    b. Copy **Service Provider Entity ID** value and paste it into the **Identifier** textbox in the **Basic SAML Configuration** section.
6. Select the **EDIT SETTINGS** under the **SSO/SLO Settings** section.

    ![Screenshot shows S S O / S L O Settings where you can select EDIT SETTINGS.](media/netskope-cloud-security-tutorial/settings.png)
7. On the **Settings** pop-up window, perform the following steps;

    ![Screenshot shows the Settings dialog box where you can enter the values described.](media/netskope-cloud-security-tutorial/configuration.png)

    a. Select **Enable SSO**.

    b. In the **IDP URL** textbox, paste the **Login URL** value, which you copied previously.

    c. In the **IDP ENTITY ID** textbox, paste the **Microsoft Entra Identifier** value, which you copied previously.

    d. Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IDP CERTIFICATE** textbox.

    e. Select **Enable SSO**.

    f. In the **IDP SLO URL** textbox, paste the **Logout URL** value, which you copied previously.

    g. Select **SUBMIT**.

### Create Netskope Administrator Console test user

In this section, a user called B.Simon is created in Netskope Administrator Console. Netskope Administrator Console supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Netskope Administrator Console, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Netskope Administrator Console Sign on URL where you can initiate the login flow.
- Go to Netskope Administrator Console Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Netskope Administrator Console for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Netskope Administrator Console tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Netskope Administrator Console for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).