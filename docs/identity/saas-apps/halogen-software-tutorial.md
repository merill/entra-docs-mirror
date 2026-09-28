---
layout: Conceptual
title: Configure Saba TalentSpace for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/halogen-software-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Saba TalentSpace.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5827cc51-b2f0-0f78-fc72-daeb8b2a88d6
document_version_independent_id: 877e9862-42d1-1f27-3e75-389f0bb8a2bc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/halogen-software-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/halogen-software-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/halogen-software-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3db6731c-8b36-cc3e-3604-e9558be9d215
---

# Configure Saba TalentSpace for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Saba TalentSpace with Microsoft Entra ID. When you integrate Saba TalentSpace with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Saba TalentSpace.
- Enable your users to be automatically signed-in to Saba TalentSpace with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Saba TalentSpace single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Saba TalentSpace supports **SP** initiated SSO

## Add Saba TalentSpace from the gallery

To configure the integration of Saba TalentSpace into Microsoft Entra ID, you need to add Saba TalentSpace from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Saba TalentSpace** in the search box.
4. Select **Saba TalentSpace** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Saba TalentSpace

Configure and test Microsoft Entra SSO with Saba TalentSpace using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Saba TalentSpace.

To configure and test Microsoft Entra SSO with Saba TalentSpace, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    - **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    - **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Saba TalentSpace SSO**- to configure the single sign-on settings on application side.
    - **Create Saba TalentSpace test user** - to have a counterpart of B.Simon in Saba TalentSpace that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Saba TalentSpace** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign on URL** text box, type the URL using the following pattern: `https://global.hgncloud.com/<COMPANY_NAME>/saml/login`

    b. In the **Identifier (Entity ID)** text box, type the URL using the following pattern: `https://global.hgncloud.com/<COMPANY_NAME>/saml/metadata`

    c. In the **Reply URL (Assertion Consumer Service URL)** text box, type the URL using the following pattern: `https://global.hgncloud.com/<COMPANY_NAME>/saml/SSO`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact [Saba TalentSpace Client support team](https://support.saba.com/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Saba TalentSpace** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

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

In this section, you enable B.Simon to use single sign-on by granting access to Saba TalentSpace.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Saba TalentSpace**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure Saba TalentSpace SSO

1. In a different browser window, sign-on to your **Saba TalentSpace** application as an administrator.
2. Select the **Options** tab.

    ![Screenshot that shows the &quot;saba TalentSpace&quot; home page with the &quot;Options&quot; tab selected.](media/halogen-software-tutorial/tutorial-halogen-12.png)
3. In the left navigation pane, select **SAML Configuration**.

    ![Screenshot that shows the &quot;User Interface&quot; left navigation pane with &quot;S A M L Configuration&quot; selected.](media/halogen-software-tutorial/tutorial-halogen-13.png)
4. On the **SAML Configuration** page, perform the following steps:

    ![Screenshot that shows the &quot;S A M L Configuration&quot; page with the &quot;Settings&quot; options highlighted.](media/halogen-software-tutorial/tutorial-halogen-14.png)

    a. As **Unique Identifier**, select **NameID**.

    b. As **Unique Identifier Maps To**, select **Username**, **Email Address**, or **Employee ID**. This is the field that needs to match with the Azure primary attribute.

    c. To upload your downloaded metadata file, select **Browse** to select the file, and then **Upload File**.

    d. To test the configuration, select **Run Test**.

    Note

    You need to wait for the message "*The SAML test is complete. Please close this window*". Then, close the opened browser window. The **Enable SAML** checkbox is only enabled if the test has been completed.

    e. Select **Enable SAML**.

    f. Select **Save Changes**.

### Create Saba TalentSpace test user

The objective of this section is to create a user called Britta Simon in Saba TalentSpace.

**To create a user called Britta Simon in Saba TalentSpace, perform the following steps:**

1. Sign on to your **Saba TalentSpace** application as an administrator.
2. Select the **User Center** tab, and then select **Create User**.

    ![Screenshot that shows the &quot;User Center&quot; tab and &quot;Create User&quot; selected.](media/halogen-software-tutorial/tutorial-halogen-300.png)
3. On the **New User** dialog page, perform the following steps:

    ![What is Microsoft Entra Connect](media/halogen-software-tutorial/tutorial-halogen-301.png)

    a. In the **First Name** textbox, type first name of the user like **B**.

    b. In the **Last Name** textbox, type last name of the user like **Simon**.

    c. In the **Username** textbox, type **B.Simon**, the user name as.

    d. In the **Password** textbox, type a password for B.Simon.

    e. Select **Save**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Saba TalentSpace Sign-on URL where you can initiate the login flow.
- Go to Saba TalentSpace Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Saba TalentSpace tile in the My Apps, you should be automatically signed in to the Saba TalentSpace for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).