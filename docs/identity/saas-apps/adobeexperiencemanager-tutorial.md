---
layout: Conceptual
title: Configure Adobe Experience Manager for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/adobeexperiencemanager-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Adobe Experience Manager.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3380548b-9803-be28-3d45-02ec6f1388b8
document_version_independent_id: 8c50bb05-c519-7cc7-ab37-195e613212f6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/adobeexperiencemanager-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/adobeexperiencemanager-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/adobeexperiencemanager-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2a9107fe-e2b3-d757-f1d9-4296f4c06085
---

# Configure Adobe Experience Manager for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Adobe Experience Manager with Microsoft Entra ID. When you integrate Adobe Experience Manager with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Adobe Experience Manager.
- Enable your users to be automatically signed-in to Adobe Experience Manager with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Adobe Experience Manager single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Adobe Experience Manager supports **SP and IDP** initiated SSO
- Adobe Experience Manager supports **Just In Time** user provisioning

## Adding Adobe Experience Manager from the gallery

To configure the integration of Adobe Experience Manager into Microsoft Entra ID, you need to add Adobe Experience Manager from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Adobe Experience Manager** in the search box.
4. Select **Adobe Experience Manager** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Adobe Experience Manager

Configure and test Microsoft Entra SSO with Adobe Experience Manager using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Adobe Experience Manager.

To configure and test Microsoft Entra SSO with Adobe Experience Manager, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Adobe Experience Manager SSO**- to configure the Single Sign-On settings on application side.
    1. **Create Adobe Experience Manager test user** - to have a counterpart of Britta Simon in Adobe Experience Manager that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Adobe Experience Manager** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type a unique value that you define on your AEM server as well.

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<AEM Server Url>/saml_login`

    Note

    The Reply URL value isn't real. Update Reply URL value with the actual reply URL. To get this value, contact the [Adobe Experience Manager Client support team](https://helpx.adobe.com/support/experience-manager.html) to get this value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type your Adobe Experience Manager server URL.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
8. On the **Set up Adobe Experience Manager** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Adobe Experience Manager SSO

1. In another browser window, open the **Adobe Experience Manager** admin portal.
2. Select **Settings** &gt; **Security** &gt; **Users**.

    ![Screenshot that shows the Users tile in the Adobe Experience Manager.](media/adobe-experience-manager-tutorial/user.png)
3. Select **Administrator** or any other relevant user.
4. Select **Account settings** &gt; **Manage TrustStore**.

    ![Screenshot that shows Manage TrustStore under Account settings.](media/adobe-experience-manager-tutorial/manage-trust.png)
5. Under **Add Certificate from CER file**, select **Select Certificate File**. Browse to and select the certificate file, which you already downloaded.

    ![Screenshot that highlights the Select Certificate File button.](media/adobe-experience-manager-tutorial/certificate-file.png)
6. The certificate is added to the TrustStore. Note the alias of the certificate.

    ![Screenshot that shows that the certificate is added to the TrustStore.](media/adobe-experience-manager-tutorial/trust-store.png)
7. On the **Users** page, select **authentication-service**.

    ![Screenshot that highlights authentication-service on the screen.](media/adobe-experience-manager-tutorial/authentication-service.png)
8. Select **Account settings** &gt; **Create/Manage KeyStore**. Create KeyStore by supplying a password.

    ![Screenshot that highlights Manage KeyStore.](media/adobe-experience-manager-tutorial/manage-key-store.png)
9. Go back to the admin screen. Then select **Settings** &gt; **Operations** &gt; **Web Console**.

    ![Screenshot that highlights Web Console under Operations within the Settings section.](media/adobe-experience-manager-tutorial/web-console.png)

    This opens the configuration page.

    ![Configure the single sign-on save button.](media/adobe-experience-manager-tutorial/configuration-page.png)
10. Find **Adobe Granite SAML 2.0 Authentication Handler**. Then select the **Add** icon.

    ![Screenshot that highlights Adobe Granite SAML 2.0 Authentication Handler.](media/adobe-experience-manager-tutorial/saml-handler.png)
11. Take the following actions on this page.

    ![Screenshot shows for Configure Single Sign-On Save button.](media/adobe-experience-manager-tutorial/adobe-configuration.png)

    a. In the **Path** box, enter **/**.

    b. In the **IDP URL** box, enter the **Login URL** value that you copied.

    c. In the **IDP Certificate Alias** box, enter the **Certificate Alias** value that you added in TrustStore.

    d. In the **Security Provided Entity ID** box, enter the unique **Microsoft Entra Identifier** value that you configured.

    e. In the **Assertion Consumer Service URL** box, enter the **Reply URL** value that you configured.

    f. In the **Password of Key Store** box, enter the **Password** that you set in KeyStore.

    g. In the **User Attribute ID** box, enter the **Name ID** or another user ID that's relevant in your case.

    h. Select **Autocreate CRX Users**.

    i. In the **Logout URL** box, enter the unique **Logout URL** value that you got.

    j. Select **Save**.
12. In **Apache Sling Referrer Filter** section, perform the below steps:

    ![Screenshot shows for Sling Referrer Filter.](media/adobe-experience-manager-tutorial/allow-host.png)

    a. Ensure **allow.empty** value is set to true.

    b. Add `login.microsoftonline.com` to the **Allow Hosts**.

    c. Select **Save**.

### Create Adobe Experience Manager test user

In this section, you create a user called Britta Simon in Adobe Experience Manager. If you selected the **Autocreate CRX Users** option, users are created automatically after successful authentication.

If you want to create users manually, work with the [Adobe Experience Manager support team](https://helpx.adobe.com/support/experience-manager.html) to add the users in the Adobe Experience Manager platform.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Adobe Experience Manager Sign-on URL where you can initiate the login flow.
- Go to Adobe Experience Manager Sign on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Adobe Experience Manager for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the Adobe Experience Manager tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Adobe Experience Manager for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).