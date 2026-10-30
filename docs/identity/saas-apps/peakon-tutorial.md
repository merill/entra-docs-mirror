---
layout: Conceptual
title: Configure Peakon for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/peakon-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Peakon.
ms.topic: how-to
ms.date: 2026-06-09T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: eda435c1-acf8-c93c-9ce3-770b65990426
document_version_independent_id: c51941c4-cc9b-f40b-c06f-c8a58745db38
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/peakon-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/peakon-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/peakon-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 15831976-e830-773b-6a17-8b874033b743
---

# Configure Peakon for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Peakon with Microsoft Entra ID. When you integrate Peakon with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Peakon.
- Enable your users to be automatically signed-in to Peakon with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Peakon is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Peakon single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Peakon supports **SP** and **IDP** initiated SSO.
- Peakon supports [**automated** user provisioning and deprovisioning](peakon-provisioning-tutorial) (recommended).

## Add Peakon from the gallery

To configure the integration of Peakon into Microsoft Entra ID, you need to add Peakon from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Peakon** in the search box.
4. Select **Peakon** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Peakon

Configure and test Microsoft Entra SSO with Peakon using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Peakon.

To configure and test Microsoft Entra SSO with Peakon, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Peakon SSO**- to configure the single sign-on settings on application side.
    1. **Create Peakon test user** - to have a counterpart of B.Simon in Peakon that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Peakon** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://app.peakon.com/saml/<companyid>/metadata`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://app.peakon.com/saml/<companyid>/assert`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://app.peakon.com/login`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL which is explained later in the article. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Raw)** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/certificateraw.png)
8. On the **Set up Peakon** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Peakon SSO

1. In a different web browser window, sign in to Peakon as an Administrator.
2. In the menu bar on the left side of the page, select **Configuration**, then navigate to **Integrations**.

    ![Screenshot shows the Configuration](media/peakon-tutorial/menu.png)
3. On **Integrations** page, select **Single Sign-On**.

    ![Screenshot shows the Single](media/peakon-tutorial/profile.png)
4. Under **Single Sign-On** section, select **Enable**.

    ![Screenshot shows to enable Single Sign-On](media/peakon-tutorial/enable.png)
5. On the **Single sign-on for employees using SAML** section, perform the following steps:

    ![Screenshot shows SAML Single sign-on](media/peakon-tutorial/settings.png)

    a. In the **SSO Login URL** textbox, paste the value of **Login URL**, which you copied previously.

    b. In the **SSO Logout URL** textbox, paste the value of **Logout URL**, which you copied previously.

    c. Select **Choose file** to upload the certificate that you have downloaded, into the Certificate box.

    d. Select the **icon** to copy the **Entity ID** and paste in **Identifier** textbox in **Basic SAML Configuration** section.

    e. Select the **icon** to copy the **Reply URL (ACS)** and paste in **Reply URL** textbox in **Basic SAML Configuration** section.

    f. Select **Save**.

### Create Peakon test user

For enabling Microsoft Entra users to sign in to Peakon, they must be provisioned into Peakon. In the case of Peakon, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to your Peakon company site as an administrator.
2. In the menu bar on the left side of the page, select **Configuration**, then navigate to **Employees**.

    ![Screenshot shows the employee](media/peakon-tutorial/employee.png)
3. On the top right side of the page, select **Add employee**.

    ![Screenshot shows to add employee](media/peakon-tutorial/add-employee.png)
4. On the **New employee** dialog page, perform the following steps:

    ![Screenshot shows the new employee](media/peakon-tutorial/create.png)

    1. In the **Name** textbox, type first name as **Britta** and last name as **simon**.
    2. In the **Email** textbox, type the email address like **Brittasimon@contoso.com**.
    3. Select **Create employee**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Peakon Sign on URL where you can initiate the login flow.
- Go to Peakon Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Peakon for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Peakon tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Peakon for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).