---
layout: Conceptual
title: Configure KnowledgeOwl for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/knowledgeowl-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and KnowledgeOwl.
ms.topic: how-to
ms.date: 2026-03-19T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 55241c67-8ddc-bc7d-be2d-82584b83feac
document_version_independent_id: a96e612f-d6eb-7a76-b58c-1cddc081312f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/knowledgeowl-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/knowledgeowl-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/knowledgeowl-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 03df7aab-bd10-0cdd-0a15-2113a1eb28a8
---

# Configure KnowledgeOwl for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate KnowledgeOwl with Microsoft Entra ID. When you integrate KnowledgeOwl with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to KnowledgeOwl.
- Enable your users to be automatically signed-in to KnowledgeOwl with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- KnowledgeOwl single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- KnowledgeOwl supports **SP and IDP** initiated SSO.
- KnowledgeOwl supports **Just In Time** user provisioning.

## Add KnowledgeOwl from the gallery

To configure the integration of KnowledgeOwl into Microsoft Entra ID, you need to add KnowledgeOwl from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **KnowledgeOwl** in the search box.
4. Select **KnowledgeOwl** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for KnowledgeOwl

Configure and test Microsoft Entra SSO with KnowledgeOwl using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in KnowledgeOwl.

To configure and test Microsoft Entra SSO with KnowledgeOwl, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure KnowledgeOwl SSO**- to configure the single sign-on settings on application side.
    1. **Create KnowledgeOwl test user** - to have a counterpart of B.Simon in KnowledgeOwl that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **KnowledgeOwl** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type the URL using one of the following patterns:

    ```http
    https://app.knowledgeowl.com/sp
    https://app.knowledgeowl.com/sp/id/<unique ID>
    ```

    b. In the **Reply URL** text box, type the URL using one of the following patterns:

    ```http
    https://subdomain.knowledgeowl.com/help/saml-login
    https://subdomain.knowledgeowl.com/docs/saml-login
    https://subdomain.knowledgeowl.com/home/saml-login
    https://privatedomain.com/help/saml-login
    https://privatedomain.com/docs/saml-login
    https://privatedomain.com/home/saml-login
    ```
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL using one of the following patterns:

    ```http
    https://subdomain.knowledgeowl.com/help/saml-login
    https://subdomain.knowledgeowl.com/docs/saml-login
    https://subdomain.knowledgeowl.com/home/saml-login
    https://privatedomain.com/help/saml-login
    https://privatedomain.com/docs/saml-login
    https://privatedomain.com/home/saml-login
    ```

    Note

    These values aren't real. You'll need to update these value from actual Identifier, Reply URL, and Sign-On URL which is explained later in the article.
7. KnowledgeOwl application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, KnowledgeOwl application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute | Namespace |
    | --- | --- | --- |
    | ssoid | user.mail | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims` |
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Raw)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificateraw.png)
10. On the **Set up KnowledgeOwl** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure KnowledgeOwl SSO

1. In a different web browser window, sign in to your KnowledgeOwl company site as an administrator.
2. Select **Security and access** and then select **Single sign-on**.
3. In the **SAML Settings** tab, perform the following steps:

    ![Screenshot shows the SAML settings where you can enable SAML SSO reader logins mentioned here.](media/knowledgeowl-tutorial/sso-saml-settings.png)

    1. Select **Enable SAML SSO reader logins**.

    ![Screenshot shows the Service provider metadata section where you can copy the values mentioned here.](media/knowledgeowl-tutorial/service-provider-metadata.png)

    1. In the **Service provider metadata** section, copy the **SP entity ID** value and paste it into the **Identifier (Entity ID)** in the **Basic SAML Configuration** section on the Azure portal.
    2. In the **Service provider metadata** section, copy the **SP login URL** value and paste it into the **Sign-on URL and Reply URL** textboxes in the **Basic SAML Configuration** section on the Azure portal.

    ![Screenshot shows the Identity provider metadata section where you can complete the steps mentioned here.](media/knowledgeowl-tutorial/saml-identity-provider-metadata.png)

    1. In the **Identity provider metadata** section, paste the **Microsoft Entra Identifier** value you previously copied into the **IdP entityID** textbox.
    2. Paste the **Login URL** value you previously copied into the **IdP login URL**.
    3. Paste the **Logout URL** you previously copied into the **IdP logout URL** textbox.
    4. Upload the downloaded certificate from the Azure portal by selecting the **Upload certificate** link beneath **IdP certificate**.
    5. Select **Save** at the bottom of the section.
4. Open the **SAML attribute map** tab to map attributes and perform the following steps:

    ![Screenshot shows Map SAML Attributes where you can make the changes described here.](media/knowledgeowl-tutorial/saml-attribute-map.png)

    1. Enter `https://schemas.xmlsoap.org/ws/2005/05/identity/claims/ssoid` into the **SSO ID** textbox.
    2. Enter `https://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` into the **Username/Email** textbox.
    3. Enter `https://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname` into the **First Name** textbox.
    4. Enter `https://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname` into the **Last Name** textbox.
    5. Select **Save** at the bottom of the page.

    ![Screenshot shows the Save button.](media/knowledgeowl-tutorial/saml-attribute-map-save.png)

### Create KnowledgeOwl test user

In this section, a user called B.Simon is created in KnowledgeOwl. KnowledgeOwl supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in KnowledgeOwl, a new one is created after authentication.

Note

If you need to create a user manually, contact [KnowledgeOwl support team](mailto:support@knowledgeowl.com).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated

- Select **Test this application**, this option redirects to KnowledgeOwl Sign on URL where you can initiate the login flow.
- Go to the KnowledgeOwl sign-on URL directly and initiate the login flow from there.

#### IDP initiated

- Select **Test this application**, in the Azure portal and you should be automatically signed in to the KnowledgeOwl application for which you set up the SSO.

You can also use the Microsoft My Apps portal to test the application in any mode. When you select the KnowledgeOwl tile in the My Apps portal, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the KnowledgeOwl application for which you set up the SSO. For more information about the My Apps portal, see [Introduction to My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).