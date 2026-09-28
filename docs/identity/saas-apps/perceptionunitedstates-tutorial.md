---
layout: Conceptual
title: Configure UltiPro Perception for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/perceptionunitedstates-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and UltiPro Perception.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 6778ca20-3c9b-b185-cd9c-d98e175ea440
document_version_independent_id: 6fe6136f-fc51-acb3-cea1-640a9b318f52
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/perceptionunitedstates-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/perceptionunitedstates-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/perceptionunitedstates-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 65b66569-c1cf-a417-2598-73d00dd7b1c4
---

# Configure UltiPro Perception for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate UltiPro Perception with Microsoft Entra ID. When you integrate UltiPro Perception with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to UltiPro Perception.
- Enable your users to be automatically signed-in to UltiPro Perception with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- UltiPro Perception single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- UltiPro Perception supports **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add UltiPro Perception from the gallery

To configure the integration of UltiPro Perception into Microsoft Entra ID, you need to add UltiPro Perception from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **UltiPro Perception** in the search box.
4. Select **UltiPro Perception** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for UltiPro Perception

Configure and test Microsoft Entra SSO with UltiPro Perception using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in UltiPro Perception.

To configure and test Microsoft Entra SSO with UltiPro Perception, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure UltiPro Perception SSO**- to configure the single sign-on settings on application side.
    1. **Create UltiPro Perception test user** - to have a counterpart of B.Simon in UltiPro Perception that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **UltiPro Perception** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** page, perform the following steps:

    a. In the **Reply URL** text box, type a URL using the following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`

    b. The **UltiPro Perception** application requires the **Microsoft Entra Identifier** value as &lt;entity\_id&gt;, which you get from the **Set up UltiPro Perception** section, to be URI-encoded. To get the URI-encoded value, use the following link: **http://www.url-encode-decode.com/**.

    c. After getting the URI-encoded value combine it with the **Reply URL** as mentioned below-

    `https://perception.kanjoya.com/sso?idp=<URI encoded entity_id>`

    d. Paste the above value in the **Reply URL** textbox.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up UltiPro Perception** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure UltiPro Perception SSO

1. In another browser window, sign on to your UltiPro Perception company site as an administrator.
2. In the main toolbar, select **Account Settings**.

    ![Screenshot that shows &quot;Account Settings&quot; selected from the main toolbar.](media/perceptionunitedstates-tutorial/user.png)
3. On the **Account Settings** page, perform the following steps:

    ![UltiPro Perception user](media/perceptionunitedstates-tutorial/account.png)

    a. In the **Company Name** textbox, type the name of the **Company**.

    b. In the **Account Name** textbox, type the name of the **Account**.

    c. In **Default Reply-To Email** text box, type the valid **Email**.

    d. Select **SSO Identity Provider** as **SAML 2.0**.
4. On the **SSO Configuration** page, perform the following steps:

    ![UltiPro Perception SSO Configuration.](media/perceptionunitedstates-tutorial/configuration.png)

    a. Select **SAML NameID Type** as **EMAIL**.

    b. In the **SSO Configuration Name** textbox, type the name of your **Configuration**.

    c. In **Identity Provider Name** textbox, paste the value of **Microsoft Entra Identifier**.

    d. In **SAML Domain textbox**, enter the domain like @contoso.com.

    e. Select **Upload Again** to upload the **Metadata XML** file.

    f. Select **Update**.

### Create UltiPro Perception test user

In this section, you create a user called Britta Simon in UltiPro Perception. Work with [UltiPro Perception support team](https://www.ultimatesoftware.com/Contact/ContactUs) to add the users in the UltiPro Perception platform.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the UltiPro Perception for which you set up the SSO.
- You can use Microsoft My Apps. When you select the UltiPro Perception tile in the My Apps, you should be automatically signed in to the UltiPro Perception for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).