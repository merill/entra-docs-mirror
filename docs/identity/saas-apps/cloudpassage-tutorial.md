---
layout: Conceptual
title: Configure CloudPassage for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/cloudpassage-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and CloudPassage.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 31376c24-e684-659f-4cdf-9e77b4f57f76
document_version_independent_id: 5ce7deea-916d-0ea6-01a1-656e6d95b44c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/cloudpassage-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/cloudpassage-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/cloudpassage-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f58a77fb-4dd7-f8e2-2ff2-ce53d12c9c5b
---

# Configure CloudPassage for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate CloudPassage with Microsoft Entra ID. When you integrate CloudPassage with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to CloudPassage.
- Enable your users to be automatically signed in to CloudPassage with their Microsoft Entra accounts.
- Manage your accounts in one central location.

To learn more about SaaS app integration with Microsoft Entra ID, see [What is application access and single sign-on with Microsoft Entra ID](../enterprise-apps/what-is-single-sign-on).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- CloudPassage single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- CloudPassage supports **SP** initiated SSO

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Adding CloudPassage from the gallery

To configure the integration of CloudPassage into Microsoft Entra ID, you need to add CloudPassage from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **CloudPassage** in the search box.
4. Select **CloudPassage** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra single sign-on for CloudPassage

Configure and test Microsoft Entra SSO with CloudPassage using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in CloudPassage.

To configure and test Microsoft Entra SSO with CloudPassage, complete the following building blocks:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure CloudPassage SSO**- to configure the single sign-on settings on application side.
    1. **Create CloudPassage test user** - to have a counterpart of B.Simon in CloudPassage that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **CloudPassage** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Sign-on URL** text box, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`. You can get your value for this attribute by selecting **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.

    ![Screenshot shows the CloudPassage portal with the S S O Setup Documentation link called out.](media/cloudpassage-tutorial/tutorial_cloudpassage_05.png)

    Note

    These values aren't real. Update these values with the actual Sign-On URL and Reply URL. Contact [CloudPassage Client support team](https://fidelissecurity.com/contact/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/edit-attribute.png)
7. In addition to above, CloudPassage application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirement.

    | Name | Source Attribute |
    | --- | --- |
    | firstname | user.givenname |
    | lastname | user.surname |
    | email | user.mail |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. On the **Set up CloudPassage** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure CloudPassage SSO

1. In a different browser window, sign-on to your CloudPassage company site as administrator.
2. In the menu on the top, select **Settings**, and then select **Site Administration**.

    ![Screenshot shows the CloudPassage site with Site Administration selected.](media/cloudpassage-tutorial/tutorial_cloudpassage_07.png)
3. Select the **Authentication Settings** tab.

    ![Screenshot shows the CloudPassage site with the Authentication Settings tab selected.](media/cloudpassage-tutorial/tutorial_cloudpassage_08.png)
4. In the **Single Sign-on Settings** section, perform the following steps:

    ![Screenshot shows the Single Sign-on Settings section where you can enter the information in this step.](media/cloudpassage-tutorial/tutorial_cloudpassage_09.png)

    a. Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.

    b. Paste **Microsoft Entra Identifier** into the **SAML issuer URL** textbox.

    c. Paste **Login URL** into the **SAML endpoint URL** textbox.

    d. Paste **Logout URL** into the **Logout landing page** textbox.

    e. Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.

    f. Select **Save**.

### Create CloudPassage test user

The objective of this section is to create a user called B.Simon in CloudPassage.

**To create a user called B.Simon in CloudPassage, perform the following steps:**

1. Sign-on to your **CloudPassage** company site as an administrator.
2. In the toolbar on the top, select **Settings**, and then select **Site Administration**.

    ![Screenshot shows CloudPassage with Site Administration selected.](media/cloudpassage-tutorial/tutorial_cloudpassage_15.png)
3. Select the **Users** tab, and then select **Add New User**.

    ![Screenshot shows CloudPassage Site Administration with the Users tab selected and the option to Add New User.](media/cloudpassage-tutorial/tutorial_cloudpassage_16.png)
4. In the **Add New User** section, perform the following steps:

    ![Screenshot shows the Add New User section where you can specify user information.](media/cloudpassage-tutorial/tutorial_cloudpassage_17.png)

    a. In the **First Name** textbox, type Britta.

    b. In the **Last Name** textbox, type Simon.

    c. In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Microsoft Entra ID.

    d. As **Access Type**, select **Enable Halo Portal Access**.

    e. Select **Add**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration using the Access Panel.

When you select the CloudPassage tile in the Access Panel, you should be automatically signed in to the CloudPassage for which you set up SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).