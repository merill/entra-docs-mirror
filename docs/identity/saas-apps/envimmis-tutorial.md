---
layout: Conceptual
title: Configure Envi MMIS for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/envimmis-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Envi MMIS.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9507604e-86a1-e428-b2a0-88cd1ea0c0c7
document_version_independent_id: bbd50568-666d-6104-5a8e-c4a003bf1cfc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/envimmis-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/envimmis-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/envimmis-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0230c43f-0b7e-f17f-6ba6-d537ef642139
---

# Configure Envi MMIS for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Envi MMIS with Microsoft Entra ID. When you integrate Envi MMIS with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Envi MMIS.
- Enable your users to be automatically signed-in to Envi MMIS with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Envi MMIS single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Envi MMIS supports **SP** and **IDP** initiated SSO.

## Add Envi MMIS from the gallery

To configure the integration of Envi MMIS into Microsoft Entra ID, you need to add Envi MMIS from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Envi MMIS** in the search box.
4. Select **Envi MMIS** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Envi MMIS

Configure and test Microsoft Entra SSO with Envi MMIS using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Envi MMIS.

To configure and test Microsoft Entra SSO with Envi MMIS, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Envi MMIS SSO**- to configure the single sign-on settings on application side.
    1. **Create Envi MMIS test user** - to have a counterpart of B.Simon in Envi MMIS that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Envi MMIS** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, If you wish to configure the application in **IDP** initiated mode, perform the following steps:

    1. In the **Identifier** text box, type a URL using the following pattern: `https://www.<CUSTOMER DOMAIN>.com/Account`
    2. In the **Reply URL** text box, type a URL using the following pattern: `https://www.<CUSTOMER DOMAIN>.com/Account/Acs`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://www.<CUSTOMER DOMAIN>.com/Account`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [Envi MMIS Client support team](mailto:support@ioscorp.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set-up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
8. On the **Set up Envi MMIS** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Envi MMIS SSO

1. In a different web browser window, sign into your Envi MMIS site as an administrator.
2. Select **My Domain** tab.

    ![Screenshot that shows the &quot;User&quot; menu with &quot;My Domain&quot; selected.](media/envimmis-tutorial/domain.png)
3. Select **Edit**.

    ![Screenshot that shows the &quot;Edit&quot; button selected.](media/envimmis-tutorial/edit-icon.png)
4. Select **Use remote authentication** checkbox and then select **HTTP Redirect** from the **Authentication Type** dropdown.

    ![Screenshot that shows the &quot;Details&quot; tab with &quot;Use remote authentication&quot; checked and &quot;H T T P Redirect&quot; selected.](media/envimmis-tutorial/details.png)
5. Select **Resources** tab and then select **Upload Metadata**.

    ![Screenshot that shows the &quot;Resources&quot; tab with the &quot;Upload Metadata&quot; action selected.](media/envimmis-tutorial/metadata.png)
6. In the **Upload Metadata** pop-up, perform the following steps:

    ![Screenshot that shows the &quot;Upload Metadata&quot; pop-up with the &quot;File&quot; option selected and the &quot;choose file&quot; icon and &quot;OK&quot; button highlighted.](media/envimmis-tutorial/file.png)

    1. Select **File** option from the **Upload From** dropdown.
    2. Upload the downloaded metadata file from Azure portal by selecting the **choose file icon**.
    3. Select **Ok**.
7. After uploading the downloaded metadata file, the fields gets populated automatically. Select **Update**.

    ![Configure Single Sign-On Save button](media/envimmis-tutorial/fields.png)

### Create Envi MMIS test user

To enable Microsoft Entra users to sign in to Envi MMIS, they must be provisioned into Envi MMIS. In the case of Envi MMIS, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to your Envi MMIS company site as an administrator.
2. Select **User List** tab.

    ![Screenshot that shows the &quot;User&quot; menu with &quot;User List&quot; selected.](media/envimmis-tutorial/list.png)
3. Select **Add User** button.

    ![Screenshot that shows the &quot;Users&quot; section with the &quot;Add User&quot; button selected.](media/envimmis-tutorial/user.png)
4. In the **Add User** section, perform the following steps:

    ![Screenshot that shows to Add Employee.](media/envimmis-tutorial/add-user.png)

    1. In the **User Name** textbox, type the username of Britta Simon account like **brittasimon@contoso.com**.
    2. In the **First Name** textbox, type the first name of BrittaSimon like **Britta**.
    3. In the **Last Name** textbox, type the last name of BrittaSimon like **Simon**.
    4. Enter the Title of the user in the **Title** of the textbox.
    5. In the **Email Address** textbox, type the email address of Britta Simon account like **brittasimon@contoso.com**.
    6. In the **SSO User Name** textbox, type the username of Britta Simon account like **brittasimon@contoso.com**.
    7. Select **Save**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Envi MMIS Sign on URL where you can initiate the login flow.
- Go to Envi MMIS Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Envi MMIS for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Envi MMIS tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Envi MMIS for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).