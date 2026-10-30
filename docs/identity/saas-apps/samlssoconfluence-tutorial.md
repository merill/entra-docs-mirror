---
layout: Conceptual
title: Configure SAML SSO for Confluence by resolution GmbH for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/samlssoconfluence-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SAML SSO for Confluence by resolution GmbH.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: e46e65de-9443-80e9-954a-f82f87a8fa1e
document_version_independent_id: 5e7d2e96-93eb-4047-07a8-0654d2ca55c2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/samlssoconfluence-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/samlssoconfluence-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/samlssoconfluence-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d6c4a574-8c46-334d-d25e-3c8db3f89a34
---

# Configure SAML SSO for Confluence by resolution GmbH for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SAML SSO for Confluence by resolution GmbH with Microsoft Entra ID. When you integrate SAML SSO for Confluence by resolution GmbH with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SAML SSO for Confluence by resolution GmbH.
- Enable your users to be automatically signed-in to SAML SSO for Confluence by resolution GmbH with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SAML SSO for Confluence by resolution GmbH single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- SAML SSO for Confluence by resolution GmbH supports **SP and IDP** initiated SSO

## Add SAML SSO for Confluence by resolution GmbH from the gallery

To configure the integration of SAML SSO for Confluence by resolution GmbH into Microsoft Entra ID, you need to add SAML SSO for Confluence by resolution GmbH from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SAML SSO for Confluence by resolution GmbH** in the search box.
4. Select **SAML SSO for Confluence by resolution GmbH** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SAML SSO for Confluence by resolution GmbH

Configure and test Microsoft Entra SSO with SAML SSO for Confluence by resolution GmbH using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SAML SSO for Confluence by resolution GmbH.

To configure and test Microsoft Entra SSO with SAML SSO for Confluence by resolution GmbH, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SAML SSO for Confluence by resolution GmbH SSO**- to configure the Single Sign-On settings on application side.
    1. **Create SAML SSO for Confluence by resolution GmbH test user** - to have a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SAML SSO for Confluence by resolution GmbH** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SAML SSO for Confluence by resolution GmbH SSO

1. In a different web browser window, log in to your **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.
2. Hover on cog and select the **Add-ons**.

    ![Screenshot that shows the &quot;Cog&quot; icon selected, and &quot;Add-ons&quot; selected from the drop-down.](media/saml-sso-confluence-tutorial/add-on-1.png)
3. You're redirected to Administrator Access page. Enter the password and select **Confirm** button.

    ![Screenshot that shows the &quot;Administrator Access&quot; page with the &quot;Confirm&quot; button selected.](media/saml-sso-confluence-tutorial/add-on-2.png)
4. Under **ATLASSIAN MARKETPLACE** tab, select **Find new add-ons**.

    ![Screenshot that shows the &quot;Atlassian Marketplace&quot; tab with &quot;Find new add-ons&quot; selected.](media/saml-sso-confluence-tutorial/add-on.png)
5. Search **SAML Single Sign On (SSO) for Confluence** and select **Install** button to install the new SAML plugin.

    ![Screenshot that shows the &quot;Find new add-ons&quot; page with &quot;S A M L Single Sign On (S S O) for Confluence&quot; in the search box and the &quot;Install&quot; button selected.](media/saml-sso-confluence-tutorial/add-on-7.png)
6. The plugin installation will start. Select **Close**.

    ![Screenshot that shows the &quot;Installing&quot; dialog.](media/saml-sso-confluence-tutorial/add-on-8.png)

    ![Screenshot that shows the &quot;Installed and ready to go!&quot; dialog with the &quot;Close&quot; action selected.](media/saml-sso-confluence-tutorial/add-on-9.png)
7. Select **Manage**.
8. Select **Configure** to configure the new plugin.

    ![Screenshot that shows the &quot;Manage&quot; page with the &quot;Configure&quot; button selected.](media/saml-sso-confluence-tutorial/add-on-11.png)
9. This new plugin can also be found under **USERS & SECURITY** tab.

    ![Screenshot that shows the &quot;Users &amp; Security&quot; tab with &quot;S A M L SingleSignOn&quot; selected.](media/saml-sso-confluence-tutorial/add-on-3.png)
10. On **SAML SingleSignOn Plugin Configuration** page, select **Add new IdP** button to configure the settings of Identity Provider.

    ![Screenshot that shows the &quot;S A M L SingleSignOn Plugin Configuration&quot; page, with the &quot;Add new I d P&quot; button selected.](media/saml-sso-confluence-tutorial/add-on-4.png)
11. On **Choose your SAML Identity Provider** page, perform the following steps:

    ![Screenshot that shows the &quot;Choose your S A M L Identity Provider&quot; page with the &quot;I d P Type&quot;, &quot;Name&quot;, and &quot;Description&quot; text boxes highlighted.](media/saml-sso-confluence-tutorial/add-on-5-a.png)

    a. Set **Microsoft Entra ID** as the IdP type.

    b. Add **Name** of the Identity Provider (such as Microsoft Entra ID).

    c. Add **Description** of the Identity Provider (such as Microsoft Entra ID).

    d. Select **Next**.
12. On **Identity provider configuration** page, select **Next** button.
13. On **Import SAML IdP Metadata** page, perform the following steps:

    ![Screenshot that shows the &quot;Import S A M L I d P Metadata&quot; page with the &quot;Import&quot;, &quot;Load File&quot;, and &quot;Next&quot; buttons selected.](media/saml-sso-confluence-tutorial/add-on-5-c.png)

    a. Select **Load File** button and pick Metadata XML file you downloaded in Step 5.

    b. Select **Import** button.

    c. Wait briefly until import succeeds.

    d. Select **Next** button.
14. On **User ID attribute and transformation** page, select **Next** button.

    ![Screenshot that shows the &quot;User ID attribute and transformation&quot; page with the &quot;Next&quot; button selected.](media/saml-sso-confluence-tutorial/add-on-5-d.png)
15. On **User creation and update** page, select **Save & Next** to save settings.

    ![Screenshot that shows the &quot;User creation and update&quot; page with the &quot;Save &amp; Next&quot; button selected.](media/saml-sso-confluence-tutorial/add-on-6-a.png)
16. On **Test your settings** page, select **Skip test & configure manually** to skip the user test for now. This are performed in the next section and requires some settings in Azure portal.

    ![Screenshot that shows the &quot;Test your settings&quot; page with the &quot;Skip test &amp; configure manually&quot; button selected.](media/saml-sso-confluence-tutorial/add-on-6-b.png)
17. In the appearing dialog reading **Skipping the test means...**, select **OK**.

    ![Configure Single Sign-On](media/saml-sso-confluence-tutorial/add-on-6-c.png)

### Create SAML SSO for Confluence by resolution GmbH test user

To enable Microsoft Entra users to log in to SAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH. In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Log in to your SAML SSO for Confluence by resolution GmbH company site as an administrator.
2. Hover on cog and select the **User management**.

    ![Screenshot that shows the &quot;Cog&quot; icon selected, and &quot;User management&quot; selected from the menu.](media/saml-sso-confluence-tutorial/user-1.png)
3. Under Users section, select **Add users** tab. On the **“Add a User”** dialog page, perform the following steps:

    ![Add Employee](media/saml-sso-confluence-tutorial/user-2.png)

    a. In the **Username** textbox, type the email of user like Britta Simon.

    b. In the **Full Name** textbox, type the full name of user like Britta Simon.

    c. In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.

    d. In the **Password** textbox, type the password for Britta Simon.

    e. Select **Confirm Password** reenter the password.

    f. Select **Add** button.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to SAML SSO for Confluence by resolution GmbH Sign on URL where you can initiate the login flow.
- Go to SAML SSO for Confluence by resolution GmbH Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the SAML SSO for Confluence by resolution GmbH for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the SAML SSO for Confluence by resolution GmbH tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the SAML SSO for Confluence by resolution GmbH for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).