---
layout: Conceptual
title: Configure LearnUpon for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/learnupon-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and LearnUpon.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: dbcbc01a-98c6-33f7-88f2-283737a955f2
document_version_independent_id: f619e0c8-b70f-02ff-ee24-9e7b8acc5659
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/learnupon-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/learnupon-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/learnupon-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f351aa51-3af4-5422-a180-4ab0351e65a6
---

# Configure LearnUpon for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate LearnUpon with Microsoft Entra ID. When you integrate LearnUpon with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to LearnUpon.
- Enable your users to be automatically signed-in to LearnUpon with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- LearnUpon single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- LearnUpon supports **IDP** initiated SSO.
- LearnUpon supports **Just In Time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add LearnUpon from the gallery

To configure the integration of LearnUpon into Microsoft Entra ID, you need to add LearnUpon from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **LearnUpon** in the search box.
4. Select **LearnUpon** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for LearnUpon

Configure and test Microsoft Entra SSO with LearnUpon using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in LearnUpon.

To configure and test Microsoft Entra SSO with LearnUpon, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure LearnUpon SSO**- to configure the single sign-on settings on application side.
    1. **Create LearnUpon test user** - to have a counterpart of B.Simon in LearnUpon that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **LearnUpon** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    In the **Reply URL** text box, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`

    Note

    The value isn't real. Update the value with the actual Reply URL. Contact [LearnUpon Client support team](https://www.learnupon.com/contact/) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, locate the **THUMBPRINT** - This are added to your LearnUpon SAML Settings.

    ![The Certificate download link](common/certificateraw.png)
7. On the **Set up LearnUpon** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure LearnUpon SSO

1. Open another browser instance and sign in into LearnUpon with an administrator account.
2. Select the **settings** tab.

    ![Screenshot shows the settings tab.](media/learnupon-tutorial/settings.png)
3. Select **Single Sign On - SAML**, and then select **General Settings** to configure SAML settings.

    ![Screenshot shows Single Sign On - SAML selected with General Settings selected.](media/learnupon-tutorial/general-settings.png)
4. In the **General Settings** section, perform the following steps:

    ![Screenshot shows the General Settings section where you can enter the values described.](media/learnupon-tutorial/values.png)

    a. Select **Enabled**.

    b. Select **Version** as **2.0**.

    c. Select **Skip conditions** as **No**.

    d. In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.

    e. In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`.

    f. In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they select your uploaded icon from your Azure portal login screen.

    g. In the **Sign out URL** textbox, paste the **Logout URL** value, which you copied previously.

    h. Select **Manage finger prints**, and then upload the finger print of your downloaded certificate.
5. Select **User Settings**, and then perform the following steps:

    ![Screenshot shows the User Settings section where you can enter the values described.](media/learnupon-tutorial/user-settings.png)

    a. In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.

    b. In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.

### Create LearnUpon test user

In this section, a user called Britta Simon is created in LearnUpon. LearnUpon supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in LearnUpon, a new one is created after authentication. If you need to create a user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/contact/).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the LearnUpon for which you set up the SSO.
- You can use Microsoft My Apps. When you select the LearnUpon tile in the My Apps, you should be automatically signed in to the LearnUpon for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).