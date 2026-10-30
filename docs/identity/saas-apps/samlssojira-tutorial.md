---
layout: Conceptual
title: Configure SAML SSO for Jira by Resolution GmbH for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/samlssojira-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SAML SSO for Jira by resolution GmbH.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 124ee5bd-82fd-ee1d-27b0-c28ad4bce451
document_version_independent_id: 06140d23-40a3-f433-f14a-c26bdef69bbb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/samlssojira-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/samlssojira-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/samlssojira-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c883749a-8b81-7eaa-7542-773d95aa070a
---

# Configure SAML SSO for Jira by Resolution GmbH for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SAML SSO for Jira by resolution GmbH with Microsoft Entra ID. When you integrate SAML SSO for Jira by resolution GmbH with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SAML SSO for Jira by resolution GmbH.
- Enable your users to be automatically signed-in to SAML SSO for Jira by resolution GmbH with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SAML SSO for Jira by resolution GmbH single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- SAML SSO for Jira by resolution GmbH supports **SP** and **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add SAML SSO for Jira by resolution GmbH from the gallery

To configure the integration of SAML SSO for Jira by resolution GmbH into Microsoft Entra ID, you need to add SAML SSO for Jira by resolution GmbH from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SAML SSO for Jira by resolution GmbH** in the search box.
4. Select **SAML SSO for Jira by resolution GmbH** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SAML SSO for Jira by resolution GmbH

Configure and test Microsoft Entra SSO with SAML SSO for Jira by resolution GmbH using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SAML SSO for Jira by resolution GmbH.

To configure and test Microsoft Entra SSO with SAML SSO for Jira by resolution GmbH, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SAML SSO for Jira by resolution GmbH SSO**- to configure the single sign-on settings on application side.
    1. **Create SAML SSO for Jira by resolution GmbH test user** - to have a counterpart of B.Simon in SAML SSO for Jira by resolution GmbH that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SAML SSO for Jira by resolution GmbH** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, if you wish to configure the application in the **IDP** initiated mode, then perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`

    c. Select **Set additional URLs** and perform the following step, if you wish to configure the application in the **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`

    Note

    For the Identifier, Reply URL and Sign-on URL, substitute **&lt;server-base-url&gt;** with the base URL of your Jira instance. You can also refer to the patterns shown in the **Basic SAML Configuration** section. If you have a problem, contact us at [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support).
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, download the **Federation Metadata XML** and save it to your computer.

    ![The Certificate download link](common/metadataxml.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SAML SSO for Jira by resolution GmbH SSO

1. In a different web browser window, sign in to your Jira instance as an administrator.
2. Hover over the cog at the right side and select **Manage apps**.

    ![Screenshot that shows an arrow pointing at the &quot;Cog&quot; icon, and &quot;Manage apps&quot; selected from the drop-down.](media/samlssojira-tutorial/add-on-1.png)
3. If you're redirected to Administrator Access page, enter the **Password** and select the **Confirm** button.

    ![Screenshot that shows the &quot;Administrator Access&quot; page.](media/samlssojira-tutorial/add-on-2.png)
4. Jira normally redirects you to the Atlassian marketplace. If not, select **Find new apps** in the left panel. Search for **SAML Single Sign On (SSO) for JIRA** and select the **Install** button to install the SAML plugin.

    ![Screenshot that shows the &quot;Atlassian Marketplace for JIRA&quot; page with an arrow pointing at the &quot;Install&quot; button for the &quot;S A M L Single Sign On (S S O) Jira, S A M L/S S O&quot; app.](media/samlssojira-tutorial/store.png)
5. The plugin installation will start. When it's done, select the **Close** button.

    ![Screenshot that shows the &quot;Installing&quot; dialog.](media/samlssojira-tutorial/store-2.png)

    ![Screenshot that shows the &quot;Installed and ready to go!&quot; dialog with the &quot;Close&quot; button selected.](media/samlssojira-tutorial/store-3.png)
6. Then, select **Manage**.
7. Afterwards, select **Configure** to configure the just installed plugin.

    ![Screenshot that shows the &quot;Manage apps&quot; page, with the &quot;Configure&quot; button selected for the &quot;S A M L SingleSignOn for Jira&quot; app.](media/samlssojira-tutorial/store-5.png)
8. In the **SAML SingleSignOn Plugin Configuration** wizard, select **Add new IdP** to configure Microsoft Entra ID as a new Identity Provider.

    ![Screenshot shows the &quot;Welcome&quot; page, with the &quot;Add new I d P&quot; button selected.](media/samlssojira-tutorial/add-on-4.png)
9. On the **Choose your SAML Identity Provider** page, perform the following steps:

    ![Screenshot that shows the &quot;Choose your S A M L Identity Provider&quot; page with the &quot;I d P Type&quot; and &quot;Name&quot; text boxes highlighted, and the &quot;Next&quot; button selected.](media/samlssojira-tutorial/identity-provider.png)

    a. Set **Microsoft Entra ID** as the IdP type.

    b. Add the **Name** of the Identity Provider (such as Microsoft Entra ID).

    c. Add an (optional) **Description** of the Identity Provider (such as Microsoft Entra ID).

    d. Select **Next**.
10. On the **Identity provider configuration** page, select **Next**.
11. On **Import SAML IdP Metadata** page, perform the following steps:

    ![Screenshot that shows the &quot;Import S A M L I d P Metadata&quot; page with the &quot;Select Metadata X M L File&quot; action selected.](media/samlssojira-tutorial/metadata.png)

    a. Select the **Select Metadata XML File** button and pick the **Federation Metadata XML** file you downloaded before.

    b. Select the **Import** button.

    c. Wait briefly until the import succeeds.

    d. Select the **Next** button.
12. On **User ID attribute and transformation** page, select the **Next** button.

    ![Screenshot that shows the &quot;User I D attribute and transformation&quot; page with the &quot;Next&quot; button selected.](media/samlssojira-tutorial/transformation.png)
13. On the **User creation and update** page, select **Save & Next** to save the settings.

    ![Screenshot that shows the &quot;User creation and update&quot; page with the &quot;Save &amp; Next&quot; button selected.](media/samlssojira-tutorial/update.png)
14. On the **Test your settings** page, select **Skip test & configure manually** to skip the user test for now. This are performed in the next section and requires some settings.

    ![Screenshot that shows the &quot;Test your settings&quot; page with the &quot;Skip test &amp; configure manually&quot; button selected.](media/samlssojira-tutorial/test.png)
15. Select **OK** to skip the warning.

    ![Screenshot that shows the warning dialog with the &quot;O K&quot; button selected.](media/samlssojira-tutorial/warning.png)

### Create SAML SSO for Jira by resolution GmbH test user

To enable Microsoft Entra users to sign in to SAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH. For the case of this article, you have to do the provisioning by hand. However, there are also other provisioning models available for the SAML SSO plugin by resolution, for example **Just In Time** provisioning. Refer to their documentation at [SAML SSO by resolution GmbH](https://wiki.resolution.de/doc/saml-sso/latest/all). If you have a question about it, contact support at [resolution support](https://www.resolution.de/go/support).

**To manually provision a user account, perform the following steps:**

1. Sign in to Jira instance as an administrator.
2. Hover over the cog and select **User management**.

    ![Screenshot that shows an arrow pointing at the &quot;Cog&quot; icon with &quot;User management&quot; selected from the drop-down.](media/samlssojira-tutorial/user-1.png)
3. If you're redirected to the Administrator Access page, then enter the **Password** and select the **Confirm** button.

    ![Screenshot that shows the &quot;Administrator Access&quot; page with the &quot;Password&quot; textbox highlighted.](media/samlssojira-tutorial/user-2.png)
4. Under the **User management** tab section, select **create user**.

    ![Screenshot that shows the &quot;User management&quot; tab with the &quot;Create user&quot; button selected.](media/samlssojira-tutorial/user-3-new.png)
5. On the **“Create new user”** dialog page, perform the following steps. You have to create the user exactly like in Microsoft Entra ID:

    ![Add Employee](media/samlssojira-tutorial/user-4-new.png)

    a. In the **Email address** textbox, type the email address of the user: **BrittaSimon@contoso.com**.

    b. In the **Full Name** textbox, type full name of the user: **Britta Simon**.

    c. In the **Username** textbox, type the email address of the user: **BrittaSimon@contoso.com**.

    d. In the **Password** textbox, enter the password of the user.

    e. Select **Create user** to finish the user creation.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to SAML SSO for Jira by resolution GmbH Sign on URL where you can initiate the login flow.
- Go to SAML SSO for Jira by resolution GmbH Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the SAML SSO for Jira by resolution GmbH for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the SAML SSO for Jira by resolution GmbH tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the SAML SSO for Jira by resolution GmbH for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Enable SSO redirection for Jira

As noted in the section before, there are currently two ways to trigger the single sign-on. Either by using the **Azure portal** or using **a special link to your Jira instance**. The SAML SSO plugin by resolution GmbH also allows you to trigger single sign-on by simply **accessing any URL pointing to your Jira instance**.

In essence, all users accessing Jira is redirected to the single sign-on after activating an option in the plugin.

To activate SSO redirect, do the following in **your Jira instance**:

1. Access the configuration page of the SAML SSO plugin in Jira.
2. Select **Redirection** in the left panel.
3. Tick **Enable SSO Redirect**.

    ![Partial screenshot of the Jira SAML SingleSignOn Plugin Configuration page highlighting the selected &quot;Enable SSO Redirect&quot; check box.](media/samlssojira-tutorial/configure-2.png)
4. Press the **Save Settings** button in the top right corner.

After activating the option, you can still reach the username/password prompt if the **Enable nosso** option is ticked by navigating to `https://<server-base-url>/login.jsp?nosso`. As always, substitute **&lt;server-base-url&gt;** with your base URL.