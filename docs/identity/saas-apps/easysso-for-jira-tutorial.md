---
layout: Conceptual
title: Configure EasySSO for Jira for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/easysso-for-jira-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and EasySSO for Jira.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 41583a7e-864e-a476-27fb-8cee8619ef0d
document_version_independent_id: c1c6cf37-1f85-9db2-0391-96e6b2521314
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/easysso-for-jira-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/easysso-for-jira-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/easysso-for-jira-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f16a901e-5f08-9e49-bd9f-847dd508e009
---

# Configure EasySSO for Jira for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate EasySSO for Jira with Microsoft Entra ID. When you integrate EasySSO for Jira with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Jira.
- Enable your users to be automatically signed-in to Jira with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- EasySSO for Jira single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- EasySSO for Jira supports **SP and IDP** initiated SSO.
- EasySSO for Jira supports **Just In Time** user provisioning.

## Add EasySSO for Jira from the gallery

To configure the integration of EasySSO for Jira into Microsoft Entra ID, you need to add EasySSO for Jira from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **EasySSO for Jira** in the search box.
4. Select **EasySSO for Jira** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for EasySSO for Jira

Configure and test Microsoft Entra SSO with EasySSO for Jira using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in EasySSO for Jira.

To configure and test Microsoft Entra SSO with EasySSO for Jira, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure EasySSO for Jira SSO**- to configure the single sign-on settings on application side.
    1. **Create EasySSO for Jira test user** - to have a counterpart of B.Simon in EasySSO for Jira that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **EasySSO for Jira** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/easysso/saml`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/easysso/saml`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<server-base-url>/login.jsp`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [EasySSO support team](mailto:support@techtime.co.nz) to get these values if in doubt. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. EasySSO for Jira application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, EasySSO for Jira application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | urn:oid:0.9.2342.19200300.100.1.1 | user.userprincipalname |
    | urn:oid:0.9.2342.19200300.100.1.3 | user.mail |
    | urn:oid:2.16.840.1.113730.3.1.241 | user.displayname |
    | urn:oid:2.5.4.4 | user.surname |
    | urn:oid:2.5.4.42 | user.givenname |

    In case your Microsoft Entra users have **sAMAccountName** configured you would have to map **urn:oid:0.9.2342.19200300.100.1.1** onto **sAMAccountName** attribute.
9. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select **Download** links for **Certificate (Base64)** or **Federation Metadata XML** options and save either or all to your computer. You need it later to configure Jira EasySSO.

    ![The Certificate download link](media/easysso-for-jira-tutorial/azure-ad-saml-certificate.png)

    If you plan to perform EasySSO for Jira configuration manually with certificate, you also need to copy **Login URL** and **Microsoft Entra Identifier** from the section below and save those on your computer.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure EasySSO for Jira SSO

1. Sign into your Atlassian Jira instance with Administrator privileges and navigate to the **Manage Apps** section.

    ![Manage Apps](media/easysso-for-jira-tutorial/jira-admin-1.png)
2. On the left side locate **EasySSO** and select it.

    ![Easy SSO](media/easysso-for-jira-tutorial/jira-admin-2.png)
3. Select **SAML** option. This will take you to SAML configuration section.

    ![SAML](media/easysso-for-jira-tutorial/jira-admin-3.png)
4. Select **Certificates** tab on the top and you be presented with the following screen:

    ![Metadata URL](media/easysso-for-jira-tutorial/jira-admin-4.png)
5. Now, locate **Certificate (Base64)** or **Metadata File** you have saved in the earlier steps of **Microsoft Entra SSO** configuration. You have following options on how to proceed:

    a. Use the App Federation **Metadata File** you downloaded to local file on your computer. Select **Upload** radio button and follow the upload file dialog specific to your operating system.

    **OR**

    b. Open the App Federation **Metadata File** to see the content (in any plain text editor) of the file and copy it into the clipboard. Select **Input** option and paste clipboard content into the text field.

    **OR**

    c. Fully manual configuration. Open the App Federation **Certificate (Base64)** to see the content (in any plain text editor) of the file and copy it into the clipboard. Paste it into **IdP Token Signing Certificates** text field. Then navigate to **General** tab and fill **POST Binding URL** and **Entity ID** fields with respective values for **Login URL** and **Microsoft Entra Identifier** you saved previously.
6. Select **Save** button on the bottom of the page. You see the content of the Metadata or Certificate files is parsed into the configuration fields. EasySSO for Jira configuration is complete.
7. For the best testing experience, navigate to **Look & Feel** tab and check the **SAML Login Button** option on. This will enable separate button on the Jira login screen specifically to test your Microsoft Entra SAML integration end to end. You can leave this button on and configure its placement, colour and translation for production mode, too.

    ![Look &amp; Feel](media/easysso-for-jira-tutorial/jira-admin-5.png)

    Note

    Should you have any issues, please contact [EasySSO support team](mailto:support@techtime.co.nz).

### Create EasySSO for Jira test user

In this section, a user called Britta Simon is created in Jira. EasySSO for Jira supports just-in-time user provisioning, which is **disabled** by default. To enable user provisioning, you have to explicitly check **Create user on successful login** option on in the General section of EasySSO plugin configuration. If a user doesn't already exist in Jira, a new one is created after authentication.

However, if you don't wish to enable automatic user provisioning on the user first login, users must exist in backend User Directories the Jira instance make use of, such as LDAP or Atlassian Crowd.

![User provisioning](media/easysso-for-jira-tutorial/jira-admin-6.png)

## Test SSO

### IdP-initiated workflow

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the EasySSO for Jira for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the EasySSO for Jira tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the EasySSO for Jira for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

### SP-initiated workflow

In this section, you test your Microsoft Entra single sign-on configuration using Jira **SAML Login** button.

![User SAML login](media/easysso-for-jira-tutorial/jira-admin-7.png)

This scenario presumes you have enabled **SAML Login Button** in **Look & Feel** tab in your Jira EasySSO configuration page (see above). Open your Jira login URL in browser incognito mode to avoid any interference with your existing sessions. Select **SAML Login** button and you get redirected to Microsoft Entra user authentication flow. Once successfully completed you be redirected back to your Jira instance as authenticated user via SAML.

There's a possibility you may encounter the following screen after getting redirected back from Microsoft Entra ID.

![EasySSO failure screen](media/easysso-for-jira-tutorial/jira-admin-8.png)

In this case you have to follow the [instructions on this page](https://techtime.co.nz/display/TECHTIME/EasySSO+How+to+get+the+logs#EasySSOHowtogetthelogs-RETRIEVINGTHELOGS) to get access to **atlassian-jira.log** file. Details of the error is available by the reference ID found on EasySSO error page.

Should you have any issues digesting the log messages, please contact [EasySSO support team](mailto:support@techtime.co.nz).