---
layout: Conceptual
title: Configure Periscope Data for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/periscope-data-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Periscope Data.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 42057efd-eae5-3129-4d14-f7f8b710f5e0
document_version_independent_id: a6426fe6-07f3-0752-e244-d739993a9267
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/periscope-data-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/periscope-data-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/periscope-data-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0e3de108-111d-82a1-73a3-fc5dd8b05552
---

# Configure Periscope Data for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Periscope Data with Microsoft Entra ID. When you integrate Periscope Data with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Periscope Data.
- Enable your users to be automatically signed-in to Periscope Data with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Periscope Data single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Periscope Data supports **SP** initiated SSO.

## Add Periscope Data from the gallery

To configure the integration of Periscope Data into Microsoft Entra ID, you need to add Periscope Data from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Periscope Data** in the search box.
4. Select **Periscope Data** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Periscope Data

Configure and test Microsoft Entra SSO with Periscope Data using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Periscope Data.

To configure and test Microsoft Entra SSO with Periscope Data, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Periscope Data SSO**- to configure the single sign-on settings on application side.
    1. **Create Periscope Data test user** - to have a counterpart of B.Simon in Periscope Data that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Periscope Data** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://app.periscopedata.com/<SITENAME>/sso`

    b. In the **Sign on URL** text box, type a URL using one of the following patterns:

    | **Sign on URL** |
    | --- |
    | `https://app.periscopedata.com/` |
    | `https://app.periscopedata.com/app/<SITENAME>` |

    Note

    The Sign on URL value isn't real. Update the values with the actual Sign on URL. Contact [Periscope Data Client support team](mailto:support@periscopedata.com) to get this value and the Identifier value you get from the **Configure Periscope Data Single Sign-On** section which is explained later in the article. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Periscope Data SSO

1. In a different web browser window, sign in to Periscope Data as an Administrator.
2. Open the gear menu in the bottom left and open the **Billing** &gt; **Security** menu and perform the following steps. Only admins have access to these settings.

    ![Screenshot that shows the &quot;Security&quot; dialog with selected settings.](media/periscope-data-tutorial/settings.png)

    a. Copy the **App Federation Metadata URL** from step #5 **SAML Signing Certificate** and open it in a browser. This will open up an XML document.

    b. In the **Single Sign-On** textbox, select **Microsoft Entra ID**.

    c. Find the tag **SingleSignOnService** and paste the **Location** value in the **SSO URL** textbox.

    d. Find the tag **SingleLogoutService** and paste the **Location** value in the **SLO URL** textbox.

    e. Copy the **Identifier** value for your instance and paste it in **Identifier (Entity ID)** textbox of **Basic SAML Configuration** section.

    f. Find the first tag of the XML file, copy the value of **entityID** and paste it in the **Issuer** textbox.

    g. Find the tag **IDPSSODescriptor** with SAML protocol. Within that section, find the tag **KeyDescriptor** with **use=signing**. copy the value of **X509Certificate** and paste it in the **Certificate** textbox.

    h. Sites with multiple spaces can choose the default space from the **Default Space** drop down. This are the space new users get added to when they log in to Periscope Data for the first time and are provisioned through the Active Directory Single Sign On.

    i. Finally, select **Save** and **confirm** the SSO settings change by typing **Logout**.

    ![Screenshot that shows the &quot;Update S S O Configuration&quot; dialog with &quot;logout&quot; typed in the textbox and the &quot;Confirm&quot; button selected.](media/periscope-data-tutorial/configure.png)

### Create Periscope Data test user

To enable Microsoft Entra users to log in to Periscope Data, they must be provisioned into Periscope Data. In Periscope Data, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Log in to Periscope Data as an Administrator.
2. Select the **Settings** icon on the left bottom of the menu and navigate to **Permissions**.

    ![Screenshot that shows the &quot;Settings&quot; menu with &quot;Permissions&quot; selected.](media/periscope-data-tutorial/menu.png)
3. Select the **ADD USER** and perform the following steps:

    ![Periscope Data Configure information](media/periscope-data-tutorial/user.png)

    a. In **First Name** text box, enter the first name of user like **Britta**.

    b. In **Last Name** text box, enter the last name of user like **Simon**.

    c. In **Email** text box, enter the email of user like **brittasimon@contoso.com**.

    d. Select **ADD**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Periscope Data Sign-on URL where you can initiate the login flow.
- Go to Periscope Data Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Periscope Data tile in the My Apps, this option redirects to Periscope Data Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).