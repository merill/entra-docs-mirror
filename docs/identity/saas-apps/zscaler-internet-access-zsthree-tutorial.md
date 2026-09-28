---
layout: Conceptual
title: Configure Zscaler Internet Access ZSThree for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zscaler-internet-access-zsthree-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Zscaler Internet Access ZSThree.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: d3df52f3-4c1c-6f30-23f1-e69ec557c2ab
document_version_independent_id: d3df52f3-4c1c-6f30-23f1-e69ec557c2ab
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zscaler-internet-access-zsthree-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zscaler-internet-access-zsthree-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zscaler-internet-access-zsthree-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ae28c277-6077-2070-5e5c-f41bb1f4cf8e
---

# Configure Zscaler Internet Access ZSThree for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Zscaler Internet Access ZSThree with Microsoft Entra ID. When you integrate Zscaler Internet Access ZSThree with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Zscaler Internet Access ZSThree.
- Enable your users to be automatically signed-in to Zscaler Internet Access ZSThree with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Zscaler Internet Access ZSThree is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ |  | ✅ |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Zscaler Internet Access ZSThree single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Zscaler Internet Access ZSThree supports **SP** initiated SSO.
- Zscaler Internet Access ZSThree supports **Just In Time** user provisioning.
- Zscaler Internet Access ZSThree supports [Automated user provisioning](zscaler-three-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Zscaler Internet Access ZSThree from the gallery

To configure the integration of Zscaler Internet Access ZSThree into Microsoft Entra ID, you need to add Zscaler Internet Access ZSThree from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Zscaler Internet Access ZSThree** in the search box.
4. Select **Zscaler Internet Access ZSThree** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Zscaler Internet Access ZSThree

Configure and test Microsoft Entra SSO with Zscaler Internet Access ZSThree using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Zscaler Internet Access ZSThree.

To configure and test Microsoft Entra SSO with Zscaler Internet Access ZSThree, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Zscaler Internet Access ZSThree SSO**- to configure the single sign-on settings on application side.
    1. **Create Zscaler Internet Access ZSThree test user** - to have a counterpart of B.Simon in Zscaler Internet Access ZSThree that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zscaler Internet Access ZSThree** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    In the **Sign-on URL** text box, type the URL: `https://login.zscalerthree.net/sfc_sso`
6. Your Zscaler Internet Access ZSThree application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows User Attributes with the Edit icon selected.](common/edit-attribute.png)
7. In addition to above, Zscaler Internet Access ZSThree application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirement.

    | Name | Source Attribute |
    | --- | --- |
    | memberOf | user.assignedroles |

    Note

    Please select [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui) to know how to configure Role in Microsoft Entra ID.
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. On the **Set up Zscaler Internet Access ZSThree** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Zscaler Internet Access ZSThree SSO

1. In a different web browser window, sign in to your Zscaler Internet Access ZSThree company site as an administrator
2. Go to **Administration &gt; Authentication &gt; Authentication Settings** and perform the following steps:

    ![Screenshot shows the Zscaler One site with steps as described.](media/zscaler-three-tutorial/settings.png)

    a. Under Authentication Type, choose **SAML**.

    b. Select **Configure SAML**.
3. On the **Edit SAML** window, perform the following steps: and select Save.

    ![Manage Users &amp; Authentication](media/zscaler-three-tutorial/authentication.png)

    a. In the **SAML Portal URL** textbox, Paste the **Login URL**..

    b. In the **Login Name Attribute** textbox, enter **NameID**.

    c. Select **Upload**, to upload the Azure SAML signing certificate that you have downloaded from Azure portal in the **Public SSL Certificate**.

    d. Toggle the **Enable SAML Auto-Provisioning**.

    e. In the **User Display Name Attribute** textbox, enter **displayName** if you want to enable SAML auto-provisioning for displayName attributes.

    f. In the **Group Name Attribute** textbox, enter **memberOf** if you want to enable SAML auto-provisioning for memberOf attributes.

    g. In the **Department Name Attribute** Enter **department** if you want to enable SAML auto-provisioning for department attributes.

    h. Select **Save**.
4. On the **Configure User Authentication** dialog page, perform the following steps:

    ![Screenshot shows the Configure User Authentication dialog box with Activate selected.](media/zscaler-three-tutorial/user.png)

    a. However over the **Activation** menu near the bottom left.

    b. Select **Activate**.

## Configuring proxy settings

### To configure the proxy settings in Internet Explorer

1. Start **Internet Explorer**.
2. Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.

    ![Internet Options](media/zscaler-three-tutorial/tools.png)
3. Select the **Connections** tab.

    ![Connections](media/zscaler-three-tutorial/setup.png)
4. Select **LAN settings** to open the **LAN Settings** dialog.
5. In the Proxy server section, perform the following steps:

    ![Proxy server](media/zscaler-three-tutorial/server.png)

    a. Select **Use a proxy server for your LAN**.

    b. In the Address textbox, type **gateway.Zscaler Three.net**.

    c. In the Port textbox, type **80**.

    d. Select **Bypass proxy server for local addresses**.

    e. Select **OK** to close the **Local Area Network (LAN) Settings** dialog.
6. Select **OK** to close the **Internet Options** dialog.

### Create Zscaler Internet Access ZSThree test user

In this section, a user called B.Simon is created in Zscaler Internet Access ZSThree. Zscaler Internet Access ZSThree supports just-in-time provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Zscaler Internet Access ZSThree, a new one is created when you attempt to access Zscaler Internet Access ZSThree.

Note

If you need to create a user manually, contact [Zscaler Internet Access ZSThree support team](https://www.zscaler.com/company/contact).

Note

Zscaler Internet Access ZSThree also supports automatic user provisioning, you can find more details [here](zscaler-three-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Zscaler Internet Access ZSThree Sign-on URL where you can initiate the login flow.
- Go to Zscaler Internet Access ZSThree Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Zscaler Internet Access ZSThree tile in the My Apps, this option redirects to Zscaler Internet Access ZSThree Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).