---
layout: Conceptual
title: Configure Zenya for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zenya-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Zenya.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 123d5959-453a-c9d9-1d8b-30847ea2b4bf
document_version_independent_id: cc30cc4d-d87f-8a92-e7b3-891359ae95d4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zenya-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zenya-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zenya-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 256fcef0-f678-2947-804e-1c0478adc52b
---

# Configure Zenya for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Zenya with Microsoft Entra ID. When you integrate Zenya with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Zenya.
- Enable your users to be automatically signed-in to Zenya with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Zenya single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Zenya supports **SP** initiated SSO.
- Zenya supports [Automated user provisioning](zenya-provisioning-tutorial).

## Add Zenya from the gallery

To configure the integration of Zenya into Microsoft Entra ID, you need to add Zenya from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Zenya** in the search box.
4. Select **Zenya** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Zenya

Configure and test Microsoft Entra SSO with Zenya using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Zenya.

To configure and test Microsoft Entra SSO with Zenya, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Zenya SSO**- to configure the single sign-on settings on application side.
    1. **Create Zenya test user** - to have a counterpart of B.Simon in Zenya that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Retrieve configuration information from Zenya

In this section, you retrieve information from Zenya to configure Microsoft Entra single sign-on.

1. Open a web browser and go to the **SAML2 info** page in Zenya by using the following URL patterns:

    `https://<SUBDOMAIN>.zenya.work/saml2info``https://<SUBDOMAIN>.iprova.nl/saml2info``https://<SUBDOMAIN>.iprova.be/saml2info``https://<SUBDOMAIN>.iprova.eu/saml2info`

    ![Screenshot of the Zenya SAML2 information page.](media/zenya-tutorial/information.png)
2. Leave the browser tab open while you proceed with the next steps in another browser tab.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zenya** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot of the page for editing the basic SAML configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. Fill the **Sign-on URL** box with the value that's displayed behind the label **Sign-on URL** on the **Zenya SAML2 info** page. This page is still open in your other browser tab.

    b. Fill the **Identifier** box with the value that's displayed behind the label **EntityID** on the **Zenya SAML2 info** page. This page is still open in your other browser tab.

    c. Fill the **Reply-URL** box with the value that's displayed behind the label **Reply URL** on the **Zenya SAML2 info** page. This page is still open in your other browser tab.

    d. Fill the **Logout-URL** box with the value that's displayed behind the label **Logout URL** on the **Zenya SAML2 info** page. This page is still open in your other browser tab.
6. Zenya application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot showing the list of default attributes.](common/default-attributes.png)
7. In addition to above, Zenya application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute | Namespace |
    | --- | --- | --- |
    | `samaccountname` | `user.onpremisessamaccountname` | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims` |
8. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot showing SAML Signing Certificate information including a download link.](common/copy-metadataurl.png)

## Create a Microsoft Entra test user

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

## Assign the Microsoft Entra test user

In this section, you enable B.Simon to use single sign-on by granting access to Zenya.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zenya**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure Zenya SSO

1. Sign in to Zenya by using the **Administrator** account.
2. Open the **Go to** menu.
3. Select **Application management**.
4. Select **General** in the **System settings** panel.
5. Select **Edit**.
6. Scroll down to **Access control**.

    ![Screenshot showing Zenya Access control settings.](media/zenya-tutorial/access-control.png)
7. Find the setting **Users are automatically logged on with their network accounts**, and change it to **Yes, authentication via SAML**. Additional options now appear.
8. Select **Set up**.
9. Select **Next**.
10. Zenya asks if you want to download federation data from a URL or upload it from a file. Select the **From URL** option.

    ![Screenshot showing page for entering the URL for downloading Microsoft Entra metadata](media/zenya-tutorial/metadata.png)
11. Paste the metadata URL you saved in the last step of the "Configure Microsoft Entra single sign-on" section.
12. Select the arrow-shaped button to download the metadata from Microsoft Entra ID.
13. When the download is complete, the confirmation message **Valid Federation Data file downloaded** appears.
14. Select **Next**.
15. Skip the **Test login** option for now, and select **Next**.
16. In the **Claim to use** drop-down box, select **windowsaccountname**.
17. Select **Finish**.
18. You now return to the **Edit general settings** screen. Scroll down to the bottom of the page, and select **OK** to save your configuration.

## Create Zenya test user

1. Sign in to Zenya by using the **Administrator** account.
2. Open the **Go to** menu.
3. Select **Application management**.
4. Select **Users** in the **Users and user groups** panel.
5. Select **Add**.
6. In the **Username** box, enter the username of user like `B.Simon@contoso.com`.
7. In the **Full name** box, enter a full name of user like **B.Simon**.
8. Select the **No password (use single sign-on)** option.
9. In the **E-mail address** box, enter the email address of user like `B.Simon@contoso.com`.
10. Scroll down to the end of the page, and select **Finish**.

Note

Zenya also supports automatic user provisioning, you can find more details [here](zenya-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Zenya Sign-on URL where you can initiate the login flow.
- Go to Zenya Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Zenya tile in the My Apps, this option redirects to Zenya Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).