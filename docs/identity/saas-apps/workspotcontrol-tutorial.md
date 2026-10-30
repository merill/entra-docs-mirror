---
layout: Conceptual
title: Configure Workspot Control for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/workspotcontrol-tutorial
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
description: Learn how to configure single sign-on for Microsoft Entra ID and Workspot Control.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5f75a1b6-6c80-c5bc-5100-a474de177615
document_version_independent_id: 30e9edee-627e-2b88-1ad5-6cd0e7d04970
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/workspotcontrol-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/workspotcontrol-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/workspotcontrol-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 85023e54-fcef-5ab0-9dad-7a39f472bdcf
---

# Configure Workspot Control for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Workspot Control with Microsoft Entra ID. When you integrate Workspot Control with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Workspot Control.
- Enable your users to be automatically signed-in to Workspot Control with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Workspot Control single sign-on-enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Workspot Control supports SP-initiated and IDP-initiated SSO.

## Add Workspot Control from the gallery

To configure the integration of Workspot Control into Microsoft Entra ID, you need to add Workspot Control from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Workspot Control** in the search box.
4. Select **Workspot Control** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Workspot Control

Configure and test Microsoft Entra SSO with Workspot Control using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Workspot Control.

To configure and test Microsoft Entra SSO with Workspot Control, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Workspot Control SSO**- to configure the single sign-on settings on application side.
    1. **Create Workspot Control test user** - to have a counterpart of B.Simon in Workspot Control that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Workspot Control** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, if you want to configure the application in IDP-initiated mode, follow these steps:

    1. In the **identifier** text box, type a URL using the following pattern:`https://<<i></i>INSTANCENAME>-saml.workspot.com/saml/metadata`
    2. In the **reply URL** text box, type a URL using the following pattern:`https://<<i></i>INSTANCENAME>-saml.workspot.com/saml/assertion`
6. If you want to configure the application in SP-initiated mode, select **Set additional URLs**.

    In the **Sign-on URL** text box, type a URL using the following pattern:`https://<<i></i>INSTANCENAME>-saml.workspot.com/`

    Note

    These values aren't real. Replace these values with the actual identifier, reply URL, and sign-on URL. Contact the [Workspot Control Client support team](mailto:support@workspot.com) to get these values. Or you can also refer to the patterns in the **Basic SAML Configuration** section.
7. On the **Set Up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download **Certificate (Base64)** from the available options as per your requirements. Save it to your computer.

    ![The Certificate (Base64) download link](common/certificatebase64.png)
8. In the **Set up Workspot Control** section, copy the appropriate URLs as per your requirements:

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Workspot Control SSO

1. In a different web browser window, sign in to Workspot Control as a Security Administrator.
2. In the toolbar at the top of the page, select **Setup** and then **SAML**.

    ![Setup options](media/workspotcontrol-tutorial/setup.png)
3. In the **Security Assertion Markup Language Configuration** window, follow these steps:

    ![Security Assertion Markup Language Configuration window](media/workspotcontrol-tutorial/security.png)

    1. In the **Entity ID** box, paste the **Microsoft Entra Identifier** that you copied.
    2. In the **Signon Service URL** box, paste the **Login URL** that you copied.
    3. In the **Logout Service URL** box, paste the **Logout URL** that you copied.
    4. Select **Update File** to upload into the X.509 certificate the base-64 encoded certificate that you downloaded.
    5. Select **Save**.

### Create Workspot Control test user

To enable Microsoft Entra users to sign in to Workspot Control, they must be provisioned into Workspot Control. Provisioning is a manual task.

**To provision a user account, follow these steps:**

1. Sign in to Workspot Control as a Security Administrator.
2. In the toolbar at the top of the page, select **Users** and then **Add User**.

    ![&quot;Users&quot; options](media/workspotcontrol-tutorial/user.png)
3. In the **Add a New User** window, follow these steps:

    ![&quot;Add a New User&quot; window](media/workspotcontrol-tutorial/new-user.png)

    1. In **First Name** box, enter the first name of a user, such as **Britta**.
    2. In **Last Name** text box, enter the last name of the user, such as **Simon**.
    3. In **Email** box, enter the email address of the user, such as **Brittasimon@contoso.com**.
    4. Select the appropriate user role from the **Role** drop-down list.
    5. Select the appropriate user group from the **Group** drop-down list.
    6. Select **Add User**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Workspot Control Sign on URL where you can initiate the login flow.
- Go to Workspot Control Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Workspot Control for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Workspot Control tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Workspot Control for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).