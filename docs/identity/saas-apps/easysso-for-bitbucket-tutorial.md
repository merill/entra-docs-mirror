---
layout: Conceptual
title: Configure EasySSO for BitBucket for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/easysso-for-bitbucket-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and EasySSO for BitBucket.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: fecc0d6f-c4d7-7a0e-4f8c-1d29121b72d7
document_version_independent_id: 906a8303-d0c7-247f-91ca-aec5811998a1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/easysso-for-bitbucket-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/easysso-for-bitbucket-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/easysso-for-bitbucket-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 86840dd4-c4ee-006d-5897-6bdcbe4e905f
---

# Configure EasySSO for BitBucket for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate EasySSO for BitBucket with Microsoft Entra ID. When you integrate EasySSO for BitBucket with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to EasySSO for BitBucket.
- Enable your users to be automatically signed-in to EasySSO for BitBucket with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A subscription to EasySSO for BitBucket that's enabled for single sign-on (SSO).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- EasySSO for BitBucket supports SP-initiated and IdP-initiated SSO.
- EasySSO for BitBucket supports "just-in-time" user provisioning.

## Add EasySSO for BitBucket from the gallery

To configure the integration of EasySSO for BitBucket into Microsoft Entra ID, you need to add EasySSO for BitBucket from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **EasySSO for BitBucket** in the search box.
4. Select **EasySSO for BitBucket** from the results, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for EasySSO for BitBucket

Configure and test Microsoft Entra SSO with EasySSO for BitBucket by using a test user called **B.Simon**. For SSO to work, you need to establish a linked relationship between a Microsoft Entra user and the related user in EasySSO for BitBucket.

To configure and test Microsoft Entra SSO with EasySSO for BitBucket, perform the following steps:

1. Configure Microsoft Entra SSOto enable your users to use this feature.
    1. Create a Microsoft Entra test user to test Microsoft Entra single sign-on with B.Simon.
    2. Assign the Microsoft Entra test user to enable B.Simon to use Microsoft Entra single sign-on.
2. Configure EasySSO for BitBucket SSOto configure the single sign-on settings on the application side.
    1. Create an EasySSO for BitBucket test user to have a counterpart of B.Simon in EasySSO for BitBucket, linked to the Microsoft Entra representation of user.
3. Test SSO to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **EasySSO for BitBucket** application integration page, find the **Manage** section. Select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot of Set up Single Sign-On with SAML page, with pencil icon highlighted](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, if you want to configure the application in **IdP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL that uses the following pattern: `https://<server-base-url>/plugins/servlet/easysso/saml`

    b. In the **Reply URL** text box, type a URL that uses the following pattern: `https://<server-base-url>/plugins/servlet/easysso/saml`
6. Select **Set additional URLs**, and do the following step if you want to configure the application in **SP** initiated mode:

    - In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<server-base-url>/login.jsp`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact the [EasySSO support team](mailto:support@techtime.co.nz) to get these values if in doubt. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. The EasySSO for BitBucket application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot of default attributes](common/default-attributes.png)
8. The EasySSO for BitBucket application also expects a few more attributes to be passed back in the SAML response. The following table shows these. These attributes are also pre-populated, but you can review them per your requirements.

    | Name | Source attribute |
    | --- | --- |
    | urn:oid:0.9.2342.19200300.100.1.1 | user.userprincipalname |
    | urn:oid:0.9.2342.19200300.100.1.3 | user.mail |
    | urn:oid:2.16.840.1.113730.3.1.241 | user.displayname |
    | urn:oid:2.5.4.4 | user.surname |
    | urn:oid:2.5.4.42 | user.givenname |

    If your Microsoft Entra users have **sAMAccountName** configured, you have to map **urn:oid:0.9.2342.19200300.100.1.1** onto the **sAMAccountName** attribute.
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select the download links for the **Certificate (Base64)** or **Federation Metadata XML** options. Save either or both to your computer. You need it later to configure BitBucket EasySSO.

    ![Screenshot of the SAML Signing Certificate section, with download links highlighted](media/easysso-for-bitbucket-tutorial/certificate.png)

    If you plan to configure EasySSO for BitBucket manually with a certificate, you also need to copy **Login URL** and **Microsoft Entra Identifier**, and save those on your computer.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure EasySSO for BitBucket SSO

1. In a different web browser window, sign in to your Zoom company site as an administrator
2. Go to the **Administration** section.

    ![Screenshot of BitBucket instance, with gear icon highlighted](media/easysso-for-bitbucket-tutorial/bitbucket-admin-1.png)
3. Locate and select **EasySSO**.

    ![Screenshot of Easy SSO option](media/easysso-for-bitbucket-tutorial/bitbucket-admin-2.png)
4. Select **SAML**. This takes you to the SAML configuration section.

    ![Screenshot of EasySSO Admin page, with SAML highlighted](media/easysso-for-bitbucket-tutorial/bitbucket-admin-3.png)
5. Select the **Certificates** tab, and you're presented with the following screen:

    ![Screenshot of the Certificates tab, with various options highlighted](media/easysso-for-bitbucket-tutorial/bitbucket-admin-4.png)
6. Locate the **Certificate (Base64)** or **Metadata File** that you saved in the preceding section of this article. You can proceed in one of the following ways:

    - Use the App Federation **Metadata File** you downloaded to a local file on your computer. Select the **Upload** radio button, and follow the path specific to your operating system.
    - Open the App Federation **Metadata File** to see the content of the file, in any plain-text editor. Copy it onto the clipboard. Select **Input**, and paste the clipboard content into the text field.
    - Do a fully manual configuration. Open the App Federation **Certificate (Base64)** to see the content of the file, in any plain-text editor. Copy it onto the clipboard, and paste it into the **IdP Token Signing Certificates** text field. Then go to the **General** tab, and fill the **POST Binding URL** and **Entity ID** fields with the respective values for **Login URL** and **Microsoft Entra Identifier** that you saved previously.
7. Select **Save** on the bottom of the page. You'll see that the content of the metadata or certificate files is parsed into the configuration fields. EasySSO for BitBucket configuration is complete.
8. To test the configuration, go to the **Look & Feel** tab, and select **SAML Login Button**. This enables a separate button on the BitBucket sign-in screen, specifically to test your Microsoft Entra SAML integration end-to-end. You can leave this button on, and configure its placement, color, and translation for production mode, too.

    ![Screenshot of SAML page Look &amp; Feel tab, with SAML Login Button highlighted](media/easysso-for-bitbucket-tutorial/bitbucket-admin-5.png)

    Note

    If you have any problems, contact the [EasySSO support team](mailto:support@techtime.co.nz).

### Create an EasySSO for BitBucket test user

In this section, you create a user called Britta Simon in BitBucket. EasySSO for BitBucket supports just-in-time user provisioning, which is disabled by default. To enable it, you have to explicitly check **Create user on successful login** in the **General** section of EasySSO plug-in configuration. If a user doesn't already exist in BitBucket, a new one is created after authentication.

However, if you don't want to enable automatic user provisioning when the user first signs in, users must exist in user directories that the instance of BitBucket makes use of. For example, this directory might be LDAP or Atlassian Crowd.

![Screenshot of the General section of EasySSO plug-in configuration, with Create user on successful login highlighted](media/easysso-for-bitbucket-tutorial/bitbucket-admin-6.png)

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to EasySSO for BitBucket Sign on URL where you can initiate the login flow.
- Go to EasySSO for BitBucket Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the EasySSO for BitBucket for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the EasySSO for BitBucket tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the EasySSO for BitBucket for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).