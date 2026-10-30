---
layout: Conceptual
title: Configure Meraki Dashboard for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/meraki-dashboard-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Meraki Dashboard.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: e25502b7-432c-e8ff-2dde-f21e8ba6b4db
document_version_independent_id: ab9b51a1-d5c9-050b-ef67-0f1820eaf910
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/meraki-dashboard-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/meraki-dashboard-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/meraki-dashboard-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5473ef63-f697-8e17-08b6-d4a9014a87a5
---

# Configure Meraki Dashboard for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Meraki Dashboard with Microsoft Entra ID. When you integrate Meraki Dashboard with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Meraki Dashboard.
- Enable your users to be automatically signed-in to Meraki Dashboard with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Meraki Dashboard single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Meraki Dashboard supports **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Adding Meraki Dashboard from the gallery

To configure the integration of Meraki Dashboard into Microsoft Entra ID, you need to add Meraki Dashboard from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Meraki Dashboard** in the search box.
4. Select **Meraki Dashboard** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Meraki Dashboard

Configure and test Microsoft Entra SSO with Meraki Dashboard using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Meraki Dashboard.

To configure and test Microsoft Entra SSO with Meraki Dashboard, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Meraki Dashboard SSO**- to configure the single sign-on settings on application side.
    1. **Create Meraki Dashboard Admin Roles** - to have a counterpart of B.Simon in Meraki Dashboard that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Meraki Dashboard** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    In the **Reply URL** textbox, type a URL using the following pattern: `https://n27.meraki.com/saml/login/m9ZEgb/< UNIQUE ID >`

    Note

    The Reply URL value isn't real. Update this value with the actual Reply URL value, which is explained later in the article.
6. Select the **Save** button.
7. Meraki Dashboard application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, Meraki Dashboard application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | `https://dashboard.meraki.com/saml/attributes/username` | user.userprincipalname |
    | `https://dashboard.meraki.com/saml/attributes/role` | user.assignedroles |

    Note

    To understand how to configure roles in Microsoft Entra ID, see [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui).
9. In the **SAML Signing Certificate** section, select **Edit** button to open **SAML Signing Certificate** dialog.

    ![Edit SAML Signing Certificate](common/edit-certificate.png)
10. In the **SAML Signing Certificate** section, copy the **Thumbprint Value** and save it on your computer. This value needs to be converted to include colons in order for the Meraki dashboard to understand it . For example, if the thumbprint from Azure is `C2569F50A4AAEDBB8E` it will need to be changed to `C2:56:9F:50:A4:AA:ED:BB:8E` to use it later in Meraki Dashboard.

    ![Copy Thumbprint value](common/copy-thumbprint.png)
11. On the **Set up Meraki Dashboard** section, copy the Logout URL value and save it on your computer.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Meraki Dashboard SSO

1. In a different web browser window, sign in to your Meraki Dashboard company site as an administrator
2. Navigate to **Organization** &gt; **Settings**.

    ![Meraki Dashboard Settings tab](media/meraki-dashboard-tutorial/configure-1.png)
3. Under Authentication, change **SAML SSO** to **SAML SSO enabled**.

    ![Meraki Dashboard Authentication](media/meraki-dashboard-tutorial/configure-2.png)
4. Select **Add a SAML IdP**.

    ![Meraki Dashboard Add a SAML IdP](media/meraki-dashboard-tutorial/configure-3.png)
5. Paste the converted **Thumbprint** Value, which you have copied and converted in specified format as mentioned in step 9 of previous section into **X.590 cert SHA1 fingerprint** textbox. Then select **Save**. After saving, the Consumer URL will show up. Copy Consumer URL value and paste this into **Reply URL** textbox in the **Basic SAML Configuration Section**.

    ![Meraki Dashboard Configuration](media/meraki-dashboard-tutorial/configure-4.png)

### Create Meraki Dashboard Admin Roles

1. In a different web browser window, sign into meraki dashboard as an administrator.
2. Navigate to **Organization** &gt; **Administrators**.

    ![Meraki Dashboard Administrators](media/meraki-dashboard-tutorial/user-1.png)
3. In the SAML administrator roles section, select the **Add SAML role** button.

    ![Meraki Dashboard Add SAML role button](media/meraki-dashboard-tutorial/user-2.png)
4. Enter the Role **meraki\_full\_admin**, mark **Organization access** as **Full** and select **Create role**. Repeat the process for **meraki\_readonly\_admin**, this time mark **Organization access** as **Read-only** box.

    ![Meraki Dashboard create user](media/meraki-dashboard-tutorial/user-3.png)
5. Follow the below steps to map the Meraki Dashboard roles to Microsoft Entra SAML roles:

    ![Screenshot for App roles.](media/meraki-dashboard-tutorial/app-role.png)

    a. In the Azure portal, select **App Registrations**.

    b. Select All Applications and select **Meraki Dashboard**.

    c. Select **App Roles** and select **Create App role**.

    d. Enter the Display name as `Meraki Full Admin`.

    e. Select Allowed Members as `Users/Groups`.

    f. Enter the Value as `meraki_full_admin`.

    g. Enter the Description as `Meraki Full Admin`.

    h. Select **Save**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Meraki Dashboard for which you set up the SSO
- You can use Microsoft My Apps. When you select the Meraki Dashboard tile in the My Apps, you should be automatically signed in to the Meraki Dashboard for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).