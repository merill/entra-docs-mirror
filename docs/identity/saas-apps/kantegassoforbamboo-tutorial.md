---
layout: Conceptual
title: Configure Kantega SSO for Bamboo for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/kantegassoforbamboo-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Kantega SSO for Bamboo.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 95b57f1d-699a-8ca6-b604-e18ac5b0c8f6
document_version_independent_id: 62ae9f1b-983c-9fda-6925-23bc90c54bf2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/kantegassoforbamboo-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/kantegassoforbamboo-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/kantegassoforbamboo-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3480dc9a-c228-b86b-9b30-1b307f4a6a33
---

# Configure Kantega SSO for Bamboo for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Kantega SSO for Bamboo with Microsoft Entra ID. When you integrate Kantega SSO for Bamboo with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Kantega SSO for Bamboo.
- Enable your users to be automatically signed-in to Kantega SSO for Bamboo with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Kantega SSO for Bamboo single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Kantega SSO for Bamboo supports **SP and IDP** initiated SSO.

## Add Kantega SSO for Bamboo from the gallery

To configure the integration of Kantega SSO for Bamboo into Microsoft Entra ID, you need to add Kantega SSO for Bamboo from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Kantega SSO for Bamboo** in the search box.
4. Select **Kantega SSO for Bamboo** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Kantega SSO for Bamboo

Configure and test Microsoft Entra SSO with Kantega SSO for Bamboo using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Kantega SSO for Bamboo.

To configure and test Microsoft Entra SSO with Kantega SSO for Bamboo, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Kantega SSO for Bamboo SSO**- to configure the single sign-on settings on application side.
    1. **Create Kantega SSO for Bamboo test user** - to have a counterpart of B.Simon in Kantega SSO for Bamboo that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Kantega SSO for Bamboo** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-On URL. These values are received during the configuration of Bamboo plugin which is explained later in the article.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
8. On the **Set up Kantega SSO for Bamboo** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Kantega SSO for Bamboo SSO

1. In a different web browser window, sign in to your Bamboo on-premises server as an administrator.
2. Hover on cog and select the **Add-ons**.

    ![Screenshot shows Add-ons selected from the Settings menu.](media/kantegassoforbamboo-tutorial/menu.png)
3. Under Add-ons tab section, select **Find new add-ons**. Search **Kantega SSO for Bamboo (SAML & Kerberos)** and select **Install** button to install the new SAML plugin.

    ![Screenshot shows Bamboo Administration with Kantega S S O for Bamboo selected.](media/kantegassoforbamboo-tutorial/profile.png)
4. The plugin installation will start.

    ![Screenshot shows Installing progress for Kantega S S O for Bamboo.](media/kantegassoforbamboo-tutorial/settings.png)
5. Once the installation is complete, select **Close**.

    ![Screenshot shows the Close button.](media/kantegassoforbamboo-tutorial/installation.png)
6. In the **Kantega SSO for Bamboo** page, select **Manage**.
7. Select **Configure** to configure the new plugin.

    ![Screenshot shows User-installed add-ons with Configure selected.](media/kantegassoforbamboo-tutorial/license.png)
8. In the **SAML** section, select **Microsoft Entra ID** from the **Add identity provider** dropdown.
9. In the **Kantega Single Sign-on** page, select **Basic**.
10. On the **App properties** section, perform following steps:

    ![Screenshot shows the App properties section where you can provide the information in this step.](media/kantegassoforbamboo-tutorial/properties.png)

    a. Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Basic SAML Configuration** section in Azure portal.

    b. Select **Next**.
11. On the **Metadata import** section, select **Metadata file on my computer**.
12. Select **Browse file** to upload the metadata file that you previously downloaded, then select **Next**.
13. On the **Name and SSO location** section, perform following steps:

    ![Screenshot shows the Name and S S O location where Microsoft Entra ID is the identity provider name.](media/kantegassoforbamboo-tutorial/location.png)

    a. Add Name of the Identity Provider in **Identity provider name** textbox (such as Microsoft Entra ID).

    b. Select **Next**.
14. Verify the Signing certificate and select **Next**.

    ![Screenshot shows Signature verification.](media/kantegassoforbamboo-tutorial/certificate.png)
15. On the **Bamboo user accounts** section, perform following steps:

    ![Screenshot shows Bamboo user accounts where you have the option to create users.](media/kantegassoforbamboo-tutorial/accounts.png)

    a. Select **Create users in Bamboo's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no. of groups separated by comma).

    b. Select **Next**.
16. Select **Finish**.
17. On the **Known domains for Microsoft Entra ID** section, perform following steps:

    a. Select **Known domains** from the left panel of the page.

    b. Enter domain name in the **Known domains** textbox.

    c. Select **Save**.

### Create Kantega SSO for Bamboo test user

To enable Microsoft Entra users to sign in to Bamboo, they must be provisioned into Bamboo. In case of Kantega SSO for Bamboo, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to your Bamboo on-premises server as an administrator.
2. Hover on cog and select the **User management**.

    ![Screenshot shows User Management selected from the Settings menu.](media/kantegassoforbamboo-tutorial/user-management.png)
3. Select **Users**. Under the **Add user** section, Perform following steps:

    ![Screenshot shows the Add user pane where you can perform these steps.](media/kantegassoforbamboo-tutorial/add-user.png)

    a. In the **Username** textbox, type the email of user like Brittasimon@contoso.com.

    b. In the **Password** textbox, type the password of user.

    c. In the **Confirm Password** textbox, reenter the password of user.

    d. In the **Full Name** textbox, type full name of the user like Britta Simon.

    e. In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.

    f. Select **Save**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Kantega SSO for Bamboo Sign on URL where you can initiate the login flow.
- Go to Kantega SSO for Bamboo Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Kantega SSO for Bamboo for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Kantega SSO for Bamboo tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Kantega SSO for Bamboo for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).