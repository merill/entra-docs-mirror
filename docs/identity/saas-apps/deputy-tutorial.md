---
layout: Conceptual
title: Configure Deputy for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/deputy-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Deputy.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 907d9078-22fc-81fc-cb97-a6c0d065bfd2
document_version_independent_id: 850c0228-2b35-6296-a26a-e1e5350edcb0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/deputy-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/deputy-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/deputy-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 919c6920-e82a-911a-e9c2-40e2b751c9e9
---

# Configure Deputy for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Deputy with Microsoft Entra ID. When you integrate Deputy with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Deputy.
- Enable your users to be automatically signed-in to Deputy with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Deputy single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Deputy supports **SP and IDP** initiated SSO.
- Deputy supports **Just In Time** user provisioning.

## Add Deputy from the gallery

To configure the integration of Deputy into Microsoft Entra ID, you need to add Deputy from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Deputy** in the search box.
4. Select **Deputy** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Deputy

Configure and test Microsoft Entra SSO with Deputy using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Deputy.

To configure and test Microsoft Entra SSO with Deputy, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Deputy SSO**- to configure the single sign-on settings on application side.
    1. **Create Deputy test user** - to have a counterpart of B.Simon in Deputy that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Deputy** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, If you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using one of the following patterns:

    ```http
    https://<subdomain>.<region>.au.deputy.com
    https://<subdomain>.<region>.ent-au.deputy.com
    https://<subdomain>.<region>.na.deputy.com
    https://<subdomain>.<region>.ent-na.deputy.com
    https://<subdomain>.<region>.eu.deputy.com
    https://<subdomain>.<region>.ent-eu.deputy.com
    https://<subdomain>.<region>.as.deputy.com
    https://<subdomain>.<region>.ent-as.deputy.com
    https://<subdomain>.<region>.la.deputy.com
    https://<subdomain>.<region>.ent-la.deputy.com
    https://<subdomain>.<region>.af.deputy.com
    https://<subdomain>.<region>.ent-af.deputy.com
    https://<subdomain>.<region>.an.deputy.com
    https://<subdomain>.<region>.ent-an.deputy.com
    https://<subdomain>.<region>.deputy.com
    ```

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    ```http
    https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.
    https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs
    https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs
    ```
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`

    Note

    Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [Deputy Client support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. Deputy application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
8. In addition to above, Deputy application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | First name | user.givenname |
    | Last name | user.surname |
9. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
10. On the **Set up Deputy** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Deputy SSO

1. Login to your Deputy account as an administrator.
2. In the upper right corner, select your account, select **Business settings**.

    ![Screenshot for Business settings](media/deputy-tutorial/business-settings.png)
3. Then under the **General** tab, select **Single Sign-On settings**.

    ![Screenshot for Single Sign-On settings](media/deputy-tutorial/general.png)
4. On this **Single Sign-On settings** page, perform the below steps.

    ![Configure Single Sign-On](media/deputy-tutorial/configuration.png)

    a. Select **Enable single sign-on**.

    b. In the **Identity provider login URL** textbox, paste the **Login URL** which you copied previously.

    c. In the **Identity provider issuer** textbox, paste the **Identifier(Entity ID)** which you copied previously.

    d. Open the downloaded **Certificate (Base64)** into Notepad and paste the content into the **X.509 certificate** textbox.

    e. Enable the **Single sign-on login required**, if you want to login with SSO.

    f. Enable the **Just-in-time provisioning** and in the **First name** and **Last name** fields, give the names of the attributes you have set up in **User Attributes & Claims** section, like `First name` and `Last name`.

    g. Select **Apply changes**.

### Create Deputy test user

In this section, a user called Britta Simon is created in Deputy. Deputy supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Deputy, a new one is created after authentication.

#### To add the user manually, perform the following steps:

1. Log in to your Deputy company site as an administrator.
2. On the top navigation pane, select **People**.
3. Select the **Add People** button and select **Add Single Person**.

    ![Add People](media/deputy-tutorial/create-user-1.png)
4. Perform the following steps in the **General** tab to add a user.

    ![New User](media/deputy-tutorial/create-user-2.png)

    a. In the **First name** and **Last name** textboxes, fill the fields like **Britta** and **Simon**.

    b. In the **Work at** textbox, type the business name.

    c. Select **Save** button.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to TeamzSkill Sign on URL where you can initiate the login flow.
- Go to TeamzSkill Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the TeamzSkill for which you set up the SSO

You can also use Microsoft My Apps to test the application in any mode. When you select the TeamzSkill tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the TeamzSkill for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).