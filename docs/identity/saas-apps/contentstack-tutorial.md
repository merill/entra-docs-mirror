---
layout: Conceptual
title: Configure Contentstack for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/contentstack-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Contentstack.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: c65992b4-3d35-ca4e-7621-4d6cf62375ca
document_version_independent_id: c65992b4-3d35-ca4e-7621-4d6cf62375ca
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/contentstack-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/contentstack-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/contentstack-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 73ff815b-8f6a-6eee-d793-d85218b0ac44
---

# Configure Contentstack for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Contentstack with Microsoft Entra ID. When you integrate Contentstack with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Contentstack.
- Enable your users to be automatically signed-in to Contentstack with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Contentstack single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Contentstack supports both **SP and IDP** initiated SSO.
- Contentstack supports **Just In Time** user provisioning.

## Add Contentstack from the gallery

To configure the integration of Contentstack into Microsoft Entra ID, you need to add Contentstack from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Contentstack** in the search box.
4. Select **Contentstack** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Contentstack

Configure and test Microsoft Entra SSO with Contentstack using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Contentstack.

To configure and test Microsoft Entra SSO with Contentstack, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Contentstack SSO**- to configure the single sign-on settings on application side.
    1. **Create Contentstack test user** - to have a counterpart of B.Simon in Contentstack that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator) and browse to **Entra ID** &gt; **Enterprise apps**.
2. Now select **+ New Application** and search for Contentstack then select **Create**. Once created, now go to **Setup single sign on** or select the **Single sign-on** link from the left menu.

    ![Screenshot shows the new application creation.](media/contentstack-tutorial/create.png)
3. Next, on the **Select a single sign-on method** page, select **SAML**.

    ![Screenshot shows how to select a single sign-on method.](media/contentstack-tutorial/single.png)
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](media/contentstack-tutorial/edit.png)
5. In the **Basic SAML Configuration** section, you need to perform a few steps. To obtain the information necessary for these steps, you first need to go to the Contentstack application and create **SSO Name** and **ACS URL** in the following manner:

    a. Log in to your Contentstack account, go to the Organization Settings page, and select the **Single Sign-On** tab.

    ![Screenshot shows the steps for Basic SAML Configuration.](media/contentstack-tutorial/page.png)

    b. Enter an **SSO Name** of your choice, and select **Create**.

    ![Screenshot shows how to enter or create name.](media/contentstack-tutorial/names.png)

    Note

    For example, if your company name is “Acme, Inc.” enter “acme” here. This name is used as one of the login credentials by the organization users while signing in. The SSO Name can contain only alphabets (in lowercase), numbers (0-9), and/or hyphens (-).

    c. When you select **Create**, this will generate the **Assertion Consumer Service URL** or ACS URL, and other details such as **Entity ID**, **Attributes**, and **NameID Format**.

    ![Screenshot shows generating the values to configure.](media/contentstack-tutorial/value.png)
6. Back in the **Basic SAML Configuration** section, paste the **Entity ID** and the **ACS URL** generated in the above set of steps, against the **Identifier (Entity ID)** and **Reply URL** sections respectively, and save the entries.

    1. In the **Identifier** text box, paste the **Entity ID** value, which you have copied from Contentstack.

        ![Screenshot shows how to paste the Identifier value.](media/contentstack-tutorial/entity.png)
    2. In the **Reply URL** text box, paste the **ACS URL**, which you have copied from Contentstack.

        ![Screenshot shows how to paste the Reply URL.](media/contentstack-tutorial/reply.png)
7. This is an optional step. If you wish to configure the application in SP-initiated mode, enter the Sign-on URL against the Sign-on URL section:

    ![Screenshot shows how to paste the Sign on URL.](media/contentstack-tutorial/optional.png)

    Note

    You find the **SSO One-Select URL** (that is, the Sign on URL) when you complete configuring Contentstack SSO. ![Screenshot shows how to enable the access page.](media/contentstack-tutorial/click.png)
8. Contentstack application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](media/contentstack-tutorial/claims.png)
9. In addition to above, Contentstack application expects a few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements. This is an optional step.

    | Name | Source Attribute |
    | --- | --- |
    | roles | user.assignedroles |

    Note

    Please select [here](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui) to know how to configure Role in Microsoft Entra ID.
10. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
11. On the **Set up Contentstack** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Contentstack SSO

1. Log in to your Contentstack company site as an administrator.
2. Go to the Organization Settings page and select the **Single Sign-On** tab on the left menu.
3. In the **Single Sign-On** page, navigate to **SSO Configuration** section and perform the following steps:

    1. Enter a valid **SSO Name** of your choice and select **Create**.

        ![Screenshot shows settings of the configuration.](media/contentstack-tutorial/name.png)

        Note

        For example, if your company name is “Acme, Inc.” enter “acme” here. This name is used as one of the login credentials by the organization users while signing in. The SSO Name can contain only alphabets (in lowercase), numbers (0-9), and/or hyphens (-).
    2. When you select **Create**, this will generate the **Assertion Consumer Service URL** or ACS URL, and other details such as **Entity ID**, **Attributes**, and **NameID Format** and select **Next**.

        ![Screenshot shows the configuration values.](media/contentstack-tutorial/values.png)
4. Navigate to **Idp Configuration** tab and perform the following steps:

    ![Screenshot shows the login values from Identity.](media/contentstack-tutorial/admin.png)

    1. In the **Single Sign-On Url** textbox, paste the **Login URL**, which you have copied from the Microsoft Entra admin center.
    2. Open the downloaded **Certificate (Base64)** from Microsoft Entra admin center and upload into the **Certificate** field.
    3. Select **Next**.
5. Next, you need to create role mapping in Contentstack.

    Note

    You only be able to view and perform this step if IdP Role Mapping is part of your Contentstack plan.
6. In the **User Management** section of Contentstack's SSO Setup page, you see [**Strict Mode**](https://www.contentstack.com/docs/developers/single-sign-on/set-up-sso-in-contentstack#strict-mode) (authorize access to organization users only via SSO login) and [**Session Timeout**](https://www.contentstack.com/docs/developers/single-sign-on/set-up-sso-in-contentstack#session-timeout) (define session duration for a user signed in through SSO). Below these options, you also see the [**Advanced Settings**](https://www.contentstack.com/docs/developers/single-sign-on/set-up-sso-in-contentstack#advanced-settings) option.

    ![Screenshot shows User Management section.](media/contentstack-tutorial/manage.png)
7. Select the **Advanced Settings** to expand the IdP Role Mapping section to map IdP roles to Contentstack. This is an optional step.
8. In the **Add Role Mapping** section, select the **+ ADD ROLE MAPPING** link to add the mapping details of an IdP role which includes the following details:

    ![Screenshot shows how to add the mapping details.](media/contentstack-tutorial/roles.png)

    1. In the **IdP Role Identifier**, enter the IdP group/role identifier (for example, "developers"), which you can use the value from your manifest.
    2. For the **Organization Roles**, select either **Admin** or **Member** role to the mapped group/role.
    3. For the **Stack-Level Permissions** (optional) assign stacks and the corresponding stack-level roles to this role. Likewise, you can add more role mappings for your Contentstack organization. To add a new Role mapping, select **+ ADD ROLE MAPPING** and enter the details.
    4. Keep **Role Delimiter** blank as Microsoft Entra ID usually returns roles in an array.
    5. Finally, select the **Enable IdP Role Mapping** checkbox to enable the feature and select **Next**.

    Note

    For more information, please refer [Contentstack SSO guide](https://www.contentstack.com/docs/developers/single-sign-on).
9. Before enabling SSO, it's recommended that you need to test the SSO settings configured so far. To do so, perform the following steps:

    1. Select the **Test SSO** button and it will take you to Contentstack's Log in via SSO page where you need to specify your organization's SSO name.
    2. Then, select Continue to go to your IdP sign in page.
    3. Sign in to your account and if you're able to sign in to your IdP, your test is successful.
    4. On successful connection, you see a success message as follows.

    ![Screenshot shows the successful test connection.](media/contentstack-tutorial/success.png)
10. Once you have tested your SSO settings, select **Enable SSO** to enable SSO for your Contentstack organization.

    ![Screenshot shows the enable testing section.](media/contentstack-tutorial/test.png)
11. Once this is enabled, users can access the organization through SSO. If needed, you can also **Disable SSO** from this page as well.

    ![Screenshot shows disabling the access page.](media/contentstack-tutorial/access.png)

### Create Contentstack test user

In this section, a user called Britta Simon is created in Contentstack. Contentstack supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Contentstack, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application** in Microsoft Entra admin center. this option redirects to Contentstack Sign-on URL where you can initiate the login flow.
- Go to Contentstack Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application** in Microsoft Entra admin center and you should be automatically signed in to the Contentstack for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Contentstack tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Contentstack for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).