---
layout: Conceptual
title: Configure Leapsome for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/leapsome-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Leapsome.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: c642b37e-d912-65ec-3543-2cbe561171ce
document_version_independent_id: 52398212-e72e-5418-1268-b222db465358
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/leapsome-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/leapsome-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/leapsome-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1b265458-c8be-7e85-a4b4-5f9c227d6692
---

# Configure Leapsome for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Leapsome with Microsoft Entra ID. When you integrate Leapsome with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Leapsome.
- Enable your users to be automatically signed-in to Leapsome with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Leapsome single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Leapsome supports **SP and IDP** initiated SSO.
- Leapsome supports [Automated user provisioning](leapsome-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Leapsome from the gallery

To configure the integration of Leapsome into Microsoft Entra ID, you need to add Leapsome from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Leapsome** in the search box.
4. Select **Leapsome** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Leapsome

Configure and test Microsoft Entra SSO with Leapsome using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Leapsome.

To configure and test Microsoft Entra SSO with Leapsome, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Leapsome SSO**- to configure the single sign-on settings on application side.
    1. **Create Leapsome test user** - to have a counterpart of B.Simon in Leapsome that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Leapsome** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type the URL: `https://www.leapsome.com`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://www.leapsome.com/api/users/auth/saml/<CLIENTID>/assert`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://www.leapsome.com/api/users/auth/saml/<CLIENTID>/login`

    Note

    The preceding Reply URL and Sign-on URL value isn't real value. You update these with the actual values, which is explained later in the article.
7. Leapsome application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, Leapsome application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute | Namespace |
    | --- | --- | --- |
    | firstname | user.givenname | https://schemas.xmlsoap.org/ws/2005/05/identity/claims |
    | lastname | user.surname | https://schemas.xmlsoap.org/ws/2005/05/identity/claims |
    | title | user.jobtitle | https://schemas.xmlsoap.org/ws/2005/05/identity/claims |
    | picture | URL to the employee's picture | https://schemas.xmlsoap.org/ws/2005/05/identity/claims |
    |  |  |  |

    Note

    The value of picture attribute isn't real. Update this value with actual picture URL. To get this value contact [Leapsome Client support team](mailto:support@leapsome.com).
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
10. On the **Set up Leapsome** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Leapsome SSO

1. In a different web browser window, sign in to Leapsome as a Security Administrator.
2. On the top right, Select Settings logo and then select **Admin Settings**.

    ![Leapsome set](media/leapsome-tutorial/admin.png)
3. On the left menu bar select **Single Sign On (SSO)**, and on the **SAML-based single sign-on (SSO)** page perform the following steps:

    ![Leapsome saml](media/leapsome-tutorial/settings.png)

    a. Select **Enable SAML-based single sign-on**.

    b. Copy the **Login URL (point your users here to start login)** value and paste it into the **Sign-on URL** textbox in **Basic SAML Configuration** section.

    c. Copy the **Reply URL (receives response from your identity provider)** value and paste it into the **Reply URL** textbox in **Basic SAML Configuration** section.

    d. In the **SSO Login URL (provided by identity provider)** textbox, paste the value of **Login URL**, which you copied.

    e. Copy the Certificate that you have downloaded from Azure portal without `--BEGIN CERTIFICATE and END CERTIFICATE--` comments and paste it in the **Certificate (provided by identity provider)** textbox.

    f. Select **UPDATE SSO SETTINGS**.

### Create Leapsome test user

In this section, you create a user called Britta Simon in Leapsome. Work with [Leapsome Client support team](mailto:support@leapsome.com) to add the users or the domain that must be added to an allow list for the Leapsome platform. If the domain is added by the team, users get automatically provisioned to the Leapsome platform. Users must be created and activated before you use single sign-on.

Leapsome also supports automatic user provisioning, you can find more details [here](leapsome-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Leapsome Sign on URL where you can initiate the login flow.
- Go to Leapsome Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Leapsome for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Leapsome tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Leapsome for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).