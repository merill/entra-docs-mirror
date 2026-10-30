---
layout: Conceptual
title: Configure Cloud Academy for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/cloud-academy-sso-tutorial
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
description: In this article,  you learn how to configure single sign-on between Microsoft Entra ID and Cloud Academy.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: d2a6e8fc-309b-db17-5516-504ede1277b1
document_version_independent_id: b9a6df04-1d95-e040-ad4d-41a849858875
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/cloud-academy-sso-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/cloud-academy-sso-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/cloud-academy-sso-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b06bce0a-e2ac-a311-66b0-b404b05e169e
---

# Configure Cloud Academy for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Cloud Academy with Microsoft Entra ID. When you integrate Cloud Academy with Microsoft Entra ID, you can:

- Use Microsoft Entra ID to control who can access Cloud Academy.
- Enable your users to be automatically signed in to Cloud Academy with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Cloud Academy subscription with single sign-on (SSO) enabled.

## Article description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Cloud Academy supports **SP** initiated SSO.
- Cloud Academy supports **Just In Time** user provisioning.
- Cloud Academy supports [Automated user provisioning](cloud-academy-sso-provisioning-tutorial).

## Add Cloud Academy from the gallery

To configure the integration of Cloud Academy into Microsoft Entra ID, you need to add Cloud Academy from the gallery to your list of managed SaaS apps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **Cloud Academy** in the search box.
4. Select **Cloud Academy** in the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Cloud Academy

You'll configure and test Microsoft Entra SSO with Cloud Academy by using a test user named **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the corresponding user in Cloud Academy.

To configure and test Microsoft Entra SSO with Cloud Academy, you complete these high-level steps:

1. **Configure Microsoft Entra SSO**to enable your users to use the feature.
    1. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on.
    2. **Grant access to the test user** to enable the user to use Microsoft Entra single sign-on.
2. **Configure single sign-on for Cloud Academy**on the application side.
    1. **Create a Cloud Academy test user** as a counterpart to the Microsoft Entra representation of the user.
3. **Test SSO** to verify that the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Azure portal:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Cloud Academy** application integration page, in the **Manage** section, select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil button for **Basic SAML Configuration** to edit the settings:

    ![Screenshot that shows the pencil button for editing the basic SAML configuration.](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, update the **Identifier** text box, type the following URLs and proceed:

    | Identifier |
    | --- |
    | `urn:federation:cloudacademy` |
6. In the **Basic SAML Configuration** section, update the **Reply URL** text box, type one of the following URLs and proceed:

    | Reply URL |
    | --- |
    | `https://cloudacademy.com/labs/social/complete/saml/` |
    | `https://app.qa.com/labs/social/complete/saml/` |
7. In the **Basic SAML Configuration** section, update the **Sign-on URL** text box, type one of the following URLs and save it:

    | Sign-on URL |
    | --- |
    | `https://cloudacademy.com/login/enterprise/` |
    | `https://app.qa.com/login/enterprise/` |
8. Select the pencil button for **SAML Signing Certificate** to edit the settings:

    ![Screenshot that shows how to edit the certificate.](common/edit-certificate.png)
9. Download the **PEM certificate**:

    ![Screenshot that shows how to download the P E M certificate.](common/certificate-base64-download.png)
10. On the **Set up Cloud Academy** section, copy the **Login URL**:

    ![Screenshot that shows the copy button for the login U R L.](common/copy_configuration_urls.png)

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

### Grant access to the test user

In this section, you enable B.Simon to use Azure single sign-on by granting that user access to Cloud Academy.

1. Browse to **Entra ID** &gt; **Enterprise apps**.
2. In the applications list, select **Cloud Academy**.
3. On the app's overview page, in the **Manage** section, select **Users and groups**:
4. Select **Add user**, and then select **Users and groups** in the **Add Assignment** dialog box:
5. In the **Users and groups** dialog box, select **B.Simon** in the **Users** list, and then select the **Select** button at the bottom of the screen.
6. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
7. In the **Add Assignment** dialog box, select **Assign**.

## Configure single sign-on for Cloud Academy

1. In a different browser window, sign in to your Cloud Academy company site as administrator.
2. On the home page, select the **Azure Integration Team** icon, and then select **Settings** in the left menu.
3. On the **INTEGRATIONS** tab, select the **SSO** card.

    ![Screenshot that shows the Settings &amp; Integrations option.](media/cloud-academy-sso-tutorial/integrations.png)
4. Select **Start Configuring** to set up SSO.
5. On the **General Settings** page, complete the following steps:

    ![Screenshot that shows integrations in general settings.](media/cloud-academy-sso-tutorial/general-settings.png)

    1. In the **SSO URL (Location)** box, paste the login URL value that you copied, in step 9 of Configure Microsoft Entra SSO.
    2. Open the downloaded Base64 certificate in Notepad. Paste its contents into the **Certificate** box.
6. Perform the following steps in the below page:

    ![Screenshot that shows the Integrations in additional settings.](media/cloud-academy-sso-tutorial/additional-settings.png)

    1. In the **SAML Attributes Mapping** section, fill in the required fields with the source attribute values:

        `http://schemas.microsoft.com/identity/claims/objectidentifier``http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname``http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname``http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`
    2. In the **Security Settings** section, select the **Authentication Requests Signed?** check box to set this value to **True**.
    3. In the **Extra Settings(Optional)** section, fill the **Logout URL** box with the logout URL value that you copied, in step 9 of Configure Microsoft Entra SSO.
7. Select **Save and Test**.
8. Next, a dialog shows the service provider information. Download the XML file:

    ![Screenshot that shows downloading the metadata configuration file.](media/cloud-academy-sso-tutorial/set-up-provider-information.png)
9. Now that you have the XML file of the service provider, go back to the application you created. In the **Single sign-on** section, upload the metadata file:

    ![Screenshot that shows uploading the metadata in the Azure application.](media/cloud-academy-sso-tutorial/upload-metadata.png)
10. Now that you've updated the service provider metadata, you can go back to the SSO panel of your Cloud Academy company site and proceed with the test and activation. In the service provider dialog, select **Continue**:

    ![Screenshot that shows the service provider dialog.](media/cloud-academy-sso-tutorial/continue-sso-activation.png)
11. Select **Test SSO connection** to start the test flow:

    ![Screenshot that shows the Test S S O connection button.](media/cloud-academy-sso-tutorial/test-sso-connection.png)

    Note

    If you're signed in to Cloud Academy by using the test user account you created, proceed with the test flow. Otherwise, close the dialog, scroll up to **General Settings**, copy and paste the subdomain URL in a private or incognito browser tab, and then sign in as the test user. If sign-in is successful, you can close the browser tab and select **Save and Test**. A browser tab will reopen the service provider dialog. Select **continue**, and then select **Test SSO connection** again. Finally, select **Test was successful** because you've already tested sign-in by using a private or incognito tab.

    Continue to the next step.
12. If sign-in is successful, you can activate SSO integration for the entire organization:

    ![Screenshot that shows S S O activation is successful.](media/cloud-academy-sso-tutorial/test-successful.png)

Note

For more information about how to configure Cloud Academy, see [Setting Up Single Sign-On](https://support.cloudacademy.com/hc/articles/360043908452-Setting-Up-Single-Sign-On).

### Create a Cloud Academy test user

In this section, a user called B.Simon is created in Cloud Academy. Cloud Academy supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Cloud Academy, a new one is created after authentication.

Cloud Academy also supports automatic user provisioning. For more information, see the [Cloud Academy SSO provisioning article](cloud-academy-sso-provisioning-tutorial).

## Test SSO

In this section, you test your Microsoft Entra SSO configuration by using one of the following options:

- In the Azure portal, select **Test this application**. You're redirected to the Cloud Academy sign-on URL and you can initiate the sign-in flow.
- Go to Cloud Academy sign-on URL directly and initiate the sign-in flow from there.
- You can use Microsoft My Apps. When you select the Cloud Academy tile in the My Apps portal, this option redirects to Cloud Academy sign-on URL. For more information about the My Apps portal, see [Introduction to My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).