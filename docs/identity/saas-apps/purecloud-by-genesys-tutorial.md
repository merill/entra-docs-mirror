---
layout: Conceptual
title: Configure Genesys Cloud for Azure for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/purecloud-by-genesys-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Genesys Cloud for Azure.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: db012cc2-7ad5-65d3-f1f2-a0bf1d2321e0
document_version_independent_id: fc1493e2-cfdc-7ba2-ad6f-9dbac75ea869
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/purecloud-by-genesys-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/purecloud-by-genesys-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/purecloud-by-genesys-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e7655fbc-8893-263b-16bc-fadc58901fd5
---

# Configure Genesys Cloud for Azure for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Genesys Cloud for Azure with Microsoft Entra ID. When you integrate Genesys Cloud for Azure with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Genesys Cloud for Azure.
- Enable your users to be automatically signed-in to Genesys Cloud for Azure with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Genesys Cloud for Azure single sign-on (SSO)–enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Genesys Cloud for Azure supports **SP and IDP** initiated SSO.
- Genesys Cloud for Azure supports [Automated user provisioning](purecloud-by-genesys-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Genesys Cloud for Azure from the gallery

To configure integration of Genesys Cloud for Azure into Microsoft Entra ID, you must add Genesys Cloud for Azure from the gallery to your list of managed SaaS apps. To do this, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Genesys Cloud for Azure** in the search box.
4. Select **Genesys Cloud for Azure** from the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Genesys Cloud for Azure

Configure and test Microsoft Entra SSO with Genesys Cloud for Azure using a test user named **B.Simon**. For SSO to work, you must establish a link relationship between a Microsoft Entra user and the related user in Genesys Cloud for Azure.

To configure and test Microsoft Entra SSO with Genesys Cloud for Azure, perform the following steps:

1. **Configure Microsoft Entra SSO**to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Genesys Cloud for Azure SSO**to configure the single sign-on settings on application side.
    1. **Create Genesys Cloud for Azure test user** to have a counterpart of B.Simon in Genesys Cloud for Azure that's linked to the Microsoft Entra representation of user.
3. **Test SSO** to verify whether the configuration works.

## Configure Microsoft Entra SSO

To enable Microsoft Entra SSO in the Azure portal, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Genesys Cloud for Azure** application integration page, find the **Manage** section and select **single sign-on**.
3. On the **Select a Single Sign-On method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, if you want to configure the application in **IDP**-initiated mode, perform the following steps:

    a. In the **Identifier** box, enter the URLs that corresponds to your region:

    | Identifier URL |
    | --- |
    | https://login.mypurecloud.com/saml |
    | https://login.mypurecloud.de/saml |
    | https://login.mypurecloud.jp/saml |
    | https://login.mypurecloud.ie/saml |
    | https://login.mypurecloud.com.au/saml |
    |  |

    b. In the **Reply URL** box, enter the URLs that corresponds to your region:

    | Reply URL |
    | --- |
    | https://login.mypurecloud.com/saml |
    | https://login.mypurecloud.de/saml |
    | https://login.mypurecloud.jp/saml |
    | https://login.mypurecloud.ie/saml |
    | https://login.mypurecloud.com.au/saml |
    |  |
6. Select **Set additional URLs** and take the following step if you want to configure the application in **SP** initiated mode:

    In the **Sign-on URL** box, enter the URLs that corresponds to your region:

    | Sign-on URL |
    | --- |
    | https://login.mypurecloud.com |
    | https://login.mypurecloud.de |
    | https://login.mypurecloud.jp |
    | https://login.mypurecloud.ie |
    | https://login.mypurecloud.com.au |
    |  |
7. Genesys Cloud for Azure application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes:

    ![image](common/default-attributes.png)
8. Additionally, Genesys Cloud for Azure application expects a few more attributes to be passed back in the SAML response, as shown in the following table. These attributes are also pre-populated, but you can review them as needed.

    | Name | Source attribute |
    | --- | --- |
    | Email | user.userprincipalname |
    | OrganizationName | `Your organization name` |
9. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
10. In the **Set up Genesys Cloud for Azure** section, copy the appropriate URL (or URLs), based on your requirements.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Genesys Cloud for Azure SSO

1. In a different web browser window, sign in to Genesys Cloud for Azure as an administrator.
2. Select **Admin** at the top and then go to **Single Sign-on** under **Integrations**.

    ![Screenshot shows the PureCloud Admin window where you can select Single Sign-on.](media/purecloud-by-genesys-tutorial/configure-1.png)
3. Switch to the **ADFS/Azure AD(Premium)** tab, and then follow these steps:

    ![Screenshot shows the Integrations page where you can enter the values described.](media/purecloud-by-genesys-tutorial/configure-2.png)

    a. Select **Browse** to upload the base-64 encoded certificate that you downloaded into the **ADFS Certificate**.

    b. In the **ADFS Issuer URI** box, paste the value of **Microsoft Entra Identifier** that you copied.

    c. In the **Target URI** box, paste the value of **Login URL** that you copied.

    d. For the **Relying Party Identifier** value, go to the Azure portal, and then on the **Genesys Cloud for Azure** application integration page, select the **Properties** tab and copy the **Application ID** value. Paste it into the **Relying Party Identifier** box.

    ![Screenshot shows the Properties pane where you can find the Application ID value.](media/purecloud-by-genesys-tutorial/configuration.png)

    e. Select **Save**.

### Create Genesys Cloud for Azure test user

To enable Microsoft Entra users to sign in to Genesys Cloud for Azure, they must be provisioned into Genesys Cloud for Azure. In Genesys Cloud for Azure, provisioning is a manual task.

**To provision a user account, follow these steps:**

1. Log in to Genesys Cloud for Azure as an administrator.
2. Select **Admin** at the top and go to **People** under **People & Permissions**.

    ![Screenshot shows the PureCloud Admin window where you can select People.](media/purecloud-by-genesys-tutorial/configure-3.png)
3. On the **People** page, select **Add Person**.

    ![Screenshot shows the People page where you can add a person.](media/purecloud-by-genesys-tutorial/configure-4.png)
4. In the **Add People to the Organization** dialog box, follow these steps:

    ![Screenshot shows the page where you can enter the values described.](media/purecloud-by-genesys-tutorial/configure-5.png)

    a. In the **Full Name** box, enter the name of a user. For example: **B.simon**.

    b. In the **Email** box, enter the email of the user. For example: **b.simon@contoso.com**.

    c. Select **Create**.

Note

Genesys Cloud for Azure also supports automatic user provisioning, you can find more details [here](purecloud-by-genesys-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Genesys Cloud for Azure Sign on URL where you can initiate the login flow.
- Go to Genesys Cloud for Azure Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Genesys Cloud for Azure for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Genesys Cloud for Azure tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Genesys Cloud for Azure for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).