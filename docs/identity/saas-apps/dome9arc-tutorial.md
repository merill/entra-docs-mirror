---
layout: Conceptual
title: Configure Check Point CloudGuard Posture Management for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/dome9arc-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Check Point CloudGuard Posture Management.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: bbdd1ae7-b1b1-5384-ba4a-fb57daf9e927
document_version_independent_id: 06e8ffcb-f967-1fd4-ad9c-fb71c28241b8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/dome9arc-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/dome9arc-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/dome9arc-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0676e68d-8069-c399-d389-d3eb95ad0e69
---

# Configure Check Point CloudGuard Posture Management for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Check Point CloudGuard Posture Management with Microsoft Entra ID. When you integrate Check Point CloudGuard Posture Management with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Check Point CloudGuard Posture Management.
- Enable your users to be automatically signed-in to Check Point CloudGuard Posture Management with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Check Point CloudGuard Posture Management single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Check Point CloudGuard Posture Management supports **SP and IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Adding Check Point CloudGuard Posture Management from the gallery

To configure the integration of Check Point CloudGuard Posture Management into Microsoft Entra ID, you need to add Check Point CloudGuard Posture Management from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Check Point CloudGuard Posture Management** in the search box.
4. Select **Check Point CloudGuard Posture Management** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Check Point CloudGuard Posture Management

Configure and test Microsoft Entra SSO with Check Point CloudGuard Posture Management using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Check Point CloudGuard Posture Management.

To configure and test Microsoft Entra SSO with Check Point CloudGuard Posture Management, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Check Point CloudGuard Posture Management SSO**- to configure the single sign-on settings on application side.
    1. **Create Check Point CloudGuard Posture Management test user** - to have a counterpart of B.Simon in Check Point CloudGuard Posture Management that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Check Point CloudGuard Posture Management** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following step:

    In the **Reply URL** text box, type a URL using the following pattern: `https://secure.dome9.com/sso/saml/<YOURCOMPANYNAME>`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://secure.dome9.com/sso/saml/<YOURCOMPANYNAME>`

    Note

    These values aren't real. Update these values with the actual Reply URL and Sign-on URL. You get the `<company name>` value from the **Configure Check Point CloudGuard Posture Management SSO** section, which is explained later in the article. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. Check Point CloudGuard Posture Management application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/edit-attribute.png)
8. In addition to above, Check Point CloudGuard Posture Management application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirement.

    | Name | Source Attribute |
    | --- | --- |
    | memberof | user.assignedroles |

    Note

    Select [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui) to know how to create roles in Microsoft Entra ID.
9. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
10. On the **Set up Check Point CloudGuard Posture Management** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Check Point CloudGuard Posture Management SSO

1. In a different web browser window, sign in to your Check Point CloudGuard Posture Management company site as an administrator
2. Select the **Profile Settings** on the right top corner and then select **Account Settings**.

    ![Screenshot that shows the &quot;Profile Settings&quot; menu with &quot;Account Settings&quot; selected.](media/dome9arc-tutorial/account-settings.png)
3. Navigate to **SSO** and then select **ENABLE**.

    ![Screenshot that shows the &quot;S S O&quot; tab and &quot;Enable&quot; selected.](media/dome9arc-tutorial/enable.png)
4. In the SSO Configuration section, perform the following steps:

    ![Check Point CloudGuard Posture Management Configuration](media/dome9arc-tutorial/configuration.png)

    a. Enter company name in the **Account ID** textbox. This value is to be used in the **Reply** and **Sign on** URL mentioned in **Basic SAML Configuration** section of Azure portal.

    b. In the **Issuer** textbox, paste the value of **Microsoft Entra Identifier**, which you have copied form the Azure portal.

    c. In the **Idp endpoint url** textbox, paste the value of **Login URL**, which you have copied form the Azure portal.

    d. Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox.

    e. Select **Save**.

### Create Check Point CloudGuard Posture Management test user

To enable Microsoft Entra users to sign in to Check Point CloudGuard Posture Management, they must be provisioned into application. Check Point CloudGuard Posture Management supports just-in-time provisioning but for that to work properly, user have to select particular **Role** and assign the same to the user.

Note

To learn how to create a **Role** and for other information, see the [CloudGuard Admin Guide](https://blog.checkpoint.com/securing-the-cloud/how-to-use-compliance-engine-pci-dome9).

For 24/7 assistance, contact [Check Point Support](https://www.checkpoint.com/support-services/contact-support/).

**To provision a user account manually, perform the following steps:**

1. Sign in to your Check Point CloudGuard Posture Management company site as an administrator.
2. Select the **Users & Roles** and then select **Users**.

    ![Screenshot that shows &quot;Users &amp; Roles&quot; with the &quot;Users&quot; action selected.](media/dome9arc-tutorial/users.png)
3. Select **ADD USER**.

    ![Screenshot that shows &quot;Users &amp; Roles&quot; with the &quot;ADD USER&quot; button selected.](media/dome9arc-tutorial/add-user.png)
4. In the **Create User** section, perform the following steps:

    ![Add Employee](media/dome9arc-tutorial/create-user.png)

    a. In the **Email** textbox, type the email of user like B.Simon@contoso.com.

    b. In the **First Name** textbox, type first name of the user like B.

    c. In the **Last Name** textbox, type last name of the user like Simon.

    d. Make **SSO User** as **On**.

    e. Select **CREATE**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Check Point CloudGuard Posture Management Sign on URL where you can initiate the login flow.
- Go to Check Point CloudGuard Posture Management Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Check Point CloudGuard Posture Management for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the Check Point CloudGuard Posture Management tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Check Point CloudGuard Posture Management for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).