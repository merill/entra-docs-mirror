---
layout: Conceptual
title: Configure AnswerHub for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/answerhub-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and AnswerHub.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 66674c27-3fe9-7025-d8c0-2cf24c0e8cde
document_version_independent_id: 234f9b3e-e1d4-04b1-fd29-cf4512b16a8b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/answerhub-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/answerhub-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/answerhub-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 64d9f508-3d94-3a19-d1b4-79155e7178c7
---

# Configure AnswerHub for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate AnswerHub with Microsoft Entra ID. When you integrate AnswerHub with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to AnswerHub.
- Enable your users to be automatically signed-in to AnswerHub with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- AnswerHub single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- AnswerHub supports SP-initiated SSO.

## Add AnswerHub from the gallery

To configure the integration of AnswerHub into Microsoft Entra ID, you need to add AnswerHub from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **AnswerHub** in the search box.
4. Select **AnswerHub** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Set up and test Microsoft Entra SSO for AnswerHub

Configure and test Microsoft Entra SSO with AnswerHub using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in AnswerHub.

To configure and test Microsoft Entra SSO with AnswerHub, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure AnswerHub SSO**- to configure the single sign-on settings on application side.
    1. **Create AnswerHub test user** - to have a counterpart of B.Simon in AnswerHub that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **AnswerHub** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, complete the following steps:

    a. In the **Identifier (Entity ID)** box, enter a URL that has this pattern: `https://<company>.answerhub.com`

    b. In the **Sign on URL** box, enter a URL that has this pattern: `https://<company>.answerhub.com`

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact the [AnswerHub support team](mailto:success@answerhub.com) to get the values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select the **Download** link next to **Certificate (Base64)**, per your requirements, and save the certificate on your computer.

    ![Certificate download link](common/certificatebase64.png)
7. In the **Set up AnswerHub** section, copy the appropriate URL or URLs, based on your requirements.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure AnswerHub SSO

In this section, you set up single sign-on for AnswerHub.

**To configure AnswerHub single sign-on:**

1. In a different web browser window, sign in to your AnswerHub company site as an admin.

    Note

    If you need help configuring AnswerHub, contact the [AnswerHub support team](mailto:success@answerhub.com.).
2. Go to **Administration**.
3. On the **User and Groups** tab, in the left pane, in the **Social Settings** section, select **SAML Setup**.
4. On the **IDP Config** tab, complete these steps:

    ![Screenshot shows AnswerHub page with the Users &amp; Groups tab selected.](media/answerhub-tutorial/admin.png)

    a. In the **IDP Login URL** box, paste the **Login URL** that you copied.

    b. In the **IDP Logout URL** box, paste the **Logout URL** that you copied.

    c. In the **IDP Name Identifier Format** box, enter the **Identifier** value selected in the **User Attributes** section on the Azure portal.

    d. Select **Keys and Certificates**.
5. In the **Keys and Certificates** section, complete these steps:

    ![Keys and Certificates section](media/answerhub-tutorial/users.png)

    a. Open the Base64-encoded certificate that you downloaded in Notepad, copy its contents, and then paste the contents into the **IDP Public Key (x509 Format)** box.

    b. Select **Save**.
6. On the **IDP Config** tab, select **Save** again.

### Create AnswerHub test user

To enable Microsoft Entra users to sign in to AnswerHub, you need to add them in AnswerHub. In AnswerHub, this task is done manually.

**To set up a user account:**

1. Sign in to your **AnswerHub** company site as an admin.
2. Go to **Administration**.
3. Select the **Users & Groups** tab.
4. In the left pane, in the **Manage Users** section, select **Create or import users**, and then select **Users & Groups**.

    ![Screenshot shows AnswerHub page with the Users &amp; Groups tab selected and the Create or import users link called out.](media/answerhub-tutorial/groups.png)
5. In the appropriate boxes, enter the **Email address**, **Username**, and **Password** of a valid Microsoft Entra account that you want to add, and then select **Save**.

Note

You can use any other user account creation tool or API provided by AnswerHub to set up Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to AnswerHub Sign-on URL where you can initiate the login flow.
- Go to AnswerHub Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the AnswerHub tile in the My Apps, this option redirects to AnswerHub Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).