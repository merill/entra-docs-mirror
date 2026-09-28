---
layout: Conceptual
title: Configure Clear Review for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/clearreview-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Clear Review.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4d1d497f-d4ae-0dd7-cf09-2d875fd90d57
document_version_independent_id: 0a4aa291-d9f3-c131-fd3c-692801ae9658
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/clearreview-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/clearreview-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/clearreview-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 51d6598f-ec0f-72bd-eaca-82bf5bfcac96
---

# Configure Clear Review for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Clear Review with Microsoft Entra ID. When you integrate Clear Review with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Clear Review.
- Enable your users to be automatically signed-in to Clear Review with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Clear Review is available in the following [national cloud deployments](/en-us/graph/deployments).

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

- Clear Review single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Clear Review supports **SP and IDP** initiated SSO.

## Add Clear Review from the gallery

To configure the integration of Clear Review into Microsoft Entra ID, you need to add Clear Review from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Clear Review** in the search box.
4. Select **Clear Review** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Clear Review

Configure and test Microsoft Entra SSO with Clear Review using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Clear Review.

To configure and test Microsoft Entra SSO with Clear Review, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Clear Review SSO**- to configure the single sign-on settings on application side.
    1. **Create Clear Review test user** - to have a counterpart of B.Simon in Clear Review that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Clear Review** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<CUSTOMER_NAME>.clearreview.com/sso/metadata/`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<CUSTOMER_NAME>.clearreview.com/sso/acs/`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<CUSTOMER_NAME>.clearreview.com`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [Clear Review Client support team](https://clearreview.com/contact/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. Clear Review application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes, whereas **nameidentifier** is mapped with **user.userprincipalname**. Clear Review application expects **nameidentifier** to be mapped with **user.mail**, so you need to edit the attribute mapping by selecting **Edit** icon and change the attribute mapping.

    ![Screenshot shows User Attributes with the Edit icon selected.](common/edit-attribute.png)
8. On the **User Attributes & Claims** dialog, perform the following steps:

    a. Select **Edit icon** on the right of **Name identifier value**.

    ![Screenshot shows User Attributes &amp; Claims with the Edit icon selected.](media/clearreview-tutorial/attribute-2.png)

    ![Screenshot shows the Manage user claims dialog box where you can enter the values described.](media/clearreview-tutorial/attribute-1.png)

    b. From the **Source attribute** list, select the **user.mail** attribute value for that row.

    c. Select **Save**.
9. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
10. On the **Set up Clear Review** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Clear Review SSO

1. To configure single sign-on on **Clear Review** side, open the **Clear Review** portal with admin credentials.
2. Select **Admin** from the left navigation.

    ![Screenshot shows the Clear Review portal with Admin selected.](media/clearreview-tutorial/admin.png)
3. In the **Integrations** section at the bottom of the page select the **Change** button to the right of **Single Sign-On Settings**.

    ![Screenshot shows the Single Sign-On Change button.](media/clearreview-tutorial/integrations.png)
4. Perform following steps on **Single Sign-On Settings** page.

    ![Screenshot shows the Single Sign-On Settings page where you can enter the information in this step.](media/clearreview-tutorial/settings.png)

    a. In the **Issuer URL** textbox, paste the value of **Microsoft Entra Identifier**..

    b. In the **SAML Endpoint** textbox, paste the value of **Login URL**..

    c. In the **SLO Endpoint** textbox, paste the value of **Logout URL**..

    d. Open the downloaded certificate in notepad and paste the content in the **X.509 Certificate** textbox.

    e. Select **Save**.

### Create Clear Review test user

In this section, you create a user called Britta Simon in Clear Review. Please work with [Clear Review support team](https://clearreview.com/contact/) to add the users in the Clear Review platform.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Clear Review Sign on URL where you can initiate the login flow.
- Go to Clear Review Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Clear Review for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Clear Review tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Clear Review for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).