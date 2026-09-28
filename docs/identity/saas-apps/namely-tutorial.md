---
layout: Conceptual
title: Configure Namely for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/namely-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Namely.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: fbab62a2-fe46-8aba-1ada-d4dfc70217e5
document_version_independent_id: 1b0be877-ede9-1d86-1345-cf202044e581
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/namely-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/namely-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/namely-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 02569bd4-dece-57b0-1284-56bc65370234
---

# Configure Namely for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Namely with Microsoft Entra ID. When you integrate Namely with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Namely.
- Enable your users to be automatically signed-in to Namely with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Namely single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Namely supports **SP** initiated SSO.

## Add Namely from the gallery

To configure the integration of Namely into Microsoft Entra ID, you need to add Namely from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Namely** in the search box.
4. Select **Namely** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Namely

Configure and test Microsoft Entra SSO with Namely using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Namely.

To configure and test Microsoft Entra SSO with Namely, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Namely SSO**- to configure the single sign-on settings on application side.
    1. **Create Namely test user** - to have a counterpart of B.Simon in Namely that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Namely** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<subdomain>.namely.com`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<subdomain>.namely.com/saml/metadata`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact [Namely Client support team](https://www.namely.com/contact/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Namely** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Namely SSO

1. In another browser window, sign on to your Namely company site as an administrator.
2. In the toolbar on the top, select **Company**.

    ![Screenshot shows the Company value selected.](media/namely-tutorial/company.png)
3. Select the **Settings** tab.

    ![Screenshot shows the Company Settings tab selected.](media/namely-tutorial/settings.png)
4. Select **SAML**.

    ![Screenshot shows SAML selected.](media/namely-tutorial/general.png)
5. On the **SAML Settings** page, perform the following steps:

    ![Screenshot shows SAML Settings where you can enter the values described.](media/namely-tutorial/settings-page.png)

    a. Select **Enable SAML**.

    b. In the **Identity provider SSO url** textbox, paste the value of **Login URL**.

    c. Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.

    d. Select **Save**.

### Create Namely test user

The objective of this section is to create a user called Britta Simon in Namely.

**To create a user called Britta Simon in Namely, perform the following steps:**

1. Sign-on to your Namely company site as an administrator.
2. In the toolbar on the top, select **People**.

    ![Screenshot shows the People value selected.](media/namely-tutorial/people.png)
3. Select the **Directory** tab.

    ![Screenshot shows the People Directory tab selected.](media/namely-tutorial/directory.png)
4. Select **Add New Person**.

    ![Screenshot shows the Add New Person option.](media/namely-tutorial/add-person.png)
5. On the **Add New Person** dialog, perform the following steps:

    a. In the **First name** textbox, type **Britta**.

    b. In the **Last name** textbox, type **Simon**.

    c. In the **Email** textbox, type the **email address** of BrittaSimon.

    d. Select **Save**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Namely Sign-on URL where you can initiate the login flow.
- Go to Namely Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Namely tile in the My Apps, this option redirects to Namely Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).