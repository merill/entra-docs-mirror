---
layout: Conceptual
title: Configure Tableau Cloud for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/tableauonline-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Tableau Cloud.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: cbfa13a7-4d2d-b203-d7fa-760833a745cb
document_version_independent_id: 72ff67dc-732d-478e-1595-9d4bd6737714
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/tableauonline-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/tableauonline-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/tableauonline-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 28a2adaa-13ff-ca76-439b-870217764a17
---

# Configure Tableau Cloud for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Tableau Cloud with Microsoft Entra ID. When you integrate Tableau Cloud with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Tableau Cloud.
- Enable your users to be automatically signed-in to Tableau Cloud with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Tableau Cloud is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Tableau Cloud single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Tableau Cloud supports **SP** initiated SSO.
- Tableau Cloud supports [**automated user provisioning and deprovisioning**](tableau-online-provisioning-tutorial) (recommended).

## Add Tableau Cloud from the gallery

To configure the integration of Tableau Cloud into Microsoft Entra ID, you need to add Tableau Cloud from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Tableau Cloud** in the search box.
4. Select **Tableau Cloud** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Tableau Cloud

In this section, you configure and test Microsoft Entra single sign-on with Tableau Cloud based on a test user called **Britta Simon**. For single sign-on to work, a link relationship between a Microsoft Entra user and the related user in Tableau Cloud needs to be established.

To configure and test Microsoft Entra SSO with Tableau Cloud, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Tableau Cloud SSO**- to configure the single sign-on settings on application side.
    1. **Create Tableau Cloud test user** - to have a counterpart of B.Simon in Tableau Cloud that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Tableau Cloud** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://sso.online.tableau.com/public/sp/metadata?alias=<entityid>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://sso.online.tableau.com/public/sp/<CUSTOM_URL>`

    c. In the **Sign on URL** text box, type the URL: `https://sso.online.tableau.com`

    Note

    You get the `<entityid>` value from the **Set up Tableau Cloud** section in this article. The entity ID value is **Microsoft Entra identifier** value in **Set up Tableau Cloud** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Tableau Cloud** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Tableau Cloud SSO

1. In a different web browser window, sign in to your up Tableau Cloud company site as an administrator
2. Go to **Settings** and then **Authentication**.

    ![Screenshot shows Authentication selected from the Settings menu.](media/tableauonline-tutorial/menu.png)
3. To enable SAML, Under **Authentication types** section. Check **Enable an additional authentication method** and then check **SAML** checkbox.

    ![Screenshot shows the Authentication types section where you can select the values.](media/tableauonline-tutorial/authentication.png)
4. Scroll down up to **Import metadata file into Tableau Cloud** section. Select Browse and import the metadata file, which you have downloaded from Microsoft Entra ID. Then, select **Apply**.

    ![Screenshot shows the section where you can import the metadata file.](media/tableauonline-tutorial/metadata.png)
5. In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**. To get this information from Microsoft Entra ID:

    a. In the Azure portal, go on the **Tableau Cloud** application integration page.

    b. In the **User Attributes & Claims** section, select the edit icon, perform the following steps to add SAML token attribute as shown in the below table:

    ![Screenshot shows the User Attributes &amp; Claims section where you can select the edit icon.](media/tableauonline-tutorial/attribute-section.png)

    | Name | Source Attribute |
    | --- | --- |
    | DisplayName | user.displayname |

    c. Copy the namespace value for these attributes: givenname, email and surname by using the following steps:

    ![Screenshot shows the Givenname, Surname, and Emailaddress attributes.](media/tableauonline-tutorial/name.png)

    d. Select **user.givenname** value

    e. Copy the value from the **Namespace** and **Claim name** textbox.

    ![Screenshot shows the Manage user claims section where you can enter the Namespace.](media/tableauonline-tutorial/attributes.png)

    f. To copy the namespace values for the email and surname repeat the above steps.

    g. Switch to the Tableau Cloud application, then set the **User Attributes & Claims** section as follows:

    - Email: **mail** or **userprincipalname**
    - Full name: **displayname**

    ![Screenshot shows the Match attributes section where you can enter the values.](media/tableauonline-tutorial/claims.png)

### Create Tableau Cloud test user

In this section, you create a user called Britta Simon in Tableau Cloud.

1. On **Tableau Cloud**, select **Settings** and then **Authentication** section. Scroll down to **Manage Users** section. Select **Add Users** and then select **Enter Email Addresses**.

    ![Screenshot shows the Manage users section where you can select Add users.](media/tableauonline-tutorial/users.png)
2. Select **Add users for (SAML) authentication**. In the **Enter email addresses** textbox add britta.simon@contoso.com

    ![Screenshot shows the Add Users page where you can enter an email address.](media/tableauonline-tutorial/add-users.png)
3. Select **Add Users**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Tableau Cloud Sign-on URL where you can initiate the login flow.
- Go to Tableau Cloud Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Tableau Cloud tile in the My Apps, this option redirects to Tableau Cloud Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).