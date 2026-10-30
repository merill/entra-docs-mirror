---
layout: Conceptual
title: Configure NAVEX IRM (Lockpath/Keylight) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/navex-irm-keylight-lockpath-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and NAVEX IRM (Lockpath/Keylight).
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: e3c865f2-2b0b-71ab-c7ce-e5cb6e68f1b1
document_version_independent_id: 249972b7-cbe4-7c7c-9eb1-de4fd0bbcf38
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/navex-irm-keylight-lockpath-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/navex-irm-keylight-lockpath-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/navex-irm-keylight-lockpath-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: bb7b405e-4a8f-b454-80d5-fbe94a61f549
---

# Configure NAVEX IRM (Lockpath/Keylight) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate NAVEX IRM (Lockpath/Keylight) with Microsoft Entra ID. When you integrate NAVEX IRM (Lockpath/Keylight) with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to NAVEX IRM (Lockpath/Keylight).
- Enable your users to be automatically signed-in to NAVEX IRM (Lockpath/Keylight) with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- NAVEX IRM (Lockpath/Keylight) single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- NAVEX IRM (Lockpath/Keylight) supports **SP** initiated SSO.
- NAVEX IRM (Lockpath/Keylight) supports **Just In Time** user provisioning.

## Add NAVEX IRM (Lockpath/Keylight) from the gallery

To configure the integration of NAVEX IRM (Lockpath/Keylight) into Microsoft Entra ID, you need to add NAVEX IRM (Lockpath/Keylight) from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **NAVEX IRM (Lockpath/Keylight)** in the search box.
4. Select **NAVEX IRM (Lockpath/Keylight)** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for NAVEX IRM (Lockpath/Keylight)

Configure and test Microsoft Entra SSO with NAVEX IRM (Lockpath/Keylight) using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in NAVEX IRM (Lockpath/Keylight).

To configure and test Microsoft Entra SSO with NAVEX IRM (Lockpath/Keylight), perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure NAVEX IRM (Lockpath/Keylight) SSO**- to configure the single sign-on settings on application side.
    1. **Create NAVEX IRM (Lockpath/Keylight) test user** - to have a counterpart of B.Simon in NAVEX IRM (Lockpath/Keylight) that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

In this section, you enable Microsoft Entra single sign-on.

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **NAVEX IRM (Lockpath/Keylight)** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<COMPANY_NAME>.keylightgrc.com`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://<COMPANY_NAME>.keylightgrc.com/Login.aspx`

    c. In the **Sign on URL** text box, type a URL using the following pattern: `https://<COMPANY_NAME>.keylightgrc.com/`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [NAVEX IRM (Lockpath/Keylight) Client support team](https://www.lockpath.com/contact/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Raw)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificateraw.png)
7. On the **Set up NAVEX IRM (Lockpath/Keylight)** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure NAVEX IRM (Lockpath/Keylight) SSO

1. To enable SSO in NAVEX IRM (Lockpath/Keylight), perform the following steps:

    a. Sign on to your NAVEX IRM (Lockpath/Keylight) account as administrator.

    b. In the menu on the top, select **User Icon**, and select **Setup**.

    ![Screenshot that shows the &quot;Person&quot; icon selected, and &quot;Keylight Setup&quot; selected from the drop-down.](media/keylight-tutorial/setup-icon.png)

    c. In the treeview on the left, select **SAML**.

    ![Screenshot that shows &quot;S A M L&quot; selected in the tree view.](media/keylight-tutorial/tree-view.png)

    d. On the **SAML Settings** dialog, select **Edit**.

    ![Screenshot that shows the &quot;S A M L Settings&quot; window with the &quot;Edit&quot; button selected.](media/keylight-tutorial/edit-icon.png)
2. On the **Edit SAML Settings** dialog page, perform the following steps:

    ![Configure Single Sign-On](media/keylight-tutorial/settings.png)

    a. Set **SAML authentication** to **Active**.

    b. In the **Identity Provider Login URL** textbox, paste the **Login URL** value which you copied previously.

    c. In the **Identity Provider Logout URL** textbox, paste the **Logout URL** value which you copied previously.

    d. Select **Choose File** to select your downloaded NAVEX IRM (Lockpath/Keylight) certificate, and then select **Open** to upload the certificate.

    e. Set **SAML User Id location** to **NameIdentifier element of the subject statement**.

    f. Provide the **Service Provider Entity Id** using the following pattern: `https://<CompanyName>.keylightgrc.com`.

    g. Set **Auto-provision users** to **Active**.

    h. Set **Auto-provision account type** to **Full User**.

    i. Set **Auto-provision security role**, select **Standard User with SAML**.

    j. Set **Auto-provision security config**, select **Standard User Configuration**.

    k. In the **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    l. In the **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.

    m. In the **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.

    n. Select **Save**.

### Create NAVEX IRM (Lockpath/Keylight) test user

In this section, a user called Britta Simon is created in NAVEX IRM (Lockpath/Keylight). NAVEX IRM (Lockpath/Keylight) supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in NAVEX IRM (Lockpath/Keylight), a new one is created after authentication. If you need to create a user manually, you need to contact the [NAVEX IRM (Lockpath/Keylight) Customer support team](https://www.lockpath.com/contact/).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to NAVEX IRM (Lockpath/Keylight) Sign-on URL where you can initiate the login flow.
- Go to NAVEX IRM (Lockpath/Keylight) Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the NAVEX IRM (Lockpath/Keylight) tile in the My Apps, this option redirects to NAVEX IRM (Lockpath/Keylight) Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).