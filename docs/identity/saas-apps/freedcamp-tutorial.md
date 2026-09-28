---
layout: Conceptual
title: Configure Freedcamp for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/freedcamp-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Freedcamp.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 48daff15-f0f1-22e5-752b-faef6b94581d
document_version_independent_id: 2880049d-1f1b-9be8-49bf-9deacb17281c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/freedcamp-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/freedcamp-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/freedcamp-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7fd69c2a-61db-58b1-22f3-d34101ad2eef
---

# Configure Freedcamp for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Freedcamp with Microsoft Entra ID. When you integrate Freedcamp with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Freedcamp.
- Enable your users to be automatically signed-in to Freedcamp with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Freedcamp is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Freedcamp single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Freedcamp supports **SP and IDP** initiated SSO.

## Add Freedcamp from the gallery

To configure the integration of Freedcamp into Microsoft Entra ID, you need to add Freedcamp from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Freedcamp** in the search box.
4. Select **Freedcamp** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Freedcamp

Configure and test Microsoft Entra SSO with Freedcamp using a test user called **Britta Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Freedcamp.

To configure and test Microsoft Entra SSO with Freedcamp, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Freedcamp SSO**- to configure the single sign-on settings on application side.
    1. **Create Freedcamp test user** - to have a counterpart of B.Simon in Freedcamp that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Freedcamp** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    1. In the **Identifier** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.freedcamp.com/sso/<UNIQUEID>`
    2. In the **Reply URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.freedcamp.com/sso/acs/<UNIQUEID>`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.freedcamp.com/login`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Users can also enter the URL values with respect to their own customer domain and they may not be necessarily of the pattern `freedcamp.com`, they can enter any customer domain specific value, specific to their application instance. Also you can contact [Freedcamp Client support team](mailto:devops@freedcamp.com) for further information on URL patterns.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up Freedcamp** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Freedcamp SSO

1. In a different web browser window, sign in to your Freedcamp company site as an administrator
2. On the top-right corner of the page, select **profile** and then navigate to **My Account**.

    ![Screenshot that shows &quot;Profile&quot; and &quot;My Account&quot; selected.](media/freedcamp-tutorial/config01.png)
3. From the left side of the menu bar, select **SSO** and on the **Your SSO connections** page perform the following steps:

    ![Screenshot that shows &quot;S S O&quot; selected in the left-side menu bar and the &quot;Your S S O connections&quot; page with values entered and the &quot;Submit&quot; button selected.](media/freedcamp-tutorial/config02.png)

    a. In the **Title** text box, type the title.

    b. In the **Entity ID** text box, Paste the **Microsoft Entra Identifier** value, which you copied previously.

    c. In the **Login URL** text box, Paste the **Login URL** value, which you copied previously.

    d. Open the Base64 encoded certificate in notepad, copy its content and paste it into the **Certificate** text box.

    e. Select **Submit**.

### Create Freedcamp test user

To enable Microsoft Entra users, sign in to Freedcamp, they must be provisioned into Freedcamp. In Freedcamp, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. In a different web browser window, sign in to Freedcamp as a Security Administrator.
2. On the top-right corner of the page, select **profile** and then navigate to **Manage System**.

    ![Freedcamp configuration](media/freedcamp-tutorial/config03.png)
3. On the right side of the Manage System page, perform the following steps:

    ![Screenshot that shows the &quot;Add Or Invite Users&quot; button selected, the &quot;Email&quot; field highlighted, and the &quot;Add User&quot; button selected.](media/freedcamp-tutorial/config04.png)

    a. Select **Add or invite Users**.

    b. In the **Email** text box, enter the email of user like `Brittasimon@contoso.com`.

    c. Select **Add User**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Freedcamp Sign on URL where you can initiate the login flow.
- Go to Freedcamp Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Freedcamp for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Freedcamp tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Freedcamp for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).