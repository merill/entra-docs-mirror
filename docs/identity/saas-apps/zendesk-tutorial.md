---
layout: Conceptual
title: Configure Zendesk for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/zendesk-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Zendesk.
ms.topic: how-to
ms.date: 2024-05-17T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 16ae6014-a5f6-03f3-4ad4-4425cfe5b6ca
document_version_independent_id: 1d3d0543-89f7-180a-e52a-b5668a314e6a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/zendesk-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/zendesk-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/zendesk-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: abe85aa3-b50f-4ba0-4a26-490766af674f
---

# Configure Zendesk for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Zendesk with Microsoft Entra ID. When you integrate Zendesk with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Zendesk.
- Enable your users to be automatically signed-in to Zendesk with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Zendesk single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Zendesk supports **SP** initiated SSO.
- Zendesk supports [**Automated** user provisioning](zendesk-provisioning-tutorial).

## Adding Zendesk from the gallery

To configure the integration of Zendesk into Microsoft Entra ID, you need to add Zendesk from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Zendesk** in the search box.
4. Select **Zendesk** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Zendesk

Configure and test Microsoft Entra SSO with Zendesk using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Zendesk.

To configure and test Microsoft Entra SSO with Zendesk, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Zendesk SSO**- to configure the single sign-on settings on application side.
    1. **Create Zendesk test user** - to have a counterpart of B.Simon in Zendesk that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Zendesk** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to Edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<subdomain>.zendesk.com`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<subdomain>.zendesk.com`

    c. In the **Reply URL** text box, type a URL using the following pattern: `https://<subdomain>.zendesk.com/access/saml`

    Note

    These values aren't real. Update these values with the actual Sign on URL, Identifier and Reply URL. Contact [Zendesk Client support team](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Zendesk application expects the SAML assertions in a specific format. There are no mandatory SAML attributes but optionally you can manage from the **User Attributes** section on application integration page. On the **Set up Single Sign-On with SAML** page, select **Edit** button to open **User Attributes** dialog.

    ![Screenshot shows User Attributes with the Edit icon selected.](common/edit-attribute.png)

    Note

    You use extension attributes to add attributes that aren't in Microsoft Entra ID by default. Select [User attributes that can be set in SAML](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.
7. In the **SAML Signing Certificate** section, select **Edit** button to open **SAML Signing Certificate** dialog.

    ![Screenshot shows to edit SAML Signing Certificate.](common/edit-certificate.png)
8. In the **SAML Signing Certificate** section, copy the **Thumbprint Value** and save it on your computer.

    ![Screenshot shows to copy Thumbprint value.](common/copy-thumbprint.png)
9. On the **Set up Zendesk** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Zendesk SSO

You can set up one SAML configuration for team members and a second SAML configuration for end users.

1. In a different web browser window, sign in to your up Zendesk company site as an administrator
2. In the **Zendesk Admin Center**, go to **Account -&gt; Security -&gt; Single sign-on**, then select **Create SSO configuration** and select **SAML**.

    ![Screenshot shows the Zendesk Admin Center with Security settings selected.](media/zendesk-tutorial/zendesk-create-sso-configuration.png)
3. Perform the following steps in the **Single sign-on** page.

    ![Screenshot shows Single sign-on.](media/zendesk-tutorial/zendesk-saml-configuration-settings.png)

    a. In **Configuration name**, enter a name for your configuration. Up to two SAML and two JWT configurations are possible.

    b. In **SAML SSO URL** textbox, paste the value of **Login URL**.

    c. In **Certificate fingerprint** textbox, paste the **Thumbprint** value of certificate.

    d. In **Remote logout URL** textbox, paste the value of **Logout URL**.

    e. Select **Save**.

After creating your SAML configuration, you must activate it by assigning it to end users or team members.

1. In the **Zendesk Admin Center**, go to **Account -&gt; Security** and select either **Team member authentication** or **End user authentication**.
2. If you're assigning the configuration to team members, select **External authentication** to show the authentication options. These options are already displayed for end users.
3. Select the **Single sign-on (SSO)** option in the **External authentication** section, then select the name of the SSO configuration you want to use.
4. Select the primary SSO method for this group of users if you have more than one authentication method assigned to the group. This option sets the default method used when users go to a page that requires authentication.
5. Select **Save**.

### Create Zendesk test user

The objective of this section is to create a user called Britta Simon in Zendesk. Zendesk supports automatic user provisioning, which is by default enabled. You can find more details [here](zendesk-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Zendesk Sign-on URL where you can initiate the login flow.
- Go to Zendesk Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Zendesk tile in the My Apps, this option redirects to Zendesk Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).