---
layout: Conceptual
title: Configure Questetra BPM Suite for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/questetra-bpm-suite-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Questetra BPM Suite.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 7658c481-3e4a-68fe-86ac-9c68a711e696
document_version_independent_id: 59bf708f-d81b-8c76-604c-cfbd943c9725
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/questetra-bpm-suite-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/questetra-bpm-suite-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/questetra-bpm-suite-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c0776266-ac3a-7777-29d0-44efdbba98f7
---

# Configure Questetra BPM Suite for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Questetra BPM Suite with Microsoft Entra ID. When you integrate Questetra BPM Suite with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Questetra BPM Suite.
- Enable your users to be automatically signed-in to Questetra BPM Suite with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Questetra BPM Suite single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Questetra BPM Suite supports **SP** initiated SSO.

## Add Questetra BPM Suite from the gallery

To configure the integration of Questetra BPM Suite into Microsoft Entra ID, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Questetra BPM Suite** in the search box.
4. Select **Questetra BPM Suite** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Questetra BPM Suite

Configure and test Microsoft Entra SSO with Questetra BPM Suite using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Questetra BPM Suite.

To configure and test Microsoft Entra SSO with Questetra BPM Suite, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Questetra BPM Suite SSO**- to configure the single sign-on settings on application side.
    1. **Create Questetra BPM Suite test user** - to have a counterpart of B.Simon in Questetra BPM Suite that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Questetra BPM Suite** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<subdomain>.questetra.net/`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://<subdomain>.questetra.net/saml/SSO/alias/bpm`

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. You can get these values from **SP Information** section on your **Questetra BPM Suite** company site, which is explained later in the article or contact [Questetra BPM Suite Client support team](https://support.questetra.com/support-service/). You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Questetra BPM Suite** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Questetra BPM Suite SSO

1. In a different web browser window, Sign in to your **Questetra BPM Suite** company site as an administrator.
2. In the menu on the top, select **System Settings**.

    ![Screenshot shows System Settings selected from your Questetra BPM Suite company site.](media/questetra-bpm-suite-tutorial/settings.png)
3. To open the **SingleSignOnSAML** page, select **SSO (SAML)**.

    ![Screenshot shows S S O (SAML) selected.](media/questetra-bpm-suite-tutorial/apps.png)
4. On your **Questetra BPM Suite** company site, in the **SP Information** section, perform the following steps:

    a. Copy the **ACS URL**, and then paste it into the **Sign On URL** textbox in the **Basic SAML Configuration** section from Azure portal.

    b. Copy the **Entity ID**, and then paste it into the **Identifier** textbox in the **Basic SAML Configuration** section from Azure portal.
5. On your **Questetra BPM Suite** company site, perform the following steps:

    ![Configure Single Sign-On](media/questetra-bpm-suite-tutorial/certificate.png)

    a. Select **Enable Single Sign-On**.

    b. In **Entity ID** textbox, paste the value of **Microsoft Entra Identifier**..

    c. In **Sign-in page URL** textbox, paste the value of **Login URL**..

    d. In **Sign-out page URL** textbox, paste the value of **Logout URL**..

    e. In the **NameID format** textbox, type `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`.

    f. Open your **Base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.

    g. Select **Save**.

### Create Questetra BPM Suite test user

The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.

**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**

1. Sign in to your Questetra BPM Suite company site as an administrator.
2. Go to **System Settings &gt; User List &gt; New User**.
3. On the New User dialog, perform the following steps:

    ![Create test user](media/questetra-bpm-suite-tutorial/users.png)

    a. In the **Name** textbox, type **name** of the user britta.simon@contoso.com.

    b. In the **Email** textbox, type **email** of the user britta.simon@contoso.com.

    c. In the **Password** textbox, type a **password** of the user.

    d. Select **Add new user**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Questetra BPM Suite Sign-on URL where you can initiate the login flow.
- Go to Questetra BPM Suite Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Questetra BPM Suite tile in the My Apps, this option redirects to Questetra BPM Suite Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).