---
layout: Conceptual
title: Configure Mitel Connect for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/mitel-connect-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Mitel Connect.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 7af27748-31ff-2865-66c5-0bec0d9b6c66
document_version_independent_id: 71920043-e30c-ab9a-e839-5e8034cc8456
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/mitel-connect-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/mitel-connect-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/mitel-connect-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: cb6dbd04-9631-07d8-6387-90724cdba9af
---

# Configure Mitel Connect for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to use the Mitel Connect app to integrate Microsoft Entra ID with Mitel MiCloud Connect or CloudLink Platform. The Mitel Connect app is available in the Azure Gallery. Integrating Microsoft Entra ID with MiCloud Connect or CloudLink Platform provides you with the following benefits:

- You can control users' access to MiCloud Connect apps and to CloudLink apps in Microsoft Entra ID by using their enterprise credentials.
- You can enable users on your account to be automatically signed in to MiCloud Connect or CloudLink (single sign-on) by using their Microsoft Entra accounts.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Mitel MiCloud Connect account or Mitel CloudLink account, depending on the application you want to configure.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on (SSO).

- Mitel Connect supports **SP** initiated SSO.

## Adding Mitel Connect from the gallery

To configure the integration of Mitel Connect into Microsoft Entra ID, you need to add Mitel Connect from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Mitel Connect** in the search box.
4. Select **Mitel Connect** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO

In this section, you configure and test Microsoft Entra SSO with MiCloud Connect or CloudLink Platform based on a test user named ***Britta Simon***. For single sign-on to work, a link must be established between the user in Azure portal and the corresponding user on the Mitel platform. Refer to the following sections for information about configuring and testing Microsoft Entra SSO with MiCloud Connect or CloudLink Platform.

- Configure and test Microsoft Entra SSO with MiCloud Connect
- Configure and test Microsoft Entra SSO with CloudLink Platform

## Configure and test Microsoft Entra SSO with MiCloud Connect

To configure and test Microsoft Entra single sign-on with MiCloud Connect:

1. **Configure MiCloud Connect for SSO with Microsoft Entra ID** - to enable your users to use this feature and to configure the SSO settings on the application side.
2. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
3. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
4. **Create a Mitel MiCloud Connect test user** - to have a counterpart of Britta Simon on your MiCloud Connect account that's linked to the Microsoft Entra representation of the user.
5. **Test SSO** - to verify whether the configuration works.

## Configure MiCloud Connect for SSO with Microsoft Entra ID

In this section, you enable Microsoft Entra single sign-on for MiCloud Connect in the Azure portal and configure your MiCloud Connect account to allow SSO using Microsoft Entra ID.

To configure MiCloud Connect with SSO for Microsoft Entra ID, it's easiest to open the Azure portal and the Mitel Account portal side by side. You'll need to copy some information to the Mitel Account portal and some from the Mitel Account portal to the Azure portal.

1. To open the configuration page in the Azure portal:

    1. On the **Mitel Connect** application integration page, select **Single sign-on**.
    2. In the **Select a Single sign-on method** dialog box, select **SAML**. The SAML-based sign-on page is displayed.
2. To open the configuration dialog box in the Mitel Account portal:

    1. On the **Phone System** menu, select **Add-On Features**.
    2. To the right of **Single Sign-On**, select **Activate** or **Settings**.

    The Connect single sign-on Settings dialog box appears.
3. Select the **Enable Single Sign-On** check box.

    ![Screenshot that shows the Mitel Connect Single Sign-On Settings page, with the Enable Single Sign-On check box selected.](media/mitel-connect-tutorial/mitel-connect-enable.png)
4. In the Azure portal, select the **Edit** icon in the **Basic SAML Configuration** section.

    ![Screenshot shows the Set up Single Sign-On with SAML page with the edit icon selected.](common/edit-urls.png)

    The Basic SAML Configuration dialog box appears.
5. Copy the URL from the **Mitel Identifier (Entity ID)** field in the Mitel Account portal and paste it into the **Identifier (Entity ID)** field.
6. Copy the URL from the **Reply URL (Assertion Consumer Service URL)** field in the Mitel Account portal and paste it into the **Reply URL (Assertion Consumer Service URL)** field.

    ![Screenshot shows Basic SAML Configuration in the Azure portal and the Set Up Identity Provider section in the Mitel Account portal with lines indicating the relationship between them.](media/mitel-connect-tutorial/mitel-azure-basic-configuration.png)
7. In the **Sign-on URL** text box, type one of the following URLs:

    1. **https://portal.shoretelsky.com** - to use the Mitel Account portal as your default Mitel application
    2. **https://teamwork.shoretel.com** - to use Teamwork as your default Mitel application

    Note

    The default Mitel application is the application that's accessed when a user selects the Mitel Connect tile in the Access Panel. This is also the application accessed when doing a test setup from Microsoft Entra ID.
8. Select **Save** in the **Basic SAML Configuration** dialog box.
9. In the **SAML Signing Certificate** section on the **SAML-based sign-on** page in the Azure portal, select **Download** next to **Certificate (Base64)** to download the **Signing Certificate** and save it to your computer.

    ![Screenshot shows the SAML Signing Certificate pane where you can download a certificate.](media/mitel-connect-tutorial/azure-signing-certificate.png)
10. Open the Signing Certificate file in a text editor, copy all data in the file, and then paste the data in the **Signing Certificate** field in the Mitel Account portal.

    ![Screenshot shows the Signing Certificate field.](media/mitel-connect-tutorial/mitel-connect-signing-certificate.png)
11. In the **Setup Mitel Connect** section on the **SAML-based sign-on** page of the Azure portal:

    1. Copy the URL from the **Login URL** field and paste it into the **Sign-in URL** field in the Mitel Account portal.
    2. Copy the URL from the **Microsoft Entra Identifier** field and paste it into the **Entity ID** field in the Mitel Account portal.
12. Select **Save** on the **Connect Single Sign-On Settings** dialog box in the Mitel Account portal.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Create a Mitel MiCloud Connect test user

In this section, you create a user named Britta Simon on your MiCloud Connect account. Users must be created and activated before using single sign-on.

For details about adding users in the Mitel Account portal, see the Adding a User article in the Mitel Knowledge Base.

Create a user on your MiCloud Connect account with the following details:

- **Name:** Britta Simon
- **Business Email Address:**`brittasimon@<yourcompanydomain>.<extension>` (Example: brittasimon@contoso.com)
- **Username:**`brittasimon@<yourcompanydomain>.<extension>` (Example: brittasimon@contoso.com; the user’s username is typically the same as the user’s business email address)

Note

The user’s MiCloud Connect username must be identical to the user’s email address in Azure.

### Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Mitel Connect Sign-on URL where you can initiate the sign-in flow.
- Go to Mitel Connect Sign-on URL directly and initiate the sign-in flow from there.
- You can use Microsoft My Apps. When you select the Mitel Connect tile in the My Apps, this option redirects to MiCloud Connect Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Configure and test Microsoft Entra SSO with CloudLink Platform

This section describes how to enable Microsoft Entra SSO for CloudLink platform in the Azure portal and how to configure your CloudLink platform account to allow single sign-on using Microsoft Entra ID.

To configure CloudLink platform with single sign-on for Microsoft Entra ID, it's recommended that you open the Azure portal and the CloudLink Accounts portal side by side as you need to copy some information to the CloudLink Accounts portal and vice versa.

1. To open the configuration page in the Azure portal:

    1. On the **Mitel Connect** application integration page, select **Single sign-on**.
    2. In the **Select a Single sign-on method** dialog box, select **SAML**. The **SAML-based Sign-on** page opens, displaying the **Basic SAML Configuration** section.

        ![Screenshot shows the SAML-based Sign-on page with Basic SAML Configuration.](media/mitel-connect-tutorial/mitel-azure-saml-settings.png)
2. To access the **Microsoft Entra Single Sign On** configuration panel in the CloudLink Accounts portal:

    1. Go to the **Account Information** page of the customer account with which you want to enable the integration.
    2. In the **Integrations** section, select **+ Add new**. A pop-up screen displays the **Integrations** panel.
    3. Select the **3rd party** tab. A list of supported third-party applications is displayed. Select the **Add** button associated with **Microsoft Entra Single Sign On**, and select **Done**.

        The **Microsoft Entra Single Sign On** is enabled for the customer account and is added to the **Integrations** section of the **Account Information** page.
    4. Select **Complete Setup**. The **Microsoft Entra Single Sign On** configuration panel opens.

        ![Screenshot shows Microsoft Entra Single Sign-On configuration.](media/mitel-connect-tutorial/mitel-cloudlink-sso-setup.png)

        Mitel recommends that the **Enabled Mitel Credentials (Optional)** check box in the **Optional Mitel credentials** section isn't selected. Select this check box only if you want the user to sign in to the CloudLink application using the Mitel credentials in addition to the single sign-on option.
3. In the Azure portal, from the **SAML-based Sign-on** page, select the **Edit** icon in the **Basic SAML Configuration** section. The **Basic SAML Configuration** panel opens.

    ![Screenshot shows the Basic SAML Configuration pane with the Edit icon selected.](media/mitel-connect-tutorial/mitel-azure-saml-basic.png)
4. Copy the URL from the **Mitel Identifier (Entity ID)** field in the CloudLink Accounts portal and paste it into the **Identifier (Entity ID)** field.
5. Copy the URL from the **Reply URL (Assertion Consumer Service URL)** field in the CloudLink Accounts portal and paste it into the **Reply URL (Assertion Consumer Service URL)** field.

    ![Screenshot shows the relation between pages in the CloudLink Accounts portal and the Azure portal.](media/mitel-connect-tutorial/mitel-cloudlink-saml-mapping.png)
6. In the **Sign-on URL** text box, type the URL `https://accounts.mitel.io` to use the CloudLink Accounts portal as your default Mitel application.

    ![Screenshot shows the Sign on U R L text box.](media/mitel-connect-tutorial/mitel-cloudlink-sign-on-url.png)

    Note

    The default Mitel application is the application that opens when a user selects the Mitel Connect tile in the Access Panel. This is also the application accessed when the user configures a test setup from Microsoft Entra ID.
7. Select **Save** in the **Basic SAML Configuration** dialog box.
8. In the **SAML Signing Certificate** section on the **SAML-based sign-on** page in the Azure portal, select **Download** beside **Certificate (Base64)** to download the **Signing Certificate**. Save the certificate on your computer.

    ![Screenshot shows the SAML Signing Certificate section where you can download a Base64 certificate.](media/mitel-connect-tutorial/mitel-cloudlink-save-certificate.png)
9. Open the Signing Certificate file in a text editor, copy all data in the file, and then paste the data into the **Signing Certificate** field in the CloudLink Accounts portal.

    Note

    If you have more than one certificate, we recommend that you paste them one after the other.
10. In the **Set up Mitel Connect** section on the **SAML-based sign-on** page of the Azure portal:

    1. Copy the URL from the **Login URL** field and paste it into the **Sign-in URL** field in the CloudLink Accounts portal.
    2. Copy the URL from the **Microsoft Entra Identifier** field and paste it into the **IDP Identifier (Entity ID)** field in the CloudLink Accounts portal.

        ![Screenshot shows the source for the values described here in Mintel Connect.](media/mitel-connect-tutorial/mitel-cloudlink-copy-settings.png)
11. Select **Save** on the **Microsoft Entra Single Sign On** panel in the CloudLink Accounts portal.

### Create a Microsoft Entra test user

In this section, you create a test user called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Assign the Microsoft Entra test user

In this section, you enable B.Simon to use single sign-on by granting access to Mitel Connect.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Mitel Connect**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Added Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Added Assignment** dialog, select the **Assign** button.

### Create a CloudLink test user

This section describes how to create a test user named ***Britta Simon*** on your CloudLink platform. Users must be created and activated before they can use single sign-on.

For details about adding users in the CloudLink Accounts portal, see ***Managing Users*** in the [CloudLink Accounts documentation](https://www.mitel.com/document-center/technology/cloudlink).

Create a user on your CloudLink Accounts portal with the following details:

- Name: Britta Simon
- First Name: Britta
- Last Name: Simon
- Email: BrittaSimon@contoso.com

Note

The user's CloudLink email address must be identical to the **User Principal Name**.

### Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to CloudLink Sign-on URL where you can initiate the sign-in flow.
- Go to CloudLink Sign-on URL directly and initiate the sign-in flow from there.
- You can use Microsoft My Apps. When you select the Mitel Connect tile in the My Apps, this option redirects to CloudLink Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).