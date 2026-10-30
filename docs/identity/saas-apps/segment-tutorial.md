---
layout: Conceptual
title: Configure Segment for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/segment-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Segment.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 41e66989-5060-c931-9fff-5ba6825eeaf0
document_version_independent_id: ce38c0ea-904f-c221-c323-e55cc5ba2138
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/segment-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/segment-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/segment-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9d2ba9f3-8a03-b3ea-0875-3c1cec2fe732
---

# Configure Segment for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Segment with Microsoft Entra ID. When you integrate Segment with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Segment.
- Enable your users to be automatically signed-in to Segment with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Segment single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Segment supports **SP and IDP** initiated SSO.
- Segment supports **Just In Time** user provisioning.
- Segment supports [Automated user provisioning](segment-provisioning-tutorial).

## Add Segment from the gallery

To configure the integration of Segment into Microsoft Entra ID, you need to add Segment from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Segment** in the search box.
4. Select **Segment** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Segment

Configure and test Microsoft Entra SSO with Segment using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Segment.

To configure and test Microsoft Entra SSO with Segment, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Segment SSO**- to configure the single sign-on settings on application side.
    1. **Create Segment test user** - to have a counterpart of B.Simon in Segment that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Segment** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a value using the following pattern: `urn:auth0:segment-prod:samlp-<CUSTOMER_VALUE>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://segment-prod.auth0.com/login/callback?connection=<CUSTOMER_VALUE>`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://app.segment.com`

    Note

    These values are placeholders. You need to use the actual Identifier and Reply URL. Steps for getting these values are described later in this article.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up Segment** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Segment SSO

1. In a new web browser window, sign in to your Segment company site as an administrator.
2. Select **Settings Icon** and scroll down to **AUTHENTICATION** and select **Connections**.

    ![Screenshot that shows the &quot;Settings&quot; icon selected, and &quot;Connections&quot; selected from the &quot;Authentication&quot; menu.](media/segment-tutorial/connections.png)
3. Select **Add new Connection**.

    ![Screenshot that shows the &quot;Connections&quot; section with the &quot;Add new Connection&quot; button selected.](media/segment-tutorial/new-connections.png)
4. Select **SAML 2.0** as a connection to configure and select **Select Connection** button.

    ![Screenshot that shows the &quot;Choose a Connection&quot; section with &quot;S A M L 2.0&quot; and the &quot;Select Connection&quot; button selected.](media/segment-tutorial/select-connections.png)
5. On the following page, perform the following steps:

    ![Screenshot that shows the &quot;Configure Identity Provider&quot; page with the &quot;Single Sign-On U R L&quot; and &quot;Audience U R L&quot; text boxes highlighted, and the &quot;Next&quot; button selected.](media/segment-tutorial/configure.png)

    a. Copy the **Single Sign-On URL** value and paste it into the **Reply URL** box in the **Basic SAML Configuration** dialog box.

    b. Copy the **Audience URL** value and paste it into the **Identifier URL** box in the **Basic SAML Configuration** dialog box.

    c. Select **Next**.

    ![Segment Configuration](media/segment-tutorial/certificate.png)
6. In the **SAML 2.0 Endpoint URL** box, paste the **Login URL** value that you copied.
7. Open the downloaded **Certificate(Base64)** into Notepad and paste the content into the **Public Certificate** textbox.
8. Select **Configure Connection**.

### Create Segment test user

In this section, a user called B.Simon is created in Segment. Segment supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Segment, a new one is created after authentication.

Segment also supports automatic user provisioning, you can find more details [here](segment-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Segment Sign on URL where you can initiate the login flow.
- Go to Segment Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Segment for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Segment tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Segment for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).